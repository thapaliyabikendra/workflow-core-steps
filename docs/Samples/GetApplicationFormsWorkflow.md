# Business Logic for `GetApplicationsForm` Workflow

1. Log a message with the `applicationWorkflowInstanceId` and initiator email from `currentUserDetails`.
2. Retrieve application form data using `operationWorkflowInstanceId`.
3. Validate application data by calling the rules engine (`GETAPPLICATIONFORMDATAVALIDATIONCHECK`) with `applicationDetails`.
4. Check the validation result:
    - If **true** (valid), continue to the approval process and update stage to `PROCESSING`:
        - Retrieve final application forms using `operationWorkflowInstanceId`.
        - Log final application details.
        - For each application form:
            - Start a new workflow instance.
        - Update application stage to `COMPLETED → APPLICATION_ACTION_SUCCESS`.
        - Update operation stage and log `"Operation Workflow has completed"`.
        - End the workflow.
    - If **false** (invalid):
        - Update application stage to `REQUESTED → APPROVAL_REQUESTED`.
        - Proceed to get project manager user ID.
        - Call the API `GET_PM_USERS_API` with initiator’s email to get `pmUserId`.
        - Call the API `ROLE_CHANGE_API_CREATE` with required data:
            - Parameters: `userId`, `processId`, `taskId`, `workflowId`, `employeeId`, `employeeName`, `currentFunctionalTitle`, `newFunctionalTitle`, and the full role change object.
        - If API creation is successful, call `APPROVAL_FORWARD_CASE_API` using the returned `appUid`.
        - Update application stage to `PROCESSING → APPROVAL_REQUEST_IN_PROGRESS`.
        - Create a workflow event `RecommendChainRoleChangeApprovalResponseEvent` and wait for a response tied to `applicationWorkflowInstanceId`.
        - Upon receiving the response:
            - Log the received event data.
        - Check RoleChangeApprovalResponseStatus:
            - If **rejected**:
                - Update application stage to `FAILED → CHECKER_REJECTED`.
                - Send an email notification to the initiator.
                - update application stage to `FAILED → APPLICATION_ACTION_FAILED`.
                - Update operation stage and log `"Operation Workflow has completed"`.
                - End the workflow.
            - If **approved**:
                - Check if this was the last approver.
                - If **final approver**:
                    - Log `"Recommend Chain Completed"` with `Application Details`.
                    - Retrieve final application forms using `operationWorkflowInstanceId`.
                    - Log final application details.
                    - For each application form:
                        - Start a new workflow instance.
                    - Update application stage to `COMPLETED → APPLICATION_ACTION_SUCCESS`.
                    - Update operation stage and log `"Operation Workflow has completed"`.
                    - End the workflow.
                - If **not last**:
                    - Go to `CreateRecommendChainRoleChangeApprovalEvent` to create workflow event `RecommendChainRoleChangeApprovalResponseEvent`and run in loop.

## Workflow Definition

```json
{
  "Id": "GetApplicationsForm",
  "Version": 1,
  "DataType": "Amnil.AccessControlManagementSystem.Workflows.DynamicData, Amnil.AccessControlManagementSystem.Application.Contracts",
  "DefaultErrorBehavior": "Terminate",
  "Steps": [
    {
      "Id": "PrintTaskId",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "GetApplicationFormsData",
      "Inputs": {
        "Message": "\"Requested for application- Task Id: \" + data[\"applicationWorkflowInstanceId\"] + \", Initaitor Email\" + data[\"currentUserDetails\"].Email"
      }
    },
    {
      "Id": "GetApplicationFormsData",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GetApplicationInstanceFormsStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "ValidateRulesStepId",
      "Inputs": {
        "OperationWorkflowInstanceId": "data[\"operationWorkflowInstanceId\"]"
      },
      "Outputs": {
        "applicationDetails": "step.Response"
      }
    },
    {
      "Id": "ValidateRulesStepId",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.ValidateRulesStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "DecideIfRecommendChainApproval",
      "Inputs": {
        "RuleName": "\"GETAPPLICATIONFORMDATAVALIDATIONCHECK\"",
        "Input1": "data[\"applicationDetails\"]"
      },
      "Outputs": {
        "isValidated": "step.Response[\"isValidated\"]"
      }
    },
    {
      "Id": "DecideIfRecommendChainApproval",
      "StepType": "WorkflowCore.Primitives.Decide, WorkflowCore",
      "SelectNextStep": {
        "ApprovalInProgressRPAJobs": "Convert.ToBoolean(data[\"isValidated\"])",
        "RequestApplicationStage": "!Convert.ToBoolean(data[\"isValidated\"])"
      }
    },
    {
      "Id": "RequestApplicationStage",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "GetPMUserId",
      "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "StageName": "\"REQUESTED\"",
        "SubStageName": "\"APPROVAL_REQUESTED\"",
        "Remarks": "\"Approval process has been initiated for\" + data[\"applicationWorkflowInstanceId\"]"
      }
    },
    {
      "Id": "GetPMUserId",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "RoleChangeAPICreate",
      "Inputs": {
        "ApiRequest": {
          "@email": "data[\"currentUserDetails\"].Email"
        },
        "ApiClientName": "\"GET_PM_USERS_API\""
      },
      "Outputs": {
        "pmUserId": "step.Response[\"data\"]"
      }
    },
    {
      "Id": "RoleChangeAPICreate",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "CallForwardAPIStep",
      "Inputs": {
        "ApiRequest": {
          "@userId": "data[\"pmUserId\"].processMakerUid",
          "@processId": "data[\"processId\"]",
          "@taskId": "data[\"applicationTaskId\"]",
          "@workflowId": "data[\"applicationWorkflowInstanceId\"]",
          "@employeeId": "data[\"operationFormData\"].userAccountForm.userAccountDetails.employeeId",
          "@employeeName": "data[\"operationFormData\"].userAccountForm.userAccountDetails.userAccountName",
          "@currentfunctionalTitle": "data[\"operationFormData\"].userAccountForm.userAccountDetails.currentfunctionalTitle",
          "@newFunctionalTitle": "data[\"operationFormData\"].roleChangeOperationForm.newFunctionalTitle",
          "@roleChange": "data[\"applicationDetails\"]"
        },
        "ApiClientName": "\"ROLE_CHANGE_API_CREATE\"",
        "CurrentUserDetail": "data[\"currentUserDetails\"]"
      },
      "Outputs": {
        "appUid": "step.Response[\"appUid\"]",
        "appNumber": "step.Response[\"appNumber\"]"
      }
    },
    {
      "Id": "CallForwardAPIStep",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "ApprovalInProgressApplicationStage",
      "Inputs": {
        "ApiRequest": {
          "@caseId": "data[\"appUid\"]"
        },
        "ApiClientName": "\"APPROVAL_FORWARD_CASE_API\"",
        "CurrentUserDetail": "data[\"currentUserDetails\"]"
      },
      "Outputs": {
        "initiatorResponse": "step.Response[\"success\"]"
      }
    },
    {
      "Id": "ApprovalInProgressApplicationStage",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "CreateRecommendChainRoleChangeApprovalEvent",
      "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "StageName": "\"PROCESSING\"",
        "SubStageName": "\"APPROVAL_REQUEST_IN_PROGRESS\"",
        "Remarks": "\"Approval is currently in progress for \" + data[\"applicationWorkflowInstanceId\"]"
      }
    },
    {
      "Id": "CreateRecommendChainRoleChangeApprovalEvent",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CreateWorkflowEventStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "WaitForRecommendChainRoleChangeApprovalResponseEvent",
      "Inputs": {
        "EventName": "\"RecommendChainRoleChangeApprovalResponseEvent\"",
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]"
      },
      "Outputs": {
        "roleChangeApprovalResponseEventId": "step.WorkflowEventId"
      }
    },
    {
      "Id": "WaitForRecommendChainRoleChangeApprovalResponseEvent",
      "StepType": "WorkflowCore.Primitives.WaitFor, WorkflowCore",
      "NextStepId": "CompleteRecommendChainRoleChangeApprovalEvent",
      "Inputs": {
        "EventName": "\"RecommendChainRoleChangeApprovalResponseEvent\"",
        "EventKey": "data[\"applicationWorkflowInstanceId\"]",
        "EffectiveDate": "DateTime.UtcNow"
      },
      "Outputs": {
        "RoleChangeApprovalResponseStatus": "step.EventData"
      }
    },
    {
      "Id": "CompleteRecommendChainRoleChangeApprovalEvent",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateWorkflowEventStatusStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "PrintEventData",
      "Inputs": {
        "WorkflowEventId": "data[\"roleChangeApprovalResponseEventId\"]"
      }
    },
    {
      "Id": "PrintEventData",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "DecideIsApproved",
      "Inputs": {
        "Message": "\"Event Data for application- Task Id: \" + data[\"RoleChangeApprovalResponseStatus\"]"
      }
    },
    {
      "Id": "DecideIsApproved",
      "StepType": "WorkflowCore.Primitives.Decide, WorkflowCore",
      "SelectNextStep": {
        "DecideIfLastRecommendChainApproval": "Convert.ToBoolean(data[\"RoleChangeApprovalResponseStatus\"].IsApproved)",
        "RejectedApplication": "!Convert.ToBoolean(data[\"RoleChangeApprovalResponseStatus\"].IsApproved)"
      }
    },
    {
      "Id": "RejectedApplication",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "RoleChangeRejectedEmail",
      "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "StageName": "\"FAILED\"",
        "SubStageName": "\"CHECKER_REJECTED\"",
        "Remarks": "\"Application rejected for  \" + data[\"applicationWorkflowInstanceId\"]"
      }
    },
    {
      "Id": "RoleChangeRejectedEmail",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.SendEmailNotificationStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "FailedApplicationStage",
      "Inputs": {
        "Email": "data[\"currentUserDetails\"].Email",
        "Subject": "\"Role Change Request Rejected\"",
        "Body": "\"We regret to inform you that your recent role change request for Employee \" + data[\"operationFormData\"].roleChangeOperationForm.employeeDetails.employeeName + \" has been rejected from Current Title \" +  data[\"operationFormData\"].roleChangeOperationForm.employeeDetails.currentfunctionalTitle + \", To New Functional Title: \" + data[\"operationFormData\"].roleChangeOperationForm.newFunctionalTitle"
      }
    },
    {
      "Id": "DecideIfLastRecommendChainApproval",
      "StepType": "WorkflowCore.Primitives.Decide, WorkflowCore",
      "SelectNextStep": {
        "PrintRecommendorComplete": "Convert.ToBoolean(data[\"RoleChangeApprovalResponseStatus\"].CurrentStageData.isLastRecommendChainApprover)",
        "CreateRecommendChainRoleChangeApprovalEvent": "!Convert.ToBoolean(data[\"RoleChangeApprovalResponseStatus\"].CurrentStageData.isLastRecommendChainApprover)"
      }
    },
    {
      "Id": "PrintRecommendorComplete",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "GetFinalApplicationFormsData",
      "Inputs": {
        "Message": "\"Recommend Chain Completed \" + data[\"finalApplicationDetails\"]"
      }
    },
    {
      "Id": "ApprovalInProgressRPAJobs",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "GetFinalApplicationFormsData",
      "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "StageName": "\"PROCESSING\"",
        "SubStageName": "\"APPROVAL_REQUEST_IN_PROGRESS\"",
        "Remarks": "\"Approval is currently in RPA Jobs \" + data[\"applicationWorkflowInstanceId\"]"
      }
    },
    {
      "Id": "GetFinalApplicationFormsData",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GetApplicationInstanceFormsStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "FinalPrintTask",
      "Inputs": {
        "OperationWorkflowInstanceId": "data[\"operationWorkflowInstanceId\"]"
      },
      "Outputs": {
        "finalApplicationDetails": "step.Response"
      }
    },
    {
      "Id": "FinalPrintTask",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "ForEachStep",
      "Inputs": {
        "Message": "\"Final Application Details: \" + data[\"finalApplicationDetails\"]"
      }
    },
    {
      "Id": "ForEachStep",
      "StepType": "WorkflowCore.Primitives.ForEach, WorkflowCore",
      "NextStepId": "CompleteApplicationStage",
      "Inputs": {
        "Collection": "data[\"finalApplicationDetails\"].data"
      },
      "Do": [
        [
          {
            "Id": "StartWorkflowInstanceStep",
            "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.StartWorkflowInstanceStep, Amnil.AccessControlManagementSystem.Application",
            "Inputs": {
              "ApplicationWorkflowInstanceId": "context.Item.ApplicationWorkflowInstance"
            }
          }
        ]
      ]
    },
    {
      "Id": "CompleteApplicationStage",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "UpdateOperationStage",
      "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "StageName": "\"COMPLETED\"",
        "SubStageName": "\"APPLICATION_ACTION_SUCCESS\"",
        "Remarks": "\"Role change application has been completed successfully for operation id: \" + data[\"operationWorkflowInstanceId\"]"
      }
    },
    {
      "Id": "FailedApplicationStage",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "UpdateOperationStage",
      "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "StageName": "\"FAILED\"",
        "SubStageName": "\"APPLICATION_ACTION_FAILED\"",
        "Remarks": "\"Role change application has been completed for operation id: \" + data[\"operationWorkflowInstanceId\"]"
      }
    },
    {
      "Id": "UpdateOperationStage",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateOperationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "EndWorkflow",
      "Inputs": {
        "OperationWorkflowInstanceId": "data[\"operationWorkflowInstanceId\"]",
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "Remarks": "\"Operation Workflow has completed\""
      },
      "Outputs": {
        "OperationStatus": "step.OperationStatus"
      }
    },
    {
      "Id": "EndWorkflow",
      "StepType": "WorkflowCore.Primitives.EndStep, WorkflowCore"
    }
  ]
}
```
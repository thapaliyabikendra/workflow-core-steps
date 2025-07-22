# Sol Change (Pool Staffs) Workflow

```json
{
  "Id": "SolChangePoolStaffsWorkflow",
  "Version": 1,
  "DataType": "Amnil.AccessControlManagementSystem.Workflows.DynamicData, Amnil.AccessControlManagementSystem.Application.Contracts",
  "Steps": [
    {
      "Id": "PrintInitialRequest",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "UpdateRequestedStage",
      "Inputs": {
        "Message": "\"Sol Change Request - Employee ID: \" + data[\"operationFormData\"].userAccountForm.userAccountDetails.employeeId + \", From Sol ID: \" + data[\"operationFormData\"].userAccountForm.userAccountDetails.branchCode + \", To Sol ID: \" + data[\"operationFormData\"].roleChangeOperationForm.userAccountDetails.branchCode + \", Auth User ID: \" + data[\"operationFormData\"].userAccountForm.userAccountIdentifier + \", Is Teller: Y, New Functional Role: \" + data[\"operationFormData\"].roleChangeOperationForm.newfunctionalTitle + \", Effective Date: \" + data[\"operationFormData\"].roleChangeOperationForm.requestedFrom"
      }
    },
    {
      "Id": "UpdateRequestedStage",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "ValidateSolChangeRequest",
      "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "StageName": "\"REQUESTED\"",
        "SubStageName": "\"SOL_CHANGE_REQUESTED\"",
        "Remarks": "\"Sol Change Request submitted for Employee ID: \" + data[\"operationFormData\"].userAccountForm.userAccountDetails.employeeId + \", From Sol ID: \" + data[\"operationFormData\"].userAccountForm.userAccountDetails.branchCode + \", To Sol ID: \" + data[\"operationFormData\"].roleChangeOperationForm.userAccountDetails.branchCode"
      }
    },
    {
      "Id": "ValidateSolChangeRequest",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "CheckValidationResponse",
      "Inputs": {
        "ApiRequest": {
          "@employeeId": "data[\"operationFormData\"].userAccountForm.userAccountDetails.employeeId",
          "@fromSolId": "data[\"operationFormData\"].userAccountForm.userAccountDetails.branchCode",
          "@toSolId": "data[\"operationFormData\"].roleChangeOperationForm.userAccountDetails.branchCode",
          "@authUserId": "data[\"operationFormData\"].userAccountForm.userAccountIdentifier",
          "@isTeller": "\"Y\"",
          "@newFunctionalRole": "data[\"operationFormData\"].roleChangeOperationForm.newfunctionalTitle",
          "@effectiveDate": "data[\"operationFormData\"].roleChangeOperationForm.requestedFrom"
        },
        "ApiClientName": "\"SOL_CHANGE_VALIDATION_API\"",
        "CurrentUserDetail": "data[\"currentUserDetails\"]"
      },
      "Outputs": {
        "validationResponse": "step.Response"
      }
    },
    {
      "Id": "CheckValidationResponse",
      "StepType": "WorkflowCore.Primitives.If, WorkflowCore",
      "SelectNextStep": {
        "UpdateProcessingStage": "Convert.ToBoolean(data[\"validationResponse\"].success)",
        "UpdateFailedStage": "!Convert.ToBoolean(data[\"validationResponse\"].success)"
      }
    },
    {
      "Id": "UpdateFailedStage",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "PrintValidationError",
      "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "StageName": "\"FAILED\"",
        "SubStageName": "\"VALIDATION_FAILED\"",
        "Remarks": "\"Sol Change validation failed: \" + data[\"validationResponse\"].errorMessage"
      }
    },
    {
      "Id": "PrintValidationError",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "EndWorkflow",
      "Inputs": {
        "Message": "\"Sol Change validation failed for Employee ID: \" + data[\"operationFormData\"].userAccountForm.userAccountDetails.employeeId + \", Error: \" + data[\"validationResponse\"].errorMessage"
      }
    },
    {
      "Id": "UpdateProcessingStage",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "CreateSSMApprovalEvent",
      "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "StageName": "\"PROCESSING\"",
        "SubStageName": "\"AWAITING_SSM_APPROVAL\"",
        "Remarks": "\"Sol Change request validated successfully, awaiting SSM/State Head approval for Employee ID: \" + data[\"operationFormData\"].userAccountForm.userAccountDetails.employeeId"
      }
    },
    {
      "Id": "CreateSSMApprovalEvent",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CreateWorkflowEventStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "WaitForSSMApproval",
      "Inputs": {
        "EventName": "\"SSMApprovalResponseEvent\"",
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "EventKey": "data[\"applicationWorkflowInstanceId\"]"
      },
      "Outputs": {
        "ssmApprovalEventId": "step.WorkflowEventId"
      }
    },
    {
      "Id": "WaitForSSMApproval",
      "StepType": "WorkflowCore.Primitives.WaitFor, WorkflowCore",
      "NextStepId": "CompleteSSMApprovalEvent",
      "Inputs": {
        "EventName": "\"SSMApprovalResponseEvent\"",
        "EventKey": "data[\"applicationWorkflowInstanceId\"]",
        "EffectiveDate": "DateTime.UtcNow"
      },
      "Outputs": {
        "SSMApprovalStatus": "step.EventData"
      }
    },
    {
      "Id": "CompleteSSMApprovalEvent",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateWorkflowEventStatusStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "DecideSSMApproval",
      "Inputs": {
        "WorkflowEventId": "data[\"ssmApprovalEventId\"]"
      }
    },
    {
      "Id": "DecideSSMApproval",
      "StepType": "WorkflowCore.Primitives.Decide, WorkflowCore",
      "SelectNextStep": {
        "ProcessSSMApproval": "Convert.ToBoolean(data[\"SSMApprovalStatus\"].IsApproved)",
        "ProcessSSMRejection": "!Convert.ToBoolean(data[\"SSMApprovalStatus\"].IsApproved)"
      }
    },
    {
      "Id": "ProcessSSMRejection",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "PrintSSMRejection",
      "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "StageName": "\"REJECTED\"",
        "SubStageName": "\"SSM_REJECTED\"",
        "Remarks": "\"Sol Change request rejected by SSM/State Head for Employee ID: \" + data[\"operationFormData\"].userAccountForm.userAccountDetails.employeeId + \", Reason: \" + data[\"SSMApprovalStatus\"].RejectionReason"
      }
    },
    {
      "Id": "PrintSSMRejection",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "EndWorkflow",
      "Inputs": {
        "Message": "\"Sol Change request rejected by SSM/State Head for Employee ID: \" + data[\"operationFormData\"].userAccountForm.userAccountDetails.employeeId + \", Reason: \" + data[\"SSMApprovalStatus\"].RejectionReason"
      }
    },
    {
      "Id": "ProcessSSMApproval",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "PrintSSMApproval",
      "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "StageName": "\"PROCESSING\"",
        "SubStageName": "\"SSM_APPROVED_EXECUTING\"",
        "Remarks": "\"Sol Change request approved by SSM/State Head, proceeding to Executing Department for Employee ID: \" + data[\"operationFormData\"].userAccountForm.userAccountDetails.employeeId"
      }
    },
    {
      "Id": "PrintSSMApproval",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "CallHCSEFincoreAPI",
      "Inputs": {
        "Message": "\"Sol Change request approved by SSM/State Head for Employee ID: \" + data[\"operationFormData\"].userAccountForm.userAccountDetails.employeeId + \", proceeding to Executing Department\""
      }
    },
    {
      "Id": "CallHCSEFincoreAPI",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "CheckHCSEResponse",
      "Inputs": {
        "ApiRequest": {
          "@employeeId": "data[\"operationFormData\"].userAccountForm.userAccountDetails.employeeId",
          "@fromSolId": "data[\"operationFormData\"].userAccountForm.userAccountDetails.branchCode",
          "@toSolId": "data[\"operationFormData\"].roleChangeOperationForm.userAccountDetails.branchCode",
          "@authUserId": "data[\"operationFormData\"].userAccountForm.userAccountIdentifier",
          "@isTeller": "\"Y\"",
          "@newFunctionalRole": "data[\"operationFormData\"].roleChangeOperationForm.newfunctionalTitle",
          "@effectiveDate": "data[\"operationFormData\"].roleChangeOperationForm.requestedFrom",
          "@menuType": "\"HCSE\"",
          "@modifiedThrough": "\"HCSE menu in fincore\""
        },
        "ApiClientName": "\"HCSE_FINCORE_API\"",
        "CurrentUserDetail": "data[\"currentUserDetails\"]"
      },
      "Outputs": {
        "hcseResponse": "step.Response"
      }
    },
    {
      "Id": "CheckHCSEResponse",
      "StepType": "WorkflowCore.Primitives.If, WorkflowCore",
      "SelectNextStep": {
        "UpdateHEFMMenu": "Convert.ToBoolean(data[\"hcseResponse\"].success)",
        "UpdateHCSEFailedStage": "!Convert.ToBoolean(data[\"hcseResponse\"].success)"
      }
    },
    {
      "Id": "UpdateHEFMMenu",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "CheckHEFMResponse",
      "Inputs": {
        "ApiRequest": {
          "@employeeId": "data[\"operationFormData\"].userAccountForm.userAccountDetails.employeeId",
          "@isTellerPlaceholder": "\"Y\"",
          "@menuType": "\"HEFM\"",
          "@modifiedThrough": "\"HEFM menu with Y flag\""
        },
        "ApiClientName": "\"HEFM_MENU_API\"",
        "CurrentUserDetail": "data[\"currentUserDetails\"]"
      },
      "Outputs": {
        "hefmResponse": "step.Response"
      }
    },
    {
      "Id": "CheckHEFMResponse",
      "StepType": "WorkflowCore.Primitives.If, WorkflowCore",
      "SelectNextStep": {
        "UpdateCompletedStage": "Convert.ToBoolean(data[\"hefmResponse\"].success)",
        "UpdateHEFMFailedStage": "!Convert.ToBoolean(data[\"hefmResponse\"].success)"
      }
    },
    {
      "Id": "UpdateCompletedStage",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "PrintSuccessMessage",
      "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "StageName": "\"COMPLETED\"",
        "SubStageName": "\"SOL_CHANGE_SUCCESS\"",
        "Remarks": "\"Sol Change completed successfully for Employee ID: \" + data[\"operationFormData\"].userAccountForm.userAccountDetails.employeeId + \", From Sol ID: \" + data[\"operationFormData\"].userAccountForm.userAccountDetails.branchCode + \", To Sol ID: \" + data[\"operationFormData\"].roleChangeOperationForm.userAccountDetails.branchCode"
      }
    },
    {
      "Id": "PrintSuccessMessage",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "EndWorkflow",
      "Inputs": {
        "Message": "\"Sol Change completed successfully for Employee ID: \" + data[\"operationFormData\"].userAccountForm.userAccountDetails.employeeId + \", From Sol ID: \" + data[\"operationFormData\"].userAccountForm.userAccountDetails.branchCode + \", To Sol ID: \" + data[\"operationFormData\"].roleChangeOperationForm.userAccountDetails.branchCode + \", New Functional Role: \" + data[\"operationFormData\"].roleChangeOperationForm.newfunctionalTitle + \", Effective Date: \" + data[\"operationFormData\"].roleChangeOperationForm.requestedFrom"
      }
    },
    {
      "Id": "EndWorkflow",
      "StepType": "WorkflowCore.Primitives.EndStep, WorkflowCore"
    }
  ]
}
```
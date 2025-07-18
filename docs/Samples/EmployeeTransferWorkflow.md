# Business Logic

1. Print `"Requested - Task Id: <applicationWorkflowInstanceId>"`.
2. Update the application stage to `REQUESTED` with `"Approval Requested for task id: <applicationWorkflowInstanceId>"`
3. Call an API name `BPM_API_CLIENT` with `employeeId` from `userAccountIdentifier`
4. Update the application stage to `PROCESSING` with message `"Approval Request In Progress for task id: <applicationWorkflowInstanceId>"`
5. Check the API response:
    - If `success == false`:
        - update application stage to `FAILED` with message `"Failed - BPM API    Approval Request failed"` and Update operation stage with message`"Operation Workflow has completed"`
        - Print `"Workflow <OperationStatus>, for ApplicationWorkflowInstanceId: <applicationWorkflowInstanceId>"`
        - End the workflow
6. Log `"Processing - Waiting for BPM API Approval Response Event"`.
7. Wait for event `BPMAPIApprovalResponseEvent` with key `applicationWorkflowInstanceId`.
8. Log `"Processing - BPM API Approval Response Event received"`.
9. Check `ApprovalStatus`:
    - If `Approved`:
        1. Update application stage to `COMPLETED`, sub-stage to `CHECKER_APPROVED`, with remarks:  
           `"Checker Approved for task id: {applicationWorkflowInstanceId}"`.
        2. Log `"Processing - Checker Approved: BPM API Approval Response Event received {operationFormData}"`.
        3. Update application stage to `REQUESTED`, sub-stage to `MANUAL_ACTION_REQUIRED`, with remarks:  
           `"Manual Action Required for task id: {applicationWorkflowInstanceId}"`.
    - If `Rejected`:
        1. Update application stage to `FAILED`, sub-stage to `CHECKER_REJECTED`, with remarks:  
           `"Checker Rejected for task id: {applicationWorkflowInstanceId}"`.
        2. Log `"Processing - Checker Rejected: BPM API Approval Response Event received"`.
10. Update the operation stage with remarks: `"Operation Workflow has completed"`.
11. Log `"Workflow {OperationStatus}, for ApplicationWorkflowInstanceId: {applicationWorkflowInstanceId}"`.
12. End the workflow.

```json
{
  "Id": "PermanentEmployeeTransferWorkflowWithManualAction",
  "Version": 1,
  "DataType": "Amnil.AccessControlManagementSystem.Workflows.DynamicData, Amnil.AccessControlManagementSystem.Application.Contracts",
  "DefaultErrorBehavior": "Compensate",
  "Steps": [
    {
      "Id": "PrintTaskId",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "UpdateARequestedWorkflowStageStep",
      "Inputs": {
        "Message": "\"Requested - Task Id: \" + data[\"applicationWorkflowInstanceId\"]"
      }
    },
    {
      "Id": "UpdateARequestedWorkflowStageStep",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "CallBPMApiStep",
      "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "StageName": "\"REQUESTED\"",
        "SubStageName": "\"APPROVAL_REQUESTED\"",
        "Remarks": "\"Approval Requested for task id: \" + data[\"applicationWorkflowInstanceId\"]"
      }
    },
    {
      "Id": "CallBPMApiStep",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "ApprovalInProgressLog",
      "Inputs": {
        "ApiRequest": {
          "@employeeId": "data[\"userAccountIdentifier\"]"
        },
        "ApiClientName": "\"BPM_API_CLIENT\""
      },
      "Outputs": {
        "apiResponse1Success": "step.Response[\"success\"]"
      }
    },
    {
      "Id": "ApprovalInProgressLog",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "IfConditionAfterBPMApiCall",
      "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "StageName": "\"PROCESSING\"",
        "SubStageName": "\"APPROVAL_REQUEST_IN_PROGRESS\"",
        "Remarks": "\"Approval Request In Progress for task id: \" + data[\"applicationWorkflowInstanceId\"]"
      }
    },
    {
      "Id": "IfConditionAfterBPMApiCall",
      "StepType": "WorkflowCore.Primitives.If, WorkflowCore",
      "NextStepId": "WaitingForBPMAPIApprovalResponseEventLogger7",
      "Inputs": {
        "Condition": "!Convert.ToBoolean(data[\"apiResponse1Success\"])"
      },
      "Do": [
        [
          {
            "Id": "BPMApiCallFailureLog",
            "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
            "NextStepId": "BPMApiCallFailureLogger",
            "Inputs": {
              "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
              "StageName": "\"FAILED\"",
              "Remarks": "\"Approval Request Failed for task id: \" + data[\"applicationWorkflowInstanceId\"]"
            }
          },
          {
            "Id": "BPMApiCallFailureLogger",
            "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
            "NextStepId": "UpdateOperationStage",
            "Inputs": {
              "Message": "\"Failed - BPM API Approval Request failed\""
            }
          }
        ]
      ]
    },
    {
      "Id": "WaitingForBPMAPIApprovalResponseEventLogger7",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "WaitForBPMAPIApprovalResponseEvent8",
      "Inputs": {
        "Message": "\"Processing - Waiting for BPM API Approval Response Event\""
      }
    },
    {
      "Id": "WaitForBPMAPIApprovalResponseEvent8",
      "StepType": "WorkflowCore.Primitives.WaitFor, WorkflowCore",
      "NextStepId": "ReceivedBPMAPIApprovalResponseEventLog9",
      "Inputs": {
        "EventName": "\"BPMAPIApprovalResponseEvent\"",
        "EventKey": "data[\"applicationWorkflowInstanceId\"]",
        "EffectiveDate": "DateTime.Now"
      },
      "Outputs": {
        "ApprovalStatus": "step.EventData"
      }
    },
    {
      "Id": "ReceivedBPMAPIApprovalResponseEventLog9",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "DecideApprovalStatus",
      "Inputs": {
        "Message": "\"Processing - BPM API Approval Response Event received\""
      }
    },
    {
      "Id": "DecideApprovalStatus",
      "StepType": "WorkflowCore.Primitives.Decide, WorkflowCore",
      "SelectNextStep": {
        "UpdateBPMAPICheckerApprovedStatus": "object.Equals(data[\"ApprovalStatus\"], \"Approved\")",
        "UpdateBPMAPICheckerRejectedStatus": "object.Equals(data[\"ApprovalStatus\"], \"Rejected\")"
      }
    },
    {
      "Id": "UpdateBPMAPICheckerApprovedStatus",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "BPMAPICheckerApprovedLogger",
      "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "StageName": "\"COMPLETED\"",
        "SubStageName": "\"CHECKER_APPROVED\"",
        "Remarks": "\"Checker Approved for task id: \" + data[\"applicationWorkflowInstanceId\"]"
      }
    },
    {
      "Id": "BPMAPICheckerApprovedLogger",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "UpdateMAWorkflowStageStep",
      "Inputs": {
        "Message": "\"Processing - Checker Approved: BPM API Approval Response Event received \" + data[\"operationFormData\"]"
      }
    },
    {
      "Id": "UpdateMAWorkflowStageStep",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "PrintWorkflowCompleteMessage",
      "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "StageName": "\"REQUESTED\"",
        "SubStageName": "\"MANUAL_ACTION_REQUIRED\"",
        "Remarks": "\"Manual Action Required for task id: \" + data[\"applicationWorkflowInstanceId\"]"
      }
    },
    {
      "Id": "UpdateBPMAPICheckerRejectedStatus",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "BPMAPICheckerRejectedLog",
      "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "StageName": "\"FAILED\"",
        "SubStageName": "\"CHECKER_REJECTED\"",
        "Remarks": "\"Checker Rejected for task id: \" + data[\"applicationWorkflowInstanceId\"]"
      }
    },
    {
      "Id": "BPMAPICheckerRejectedLog",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "UpdateOperationStage",
      "Inputs": {
        "Message": "\"Processing - Checker Rejected: BPM API Approval Response Event received\""
      }
    },
    {
      "Id": "UpdateOperationStage",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateOperationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "PrintWorkflowCompleteMessage",
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
      "Id": "PrintWorkflowCompleteMessage",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "EndWorkflow",
      "Inputs": {
        "Message": "\"Workflow \" + data[\"OperationStatus\"] + \",for ApplicationWorkflowInstanceId: \" + data[\"applicationWorkflowInstanceId\"]"
      }
    },
    {
      "Id": "EndWorkflow",
      "StepType": "WorkflowCore.Primitives.EndStep, WorkflowCore"
    }
  ]
}
```
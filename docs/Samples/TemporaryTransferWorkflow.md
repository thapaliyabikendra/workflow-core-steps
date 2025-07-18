## Temporary Transfer Approval Workflow Business Logic

- Log a message indicating the start of the temporary transfer request with the employee ID.
- Update the application workflow stage to `PROCESSING` and the sub-stage to `TRANSFER_REQUESTED` with a remark indicating the processing status.
- Call an external API named `TRANSFER_APPROVAL_API` passing dynamic data:
    - `employeeId`
    - `transferDetails`
- Evaluate the API response:
    - If `data.success == true`:
        - Update the application stage to `COMPLETED` and sub-stage to `TRANSFER_APPROVED` with a success remark.
        - Log a message confirming the transfer approval with the employee ID.
    - Else:
        - Update the application stage to `FAILED` and sub-stage to `TRANSFER_DENIED` with a failure remark.
        - Log a message indicating transfer failure with the employee ID.
- End the workflow.

## Workflow

```json
{
  "Id": "TemporaryTransferApprovalWorkflow",
  "Version": 1,
  "DataType": "Amnil.AccessControlManagementSystem.Workflows.DynamicData, Amnil.AccessControlManagementSystem.Application.Contracts",
  "DefaultErrorBehavior": "Terminate",
  "Steps": [
    {
      "Id": "PrintStartMessage",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "UpdateStageProcessing",
      "Inputs": {
        "Message": "\"Temporary transfer request started for Employee ID: \" + data[\"employeeId\"]"
      }
    },
    {
      "Id": "UpdateStageProcessing",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "CallTransferApprovalApi",
      "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "StageName": "\"PROCESSING\"",
        "SubStageName": "\"TRANSFER_REQUESTED\"",
        "Remarks": "\"Processing temporary transfer request\""
      }
    },
    {
      "Id": "CallTransferApprovalApi",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "EvaluateApiResponse",
      "Inputs": {
        "ApiClientName": "\"TRANSFER_APPROVAL_API\"",
        "ApiRequest": {
          "@employeeId": "data[\"employeeId\"]",
          "@transferDetails": "data[\"transferDetails\"]"
        }
      },
      "Outputs": {
        "ApiResponse": "step.Response"
      }
    },
    {
      "Id": "EvaluateApiResponse",
      "StepType": "WorkflowCore.Primitives.If, WorkflowCore",
      "Inputs": {
        "Condition": "Convert.ToBoolean(data[\"ApiResponse\"].success) == true"
      },
      "Do": [
        [
          {
            "Id": "UpdateStageCompleted",
            "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
            "NextStepId": "PrintSuccessMessage",
            "Inputs": {
              "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
              "StageName": "\"COMPLETED\"",
              "SubStageName": "\"TRANSFER_APPROVED\"",
              "Remarks": "\"Temporary transfer approved successfully.\""
            }
          }
        ]
      ],
      "Else": [
        [
          {
            "Id": "UpdateStageFailed",
            "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
            "NextStepId": "PrintFailureMessage",
            "Inputs": {
              "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
              "StageName": "\"FAILED\"",
              "SubStageName": "\"TRANSFER_DENIED\"",
              "Remarks": "\"Temporary transfer approval failed.\""
            }
          }
        ]
      ]
    },
    {
      "Id": "PrintSuccessMessage",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "EndWorkflow",
      "Inputs": {
        "Message": "\"Transfer approved for Employee ID: \" + data[\"employeeId\"]"
      }
    },
    {
      "Id": "PrintFailureMessage",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "EndWorkflow",
      "Inputs": {
        "Message": "\"Transfer failed for Employee ID: \" + data[\"employeeId\"]"
      }
    },
    {
      "Id": "EndWorkflow",
      "StepType": "WorkflowCore.Primitives.EndStep, WorkflowCore"
    }
  ]
}
```
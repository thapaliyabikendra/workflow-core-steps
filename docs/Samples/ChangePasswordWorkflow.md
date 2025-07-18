### Business Logic:
1. Update the application stage to `PROCESSING`.
2. Call an API named `EMPLOYEE_CHANGE_PASSWORD_API` with `username` and `newPassword` from `FormData`.
3. Check the API response:
    - If `data.success == true`, update application stage to `COMPLETED` and operation stage to `COMPLETED` with message `"Password changed successfully"`.
    - Else, update application stage to `FAILED` and operation stage to `FAILED` with message `"Failed to change password"`.
4. End the workflow.


### Workflow Definition
```json
{
  "Id": "ChangePasswordWorkflow",
  "Version": 1,
  "DataType": "Amnil.AccessControlManagementSystem.Workflows.DynamicData, Amnil.AccessControlManagementSystem.Application.Contracts",
  "DefaultErrorBehavior": "Terminate",
  "Steps": [
    {
      "Id": "SetProcessingStage",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "CallChangePasswordApi",
      "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "StageName": "\"PROCESSING\"",
        "SubStageName": "\"APPLICATION_ACTION_JOB_IN_PROGRESS\"",
        "Remarks": "\"Password change process started\""
      }
    },
    {
      "Id": "CallChangePasswordApi",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "CheckApiResponse",
      "Inputs": {
        "ApiClientName": "\"EMPLOYEE_CHANGE_PASSWORD_API\"",
        "ApiRequest": {
          "@username": "data[\"FormData\"].username",
          "@newPassword": "data[\"FormData\"].newPassword"
        }
      },
      "Outputs": {
        "ChangePasswordApiResponse": "step.Response"
      }
    },
    {
      "Id": "CheckApiResponse",
      "StepType": "WorkflowCore.Primitives.If, WorkflowCore",
      "NextStepId": "EndWorkflow",
      "Inputs": {
        "Condition": "Convert.ToBoolean(data[\"ChangePasswordApiResponse\"].success)"
      },
      "Do": [
        [
          {
            "Id": "SetCompletedStage",
            "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
            "NextStepId": "SetOperationCompleted",
            "Inputs": {
              "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
              "StageName": "\"COMPLETED\"",
              "SubStageName": "\"APPLICATION_ACTION_SUCCESS\"",
              "Remarks": "\"Password changed successfully\""
            }
          },
          {
            "Id": "SetOperationCompleted",
            "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateOperationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
            "NextStepId": "EndWorkflow",
            "Inputs": {
              "OperationWorkflowInstanceId": "data[\"operationWorkflowInstanceId\"]",
              "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
              "Remarks": "\"Password changed successfully\""
            }
          }
        ]
      ],
      "Else": [
        {
          "Id": "SetFailedStage",
          "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
          "NextStepId": "SetOperationFailed",
          "Inputs": {
            "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
            "StageName": "\"FAILED\"",
            "SubStageName": "\"APPLICATION_ACTION_FAILED\"",
            "Remarks": "\"Failed to change password\""
          }
        },
        {
          "Id": "SetOperationFailed",
          "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateOperationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
          "NextStepId": "EndWorkflow",
          "Inputs": {
            "OperationWorkflowInstanceId": "data[\"operationWorkflowInstanceId\"]",
            "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
            "Remarks": "\"Failed to change password\""
          }
        }
      ]
    },
    {
      "Id": "EndWorkflow",
      "StepType": "WorkflowCore.Primitives.EndStep, WorkflowCore"
    }
  ]
}
```

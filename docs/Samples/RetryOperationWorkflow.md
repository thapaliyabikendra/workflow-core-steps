## Business Logic
- Log a message with the requested task ID from `recordData`.
- Update the record in the `FinancleRoleChangeApiRequests` table to set `WorkflowStage` as `PROCESSING`.
- Call the API client named `GET_MBL_APPLICATIONS_API_DUMMY_TEST` with `employeeName`, `roleCode`, and `roleName` taken from `recordData`.
4. Check the API response::
    - If `true`, update the `WorkflowStage` of the record to `COMPLETED`.
    - If `false`, update the `WorkflowStage` of the record to `FAILED`.
5. Log the ID of the record update response (`NocoDbResponseData`).
6. End the workflow.

## Workflow Definition
```json
{
  "Id": "RetryOperationWorkflow",
  "Version": 3,
  "DataType": "Amnil.AccessControlManagementSystem.Workflows.DynamicData, Amnil.AccessControlManagementSystem.Application.Contracts",
  "DefaultErrorBehavior": "Terminate",
  "Steps": [
    {
      "Id": "PrintTaskId",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "UpdateNocoDBStep",
      "Inputs": {
        "Message": "\"Requested - Task Id: \" + data[\"recordData\"]"
      }
    },
    {
      "Id": "UpdateNocoDBStep",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateRecordOnNocoDBStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "ApiStep",
      "Inputs": {
        "TableName": "\"FinancleRoleChangeApiRequests\"",
        "Data": {
          "@Id": "data[\"recordData\"].Id",
          "WorkflowStage": "PROCESSING"
        }
      },
      "Outputs": {
        "Data": "step.Id"
      }
    },
    {
      "Id": "ApiStep",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "UpdateWorkflowStage",
      "Inputs": {
        "ApiClientName": "\"GET_MBL_APPLICATIONS_API_DUMMY_TEST\"",
        "ApiRequest": {
          "@employeeName": "data[\"recordData\"].EmployeeName",
          "@roleCode": "data[\"recordData\"].TargetRoleCode",
          "@roleName": "data[\"recordData\"].TargetRoleName"
        }
      },
      "Outputs": {
        "ApiResponseData": "step.Response"
      }
    },
    {
      "Id": "UpdateWorkflowStage",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateRecordOnNocoDBStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "PrintApplicationTemplate",
      "Inputs": {
        "TableName": "\"FinancleRoleChangeApiRequests\"",
        "Data": {
          "@Id": "data[\"recordData\"].Id",
          "@WorkflowStage": "Convert.ToBoolean(data[\"ApiResponseData\"].success) ? \"COMPLETED\" : \"FAILED\""
        }
      },
      "Outputs": {
        "NocoDbResponseData": "step.Id"
      }
    },
    {
      "Id": "PrintApplicationTemplate",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "EndWorkflow",
      "Inputs": {
        "Message": "\"NocoDbResponseData \" + data[\"NocoDbResponseData\"]"
      }
    },
    {
      "Id": "EndWorkflow",
      "StepType": "WorkflowCore.Primitives.EndStep, WorkflowCore"
    }
  ]
}
```
# Get Application Workflow Step

## Purpose
Retrieves details of a specific application workflow, such as its configuration, status, or metadata.

## Step Type
Amnil.AccessControlManagementSystem.Workflows.Steps.GetApplicationWorkflowStep, Amnil.AccessControlManagementSystem.Application

## Parameters

### Inputs
- `OperationWorkflowId` (string): The unique identifier of the application workflow to retrieve.
- `AppName` (string): The application name.
- `AppTaskName` (string): The application task name.

### Outputs
- `Response` (JObject): The application task workflow details object.

## Usage Example
```json
{
  "Id": "GetApplicationWorkflowStep",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GetApplicationWorkflowStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "PrintApplicationTaskId",
  "Inputs": {
    "OperationWorkflowId": "data[\"operationWorkflowInstanceId\"]",
    "AppName": "\"Finacle\"",
    "AppTaskName": "\"Finacle Test Role Change\""
  },
  "Outputs": {
    "ApplicationTaskWorkflowResponse": "step.Response"
  }
}
```

## Error Handling
- Validates workflow existence.
- Handles retrieval errors.
- Logs failures.
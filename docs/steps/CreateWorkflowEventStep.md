# Create Workflow Event Step

## Purpose
Creates workflow events in the system to track workflow progress and state.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.CreateWorkflowEventStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `OperationWorkflowInstanceId` (string): ID of the operation workflow instance
- `ApplicationWorkflowInstanceId` (string): ID of the application workflow instance
- `EventName` (string): Name of the event to create
- `EventData` (JObject): Additional data associated with the event

### Outputs
- `WorkflowEventId` (string): The ID of the created workflow event

## Usage Example

```json
{
  "Id": "CreateNewWorkflowEvent",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CreateWorkflowEventStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "ProcessEvent",
  "Inputs": {
    "OperationWorkflowInstanceId": "data[\"operationWorkflowInstanceId\"]",
    "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
    "EventName": "\"APPLICATION_SUBMITTED\"",
    "EventData": {
      "status": "submitted",
      "timestamp": "DateTime.Now"
    }
  },
  "Outputs": {
    "CreatedEventId": "step.WorkflowEventId"
  }
}
```

## Error Handling
- Validates required input parameters
- Handles duplicate event creation
- Logs event creation for audit purposes

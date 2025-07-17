# Update Operation Task Stage Step

## Purpose
Updates the stage/status of an operation task in the workflow process.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateOperationTaskStageStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `OperationWorkflowInstanceId` (string): ID of the operation workflow instance
- `ApplicationWorkflowInstanceId` (string): ID of the associated application workflow instance
- `Remarks` (string, optional): Additional remarks about the stage change
- `CurrentUserId` (string, optional): The unique identifier of the user performing the update.

### Outputs
- `OperationStatus` (string): Updated status of the operation

## Usage Example

```json
{
  "Id": "UpdateOperationStage",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateOperationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "CompleteWorkflow",
  "Inputs": {
    "OperationWorkflowInstanceId": "data[\"operationWorkflowInstanceId\"]",
    "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
    "Remarks": "\"Operation completed successfully\"",
    "CurrentUserId": "data[\"currentUserId\"]"
  },
  "Outputs": {
    "OperationStatus": "step.OperationStatus",
  }
}
```

## Error Handling
- Validates operation stage transitions
- Maintains operation history
- Handles dependencies with application workflow

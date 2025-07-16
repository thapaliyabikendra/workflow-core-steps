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

### Outputs
- `OperationStatus` (string): Updated status of the operation
- `Success` (boolean): Indicates if the stage was updated successfully

## Usage Example

```json
{
  "Id": "UpdateOperationStage",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateOperationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "CompleteWorkflow",
  "Inputs": {
    "OperationWorkflowInstanceId": "data[\"operationWorkflowInstanceId\"]",
    "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
    "Remarks": "\"Operation completed successfully\""
  },
  "Outputs": {
    "Status": "step.OperationStatus",
    "Updated": "step.Success"
  }
}
```

## Error Handling
- Validates operation stage transitions
- Maintains operation history
- Handles dependencies with application workflow

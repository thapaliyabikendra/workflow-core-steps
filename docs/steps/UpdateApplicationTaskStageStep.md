# Update Application Task Stage Step

## Purpose
Updates the stage/status of an application task in the workflow process.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `ApplicationWorkflowInstanceId` (string): ID of the application workflow instance
- `StageName` (string): Name of the new stage
- `SubStageName` (string, optional): Name of the sub-stage
- `Remarks` (string, optional): Additional remarks about the stage change

### Outputs
- `Success` (boolean): Indicates if the stage was updated successfully
- `StageId` (string): ID of the new stage

## Usage Example

```json
{
  "Id": "UpdateTaskToApprovalStage",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "NotifyApprovers",
  "Inputs": {
    "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
    "StageName": "\"APPROVAL_PENDING\"",
    "SubStageName": "\"MANAGER_APPROVAL\"",
    "Remarks": "\"Application sent for manager approval\""
  },
  "Outputs": {
    "StageUpdated": "step.Success",
    "NewStageId": "step.StageId"
  }
}
```

## Error Handling
- Validates stage transitions
- Handles concurrent stage updates
- Maintains stage history for audit

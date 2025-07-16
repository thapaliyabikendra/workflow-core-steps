# Start Workflow Instance Step

## Purpose
Starts a new workflow instance based on a workflow definition.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.StartWorkflowInstanceStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `ApplicationWorkflowInstanceId` (string): ID of the application workflow instance to start

### Outputs
- `WorkflowInstanceId` (Guid): ID of the newly created workflow instance

## Usage Example

```json
{
  "Id": "StartApplicationWorkflow",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.StartWorkflowInstanceStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "ProcessStartedWorkflow",
  "Inputs": {
    "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]"
  },
  "Outputs": {
    "NewWorkflowId": "step.WorkflowInstanceId"
  }
}
```

## Error Handling
- Validates workflow definition existence
- Ensures unique workflow instances
- Handles initialization errors
- Validates input parameters

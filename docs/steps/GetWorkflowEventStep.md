# Get Workflow Event Step

## Purpose
Retrieves workflow event details and status information.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.GetWorkflowEventStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `WorkflowEventId` (string): ID of the workflow event to retrieve
- `IncludeHistory` (boolean, optional): Whether to include event history

### Outputs
- `EventData` (object): The retrieved event data
- `EventStatus` (string): Current status of the event
- `EventHistory` (array, optional): Event status history if requested

## Usage Example

```json
{
  "Id": "CheckApprovalStatus",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GetWorkflowEventStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "ProcessApprovalResult",
  "Inputs": {
    "WorkflowEventId": "data[\"approvalEventId\"]",
    "IncludeHistory": true
  },
  "Outputs": {
    "ApprovalData": "step.EventData",
    "ApprovalStatus": "step.EventStatus",
    "StatusHistory": "step.EventHistory"
  }
}
```

## Error Handling
- Event existence validation
- Access permission verification
- History data pagination
- Cache management

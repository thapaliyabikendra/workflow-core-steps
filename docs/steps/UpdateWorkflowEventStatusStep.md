# Update Workflow Event Status Step

## Purpose
Updates the status of a workflow event based on progress or results.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateWorkflowEventStatusStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `WorkflowEventId` (string): ID of the workflow event to update
- `EventData` (JObject, Optional): Updated event data
- `CurrentUserDetail` (JObject, optional): User context information for impersonation during the update

### Outputs
None

## Usage Example

```json
{
  "Id": "UpdateEventStatus",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateWorkflowEventStatusStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "WorkflowEventId": "data[\"currentEventId\"]",
    "EventData": {
      "status": "completed",
      "completedAt": "DateTime.Now",
      "result": "data[\"processResult\"]"
    },
    "CurrentUserDetail": "data[\"currentUserDetail\"]"
  }
}
```

## Error Handling
- Validates event existence
- Handles concurrent event updates
- Maintains event history

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
- `EventData` (JObject): Updated event data

### Outputs
None

## Usage Example

```json
{
  "Id": "UpdateEventStatus",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateWorkflowEventStatusStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "ProcessNextStep",
  "Inputs": {
    "WorkflowEventId": "data[\"currentEventId\"]",
    "EventData": {
      "status": "completed",
      "completedAt": "DateTime.Now",
      "result": "data[\"processResult\"]"
    }
  }
}
```

## Error Handling
- Validates event existence
- Handles concurrent event updates
- Maintains event history

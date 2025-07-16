# Bulk Update Workflow Event Status Step

## Purpose
Updates the status of multiple workflow events simultaneously.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.BulkUpdateWorkflowEventStatusStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `WorkflowEvents` (List<UpdateWorkflowEventDto>): List of events to update
  - Each item contains:
    - `WorkflowEventId` (Guid): ID of the event
    - `EventData` (JObject): Updated event data

### Outputs
None

## Usage Example

```json
{
  "Id": "BulkUpdateEvents",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.BulkUpdateWorkflowEventStatusStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "ContinueProcess",
  "Inputs": {
    "WorkflowEvents": [
      {
        "WorkflowEventId": "data[\"event1Id\"]",
        "EventData": {
          "status": "completed",
          "timestamp": "DateTime.Now"
        }
      },
      {
        "WorkflowEventId": "data[\"event2Id\"]",
        "EventData": {
          "status": "completed",
          "timestamp": "DateTime.Now"
        }
      }
    ]
  }
}
```

## Error Handling
- Transaction management for bulk updates
- Partial success handling
- Retry mechanism for failed updates

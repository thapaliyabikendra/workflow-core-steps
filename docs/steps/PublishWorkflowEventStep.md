# Publish Workflow Event Step

## Purpose
Publishes workflow events to a message bus or event system for external consumption.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.PublishWorkflowEventStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `EventName` (string): Name of the event to publish
- `EventKey` (string): Key to identify the event
- `EventData` (JObject): Event payload data

### Outputs
None

## Usage Example

```json
{
  "Id": "PublishApprovalComplete",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PublishWorkflowEventStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "FinalizeWorkflow",
  "Inputs": {    "EventName": "\"APPROVAL_COMPLETED\"",
    "EventKey": "data[\"workflowInstanceId\"]",
    "EventData": {
      "requestId": "data[\"requestId\"]",
      "approvedBy": "data[\"approverId\"]",
      "approvedAt": "DateTime.Now",
      "decision": "data[\"approvalDecision\"]"
    }
  }
  }
}
```

## Error Handling
- Logs event publishing attempts
- Validates required parameters
- Handles event publishing errors

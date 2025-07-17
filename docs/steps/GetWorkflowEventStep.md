# Get Workflow Event Step

## Purpose
Retrieves workflow event details and status information.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.GetWorkflowEventStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `OperationWorkflowEventId` (string): The unique identifier of the application workflow to retrieve
- `IncludeHistory` (boolean, optional): Whether to include event history

### Outputs
- `Response` (object): JSON object containing:
  - `totalCount` (integer): Number of events retrieved.
  - `data` (array): List of workflow event DTOs.

## Usage Example

```json
{
  "Id": "CheckApprovalStatus",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GetWorkflowEventStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "ProcessApprovalResult",
  "Inputs": {
    "OperationWorkflowEventId": "data[\"operationWorkflowInstanceId\"]",
    "IncludeHistory": true
  },
  "Outputs": {
    "Response": "step.Response"
  }
}
```

## Error Handling
- Event existence validation
- Access permission verification
- History data pagination
- Cache management

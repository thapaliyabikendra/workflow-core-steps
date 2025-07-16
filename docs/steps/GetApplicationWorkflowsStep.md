# Get Application Workflows Step

## Purpose
Retrieves application workflow information and their current states.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.GetApplicationWorkflowsStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `OperationWorkflowId` (string): ID of the operation workflow instance to get associated application workflows for

### Outputs
- `Response` (JObject): Object containing application workflows data including:  - Total count of workflows
  - Application workflow instance details including:
    - Instance IDs
    - Current stages and status
    - Associated tasks and their states
    - Workflow metadata

## Usage Example

```json
{
  "Id": "RetrieveApplicationWorkflows",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GetApplicationWorkflowsStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "ProcessWorkflows",
  "Inputs": {
    "OperationWorkflowId": "data[\"operationWorkflowId\"]"
  },
  "Outputs": {
    "ApplicationWorkflows": "step.Response"
  }
}
```

## Error Handling
- Validates operation workflow existence
- Handles missing application workflows
- Pagination for large result sets
- Error details for failed retrievals

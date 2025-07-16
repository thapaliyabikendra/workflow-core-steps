# Get Application Instance Forms Step

## Purpose
Retrieves forms associated with a specific application workflow instance.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.GetApplicationInstanceFormsStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `OperationWorkflowInstanceId` (string): ID of the application workflow instance.

### Outputs
- `Response` (JObject): 

## Usage Example
```json
{
      "Id": "GetApplicationFormsData",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GetApplicationInstanceFormsStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "CheckApplicationDetails",
      "Inputs": {
        "OperationWorkflowInstanceId": "data[\"operationWorkflowInstanceId\"]"
      },
      "Outputs": {
        "applicationDetails": "step.Response"
      }    
}
```

## Error Handling
- Validates instance existence.
- Handles retrieval errors.
- Logs failures.
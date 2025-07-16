# Generate Link Step

## Purpose
Generates a secure or dynamic link for workflow tasks or notifications.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.GenerateLinkStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `FormSlug` (string): The base URL for the link.
- `Payload` (object): Query parameters or path variables to append.

### Outputs
- `SecureUrl` (string): The generated link.

## Usage Example
```json
{
  "Id": "GenerateLink",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GenerateLinkStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "SendLink",
  "Inputs": {
    "FormSlug": "add-employees",
    "Payload": {
      "UserId": "310",
      "WorkflowId": "96549bc9-c52e-4640-9f52-bd57652265ad",
      "RequiresLogin": true,
      "Expiration": "2025-03-21"
    }
  },
  "Outputs": {
    "Response": "step.Data"
  }
}
```

## Error Handling
- Validates URL and parameters.
- Handles link generation errors.
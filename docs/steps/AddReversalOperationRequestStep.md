# Add Reversal Operation Request Step

## Purpose  
Creates a reversal operation request using a given operation workflow instance ID and optional form data. It can impersonate a specific user context during execution for audit/logging purposes.

## Step Type  
```
Amnil.AccessControlManagementSystem.Workflows.Steps.AddReversalOperationRequestStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs

- `OperationWorkflowInstanceId` (`string`): The ID of the original workflow instance for which a reversal operation is being initiated.
- `OperationForms` (`JObject`, optional): Operation-related form data to be included in the reversal request.
- `ApplicationForms` (`JObject`, optional): Application-level form data related to the reversal.
- `CurrentUserDetail` (`JObject`): Custom user context data used for impersonation during request execution.

### Outputs

- `OperationReversalWorkflowInstanceId` (`string`): The ID of the newly created reversal workflow instance.

## Usage Example

```json
{
  "Id": "AddOperationRequest",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.AddReversalOperationRequestStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "PrintApplicationTemplate",
  "Inputs": {
    "OperationWorkflowInstanceId": "data[\"operationWorkflowInstanceId\"]",
    "OperationForms": {
      "userAccountForm": {
        "userAccountIdentifier": "7002"
      }
    },
    "ApplicationForms": {
      "applicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
      "applicationForms": {
        "userAccountForm": {
          "userIdentifier": "min@yopmail.com"
        }
      }
    },
    "CurrentUserDetail": "data[\"currentUserDetail\"]"
  },
  "Outputs": {
    "OperationWorkflowInstanceId": "step.OperationReversalWorkflowInstanceId"
  }
}
```

## Error Handling

- Missing or Invalid OperationWorkflowInstanceId 
- API Call Failure
- Unhandled Exceptions
- Logging

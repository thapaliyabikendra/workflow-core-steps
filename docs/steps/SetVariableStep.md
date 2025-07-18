# Set Variable Step

## Purpose
Sets values in workflow variables that can be accessed throughout the workflow execution.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.SetVariableStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `ApplicationWorkflowInstanceId` (string): The unique identifier for the workflow instance.
- `VariableName` (string): Name of the variable to set
- `VariableValue` (object): Value to store in the variable
- `Scope` (string, optional): Scope of the variable (e.g., "Workflow", "Instance")
- `CurrentUserDetail` (JObject, optional): Current user context for impersonation during variable save

### Outputs
None

## Usage Example

```json
{
  "Id": "StoreUserData",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.SetVariableStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
    "VariableName": "\"ApprovalStatus\"",
    "VariableValue": "data[\"approvalStatus\"]",
    "CurrentUserDetail": "data[\"currentUserDetail\"]"
  }
}
```

## Error Handling
- Validates variable name and value
- Handles concurrent variable access
- Memory usage monitoring for large variables

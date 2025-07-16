# Set Variable Step

## Purpose
Sets values in workflow variables that can be accessed throughout the workflow execution.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.SetVariableStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `VariableName` (string): Name of the variable to set
- `Value` (object): Value to store in the variable
- `Scope` (string, optional): Scope of the variable (e.g., "Workflow", "Instance")

### Outputs
- `Success` (boolean): Indicates if the variable was set successfully

## Usage Example

```json
{
  "Id": "StoreUserData",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.SetVariableStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "ProcessUserData",
  "Inputs": {
    "VariableName": "userData",
    "Value": {
      "userId": "data[\"currentUserId\"]",
      "timestamp": "DateTime.Now"
    },
    "Scope": "Instance"
  }
}
```

## Error Handling
- Validates variable name and value
- Handles concurrent variable access
- Memory usage monitoring for large variables

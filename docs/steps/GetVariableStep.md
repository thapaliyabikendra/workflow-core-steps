# Get Variable Step

## Purpose
Retrieves values from workflow variables stored in the workflow context.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.GetVariableStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `VariableName` (string): Name of the variable to retrieve
- `DefaultValue` (object, optional): Default value if variable is not found

### Outputs
- `Value` (object): The retrieved variable value

## Usage Example

```json
{
  "Id": "GetUserPreferences",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GetVariableStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "ProcessPreferences",
  "Inputs": {
    "VariableName": "\"staffId\"",
    "DefaultValue": "{}"
  },
  "Outputs": {
    "staffIdData": "step.VariableValue.staffId"
  }
}
```

## Error Handling
- Returns default value if variable not found
- Type conversion errors are handled gracefully
- Variable access permissions are validated

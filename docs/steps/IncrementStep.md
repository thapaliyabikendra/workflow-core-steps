# Increment Step

## Purpose
Increments a numeric counter value in the workflow context to perform basic arithmetic operation.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.IncrementStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `VariableName` (string): Name of the variable to increment
- `IncrementBy` (number, optional): Amount to increment by (default: 1)
- `InitialValue` (number, optional): Initial value if variable doesn't exist (default: 0)

### Outputs
- `NewValue` (number): The incremented value

## Usage Example

```json
{
  "Id": "IncrementRetryCount",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.IncrementStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "VariableName": "retryCount",
    "IncrementBy": 1,
    "InitialValue": 0
  },
  "Outputs": {
    "CurrentRetries": "step.NewValue"
  }
}
```

## Error Handling
- Handles non-numeric values
- Overflow protection
- Variable access validation

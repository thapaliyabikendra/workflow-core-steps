# Validate Rules Step

## Purpose
Validates business rules and conditions against workflow data.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.ValidateRulesStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `RuleName` (string): Name of the rule set to validate
- `InputData` (object): Data to validate against rules
- `Parameters` (object, optional): Additional parameters for rule evaluation

### Outputs
- `Response` (object): JSON object containing validation results:
  - `IsValid` (boolean): Whether validation passed
  - `ValidationErrors` (array): List of validation errors if any
  - `ValidationResult` (object): Detailed validation results

## Usage Example

```json
{
  "Id": "ValidateTransferRequest",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.ValidateRulesStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "ProcessValidRequest",
  "Inputs": {
    "RuleSet": "\"TransferRequestRules\"",
    "InputData": "data[\"transferRequest\"]",
    "Parameters": {
      "maxAmount": 1000000,
      "allowedDepartments": ["HR", "Finance", "IT"]
    }
  },
  "Outputs": {
    "Response": "step.Response[\"isValidated\"]"
  }
}
```

## Error Handling
- Rule syntax validation
- Missing rule set handling
- Performance monitoring for complex rules
- Custom error messages support

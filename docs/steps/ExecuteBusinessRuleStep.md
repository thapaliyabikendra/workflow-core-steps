# Execute Business Rule Step

## Purpose
Executes business rules using the business rule engine service to apply dynamic business logic and validation during workflow execution.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.ExecuteBusinessRuleStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `RuleName` (string): The name of the business rule to execute
  - Must match a registered business rule in the business rule engine
- `Input1` (JObject): The input data object to pass to the business rule
  - Contains the data that the business rule will evaluate

### Outputs
- `Result` (BusinessRuleResultDto): The result returned from the business rule execution
  - `Success` (bool): Indicates if the business rule execution was successful
  - `Data` (object): Contains the result data from the business rule
  - `ValidationMessages` (string[]): Array of validation error messages
  - `Warnings` (string[]): Array of warning messages

## Usage Example

### User ID Generation and Validation

```json
{
  "Id": "GenerateAndValidateUserId",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.ExecuteBusinessRuleStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "RuleName": "ECC_RTG_SIPS_USERID_GENERATION",
    "Input1": {
      "staffId": "data[\"staffId\"]",
      "firstName": "data[\"firstName\"]",
      "lastName": "data[\"lastName\"]"
    }
  },
  "Outputs": {
    "GeneratedUserId": "step.Result.Data?.userId",
    "IsValid": "step.Result.Success",
    "ValidationErrors": "step.Result.ValidationMessages",
    "UserIdWarnings": "step.Result.Warnings"
  }
}
```

## Business Rule Result Structure

```csharp
public class BusinessRuleResultDto
{
    public bool Success { get; set; }
    public object? Data { get; set; }
    public string[]? ValidationMessages { get; set; }
    public string[]? Warnings { get; set; }
}
```

## Error Handling
- Invalid rule names are logged as warnings and the step continues execution
- Null or empty input data is logged as warnings and the step continues execution
- Business rule execution exceptions are logged and re-thrown for workflow error handling
- Network or service unavailability errors trigger retry mechanisms if configured

## Related Steps
- [Validate Rules Step](./ValidateRulesStep.md) - For rule-based validation
- [Print Message Step](./PrintMessageStep.md) - For logging business rule results
- [Set Variable Step](./SetVariableStep.md) - For storing business rule outputs 
# Generate Password Step

## Purpose  
Generates a random password based on specified input criteria using the `IGeneratePasswordService`.

## Step Type 
```
Amnil.AccessControlManagementSystem.Workflows.Steps.GeneratePasswordStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs

- `Length` (int): Length of the password to generate.
- `IncludeLowercase` (bool): Whether to include lowercase letter.
- `IncludeUppercase` (bool): Whether to include uppercase letters.
- `IncludeNumbers` (bool): Whether to include numeric characters.
- `IncludeSpecialCharacters` (bool): Whether to include special characters.

### Outputs
- `Password` (string): The generated password.

## Usage Example
```json
{
  "Id": "GenerateRandomPassword",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GeneratePasswordStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "Length": 12,
    "IncludeLowercase": true,
    "IncludeUppercase": true,
    "IncludeNumbers": true,
    "IncludeSpecialCharacters": true
  },
  "Outputs": {
    "GeneratedPassword": "step.Password"
  }
}
```

## Error Handling
- Invalid Input Values
- Service Failure
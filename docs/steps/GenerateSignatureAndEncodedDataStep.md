# Generate Signature And Encoded Data Step

## Purpose
Generates digital signatures and encodes data for secure data transmission or verification.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.GenerateSignatureAndEncodedDataStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `FunctionName` (string): Identifier for the remote function (e.g., "SolChange").
- `FileName` (string): Name of the .pem file containing the RSA private key, located in /app/Files/.
- `ApplicationFormData` (JObject): JSON object expected to contain a SolChangeForm sub-object with necessary fields.
- `ApplicationWorkflowInstanceId` (string): The unique identifier for the workflow instance.
- `TransactionId` (string): The unique transaction identifier.

### Outputs
- `EncodedRequestData` (JObject): The generated object with the following structure:
  - `FunctionName`: Same as input.
  - `Data`: Base64-encoded version of the serialized request.
  - `Signature`: RSA SHA256 signature of the payload.

## Usage Example

```json
{
  "Id": "GenerateSolChangeEncodedData",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GenerateSignatureAndEncodedDataStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "SolAPICallStep",
  "Inputs": {
    "FunctionName": "\"SolChange\"",
    "TransactionId": "data[\"TransactionId\"]",
    "FileName": "\"PrivateKey_20241224125743.pem\"",
    "ApplicationFormData": "data[\"applicationFormData\"]",
    "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]"
  },
  "Outputs": {
    "EncodedRequestData": "step.EncodedRequestData"
  }
}
```

## Error Handling
- Validates input data format
- Handles encoding errors
- Secure key management
- Signature verification

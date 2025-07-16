# Generate Signature And Encoded Data Step

## Purpose
Generates digital signatures and encodes data for secure data transmission or verification.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.GenerateSignatureAndEncodedDataStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `Data` (object): Data to be signed and encoded
- `SigningKey` (string): Key used for generating signature
- `EncodingType` (string, optional): Type of encoding to use (default: "Base64")

### Outputs
- `Signature` (string): Generated signature
- `EncodedData` (string): Encoded data
- `Timestamp` (string): Timestamp of signature generation

## Usage Example

```json
{
  "Id": "SignAndEncodeRequest",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GenerateSignatureAndEncodedDataStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "SendToExternalSystem",
  "Inputs": {
    "Data": "data[\"requestPayload\"]",
    "SigningKey": "\"YOUR_SIGNING_KEY\"",
    "EncodingType": "\"Base64\""
  },
  "Outputs": {
    "RequestSignature": "step.Signature",
    "EncodedPayload": "step.EncodedData",
    "SignedAt": "step.Timestamp"
  }
}
```

## Error Handling
- Validates input data format
- Handles encoding errors
- Secure key management
- Signature verification

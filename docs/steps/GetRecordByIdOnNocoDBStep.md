# Get Record By Id On NocoDB Step

## Purpose
Retrieves a specific record from a NocoDB table using its unique identifier.

## Step Type
Amnil.AccessControlManagementSystem.Workflows.Steps.GetRecordByIdOnNocoDBStep, Amnil.AccessControlManagementSystem.Application

## Parameters

### Inputs
- `TableName` (string): The name of the NocoDB table.
- `Id` (string): The unique identifier of the record to retrieve.

### Outputs
- `Data` (JObject): The retrieved record object.

## Usage Example
```json
{
  "Id": "NocoDBRecordStep",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GetRecordByIdOnNocoDBStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "PrintApplicationTemplate",
  "Inputs": {
    "TableName": "\"RPAJobs\"",
    "Id": "5g"
  },
  "Outputs": {
    "Data": "step.Data"
  }
}
```

## Error Handling
- Validates table and record existence.
- Handles retrieval errors.
- Logs failures.
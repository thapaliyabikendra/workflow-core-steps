# Add NocoDB Record Step

## Purpose
Adds a new record to a NocoDB table from workflow data.

## Step Type
Amnil.AccessControlManagementSystem.Workflows.Steps.AddNocoDBRecordStep, Amnil.AccessControlManagementSystem.Application

## Parameters

### Inputs
- `TableName` (`string`): Name of the NocoDB table.
- `Data` (`JObject`): Data to insert as a new record.
- `CurrentUserDetail` (`JObject`, Optional): JSON object with user context to impersonate while inserting.

### Outputs
- `Id` (string): The ID of the newly created record.

## Usage Example
```json
{
  "Id": "AddRecordToNocoDB",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.AddNocoDBRecordStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "TableName": "\"RPAJobs\"",
    "Data": {
      "RoleCode": "310",
      "EmployeeId": "EID208",
      "RequestFrom": "2025-03-17",
      "RequestTo": "2025-03-21"
    },
    "CurrentUserDetail": "data[\"currentUserDetail\"]"
  },
  "Outputs": {
    "Id": "step.Id"
  }
}
```

## Error Handling
- Validates table existence.
- Handles data format errors.
- Logs insertion failures.
# Delete Record On NocoDB Step

## Purpose
Deletes a record from a NocoDB table based on record ID.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.DeleteRecordOnNocoDBStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `TableName` (`string`): Name of the NocoDB table.
- `Id` (`string`): ID of the record to delete.
- `CurrentUserDetail` (`JObject`, optional): Current user context for impersonation during deletion

### Outputs
- `Data` (string): ID of the record deleted.

## Usage Example
```json
{
  "Id": "DeleteNocoDBRecord",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.DeleteRecordOnNocoDBStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "TableName": "\"Customers\"",
    "Id": "Vm",
    "CurrentUserDetail": "data[\"currentUserDetail\"]"
  },
  "Outputs": {
    "Response": "step.Data"
  }
}
```

## Error Handling
- Validates record existence.
- Handles deletion errors.
- Logs failures.
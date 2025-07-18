# Get Record On NocoDB Step

## Purpose
Retrieves records from a NocoDB table based on specified filter criteria.

## Step Type
Amnil.AccessControlManagementSystem.Workflows.Steps.GetRecordOnNocoDBStep, Amnil.AccessControlManagementSystem.Application

## Parameters

### Inputs
- `TableName` (string): The name of the NocoDB table.
- `NocoDbFilterParams` (object): The filter criteria to apply when retrieving records: 
  - `fields`(`string` or `null`): Specific fields to retrieve from the record. null will fetch all fields.
  - `where` (``string`): Conditional filter in NocoDB syntax.
  - `offset` (`string`): Used for pagination. Skips the specified number of records.
  - `limit` (`string`): Limits the number of records returned.
  - `sort` (`string`): Sorting criteria
  - `viewId` (string): View identifier, if applicable.

### Outputs
- `Data` (JObject): The retrieved record(s) matching the filter.

## Usage Example
```json
{
  "Id": "NocoDBRecordStep",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GetRecordOnNocoDBStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "TableName": "\"RPAJobs\"",
    "NocoDbFilterParams": {
      "fields": null,
      "where": "",
      "offset": "",
      "limit": "",
      "sort": "",
      "viewId": ""
    }
  },
  "Outputs": {
    "Data": "step.Data"
  }
}
```

## Error Handling
- Validates table existence.
- Handles filter and retrieval errors.
- Logs failures.
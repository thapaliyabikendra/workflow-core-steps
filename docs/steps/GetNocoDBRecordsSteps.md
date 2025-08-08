# Get Record On NocoDB Step

## Purpose

Retrieves records from a NocoDB table based on specified filter criteria.

## Step Type

Amnil.AccessControlManagementSystem.Workflows.Steps.GetRecordOnNocoDBStep, Amnil.AccessControlManagementSystem.Application

## Parameters

### Inputs

- `TableName` (string, required): The name of the NocoDB table to query
- `NocoDbFilterParams` (JObject, optional): The filter criteria to apply when retrieving records: 
  - `fields`(`string` or `null`): Specific fields to retrieve from the record. null will fetch all fields.
  - `where` (``string`): Conditional filter in NocoDB syntax.
  - `offset` (`string`): Used for pagination. Skips the specified number of records.
  - `limit` (`string`): Limits the number of records returned.
  - `sort` (`string`): Sorting criteria
  - `viewId` (string): View identifier, if applicable.
- `ResultType` (string, optional): Type of result to return. Default is "list". Options:
  - `"list"`: Returns all matching records as an array
  - `"first"`: Returns only the first matching record
  - `"last"`: Returns only the last matching record

### Outputs

- `Data` (JObject): The retrieved data in the specified format

## Usage Examples

### Basic List Query

```json
{
  "Id": "GetUserRecords",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GetNocoDBRecordsSteps, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "ProcessUserData",
  "Inputs": {
    "TableName": "\"Users\"",
    "NocoDbFilterParams": {
      "fields": null,
      "where": "(status,eq,active)",
      "offset": "",
      "limit": "",
      "sort": "",
      "viewId": ""
    },
    "ResultType": "\"list\""
  },
  "Outputs": {
    "userRecords": "step.Data"
  }
}
```

### Get First Record

```json
{
  "Id": "GetFirstUser",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GetNocoDBRecordsSteps, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "ProcessUser",
  "Inputs": {
    "TableName": "\"Users\"",
    "NocoDbFilterParams": {
      "fields": null,
      "where": "(email,eq,john@example.com)",
      "offset": "",
      "limit": "",
      "sort": "",
      "viewId": ""
    },
    "ResultType": "\"first\""
  },
  "Outputs": {
    "userRecord": "step.Data.item"
  }
}
```

### Get Last Record

```json
{
  "Id": "GetLastUser",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GetNocoDBRecordsSteps, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "ProcessUser",
  "Inputs": {
    "TableName": "\"Users\"",
    "NocoDbFilterParams": {
      "fields": null,
      "where": "(department,eq,IT)",
      "offset": "",
      "limit": "",
      "sort": "",
      "viewId": ""
    },
    "ResultType": "\"last\""
  },
  "Outputs": {
    "lastUser": "step.Data.item"
  }
}
```

## Response Formats

### List Response

```json
{
  "list": [
    {
      "id": 1,
      "name": "John Doe",
      "email": "john@example.com"
    },
    {
      "id": 2,
      "name": "Jane Smith",
      "email": "jane@example.com"
    }
  ],
  "totalCount": 2
}
```

### First/Last Response

```json
{
  "item": {
    "id": 1,
    "name": "John Doe",
    "email": "john@example.com"
  }
}
```

### Empty Response (when no records found)

```json
{
  "list": [],
  "totalCount": 0
}
```

## Error Handling

- Validates table existence.
- Handles filter and retrieval errors.
- Logs failures.
- Returns empty results instead of throwing exceptions.
- Continues workflow execution even when errors occur.

## Filter Parameters Examples

### Basic Where Clause

```json
{
  "NocoDbFilterParams": {
    "fields": null,
    "where": "(status,eq,active)",
    "offset": "",
    "limit": "",
    "sort": "",
    "viewId": ""
  }
}
```

### Multiple Conditions

```json
{
  "NocoDbFilterParams": {
    "fields": null,
    "where": "(status,eq,active)~and(department,eq,IT)",
    "offset": "",
    "limit": "",
    "sort": "",
    "viewId": ""
  }
}
```

### With Pagination

```json
{
  "NocoDbFilterParams": {
    "fields": null,
    "where": "(status,eq,active)",
    "offset": "0",
    "limit": "10",
    "sort": "",
    "viewId": ""
  }
}
```

### With Sorting

```json
{
  "NocoDbFilterParams": {
    "fields": null,
    "where": "(status,eq,active)",
    "offset": "",
    "limit": "",
    "sort": "name,asc",
    "viewId": ""
  }
}
```

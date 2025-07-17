# Update Record On NocoDB Step

## Purpose
Updates an existing record in a NocoDB table using the provided data and record identifier.

## Step Type
Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateRecordOnNocoDBStep, Amnil.AccessControlManagementSystem.Application

## Parameters

### Inputs
- `TableName` (string): The name of the NocoDB table.
- `Data` (object): The data to update in the record.
- `CurrentUserDetail` (JObject, optional): Detailed user context for impersonation during update.

### Outputs
- `Id` (string): The record id of the data updated.

## Usage Example
```json
{
  "Id": "UpdateNocoDBRecordStep",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateRecordOnNocoDBStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "TableName": "\"FinancleRoleChangeApiRequests\"",
    "Data": {
      "@ApiClientName": "\"GET_MBL_APPLICATIONS_API_DUMMY_TEST\"",
      "@WorkflowId": "",
      "@AppTaskWorkflowId": "data[\"applicationWorkflowInstanceId\"]",
      "@Status": true
    },
    "CurrentUserDetail": "data[\"currentUserDetail\"]"
  },
  "Outputs": {
    "Id": "step.Id"
  }
}
```

## Error Handling
- Validates table and record existence.
- Handles update errors.
- Logs failures.
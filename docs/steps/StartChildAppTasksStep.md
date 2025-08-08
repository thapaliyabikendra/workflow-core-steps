# Start Child App Tasks Step

## Purpose

Retrieves child workflow configurations for a given operation workflow configuration ID and returns them as structured data.

## Step Type

```
Amnil.AccessControlManagementSystem.Workflows.Steps.StartChildAppTasksStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs

- `OperationWorkflowConfigurationId` (string, required): The GUID of the operation workflow configuration to find child configurations for

### Outputs

- `Data` (JObject, optional): Contains the child workflow configurations with total count and data array

## Usage Example

```json
{
  "Id": "GetChildWorkflows",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.StartChildAppTasksStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "ProcessChildWorkflows",
  "Inputs": {
    "OperationWorkflowConfigurationId": "\"550e8400-e29b-41d4-a716-446655440000\""
  },
  "Outputs": {
    "childWorkflows": "step.Data"
  }
}
```

## Error Handling

- **Empty Configuration ID**: If OperationWorkflowConfigurationId is null or empty, logs error and continues workflow execution
- **No Child Configurations**: Returns empty result with totalCount = 0 when no child configurations are found
- **API Errors**: Logs detailed error information and throws exception to stop workflow execution
- **Invalid GUID**: Throws exception if the configuration ID is not a valid GUID format
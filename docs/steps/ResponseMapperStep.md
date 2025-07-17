# Response Mapper Step

## Purpose
Maps API response data to workflow variables using predefined mapping rules.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.ResponseMapperStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `ApiResponse` (JObject): The API response to map that will be processed by the ResponseMappingWorkflow ruleset

### Outputs
- `MappedResponse` (JObject): The mapped response data according to rules

## Usage Example

```json
{
  "Id": "MapApiResponse",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.ResponseMapperStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {    
    "ApiResponse": "data[\"rawApiResponse\"]"
  },
  "Outputs": {
    "CustomerData": "step.MappedResponse"
  }
}
```

## Error Handling
- Validates response data format
- Handles missing fields gracefully
- Maps complex nested structures
- Validates rule set existence
- Custom error messages for mapping failures

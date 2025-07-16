# Map Data Step

## Purpose  
Logs and maps arbitrary data (`JObject`) for traceability or transformation across workflow steps.

## Step Type  
```
Amnil.AccessControlManagementSystem.Workflows.Steps.MapDataStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `Data` (JObject): JSON object to pass through or log.

### Outputs
None

## Usage Example

```json
{
  "Id": "MapIntermediateData",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.MapDataStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "NextBusinessStep",
  "Inputs": {
    "Data": {
      "userId": "data[\"currentUser\"].id",
      "timestamp": "DateTime.UtcNow"
    }
  }
}
```

## Error Handling
- Invalid or null data
- Logging Failures


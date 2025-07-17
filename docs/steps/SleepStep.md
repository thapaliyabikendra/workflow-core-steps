# Sleep Step

## Purpose
Introduces a delay in workflow execution for rate limiting, cooling periods, or synchronization.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.SleepStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `Duration` (TimeSpan/string): Duration to sleep
  - Can be specified as a TimeSpan or a string like "00:00:30" for 30 seconds
- `Reason` (string, optional): Description of why the sleep is needed

### Outputs
None

## Usage Example

```json
{
  "Id": "WaitForProcessing",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.SleepStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "Duration": "\"00:00:30\"",
    "Reason": "\"Waiting for external system to process the request\""
  }
}
```

## Error Handling
- Validates duration format
- Handles workflow cancellation during sleep
- Maximum sleep duration limits

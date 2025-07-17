# Generate Task ID Step

## Purpose
Generates a unique task identifier for workflow tasks.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.GenerateTaskIdStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
None

### Outputs
- `TaskId` (string): The generated unique task identifier

## Usage Example

```json
{
  "Id": "GenerateNewTaskId",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GenerateTaskIdStep, Amnil.AccessControlManagementSystem.Application",
  "Outputs": {
    "GeneratedId": "step.TaskId"
  }
}
```

## Error Handling
- Ensures uniqueness of generated IDs
- Validates format strings
- Handles sequence overflow
- Thread-safe generation

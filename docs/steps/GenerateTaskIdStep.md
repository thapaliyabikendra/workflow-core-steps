# Generate Task ID Step

## Purpose
Generates a unique task identifier for workflow tasks.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.GenerateTaskIdStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `Prefix` (string, optional): Prefix for the task ID
- `Format` (string, optional): Custom format for the task ID
- `UseTimestamp` (boolean, optional): Whether to include timestamp in the ID

### Outputs
- `TaskId` (string): The generated unique task identifier

## Usage Example

```json
{
  "Id": "GenerateNewTaskId",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GenerateTaskIdStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "ProcessTask",
  "Inputs": {
    "Prefix": "\"TASK\"",
    "Format": "\"TASK-{timestamp}-{sequence}\"",
    "UseTimestamp": true
  },
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

# Print Message Step

## Purpose
Logs messages during workflow execution for debugging and monitoring purposes.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `Message` (string): The message to be logged
- `LogLevel` (string, optional): Log level (e.g., "Information", "Warning", "Error")

### Outputs
None

## Usage Example

```json
{
  "Id": "LogWorkflowStatus",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "ContinueWorkflow",
  "Inputs": {
    "Message": "\"Workflow status: \" + data[\"workflowStatus\"] + \" for ApplicationId: \" + data[\"applicationId\"]",
    "LogLevel": "\"Information\""
  }
}
```

## Error Handling
- Handles message formatting errors
- Validates log level values
- Ensures logging service availability

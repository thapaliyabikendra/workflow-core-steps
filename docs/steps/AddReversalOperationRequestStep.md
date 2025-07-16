# Add Reversal Operation Request Step

## Purpose
Step for temporary transfer.

## Step Type
Amnil.AccessControlManagementSystem.Workflows.Steps.AddReversalOperationRequestStep, Amnil.AccessControlManagementSystem.Application

## Parameters

### Inputs
- `OperationWorkflowInstanceId` (string): The name of the NocoDB table to update.
- `OperationForms` (JObject): A JSON object representing the data to update.
- `ApplicationForms` (JObject): A JSON object representing the data to update
- `CurrentUserDetail` (JObject)

### Output
- `Id` (string): The ID of the created record.

## Usage Example
```json
{
  "Id": "AddOperationRequest",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.AddReversalOperationRequestStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "PrintApplicationTemplate",
  "Inputs": {
    "OperationWorkflowInstanceId": "data[\"operationWorkflowInstanceId\"]",
    "OperationForms": {
        "userAccountForm": {
            "userAccountIdentifier": "7002"
        }
    },
    "ApplicationForms": {
        "applicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "applicationForms": {
            "userAccountForm": {
                "userIdentifier": "min@yopmail.com"
            }
        }
    },
    "CurrentUserDetail": "data[\"currentUserDetail\"]"
  },
  "Outputs": {
    "OperationWorkflowInstanceId": "step.Response"
  }
}
```

## Error Handling
- Missing or invalid `OperationWorkflowInstanceId`  
- Incomplete `OperationForms` / `ApplicationForms`  
- Duplicate reversal request creation attempts  

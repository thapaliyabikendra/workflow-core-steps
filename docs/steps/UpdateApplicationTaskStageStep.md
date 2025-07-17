# Update Application Task Stage Step

## Purpose
Updates the stage/status of an application task in the workflow process.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `ApplicationWorkflowInstanceId` (string): ID of the application workflow instance
- `StageName` (string): Name of the new stage
- `SubStageName` (string, optional): Name of the sub-stage
- `Remarks` (string, optional): Additional remarks about the stage change

### Outputs
None

## Usage Example

```json
{
  "Id": "UpdateTaskToApprovalStage",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
    "StageName": "\"APPROVAL_PENDING\"",
    "SubStageName": "\"MANAGER_APPROVAL\"",
    "Remarks": "\"Application sent for manager approval\""
  }
}
```

## Allowed Stages and Sub-Stages
- `COMPLETED`
  - `LINE_MANAGER_APPROVED`
  - `APPLICATION_ACTION_SUCCESS`
  - `CHECKER_APPROVED`
- `DRAFT_REQUESTED`
- `FAILED`
  - `APPLICATION_ACTION_FAILED`
  - `CHECKER_REJECTED`
- `FORWARDED`
  - `APPLICATION_FORWARDED`
- `PROCESSING`
  - `APPROVAL_REQUEST_IN_PROGRESS`
  - `RPA_JOBS_IN_PROCESSING`
  - `APPLICATION_IN_PROCESSING`
  - `APPLICATION_ACTION_JOB_IN_PROGRESS`
- `REQUESTED`
  - `APPLICATION_ACTION_TRIGGERED`
  - `APPROVAL_REQUESTED`
  - `MANUAL_ACTION_REQUIRED`
- `RESUME`
- `SCHEDULE`
- `STARTED`
  - `APPLICATION_STARTED`
- `SUSPENDED`
  - `APPLICATION_ACTION_SUSPENDED`
- `TEMPORARY`
  - `APPLICATION_ACTION_TEMPORARY`
- `TERMINATE`
- `TESTHERE`

## Error Handling
- Validates stage transitions
- Handles concurrent stage updates
- Throws exception to halt workflow execution if error occurs.

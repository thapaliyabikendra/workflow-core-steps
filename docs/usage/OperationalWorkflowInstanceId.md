
# OperationalWorkflowInstanceId

The `operationalWorkflowInstanceId` is a unique identifier for an instance of an operational workflow. It is typically passed as part of the data payload to a workflow instance when it is started.

## Origin

The `operationalWorkflowInstanceId` is expected to be present in the `data` object available to the workflow steps. It is usually injected into the workflow context when the workflow is initiated.

Example from `docs/samples/EmployeeTransferWorkflow.md`:

```json
{
    "Id": "UpdateOStep",
    "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateOperationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
    "NextStepId": "PrintWorkflowCompleteMessage",
    "Inputs": {
        "OperationWorkflowInstanceId": "data[\"operationWorkflowInstanceId\"]",
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "Stage": "COMPLETED",
        "Remarks": "\"Operation Workflow has completed\""
    }
}
```

In this example, the `UpdateOperationTaskStageStep` receives the `operationalWorkflowInstanceId` from the workflow's data context (`data["operationWorkflowInstanceId"]`).

## Usage

The `operationalWorkflowInstanceId` is used by several workflow steps to identify and act upon a specific operational workflow.

### `UpdateOperationTaskStageStep`

This step uses `operationalWorkflowInstanceId` to update the stage of a specific operational workflow instance.

### `GetApplicationWorkflowsStep`

This step uses a similar identifier, `OperationWorkflowId`, to retrieve all application workflows associated with a given operational workflow. It's likely that `operationWorkflowInstanceId` from one workflow would be used as the `OperationWorkflowId` for this step.

From `docs/steps/GetApplicationWorkflowsStep.md`:

**Inputs:**
* `OperationWorkflowId` (string): ID of the operation workflow instance to get associated application workflows for. 
# ApplicationWorkflowInstanceId

The `ApplicationWorkflowInstanceId` is a unique identifier for an instance of an application workflow. It is typically passed as part of the data payload to a workflow instance when it is started and is used extensively throughout the workflow system to track and manage application-specific workflow instances.

## Origin

The `ApplicationWorkflowInstanceId` is expected to be present in the `data` object available to the workflow steps. It is usually injected into the workflow context when the workflow is initiated.

Example from `docs/samples/EmployeeTransferWorkflow.md`:

```json
{
    "Id": "UpdateARequestedWorkflowStageStep",
    "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
    "NextStepId": "CallBPMAPI",
    "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "Stage": "REQUESTED",
        "Remarks": "\"Approval Requested for task id: \" + data[\"applicationWorkflowInstanceId\"]"
    }
}
```

In this example, the `UpdateApplicationTaskStageStep` receives the `ApplicationWorkflowInstanceId` from the workflow's data context (`data["applicationWorkflowInstanceId"]`).

## Usage

The `ApplicationWorkflowInstanceId` is used by numerous workflow steps to identify and act upon a specific application workflow instance.

## Logging and Messaging

The `ApplicationWorkflowInstanceId` is frequently used in logging and messaging to provide context about which application workflow instance is being processed:

- `"Requested - Task Id: " + data["applicationWorkflowInstanceId"]`
- `"Approval Requested for task id: " + data["applicationWorkflowInstanceId"]`
- `"Workflow {OperationStatus}, for ApplicationWorkflowInstanceId: {applicationWorkflowInstanceId}"`

## Relationship with Operational Workflows

The `ApplicationWorkflowInstanceId` often works in conjunction with `OperationWorkflowInstanceId`. While the application workflow instance handles application-specific logic, the operational workflow instance manages broader operational concerns. Both identifiers are frequently used together in steps that need to coordinate between these two workflow types. 
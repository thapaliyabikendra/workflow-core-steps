## Workflow Definition

```json
{
  "Id": "ECCIPSASBASolChangePermanentTransferApproval",
  "Version": 2,
  "DataType": "Amnil.AccessControlManagementSystem.Workflows.DynamicData, Amnil.AccessControlManagementSystem.Application.Contracts",
  "Steps": [
    {
      "Id": "PrintUserEmail",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "GetEmployeeDetails",
      "Inputs": {
        "Message": "\"Requested for application- Task ID: \" + data[\"applicationWorkflowInstanceId\"] + data[\"currentUserDetail\"].Email"
      }
    },
    {
      "Id": "GetEmployeeDetails",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "ExtractBranchId",
      "Inputs": {
        "ApiRequest": {
          "@employeeEmail": "data[\"currentUserDetail\"].Email"
        },
        "ApiClientName": "\"NOCODB_NMB_GET_EMPLOYEE_DETAILS_BY_EMAIL\""
      },
      "Outputs": {
        "employeeDetails": "step.Response[\"data\"]"
      }
    },
    {
      "Id": "ExtractBranchId",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "BranchApprovalFlow",
      "Inputs": {
        "Message": "\"Branch ID: \" + data[\"employeeDetails\"].branchId"
      }
    },
    {
      "Id": "BranchApprovalFlow",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "GetPMUserId",
      "Inputs": {
        "ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",
        "StageName": "\"REQUESTED\"",
        "SubStageName": "\"APPROVAL_REQUESTED\"",
        "Remarks": "\"Requested for application- Task ID: \" + data[\"applicationWorkflowInstanceId\"] + data[\"currentUserDetail\"].Email"
      }
    },
    {
      "Id": "GetPMUserId",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "PrintBranchApprovalCreatePMRequestInputs",
      "Inputs": {
        "ApiClientName": "\"GET_PM_USERS_API\"",
        "ApiRequest": {
          "@email": "data[\"currentUserDetail\"].Email"
        }
      },
      "Outputs": {
        "PMUserId": "step.Response[\"data\"]"
      }
    },
    {
      "Id": "PrintBranchApprovalCreatePMRequestInputs",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "PrintApplicationFormData",
      "Inputs": {
        "Message": "\"User ID: \" + data[\"PMUserId\"].processMakerUid + \"Staff Name: \" + data[\"operationFormData\"].userAccountForm.userAccountDetails.userAccountName + \"Existing Branch: \" + data[\"operationFormData\"].nmbRoleChangeForm.userAccountDetails.branch + \"Existing Department: \" + data[\"operationFormData\"].nmbRoleChangeForm.userAccountDetails.department + \"Destination Branch: \" + data[\"operationFormData\"].nmbRoleChangeForm.destinationBranch + \"Destination Department: \" + data[\"operationFormData\"].nmbRoleChangeForm.destinationFunctionalTitle + \"Task ID: \" + data[\"applicationWorkflowInstanceId\"] + \"Created At: \" + data[\"operationFormData\"].nmbRoleChangeForm.transferDate"
      }
    },
    {
      "Id": "PrintApplicationFormData",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "EndWorkflow",
      "Inputs": {
        "Message": "\"User ID: \" + data[\"PMUserId\"].processMakerUid + \"Role: \" + data[\"applicationFormData\"].eccIpsAsbaSolMovement.role + \"FromSolId: \" + data[\"applicationFormData\"].eccIpsAsbaSolMovement.fromSolId + \"ToSolId: \" + data[\"applicationFormData\"].eccIpsAsbaSolMovement.toSolId + \"Task ID: \" + data[\"applicationWorkflowInstanceId\"]"
      }
    },
    {
      "Id": "EndWorkflow",
      "StepType": "WorkflowCore.Primitives.EndStep, WorkflowCore"
    }
  ]
}
```
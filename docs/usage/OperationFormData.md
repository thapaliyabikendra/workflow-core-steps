# OperationFormData

The `operationFormData` is a JObject containing form data specific to operational workflows. It contains structured data that represents the operational context, user account details, and form-specific information needed for processing workflow operations.

## Origin

The `operationFormData` is expected to be present in the `data` object available to the workflow steps. It is typically injected into the workflow context when the workflow is initiated, containing operational form data that was submitted or collected during the workflow initiation process.

## Structure

The `operationFormData` is a JObject that contains nested form structures. Based on the usage patterns found in the codebase, it typically includes:

### Complete Sample Structure
Here's a comprehensive example of `operationFormData` for a role change operation:

```json
{
  "operationFormData": {
    "userAccountForm": {
      "userAccountDetails": {
        "employeeId": "EMP001",
        "userAccountName": "john.doe@company.com",
        "currentfunctionalTitle": "Software Engineer",
        "department": "Engineering",
        "location": "New York",
        "managerId": "MGR001",
        "hireDate": "2020-01-15"
      }
    },
    "roleChangeOperationForm": {
      "newFunctionalTitle": "Senior Software Engineer",
      "effectiveDate": "2024-01-01",
      "reason": "Performance-based promotion",
      "employeeDetails": {
        "employeeName": "John Doe",
        "currentfunctionalTitle": "Software Engineer",
        "currentSalary": 75000,
        "proposedSalary": 85000,
        "approvalLevel": "Manager"
      },
      "approvalChain": [
        {
          "approverId": "MGR001",
          "approverName": "Jane Smith",
          "approverRole": "Engineering Manager",
          "approvalOrder": 1
        },
        {
          "approverId": "DIR001",
          "approverName": "Bob Johnson",
          "approverRole": "Engineering Director",
          "approvalOrder": 2
        }
      ]
    }
  }
}
```

### Common Form Types

#### Role Change Operations
For role change workflows, the structure includes:

```json
{
  "userAccountForm": {
    "userAccountDetails": {
      "employeeId": "string",
      "userAccountName": "string", 
      "currentfunctionalTitle": "string"
    }
  },
  "roleChangeOperationForm": {
    "newFunctionalTitle": "string",
    "employeeDetails": {
      "employeeName": "string",
      "currentfunctionalTitle": "string"
    }
  }
}
```

#### Employee Transfer Operations
For employee transfer workflows, the structure includes:

```json
{
  "operationForm": {
    "employeeName": "string"
  }
}
```

## Usage

The `operationFormData` is used by various workflow steps to access operational context and form-specific information. Here are the key usage patterns:

### API Calls

#### `CallApiStep`
Uses operation form data to populate API request parameters.

Example from `docs/samples/RoleChangeApprovalWorkflow.md`:

```json
{
  "Id": "CallRoleChangeAPI",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "ApiRequest": {
      "@employeeId": "data[\"operationFormData\"].userAccountForm.userAccountDetails.employeeId",
      "@employeeName": "data[\"operationFormData\"].userAccountForm.userAccountDetails.userAccountName",
      "@currentfunctionalTitle": "data[\"operationFormData\"].userAccountForm.userAccountDetails.currentfunctionalTitle",
      "@newFunctionalTitle": "data[\"operationFormData\"].roleChangeOperationForm.newFunctionalTitle"
    }
  }
}
```

### Logging and Debugging

#### `PrintMessageStep`
Uses operation form data for logging and debugging purposes.

Example of printing operation form data:

```json
{
  "Id": "PrintOperationFormData",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "NextStep",
  "Inputs": {
    "Message": "\"Role Change Request - Employee: \" + data[\"operationFormData\"].roleChangeOperationForm.employeeDetails.employeeName + \", From: \" + data[\"operationFormData\"].roleChangeOperationForm.employeeDetails.currentfunctionalTitle + \", To: \" + data[\"operationFormData\"].roleChangeOperationForm.newFunctionalTitle + \", Effective Date: \" + data[\"operationFormData\"].roleChangeOperationForm.effectiveDate"
  }
}
```

Example from `docs/samples/EmployeeTransferWorkflow.md`:

```json
{
  "Id": "BPMAPICheckerApprovedLogger",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "Message": "\"Processing - Checker Approved: BPM API Approval Response Event received \" + data[\"operationFormData\"]"
  }
}
```

## How to Extract Data from Operation Form Data

### Accessing Nested Properties
The most common pattern is accessing deeply nested properties using dot notation:

```json
"@employeeId": "data[\"operationFormData\"].userAccountForm.userAccountDetails.employeeId"
"@employeeName": "data[\"operationFormData\"].roleChangeOperationForm.employeeDetails.employeeName"
"@newTitle": "data[\"operationFormData\"].roleChangeOperationForm.newFunctionalTitle"
```

### String Interpolation
Operation form data is often used in string interpolation for messages and API requests:

```json
"Message": "\"Role Change Request for \" + data[\"operationFormData\"].roleChangeOperationForm.employeeDetails.employeeName + \" from \" + data[\"operationFormData\"].roleChangeOperationForm.employeeDetails.currentfunctionalTitle + \" to \" + data[\"operationFormData\"].roleChangeOperationForm.newFunctionalTitle"
```

### Complete Object Access
Sometimes the entire operation form data object is passed or logged:

```json
"Message": "\"Complete Operation Form Data: \" + data[\"operationFormData\"]"
```

### Array Access
For arrays within operation form data (like approval chains):

```json
"firstApprover": "data[\"operationFormData\"].roleChangeOperationForm.approvalChain[0].approverName"
"approvalCount": "data[\"operationFormData\"].roleChangeOperationForm.approvalChain.length"
```

## Form-Specific Structures

### Role Change Operation Form
Contains user account details and role change information:

- `userAccountForm.userAccountDetails.employeeId`
- `userAccountForm.userAccountDetails.userAccountName`
- `userAccountForm.userAccountDetails.currentfunctionalTitle`
- `roleChangeOperationForm.newFunctionalTitle`
- `roleChangeOperationForm.employeeDetails.employeeName`
- `roleChangeOperationForm.employeeDetails.currentfunctionalTitle`

### Employee Transfer Operation Form
Contains employee transfer information:

- `operationForm.employeeName`

## Relationship with Application Forms

The `operationFormData` works in conjunction with `applicationFormData` (or similar application-level form data). While operation form data contains operational context, application form data typically contains application-specific information that may be processed differently.

## Data Validation

When using `operationFormData`, it's important to:

1. **Validate existence** - Check if the expected properties exist before accessing them
2. **Handle null values** - Provide fallback values for missing data
3. **Type safety** - Ensure the data types match expected formats
4. **Sanitization** - Clean the data before using it in API calls or database operations 
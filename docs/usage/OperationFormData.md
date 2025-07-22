# OperationFormData

The `operationFormData` is a JObject containing form data specific to operational workflows. It contains structured data that represents the operational context, user account details, and form-specific information needed for processing workflow operations.

## Origin

The `operationFormData` is expected to be present in the `data` object available to the workflow steps. It is typically injected into the workflow context when the workflow is initiated, containing operational form data that was submitted or collected during the workflow initiation process.

## Structure

The `operationFormData` is a JObject that contains nested form structures. Below are real examples for different workflow types:

### IT Operation Example
```json
{
  "userAccountForm": {
    "userAccountIdentifier": "89",
    "userAccountTypeId": "3a1b04e6",
    "userAccountDetails": {
      "employeeId": "8",
      "branch": "Branch",
      "branchId": "3",
      "department": "Business",
      "userAccountName": "K.C.",
      "staffId": "800",
      "currentfunctionalTitle": "BRANCH MANAGER"
    }
  }
}
```

### Temporary Transfer Example
```json
{
  "userAccountForm": {
    "userAccountIdentifier": "1",
    "userAccountTypeId": "3a1",
    "userAccountDetails": {
      "employeeId": "13",
      "branch": "Branch",
      "branchId": "7",
      "department": "Business",
      "userAccountName": "Karna",
      "staffId": "11",
      "currentfunctionalTitle": "CUSTOMER SERVICE"
    }
  },
  "nmbRoleChangeForm": {
    "userAccountIdentifier": "13",
    "userAccountTypeId": "62a0-5ae8-0aa9fc0a2ef1",
    "userAccountDetails": {
      "employeeId": "13",
      "branch": "Branch",
      "branchId": "7",
      "department": "Business",
      "userAccountName": "Karna",
      "staffId": "13",
      "currentfunctionalTitle": "CUSTOMER SERVICE"
    },
    "destinationBranch": "Branch",
    "destinationFunctionalTitle": "Business",
    "transferFrom": "2025-07-23 05:45:00",
    "transferTo": "2025-08-08 05:45:00"
  }
}
```

### MBL Role Change Example
```json
{
  "userAccountForm": {
    "userAccountIdentifier": "2804",
    "userAccountTypeId": "9890-511497e49ae8",
    "userAccountDetails": {
      "id": "k3",
      "employeeId": "2804",
      "branch": "Aabireni",
      "branchCode": "14",
      "userAccountName": "Shrestha",
      "ein": "EMP17",
      "staffId": "S-02",
      "solId": "1",
      "userEmail": "sajesh.@yaop.com",
      "designation": "Assistant General Manager",
      "currentfunctionalTitle": "SRM Business",
      "currentfunctionalTitleId": "10"
    }
  },
  "roleChangeOperationForm": {
    "userAccountIdentifier": "24",
    "userAccountTypeId": "1934-9890-511497e49ae8",
    "userAccountDetails": {
      "id": "k31",
      "employeeId": "204",
      "branch": "Aabunkhaireni",
      "branchCode": "14",
      "userAccountName": "SShrestha",
      "ein": "EMP17",
      "staffId": "S-72",
      "solId": "17",
      "userEmail": "sajesh.shrestha@yaop.com",
      "designation": "Assistant General Manager",
      "currentfunctionalTitle": "SRM Business",
      "currentfunctionalTitleId": "10"
    },
    "requestedFrom": "2025-07-18 05:45:00",
    "requestedTo": "2025-07-25 05:45:00",
    "newfunctionalTitleId": "2",
    "newfunctionalTitle": "Branch Manager"
  }
}
```

### Permanent Transfer Example
```json
{
  "userAccountForm": {
    "userAccountIdentifier": "",
    "userAccountTypeId": "",
    "userAccountDetails": {
      "employeeId": "",
      "branch": " ",
      "branchId": "",
      "department": " ",
      "userAccountName": "  ",
      "staffId": "",
      "currentfunctionalTitle": " "
    }
  },
  "nmbRoleChangeForm": {
    "userAccountIdentifier": "",
    "userAccountTypeId": "",
    "userAccountDetails": {
      "employeeId": "",
      "branch": " ",
      "branchId": "",
      "department": " ",
      "userAccountName": " ",
      "staffId": "",
      "currentfunctionalTitle": "  "
    },
    "destinationBranch": " ",
    "destinationDepartment": "",
    "destinationFunctionalTitle": " ",
    "transferDate": " "
  }
}
```

### Temporary Transfer Reversal Example
```json
{
  "userAccountForm": {
    "userAccountIdentifier": "",
    "userAccountTypeId": "",
    "userAccountDetails": {
      "id": "",
      "employeeId": "",
      "branch": "",
      "branchCode": "",
      "userAccountName": "",
      "ein": "",
      "staffId": "",
      "solId": "",
      "userEmail": "",
      "designation": "T",
      "currentfunctionalTitle": "",
      "currentfunctionalTitleId": ""
    }
  },
  "roleChangeOperationForm": {
    "userAccountIdentifier": "",
    "userAccountTypeId": "",
    "userAccountDetails": {
      "id": "",
      "employeeId": "",
      "branch": "",
      "branchCode": "",
      "userAccountName": "",
      "ein": "",
      "staffId": "",
      "solId": "",
      "userEmail": "",
      "designation": "",
      "currentfunctionalTitle": "",
      "currentfunctionalTitleId": ""
    },
    "requestedFrom": "",
    "requestedTo": "",
    "newfunctionalTitleId": "",
    "newfunctionalTitle": ""
  }
}
```

## Usage

The `operationFormData` is used by various workflow steps to access operational context and form-specific information. Here are the key usage patterns:

### API Calls

#### `CallApiStep`
Uses operation form data to populate API request parameters.

**Example for MBL Role Change:**
```json
{
  "Id": "CallRoleChangeAPI",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "ApiRequest": {
      "@employeeId": "data[\"operationFormData\"].userAccountForm.userAccountDetails.employeeId",
      "@employeeName": "data[\"operationFormData\"].userAccountForm.userAccountDetails.userAccountName",
      "@currentfunctionalTitle": "data[\"operationFormData\"].userAccountForm.userAccountDetails.currentfunctionalTitle",
      "@newFunctionalTitle": "data[\"operationFormData\"].roleChangeOperationForm.newfunctionalTitle",
      "@requestedFrom": "data[\"operationFormData\"].roleChangeOperationForm.requestedFrom",
      "@requestedTo": "data[\"operationFormData\"].roleChangeOperationForm.requestedTo"
    }
  }
}
```

### Logging and Debugging

#### `PrintMessageStep`
Uses operation form data for logging and debugging purposes.

**Example for Temporary Transfer:**
```json
{
  "Id": "PrintOperationFormData",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "NextStep",
  "Inputs": {
    "Message": "\"Temporary Transfer - Employee: \" + data[\"operationFormData\"].userAccountForm.userAccountDetails.userAccountName + \", From: \" + data[\"operationFormData\"].nmbRoleChangeForm.userAccountDetails.currentfunctionalTitle + \", To: \" + data[\"operationFormData\"].nmbRoleChangeForm.destinationFunctionalTitle + \", Transfer From: \" + data[\"operationFormData\"].nmbRoleChangeForm.transferFrom + \", Transfer To: \" + data[\"operationFormData\"].nmbRoleChangeForm.transferTo"
  }
}
```

## How to Extract Data from Operation Form Data

### Accessing Nested Properties
The most common pattern is accessing deeply nested properties using dot notation:

```json
"@employeeId": "data[\"operationFormData\"].userAccountForm.userAccountDetails.employeeId"
"@employeeName": "data[\"operationFormData\"].userAccountForm.userAccountDetails.userAccountName"
"@newTitle": "data[\"operationFormData\"].roleChangeOperationForm.newfunctionalTitle"
"@requestedFrom": "data[\"operationFormData\"].roleChangeOperationForm.requestedFrom"
"@requestedTo": "data[\"operationFormData\"].roleChangeOperationForm.requestedTo"
```

### String Interpolation
Operation form data is often used in string interpolation for messages and API requests:

```json
"Message": "\"Role Change Request for \" + data[\"operationFormData\"].userAccountForm.userAccountDetails.userAccountName + \" from \" + data[\"operationFormData\"].userAccountForm.userAccountDetails.currentfunctionalTitle + \" to \" + data[\"operationFormData\"].roleChangeOperationForm.newfunctionalTitle + \" (\" + data[\"operationFormData\"].roleChangeOperationForm.requestedFrom + \" to \" + data[\"operationFormData\"].roleChangeOperationForm.requestedTo + \")"
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

### MBL Role Change Operation Form
Contains user account details and role change information:
- `userAccountForm.userAccountDetails.employeeId`
- `userAccountForm.userAccountDetails.userAccountName`
- `userAccountForm.userAccountDetails.currentfunctionalTitle`
- `roleChangeOperationForm.newfunctionalTitle`
- `roleChangeOperationForm.requestedFrom`
- `roleChangeOperationForm.requestedTo`

### Temporary Transfer Operation Form
Contains employee transfer information:
- `userAccountForm.userAccountDetails.userAccountName`
- `nmbRoleChangeForm.userAccountDetails.currentfunctionalTitle`
- `nmbRoleChangeForm.destinationFunctionalTitle`
- `nmbRoleChangeForm.transferFrom`
- `nmbRoleChangeForm.transferTo`

## Relationship with Application Forms

The `operationFormData` works in conjunction with `applicationFormData` (or similar application-level form data). While operation form data contains operational context, application form data typically contains application-specific information that may be processed differently.

## Data Validation

When using `operationFormData`, it's important to:

1. **Validate existence** - Check if the expected properties exist before accessing them
2. **Handle null values** - Provide fallback values for missing data
3. **Type safety** - Ensure the data types match expected formats
4. **Sanitization** - Clean the data before using it in API calls or database operations 
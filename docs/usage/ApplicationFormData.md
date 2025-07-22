# ApplicationFormData

The `applicationFormData` is a JObject containing form data specific to application workflows. It contains structured data that represents the application context, role information, and form-specific details needed for processing application-level operations.

## Origin

The `applicationFormData` is expected to be present in the `data` object available to the workflow steps. It is typically injected into the workflow context when the workflow is initiated, containing application form data that was submitted or collected during the application workflow initiation process.

## Structure

The `applicationFormData` is a JObject that contains nested form structures. Based on the usage patterns found in the codebase, it typically includes:

### Complete Sample Structure
Here's a comprehensive example of `applicationFormData` for a role change application:

```json
{
  "applicationFormData": {
    "roleChange": {
      "roleCode": "SR_ENG",
      "roleName": "Senior Engineer",
      "roleDescription": "Senior level engineering role",
      "roleType": "Technical",
      "approvalRequired": true,
      "effectiveDate": "2024-01-01"
    },
    "applicationDetails": {
      "applicationType": "Role Change",
      "priority": "Normal",
      "justification": "Performance-based promotion",
      "requestedBy": "john.doe@company.com",
      "requestDate": "2023-12-15"
    },
    "validationRules": {
      "requiresApproval": true,
      "maxSalaryIncrease": 15,
      "minimumTenure": 12
    }
  }
}
```

### Common Form Types

#### Role Change Applications
For role change application workflows, the structure includes:

```json
{
  "roleChange": {
    "roleCode": "string",
    "roleName": "string",
    "roleDescription": "string"
  }
}
```

#### Access Request Applications
For access request application workflows, the structure includes:

```json
{
  "accessRequest": {
    "requestedSystems": ["string"],
    "accessLevel": "string",
    "justification": "string"
  }
}
```

## Usage

The `applicationFormData` is used by various workflow steps to access application context and form-specific information. Here are the key usage patterns:

### API Calls

#### `CallApiStep`
Uses application form data to populate API request parameters.

Example from `README.md`:

```json
{
  "Id": "CallRoleChangeAPI",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "ApiRequest": {
      "@roleCode": "data[\"applicationFormData\"].roleChange.roleCode",
      "@roleName": "data[\"applicationFormData\"].roleChange.roleName"
    }
  }
}
```

### Logging and Debugging

#### `PrintMessageStep`
Uses application form data for logging and debugging purposes.

Example of printing application form data:

```json
{
  "Id": "PrintApplicationFormData",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "NextStep",
  "Inputs": {
    "Message": "\"Role Change Application - Role Code: \" + data[\"applicationFormData\"].roleChange.roleCode + \", Role Name: \" + data[\"applicationFormData\"].roleChange.roleName + \", Requested By: \" + data[\"applicationFormData\"].applicationDetails.requestedBy"
  }
}
```

## How to Extract Data from Application Form Data

### Accessing Nested Properties
The most common pattern is accessing deeply nested properties using dot notation:

```json
"@roleCode": "data[\"applicationFormData\"].roleChange.roleCode"
"@roleName": "data[\"applicationFormData\"].roleChange.roleName"
"@requestedBy": "data[\"applicationFormData\"].applicationDetails.requestedBy"
```

### String Interpolation
Application form data is often used in string interpolation for messages and API requests:

```json
"Message": "\"Role Change Application for \" + data[\"applicationFormData\"].roleChange.roleName + \" (\" + data[\"applicationFormData\"].roleChange.roleCode + \") requested by \" + data[\"applicationFormData\"].applicationDetails.requestedBy"
```

### Complete Object Access
Sometimes the entire application form data object is passed or logged:

```json
"Message": "\"Complete Application Form Data: \" + data[\"applicationFormData\"]"
```

### Array Access
For arrays within application form data (like requested systems):

```json
"firstSystem": "data[\"applicationFormData\"].accessRequest.requestedSystems[0]"
"systemCount": "data[\"applicationFormData\"].accessRequest.requestedSystems.length"
```

## Form-Specific Structures

### Role Change Application Form
Contains role change information:

- `roleChange.roleCode`
- `roleChange.roleName`
- `roleChange.roleDescription`
- `roleChange.roleType`
- `roleChange.approvalRequired`
- `roleChange.effectiveDate`

### Access Request Application Form
Contains access request information:

- `accessRequest.requestedSystems`
- `accessRequest.accessLevel`
- `accessRequest.justification`
- `accessRequest.duration`

## Relationship with Operation Forms

The `applicationFormData` works in conjunction with `operationFormData`. While application form data contains application-specific context and role information, operation form data typically contains operational context and user details. Both are frequently used together in workflows that need to coordinate between application and operational concerns.

## Data Validation

When using `applicationFormData`, it's important to:

1. **Validate existence** - Check if the expected properties exist before accessing them
2. **Handle null values** - Provide fallback values for missing data
3. **Type safety** - Ensure the data types match expected formats
4. **Sanitization** - Clean the data before using it in API calls or database operations

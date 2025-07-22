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
  "applicationRole": {
    "centralizedOperationControl": true,
    "applicationName": "",
    "defaultRole": " ",
    "targetRole": " ",
    "roleId": "",
    "roleCode": "",
    "applicationId": "",
    "allowedPushSMSMax": "",
    "applicationName": " "
  }
}
```

### Common Form Types

#### Password Reset Applications

For password reset application workflows, the structure includes:

```json
{
  "passwordResetForm": {
    "remarks": "",
    "userName": "",
    "functionalTitle": " ",
    "applicationName": " "
  }
}
```

#### Password unlock Applications
for password unlock application workflows, the structure includes:
```json
{
  "passwordUnlockForm": {
    "remarks": " ",
    "userName": " ",
    "functionalTitle": " ",
    "applicationName": " "
  }
}
```

#### feems Temporary sol movement Applications
For temporary sol movement application workflows, the structure includes:

```json
{
  "feemsSolMovement": {
    "authority": "Maker",
    "fromSolId": "",
    "toSolId": "734"
  }
}
```

#### ccms sol movement applications
for ccms sol movement application workflows, the structure includes:
```json
{
  "ccmsSolMovement": {
    "authority": "",
    "custodian": "",
    "fromSolId": "",
    "toSolId": ""
  }
}
```

#### finacle temporary transfer applications
for finacle temporary transfer applications, the structure includes:
```json
{
  "applicationRole": {
    "finacleUserIds": " ",
    "applicationId": " ",
    "currentSol": " ",
    "currentSolId": " ",
    "currentRoleId": " ",
    "currentRoleDescription": " ",
    "roleId": " ",
    "roleCode": " ",
    "allowTellerTransaction": " ",
    "applicationName": " ",
    "defaultRole": " ",
    "targetRole": " ",
    "allowTellerTransactionDisplay": "",
    "useAppScopeRequestDates": true,
    "requestedFrom": " ",
    "requestedTo": " "
  }
}
```

#### user enable applications
for user enable applications, the structure includes:

```json
{
  "finacleUserEnableForm": {
    "remarks": " ",
    "userName": "  ",
    "functionalTitle": "",
    "applicationName": " "
  }
}
```

#### reversal applications
for reversal applications, the structure includes:
```json
{
  "reversalForm": {
    "useAppScopeRequestDates": true,
    "requestedFrom": "2025-07-29"
  }
}
```

## Usage

The `applicationFormData` is used by various workflow steps to access application context and form-specific information. Here are usage examples for the provided form types:

### API Calls

#### 1. Finacle Temporary Transfer (using `applicationRole`)
```json
{
  "Id": "CallFinacleTransferAPI",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "ApiRequest": {
      "@finacleUserId": "data[\"applicationFormData\"].applicationRole.finacleUserIds",
      "@fromSolId": "data[\"applicationFormData\"].applicationRole.currentSolId",
      "@toSolId": "data[\"applicationFormData\"].applicationRole.targetRole",
      "@requestedFrom": "data[\"applicationFormData\"].applicationRole.requestedFrom",
      "@requestedTo": "data[\"applicationFormData\"].applicationRole.requestedTo"
    }
  }
}
```

#### 2. Password Reset (using `passwordResetForm`)
```json
{
  "Id": "CallPasswordResetAPI",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "ApiRequest": {
      "@userName": "data[\"applicationFormData\"].passwordResetForm.userName",
      "@applicationName": "data[\"applicationFormData\"].passwordResetForm.applicationName",
      "@remarks": "data[\"applicationFormData\"].passwordResetForm.remarks"
    }
  }
}
```

#### 3. FEEMS Temporary Sol Movement (using `feemsSolMovement`)
```json
{
  "Id": "CallFeemsSolMovementAPI",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "ApiRequest": {
      "@authority": "data[\"applicationFormData\"].feemsSolMovement.authority",
      "@fromSolId": "data[\"applicationFormData\"].feemsSolMovement.fromSolId",
      "@toSolId": "data[\"applicationFormData\"].feemsSolMovement.toSolId"
    }
  }
}
```

### Logging and Debugging

#### 1. PrintMessageStep for Password Unlock
```json
{
  "Id": "PrintPasswordUnlockForm",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "NextStep",
  "Inputs": {
    "Message": "\"Password Unlock Request - User: \" + data[\"applicationFormData\"].passwordUnlockForm.userName + \", Application: \" + data[\"applicationFormData\"].passwordUnlockForm.applicationName + \", Remarks: \" + data[\"applicationFormData\"].passwordUnlockForm.remarks"
  }
}
```

#### 2. PrintMessageStep for CCMS Sol Movement
```json
{
  "Id": "PrintCCMSSolMovement",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "NextStep",
  "Inputs": {
    "Message": "\"CCMS Sol Movement - Authority: \" + data[\"applicationFormData\"].ccmsSolMovement.authority + \", Custodian: \" + data[\"applicationFormData\"].ccmsSolMovement.custodian + \", From: \" + data[\"applicationFormData\"].ccmsSolMovement.fromSolId + \", To: \" + data[\"applicationFormData\"].ccmsSolMovement.toSolId"
  }
}
```

#### 3. PrintMessageStep for User Enable
```json
{
  "Id": "PrintUserEnableForm",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "NextStep",
  "Inputs": {
    "Message": "\"User Enable Request - User: \" + data[\"applicationFormData\"].finacleUserEnableForm.userName + \", Application: \" + data[\"applicationFormData\"].finacleUserEnableForm.applicationName + \", Remarks: \" + data[\"applicationFormData\"].finacleUserEnableForm.remarks"
  }
}
```

#### 4. PrintMessageStep for Reversal
```json
{
  "Id": "PrintReversalForm",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "NextStep",
  "Inputs": {
    "Message": "\"Reversal Request - Use App Scope Dates: \" + data[\"applicationFormData\"].reversalForm.useAppScopeRequestDates + \", Requested From: \" + data[\"applicationFormData\"].reversalForm.requestedFrom"
  }
}
```

## How to Extract Data from Application Form Data

### Accessing Nested Properties

```json
"@finacleUserId": "data[\"applicationFormData\"].applicationRole.finacleUserIds"
"@userName": "data[\"applicationFormData\"].passwordResetForm.userName"
"@authority": "data[\"applicationFormData\"].feemsSolMovement.authority"
"@custodian": "data[\"applicationFormData\"].ccmsSolMovement.custodian"
"@requestedFrom": "data[\"applicationFormData\"].applicationRole.requestedFrom"
```

### String Interpolation

```json
"Message": "\"Finacle Transfer for \" + data[\"applicationFormData\"].applicationRole.finacleUserIds + \" from \" + data[\"applicationFormData\"].applicationRole.currentSolId + \" to \" + data[\"applicationFormData\"].applicationRole.targetRole + \" (\" + data[\"applicationFormData\"].applicationRole.requestedFrom + \" to \" + data[\"applicationFormData\"].applicationRole.requestedTo + \")"
"Message": "\"Password Reset for \" + data[\"applicationFormData\"].passwordResetForm.userName + \" on \" + data[\"applicationFormData\"].passwordResetForm.applicationName + \": \" + data[\"applicationFormData\"].passwordResetForm.remarks"
```

### Complete Object Access

```json
"Message": "\"Complete Application Form Data: \" + data[\"applicationFormData\"]"
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

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

### API Calls and PrintMessageStep Usage Examples

#### 1. applicationRole (Finacle Temporary Transfer)
**API Call:**
```json
{
  "Id": "CallFinacleTransferAPI",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "ApiRequest": {
      "@finacleUserIds": "data[\"applicationFormData\"].applicationRole.finacleUserIds",
      "@fromSolId": "data[\"applicationFormData\"].applicationRole.currentSolId",
      "@toSolId": "data[\"applicationFormData\"].applicationRole.targetRole",
      "@requestedFrom": "data[\"applicationFormData\"].applicationRole.requestedFrom",
      "@requestedTo": "data[\"applicationFormData\"].applicationRole.requestedTo"
    }
  }
}
```
**PrintMessageStep:**
```json
{
  "Id": "PrintFinacleTransfer",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "Message": "\"Finacle Transfer for \" + data[\"applicationFormData\"].applicationRole.finacleUserIds + \" from \" + data[\"applicationFormData\"].applicationRole.currentSolId + \" to \" + data[\"applicationFormData\"].applicationRole.targetRole + \" (\" + data[\"applicationFormData\"].applicationRole.requestedFrom + \" to \" + data[\"applicationFormData\"].applicationRole.requestedTo + \")\""
  }
}
```

#### 2. passwordResetForm
**API Call:**
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
**PrintMessageStep:**
```json
{
  "Id": "PrintPasswordReset",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "Message": "\"Password Reset for \" + data[\"applicationFormData\"].passwordResetForm.userName + \" on \" + data[\"applicationFormData\"].passwordResetForm.applicationName + \": \" + data[\"applicationFormData\"].passwordResetForm.remarks"
  }
}
```

#### 3. passwordUnlockForm
**API Call:**
```json
{
  "Id": "CallPasswordUnlockAPI",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "ApiRequest": {
      "@userName": "data[\"applicationFormData\"].passwordUnlockForm.userName",
      "@applicationName": "data[\"applicationFormData\"].passwordUnlockForm.applicationName",
      "@remarks": "data[\"applicationFormData\"].passwordUnlockForm.remarks"
    }
  }
}
```
**PrintMessageStep:**
```json
{
  "Id": "PrintPasswordUnlock",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "Message": "\"Password Unlock for \" + data[\"applicationFormData\"].passwordUnlockForm.userName + \" on \" + data[\"applicationFormData\"].passwordUnlockForm.applicationName + \": \" + data[\"applicationFormData\"].passwordUnlockForm.remarks"
  }
}
```

#### 4. feemsSolMovement
**API Call:**
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
**PrintMessageStep:**
```json
{
  "Id": "PrintFeemsSolMovement",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "Message": "\"FEEMS Sol Movement - Authority: \" + data[\"applicationFormData\"].feemsSolMovement.authority + \", From: \" + data[\"applicationFormData\"].feemsSolMovement.fromSolId + \", To: \" + data[\"applicationFormData\"].feemsSolMovement.toSolId"
  }
}
```

#### 5. ccmsSolMovement
**API Call:**
```json
{
  "Id": "CallCCMSSolMovementAPI",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "ApiRequest": {
      "@authority": "data[\"applicationFormData\"].ccmsSolMovement.authority",
      "@custodian": "data[\"applicationFormData\"].ccmsSolMovement.custodian",
      "@fromSolId": "data[\"applicationFormData\"].ccmsSolMovement.fromSolId",
      "@toSolId": "data[\"applicationFormData\"].ccmsSolMovement.toSolId"
    }
  }
}
```
**PrintMessageStep:**
```json
{
  "Id": "PrintCCMSSolMovement",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "Message": "\"CCMS Sol Movement - Authority: \" + data[\"applicationFormData\"].ccmsSolMovement.authority + \", Custodian: \" + data[\"applicationFormData\"].ccmsSolMovement.custodian + \", From: \" + data[\"applicationFormData\"].ccmsSolMovement.fromSolId + \", To: \" + data[\"applicationFormData\"].ccmsSolMovement.toSolId"
  }
}
```

#### 6. finacleUserEnableForm
**API Call:**
```json
{
  "Id": "CallUserEnableAPI",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "ApiRequest": {
      "@userName": "data[\"applicationFormData\"].finacleUserEnableForm.userName",
      "@applicationName": "data[\"applicationFormData\"].finacleUserEnableForm.applicationName",
      "@remarks": "data[\"applicationFormData\"].finacleUserEnableForm.remarks"
    }
  }
}
```
**PrintMessageStep:**
```json
{
  "Id": "PrintUserEnable",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "Message": "\"User Enable for \" + data[\"applicationFormData\"].finacleUserEnableForm.userName + \" on \" + data[\"applicationFormData\"].finacleUserEnableForm.applicationName + \": \" + data[\"applicationFormData\"].finacleUserEnableForm.remarks"
  }
}
```

#### 7. reversalForm
**API Call:**
```json
{
  "Id": "CallReversalAPI",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "ApiRequest": {
      "@useAppScopeRequestDates": "data[\"applicationFormData\"].reversalForm.useAppScopeRequestDates",
      "@requestedFrom": "data[\"applicationFormData\"].reversalForm.requestedFrom"
    }
  }
}
```
**PrintMessageStep:**
```json
{
  "Id": "PrintReversal",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
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

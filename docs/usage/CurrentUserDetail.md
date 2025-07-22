# CurrentUserDetail

The `CurrentUserDetail` is a JObject containing user context information that is passed to workflow steps for impersonation and user-specific operations. It provides details about the current user executing the workflow and is used extensively for authentication, authorization, and user-specific data operations.

## Origin

The `CurrentUserDetail` is expected to be present in the `data` object available to the workflow steps. It is typically injected into the workflow context when the workflow is initiated, containing user authentication and profile information.

Example from `docs/samples/RoleChangeApprovalWorkflow.md`:

```json
{
    "Id": "PrintRequestedMessage",
    "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
    "NextStepId": "UpdateARequestedWorkflowStageStep",
    "Inputs": {
        "Message": "\"Requested for application- Task Id: \" + data[\"applicationWorkflowInstanceId\"] + \", Initaitor Email\" + data[\"currentUserDetails\"].Email"
    }
}
```

In this example, the `PrintMessageStep` accesses the user's email from the `CurrentUserDetail` object (`data["currentUserDetails"].Email`).

## Structure

The `CurrentUserDetail` is a JObject that typically contains user information such as:

- **Email**: User's email address
- **User ID**: Unique identifier for the user
- **Name**: User's full name
- **Role**: User's role or permissions
- **Department**: User's department or organizational unit
- **Other user-specific attributes**

## Usage

The `CurrentUserDetail` is used by numerous workflow steps for impersonation and user context. Here are the key categories of steps that utilize this object:

### Database Operations

#### `AddNocoDBRecordStep`
Inserts records into NocoDB with user context for impersonation.

**Inputs:**
- `CurrentUserDetail` (`JObject`, Optional): JSON object with user context to impersonate while inserting

#### `UpdateRecordOnNocoDBStep`
Updates records in NocoDB with user context for impersonation.

**Inputs:**
- `CurrentUserDetail` (JObject, optional): Detailed user context for impersonation during update

## Common Access Patterns

### Accessing User Email
The most commonly accessed property is the user's email address:

```json
"Email": "data[\"currentUserDetail\"].Email"
```

### Passing Complete User Context
Many steps receive the complete user context object:

```json
"CurrentUserDetail": "data[\"currentUserDetail\"]"
```

### String Interpolation with User Data
User information is often included in log messages and notifications:

```json
"Message": "\"Requested for application- Task Id: \" + data[\"applicationWorkflowInstanceId\"] + \", Initaitor Email\" + data[\"currentUserDetails\"].Email"
```

## Impersonation Context

The primary purpose of `CurrentUserDetail` is to provide impersonation context for operations that require user authentication. This allows workflow steps to:

1. **Execute operations on behalf of the user** - Database operations, API calls, etc.
2. **Maintain audit trails** - Track which user performed specific actions
3. **Enforce authorization** - Ensure the user has permission to perform the operation
4. **Personalize responses** - Include user-specific information in notifications and logs

## Security Considerations

- The `CurrentUserDetail` contains sensitive user information and should be handled securely
- User context is used for impersonation, so it should be validated before use
- Access to user details should be logged for security auditing purposes
- The object should be sanitized before being included in log messages to prevent information leakage 
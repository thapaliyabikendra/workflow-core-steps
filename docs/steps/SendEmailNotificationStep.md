# Send Email Notification Step

## Purpose
Sends email notifications to users during workflow execution.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.SendEmailNotificationStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `Email` (string): Recipient email address.
- `Subject` (string): Email subject line.
- `Body` (string): Email message body content.-

### Outputs
None

## Usage Example

```json
{
  "Id": "SendApprovalRequest",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.SendEmailNotificationStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "Email": "data[\"currentUserDetail\"].Email",
    "Subject": "\"Employee Return Notification\"",
    "Body": "\"The employee return status is not on time. Please check the details.\""
  }
}
```

## Error Handling
- Email address validation
- Template rendering errors
- SMTP connection issues
- Delivery status tracking
- Rate limiting compliance

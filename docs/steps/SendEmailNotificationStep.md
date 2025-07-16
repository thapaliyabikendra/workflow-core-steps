# Send Email Notification Step

## Purpose
Sends email notifications to users during workflow execution.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.SendEmailNotificationStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `To` (string/array): Email recipient(s)
- `Subject` (string): Email subject
- `Body` (string): Email body content
- `Template` (string, optional): Email template name
- `TemplateData` (object, optional): Data for template rendering
- `Cc` (string/array, optional): Carbon copy recipients
- `Bcc` (string/array, optional): Blind carbon copy recipients
- `Attachments` (array, optional): File attachments

### Outputs
- `Sent` (boolean): Whether email was sent successfully
- `MessageId` (string): Unique identifier of sent email

## Usage Example

```json
{
  "Id": "SendApprovalRequest",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.SendEmailNotificationStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "WaitForResponse",
  "Inputs": {
    "To": "data[\"approverEmail\"]",
    "Subject": "\"New Approval Request\"",
    "Template": "\"ApprovalRequestEmail\"",
    "TemplateData": {
      "requestId": "data[\"requestId\"]",
      "requestedBy": "data[\"requesterName\"]",
      "requestDetails": "data[\"requestSummary\"]",
      "approvalLink": "data[\"approvalUrl\"]"
    }
  },
  "Outputs": {
    "EmailSent": "step.Sent",
    "NotificationId": "step.MessageId"
  }
}
```

## Error Handling
- Email address validation
- Template rendering errors
- SMTP connection issues
- Delivery status tracking
- Rate limiting compliance

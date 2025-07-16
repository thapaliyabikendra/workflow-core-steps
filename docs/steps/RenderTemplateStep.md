# Render Template Step

## Purpose
Renders a text or HTML template using provided data, often for notifications, emails, or document generation.

## Step Type
Amnil.AccessControlManagementSystem.Workflows.Steps.RenderTemplateStep, Amnil.AccessControlManagementSystem.Application

## Parameters

### Inputs
- `TemplateName` (string): The template string or template identifier to render.
- `Model` (JObject): The data object to use for populating the template.

### Outputs
- `Response` (string): The final rendered output.

## Usage Example
```json
{
  "Id": "RenderTemplate",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.RenderTemplateStep, Amnil.AccessControlManagementSystem.Application",
      "NextStepId": "PrintApplicationTemplate",
      "Inputs": {
        "TemplateName": "\"transfer\"",
        "Model": {
          "user": "Admin"
        }
      },
      "Outputs": {
        "RenderedContent": "step.RenderedContent"
      }
}
```

## Error Handling
- Validates template existence and syntax.
- Handles rendering errors.
- Logs failures.
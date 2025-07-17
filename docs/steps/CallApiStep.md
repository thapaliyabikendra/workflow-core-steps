# Call API Step

## Purpose
Makes HTTP requests to external APIs using a dynamic HTTP client service.

## Step Type
```
Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application
```

## Parameters

### Inputs
- `ApiRequest` (JObject): The request payload to be sent to the API
  - Contains HTTP request details like URL, method, headers, body
- `ApiClientName` (string): Name of the API client to be used
  - Must match a configured API client in the system
- `CurrentUserDetail` (JObject, Optional): User data

### Outputs
- `Response` (JObject): Contains the API response after execution
  - Includes status code, headers, and response body

## Usage Example

```json
{
  "Id": "CallExternalApi",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",
  "NextStepId": "ProcessApiResponse",
  "Inputs": {
    "ApiRequest": {
      "name": "Mike"
    },
    "ApiClientName": "EXTERNAL_SERVICE_CLIENT",
    "CurrentUserDetail": "data[\"currentUserDetail\"]"
  },
  "Outputs": {
    "ApiResponse": "step.Response[\"data\"]",
    "userId": "step.Response[\"data\"].userId"
  }
}
```

## Error Handling
- HTTP errors (4xx, 5xx) are properly logged and can trigger error workflows
- Connection timeouts and network issues are handled gracefully
- Invalid client names or configurations throw configuration errors

# Workflow Steps Documentation

This document provides description and usage of all available workflow steps in the Access Control Management System. Each step is documented with its purpose, parameters, and usage examples to help in creating workflow definitions.

## System Dependencies

### Core Dependencies
1. **API Client**
   - Required for making HTTP requests to external systems
   - Used by CallApiStep for service integrations
   - Configuration available in `/ApiClients` directory

2. **Dynamic Table**
   - Provides data presentation and manipulation capabilities
   - Used for displaying workflow data and task lists
   - API client integration for data fetching
   - Configuration available in `/DynamicTables` directory

3. **Dynamic Menu**
   - Manages navigation and action menus in the workflow UI
   - Integrates with workflow stages and user permissions
   - Configuration available in `/DynamicMenus` directory

4. **Dynamic Form**
   - Handles user input forms for workflow tasks
   - Supports dynamic form generation based on workflow context
   - Configuration available in `/DynamicForms` directory

5. **Rule Engine**
   - Manages business rules and validation logic
   - Used by ValidateRulesStep for workflow decisions
   - Configuration available in `/Rules` directory

g. **Workflow Definition**
   - Configuration available in `/Workflows/Definitions` directory



## Available Steps

### API and Integration Steps
1. [Call API Step](./CallApiStep.md)
   - For making HTTP requests to external APIs
### Workflow Management Steps
3. [Start Workflow Instance Step](./StartWorkflowInstanceStep.md)
   - For starting new workflow instances
4. [Get Application Workflows Step](./GetApplicationWorkflowsStep.md)
   - For retrieving application workflow information
5. [Create Workflow Event Step](./CreateWorkflowEventStep.md)
   - For creating workflow events
6. [Get Workflow Event Step](./GetWorkflowEventStep.md)
   - For retrieving workflow event details
7. [Update Workflow Event Status Step](./UpdateWorkflowEventStatusStep.md)
   - For updating workflow event statuses
8. [Bulk Update Workflow Event Status Step](./BulkUpdateWorkflowEventStatusStep.md)
   - For updating multiple workflow event statuses
9. [Add NocoDB Record Step](./AddNocoDBRecordStep.md)
    - For adding new record
10. [Delete Record On NocoDB Step](./DeleteRecordOnNocoDBStep.md)
    - For deleting a record
11. [Delete Record On NocoDB Step](./DeleteRecordOnNocoDBStep.md)
    - For deleting a record
12. [Generate Link Step](./GenerateLinkStep.md)
    - For generating link
13. [Get Application Instance Forms Step](./GetApplicationInstanceFormsStep.md)
    - For getting application instance deatils
14. [Get Application Workflow Step](./GetApplicationWorkflowStep.md)
    - For getting application task workflow details
15. [Get Record By Id On NocoDB Step](./GetRecordByIdOnNocoDBStep.md)
    - For getting record detail
16. [Get Record On NocoDB Step](./GetRecordOnNocoDBStep.md)
    - For getting record details
17. [Render Template Step](./RenderTemplateStep.md)
    - For getting final rendered output
18. [Update Record On NocoDB Step](./UpdateRecordOnNocoDBStep.md)
    - For updating the record

### Task and Stage Management Steps
19. [Generate Task ID Step](./GenerateTaskIdStep.md)
   - For generating unique task IDs
20. [Update Application Task Stage Step](./UpdateApplicationTaskStageStep.md)
    - For updating application task stages
21. [Update Operation Task Stage Step](./UpdateOperationTaskStageStep.md)
    - For updating operation task stages

### Utility Steps
22. [Get Variable Step](./GetVariableStep.md)
    - For retrieving workflow variables
23. [Set Variable Step](./SetVariableStep.md)
    - For setting workflow variables
24. [Print Message Step](./PrintMessageStep.md)
    - For logging messages during workflow execution
25. [Sleep Step](./SleepStep.md)
    - For introducing delays in workflow execution
26. [Increment Step](./IncrementStep.md)
    - For incrementing counter values

## General Structure

Each workflow step is defined with the following attributes:

```json
{
  "Id": "UniqueStepId",
  "StepType": "Namespace.StepClassName, AssemblyName",
  "NextStepId": "NextStepIdentifier",
  "Inputs": {
    "Parameter1": "value1",
    "Parameter2": "value2"
  },
  "Outputs": {
    "OutputParam1": "step.OutputValue1"
  }
}
```

## Error Handling

Each step includes error handling mechanisms:
- Runtime errors are logged
- Business validation errors throw UserFriendlyException
- Step failure can be caught using error handling branches in workflow definition

### Error Types
1. **Validation Errors**
   - Invalid input parameters
   - Business rule violations
   - Data format errors

2. **Runtime Errors**
   - Network failures
   - Service unavailability
   - Resource constraints

3. **Business Logic Errors**
   - Process violations
   - State transition errors
   - Authorization failures

### Error Handling Patterns
1. **Retry Pattern**
   ```json
   {
     "Id": "RetryableOperation",
     "StepType": "YourStepType",
     "RetryCount": 3,
     "RetryInterval": "TimeSpan.FromSeconds(5)"
   }
   ```

2. **Compensation Pattern**
   ```json
   {
     "Id": "CompensableStep",
     "StepType": "YourStepType",
     "CompensateWith": [
       {
         "Id": "UndoOperation",
         "StepType": "CompensationStepType"
       }
     ]
   }
   ```

3. **Error Branch Pattern**
   ```json
   {
     "Id": "OperationWithErrorHandling",
     "StepType": "YourStepType",
     "ErrorHandling": [
       {
         "ExceptionType": "ServiceException",
         "RetryCount": 3
       }
     ]
   }
   ```

### Best Practices
1. Always include error handling for critical steps
2. Use compensation steps for reversible operations
3. Implement retries for transient failures
4. Log meaningful error information
5. Use appropriate error types for different scenarios

# Primitive Step Types for Workflow Definitions

This document serves as a reference for the primitive step types that can be used in workflow definitions.

## 1. EndStep
Marks the end of a workflow.
```json
{
  "Id": "EndWorkflow",
  "StepType": "WorkflowCore.Primitives.EndStep, WorkflowCore"
}
```

## 2. WaitFor
Waits for an event to occur before proceeding.
```json
{
  "Id": "WaitForEvent",
  "StepType": "WorkflowCore.Primitives.WaitFor, WorkflowCore",
  "Inputs": {
    "EventName": "\"SOME_EVENT\"",
    "EventKey": "data[\"eventKey\"]",
    "EffectiveDate": "DateTime.Now"
  },
  "Outputs": {
    "EventData": "step.EventData"
  }
}
```

## 3. Schedule
Schedules a future execution of a set of steps.
```json
{
  "Id": "ScheduleTask",
  "StepType": "WorkflowCore.Primitives.Schedule, WorkflowCore",
  "Inputs": {
    "Interval": "TimeSpan.FromSeconds(30)"
  },
  "Do": [
    [
      {
        "Id": "PrintStep1",
        "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
        "Inputs": {
          "Message": "\"Step:\" + data[\"stepId\"]"
        }
      }
    ]
  ]
}
```

## 4. Recur
Repeatedly executes a set of steps until a condition is met.
```json
{
  "Id": "RecurringTask",
  "StepType": "WorkflowCore.Primitives.Recur, WorkflowCore",
  "Inputs": {
    "Interval": "TimeSpan.FromSeconds(60)",
    "StopCondition": "Convert.ToInt32(data[\"Counter\"]) >= 5"
  },
  "Do": [
    [
      {
        "Id": "PrintRecurringStep",
        "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
        "Inputs": {
          "Message": "\"Counter value: \" + data[\"Counter\"]"
        }
      }
    ]
  ]
}
```

## 5. If
Conditional execution based on a boolean condition.
```json
{
  "Id": "ConditionalTask",
  "StepType": "WorkflowCore.Primitives.If, WorkflowCore",
  "Inputs": {
    "Condition": "data[\"someValue\"] > 10"
  },
  "Do": [
    [
      {
        "Id": "TruePathStep",
        "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
        "Inputs": {
          "Message": "\"Condition met. someValue: \" + data[\"someValue\"]"
        }
      }
    ]
  ]
}
```

## 6. While
Repeatedly executes steps while a condition is true.
```json
{
  "Id": "WhileLoop",
  "StepType": "WorkflowCore.Primitives.While, WorkflowCore",
  "Inputs": {
    "Condition": "data[\"counter\"] < 5"
  },
  "Do": [
    [
      {
        "Id": "LoopStep",
        "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
        "Inputs": {
          "Message": "\"Loop iteration: \" + data[\"counter\"]"
        }
      }
    ]
  ]
}
```

## 7. Decide
Multi-path branching based on conditions.
```json
{
  "Id": "DecisionPoint",
  "StepType": "WorkflowCore.Primitives.Decide, WorkflowCore",
  "SelectNextStep": {
    "PathA": "data[\"value\"] == \"A\"",
    "PathB": "data[\"value\"] == \"B\"",
    "DefaultPath": "true"
  }
}
```

## 8. Parallel(ForEach)
Executes multiple branches concurrently.
```json
{
  "Id": "ForEachStep",
  "StepType": "WorkflowCore.Primitives.ForEach, WorkflowCore",
  "Do": [
    [
      {
        "Id": "Branch1Step1",
        "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
        "NextStepId": "Branch2Step1",
        "Inputs": {
          "Message": "\"Branch 1: Processing item - \" + context.Item"
        }
      },
      {
        "Id": "Branch2Step1",
        "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
        "Inputs": {
          "Message": "\"Branch 2: Processing item - \" + context.Item"
        }
      }
    ]
  ]
}
```

## 9. Non-Parallel(ForEach)
Executes Single branch.
```json
{
  "Id": "ForEachStep",
  "StepType": "WorkflowCore.Primitives.ForEach, WorkflowCore",
  "RunParallel": "false",
  "Do": [
    [
      {
        "Id": "Branch1Step1",
        "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
        "NextStepId": "Branch2Step1",
        "Inputs": {
          "Message": "\"Branch 1: Processing item - \" + context.Item"
        }
      },
      {
        "Id": "Branch2Step1",
        "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
        "Inputs": {
          "Message": "\"Branch 2: Processing item - \" + context.Item"
        }
      }
    ]
  ]
}
```

## 10. Delay
Introduces a delay in workflow execution.
```json
{
  "Id": "DelayTask",
  "StepType": "WorkflowCore.Primitives.Delay, WorkflowCore",
  "Inputs": {
    "Period": "TimeSpan.FromMinutes(5)"
  }
}
```

## Error Handling and Compensation

Many steps support error handling and compensation patterns:

1. **Retry Pattern**
```json
{
  "Id": "RetryableStep",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "Message": "\"Retrying step attempt...\""
  },
  "RetryCount": 3,
  "RetryInterval": "TimeSpan.FromSeconds(5)"
}
```

2. **Compensation Pattern**
```json
{
  "Id": "CompensableStep",
  "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
  "Inputs": {
    "Message": "\"Main step executed.\""
  },
  "CompensateWith": [
    {
      "Id": "UndoStep",
      "StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",
      "Inputs": {
        "Message": "\"Compensating action for failure.\""
      }
    }
  ]
}
```

## Best Practices

1. Always provide unique step IDs within the workflow
2. Use descriptive IDs that indicate the step's purpose
3. Handle errors appropriately using retry or compensation patterns
4. Use proper data referencing (`data["key"]`) in expressions
5. Chain steps properly using `NextStepId`
6. Keep conditions simple and readable
7. Use parallel execution judiciously to improve performance
8. Document complex workflow logic with comments

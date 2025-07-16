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
  "NextStepId": "ProcessEvent",
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
        "Id": "ScheduledStep1",
        "StepType": "SomeStep",
        "NextStepId": "ScheduledStep2"
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
        "Id": "RecurringStep",
        "StepType": "SomeStep",
        "NextStepId": "CheckCondition"
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
  "NextStepId": "DefaultPath",
  "Inputs": {
    "Condition": "data[\"someValue\"] > 10"
  },
  "Do": [
    [
      {
        "Id": "TruePathStep",
        "StepType": "SomeStep",
        "NextStepId": "NextStep"
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
        "StepType": "SomeStep",
        "NextStepId": "IncrementCounter"
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

## 8. Parallel
Executes multiple branches concurrently.
```json
{
  "Id": "ParallelExecution",
  "StepType": "WorkflowCore.Primitives.Parallel, WorkflowCore",
  "NextStepId": "ContinueAfterParallel",
  "Do": [
    [
      {
        "Id": "Branch1Step1",
        "StepType": "SomeStep",
        "NextStepId": "Branch1Step2"
      }
    ],
    [
      {
        "Id": "Branch2Step1",
        "StepType": "SomeStep",
        "NextStepId": "Branch2Step2"
      }
    ]
  ]
}
```

## 9. Delay
Introduces a delay in workflow execution.
```json
{
  "Id": "DelayTask",
  "StepType": "WorkflowCore.Primitives.Delay, WorkflowCore",
  "NextStepId": "AfterDelay",
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
  "StepType": "SomeStep",
  "RetryCount": 3,
  "RetryInterval": "TimeSpan.FromSeconds(5)"
}
```

2. **Compensation Pattern**
```json
{
  "Id": "CompensableStep",
  "StepType": "SomeStep",
  "CompensateWith": [
    {
      "Id": "UndoStep",
      "StepType": "CompensationStep",
      "Inputs": {
        "Parameter": "data[\"someValue\"]"
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

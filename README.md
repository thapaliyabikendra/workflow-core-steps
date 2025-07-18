# workflow-core-steps

## Table of Contents

[**Workflow	3**](#workflow)

[1\. ID (Id)	3](#heading=)

[2\. Version (Version)	4](#heading=)

[3\. Data Type (DataType)	4](#heading=)

[4\. Default Error Behavior (DefaultErrorBehavior)	4](#heading=)

[5\. Steps (Steps)	4](#heading=)

[1\. PrintMessageStep.cs	5](#1.-printmessagestep.cs)

[Purpose:	5](#purpose:)

[Input:	5](#input:)

[Output:	6](#output:)

[Example Workflow JSON:	6](#example-workflow-json:)

[2\. PublishWorkflowEventStep.cs	6](#2.-publishworkfloweventstep.cs)

[Purpose:	6](#purpose:-1)

[Input:	6](#input:-1)

[Output:	7](#output:-1)

[Example Workflow JSON:	7](#example-workflow-json:-1)

[3\. SendEmailNotificationStep.cs	7](#3.-sendemailnotificationstep.cs)

[Purpose:	7](#purpose:-2)

[Input:	7](#input:-2)

[Output:	8](#output:-2)

[Example Workflow JSON:	8](#example-workflow-json:-2)

[4\. SetVariableStep.cs	8](#4.-setvariablestep.cs)

[Purpose:	8](#purpose:-3)

[Input:	9](#input:-3)

[Output:	9](#output:-3)

[Example Workflow JSON:	9](#example-workflow-json:-3)

[5\. SleepStep.cs	9](#5.-sleepstep.cs)

[Purpose:	9](#purpose:-4)

[Input:	10](#input:-4)

[Output:	10](#output:-4)

[Example Workflow JSON:	10](#example-workflow-json:-4)

[6\. StartWorkflowInstanceStep.cs	10](#6.-startworkflowinstancestep.cs)

[Purpose:	10](#purpose:-5)

[Input:	11](#input:-5)

[Output:	11](#output:-5)

[Example Workflow JSON:	11](#example-workflow-json:-5)

[7\. UpdateApplicationTaskStageStep.cs	11](#7.-updateapplicationtaskstagestep.cs)

[Purpose:	11](#purpose:-6)

[Input:	11](#input:-6)

[Output:	12](#output:-6)

[Example Workflow JSON:	12](#example-workflow-json:-6)

[8\. UpdateOperationTaskStageStep.cs	13](#8.-updateoperationtaskstagestep.cs)

[Purpose:	13](#purpose:-7)

[Input:	13](#input:-7)

[Output:	14](#output:-7)

[Example Workflow JSON:	14](#example-workflow-json:-7)

[9\. UpdateWorkflowEventStatusStep.cs	15](#9.-updateworkfloweventstatusstep.cs)

[Purpose:	15](#purpose:-8)

[Input:	15](#input:-8)

[Output:	16](#output:-8)

[Example Workflow JSON:	16](#example-workflow-json:-8)

[10\. ValidateRulesStep.cs	16](#10.-validaterulesstep.cs)

[Purpose:	16](#purpose:-9)

[Input:	16](#input:-9)

[Output:	17](#output:-9)

[Example Workflow JSON:	17](#example-workflow-json:-9)

[11\. PrintMessageStep.cs	17](#11.-printmessagestep.cs)

[Purpose:	17](#purpose:-10)

[Input:	17](#input:-10)

[Output:	18](#output:-10)

[Example Workflow JSON:	18](#example-workflow-json:-10)

[12\. PublishWorkflowEventStep.cs	18](#12.-publishworkfloweventstep.cs)

[Purpose:	18](#purpose:-11)

[Input:	19](#input:-11)

[Output:	19](#output:-11)

[Example Workflow JSON:	19](#example-workflow-json:-11)

[13\. SendEmailNotificationStep.cs	19](#13.-sendemailnotificationstep.cs)

[Purpose:	19](#purpose:-12)

[Input:	20](#input:-12)

[Output:	20](#output:-12)

[Example Workflow JSON:	20](#example-workflow-json:-12)

[14\. SetVariableStep.cs	21](#14.-setvariablestep.cs)

[Purpose:	21](#purpose:-13)

[Input:	21](#input:-13)

[Output:	21](#output:-13)

[Example Workflow JSON:	21](#example-workflow-json:-13)

[15\. SleepStep.cs	22](#15.-sleepstep.cs)

[Purpose:	22](#purpose:-14)

[Input:	22](#input:-14)

[Output:	22](#output:-14)

[Example Workflow JSON:	22](#example-workflow-json:-14)

[16\. StartWorkflowInstanceStep.cs	23](#16.-startworkflowinstancestep.cs)

[Purpose:	23](#purpose:-15)

[Input:	23](#input:-15)

[Output:	23](#output:-15)

[Example Workflow JSON:	23](#example-workflow-json:-15)

[17\. UpdateApplicationTaskStageStep.cs	24](#17.-updateapplicationtaskstagestep.cs)

[Purpose:	24](#purpose:-16)

[Input:	24](#input:-16)

[Output:	24](#output:-16)

[Example Workflow JSON:	24](#example-workflow-json:-16)

[18\. UpdateOperationTaskStageStep.cs	26](#18.-updateoperationtaskstagestep.cs)

[Purpose:	26](#purpose:-17)

[Input:	26](#input:-17)

[Output:	26](#output:-17)

[Example Workflow JSON:	26](#example-workflow-json:-17)

[19\. UpdateWorkflowEventStatusStep.cs	28](#19.-updateworkfloweventstatusstep.cs)

[Purpose:	28](#purpose:-18)

[Input:	28](#input:-18)

[Output:	28](#output:-18)

[Example Workflow JSON:	28](#example-workflow-json:-18)

[20\. ValidateRulesStep.cs	29](#20.-validaterulesstep.cs)

[Purpose:	29](#purpose:-19)

[Input:	29](#input:-19)

[Output:	29](#output:-19)

[Example Workflow JSON:	29](#example-workflow-json:-19)

      21\. AddNocoDBRecordStep.cs……………………………………………………………………30

            [Purpose:	29](#purpose:-19)

[Input:	29](#input:-19)

[Output:	29](#output:-19)

[Example Workflow JSON:	29](#example-workflow-json:-19)

      22\. CallApiStep.cs	29

[Purpose:	29](#purpose:-19)

[Input:	29](#input:-19)

[Output:	29](#output:-19)

[Example Workflow JSON:	29](#example-workflow-json:-19) 

      23\. CreateWorkflowEventStep.cs	29

[Purpose:	29](#purpose:-19)

[Input:	29](#input:-19)

[Output:	29](#output:-19)

      24\. DeleteRecordOnNocoDBStep.cs	29

[Purpose:	29](#purpose:-19)

[Input:	29](#input:-19)

[Output:	29](#output:-19)

      25\. GetRecordByIdOnNocoDBStep.cs	29

[Purpose:	29](#purpose:-19)

[Input:	29](#input:-19)

[Output:	29](#output:-19)

[Example Workflow JSON:	29](#example-workflow-json:-19)

      26\. GetRecordOnNocoDBStep.cs	29

[Purpose:	29](#purpose:-19)

[Input:	29](#input:-19)

[Output:	29](#output:-19)

[Example Workflow JSON:	29](#example-workflow-json:-19)

      27\. GetWorkflowEventStep.cs	29

[Purpose:	29](#purpose:-19)

[Input:	29](#input:-19)

[Output:	29](#output:-19)

[Example Workflow JSON:	29](#example-workflow-json:-19)

      28\. IncrementStep.cs	29

[Purpose:	29](#purpose:-19)

[Input:	29](#input:-19)

[Output:	29](#output:-19)

[Example Workflow JSON:	29](#example-workflow-json:-19)

      29\. PublishWorkflowEventStep.cs	29

[Purpose:	29](#purpose:-19)

[Input:	29](#input:-19)

[Output:	29](#output:-19)

      30\. RenderTemplateStep.cs	29

[Purpose:	29](#purpose:-19)

[Input:	29](#input:-19)

[Output:	29](#output:-19)

      31\. UpdateRecordOnNocoDBStep.cs	29

[Purpose:	29](#purpose:-19)

[Input:	29](#input:-19)

[Output:	29](#output:-19)

[Example Workflow JSON:	29](#example-workflow-json:-19)

## 

## 

## 

## 

## 

## 

## 

## 

## 

## Workflow {#workflow}

Here’s a detailed explanation of key properties in the workflow JSON:

### **1\. ID (Id)**

* **Definition**: This is a unique identifier for the workflow.

* **Value in JSON**: "PermanentEmployeeTransferWorkflowOnlyApproval"

* **Purpose**:

  * Used to reference this workflow in the system.

  * Helps in managing and distinguishing different workflows.

  * Should be unique across all workflows in the application.

---

### **2\. Version (Version)**

* **Definition**: Specifies the version of the workflow.

* **Value in JSON**: 1

* **Purpose**:

  * Allows versioning of workflows, ensuring backward compatibility.

  * Helps track changes and updates over time.

  * Ensures that running instances of older workflows remain unaffected by new changes.

---

### **3\. Data Type (DataType)**

* **Definition**: Defines the type of data the workflow operates on.

* **Value in JSON**:

  **"Amnil.AccessControlManagementSystem.Workflows.DynamicData, Amnil.AccessControlManagementSystem.Application.Contracts"**

* **Purpose**:

  * Determines the data model that the workflow processes.

  * Specifies where to fetch, update, and store the workflow-related data.

  * Ensures compatibility with different components of the system.

---

### **4\. Default Error Behavior (DefaultErrorBehavior)**

* **Definition**: Determines how the workflow should respond when an error occurs.

* **Value in JSON**: "Compensate"

* **Possible Values**:

  * "Retry": The workflow retries the step if it fails.

  * "Terminate": The workflow stops execution when an error occurs.

  * "Compensate": The workflow attempts to reverse any previous steps before stopping.

* **Purpose**:

  * Provides a fail-safe mechanism.

  * Ensures that incorrect changes can be undone.

  * Enhances reliability by defining a structured response to errors.

---

### **5\. Steps (Steps)**

* **Definition**: Defines the sequence of operations that the workflow will execute.

* **Value in JSON**: A list of steps, each with specific properties.

* **Purpose**:

  * Dictates the execution flow of the workflow.

  * Includes API calls, logging, condition checks, and variable updates.

  * Ensures that all necessary tasks are performed in the correct order.

Each step contains:

1. **Id**: A unique identifier for the step.

2. **StepType**: Defines the action to be executed (e.g., log message, API call, variable update).

3. **NextStepId**: Indicates which step to execute next.

4. **Inputs**: Defines the parameters required for step execution.

5. **Outputs** (optional): Captures results from the step to be used in subsequent steps.

6. **Do** (for conditionals): Defines alternative paths based on conditions.

Here is the **complete documentation** for all the **Step classes** (.cs files) you've uploaded in both rounds, along with their **purpose**, **inputs**, **outputs**, and **workflow JSON examples** for each step:

### **1\. PrintMessageStep.cs** {#1.-printmessagestep.cs}

#### **Purpose:** {#purpose:}

Logs a custom message to provide helpful information or status updates at any point in the workflow.

#### **Input:** {#input:}

* `Message` (string): The message to be printed. Typically, it may include data from previous steps or variables (e.g., task IDs).

#### **Output:** {#output:}

* There is no output; this step simply logs information.

#### **Example Workflow JSON:** {#example-workflow-json:}

`{`

  `"Id": "PrintTaskId",`

  `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",`

  `"NextStepId": "UpdateRequestedWorkflowStageStep",`

  `"Inputs": {`

    `"Message": "\"Requested - Task Id: \" + data[\"applicationWorkflowInstanceId\"]"`

  `}`

`}`

### 

### **2\. PublishWorkflowEventStep.cs** {#2.-publishworkfloweventstep.cs}

#### **Purpose:** {#purpose:-1}

Publishes a workflow event with the provided event data.

#### **Input:** {#input:-1}

* `EventName` (string): The name of the event to publish.

* `EventKey` (string): The event key.

* `EventData` (JObject): Data to be sent with the event.

#### **Output:** {#output:-1}

* No direct output.

#### **Example Workflow JSON:** {#example-workflow-json:-1}

`{`

  `"Id": "PublishWorkflowEventStep",`

  `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PublishWorkflowEventStep, Amnil.AccessControlManagementSystem.Application",`

  `"NextStepId": "NextStepId",`

  `"Inputs": {`

    `"EventName": "EventStart",`

    `"EventKey": "key1",`

    `"EventData": "{ \"key\": \"value\" }"`

  `},`

  `"Outputs": {}`

`}`

### **3\. SendEmailNotificationStep.cs** {#3.-sendemailnotificationstep.cs}

#### **Purpose:** {#purpose:-2}

Sends an email notification with the provided content.

#### **Input:** {#input:-2}

* `Email` (string): The recipient email address.

* `Subject` (string): The subject of the email.

* `Body` (string): The body content of the email.

#### **Output:** {#output:-2}

* No direct output.

#### **Example Workflow JSON:** {#example-workflow-json:-2}

`{`

  `"Id": "SendEmailNotificationStep",`

  `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.SendEmailNotificationStep, Amnil.AccessControlManagementSystem.Application",`

  `"NextStepId": "NextStepId",`

  `"Inputs": {`

    `"Email": "test@example.com",`

    `"Subject": "Task Complete",`

    `"Body": "Your task is complete"`

  `},`

  `"Outputs": {}`

`}`

### **4\. SetVariableStep.cs** {#4.-setvariablestep.cs}

#### **Purpose:** {#purpose:-3}

Sets or updates a variable within the workflow instance.

#### **Input:** {#input:-3}

* `ApplicationWorkflowInstanceId` (string): The ID of the application workflow instance.

* `VariableName` (string): The name of the variable to set.

* `VariableValue` (object): The value to assign to the variable.

#### **Output:** {#output:-3}

* No direct output.

#### **Example Workflow JSON:** {#example-workflow-json:-3}

`{`

  `"Id": "SetVariableStep",`

  `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.SetVariableStep, Amnil.AccessControlManagementSystem.Application",`

  `"NextStepId": "NextStepId",`

  `"Inputs": {`

    `"ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",`

    `"VariableName": "Status",`

    `"VariableValue": "Completed"`

  `},`

  `"Outputs": {}`

`}`

### **5\. SleepStep.cs** {#5.-sleepstep.cs}

#### **Purpose:** {#purpose:-4}

Pauses the workflow for a specified duration.

#### **Input:** {#input:-4}

* `Period` (TimeSpan): The duration to pause the workflow.

#### **Output:** {#output:-4}

* No direct output.

#### **Example Workflow JSON:** {#example-workflow-json:-4}

`{`

  `"Id": "SleepStep",`

  `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.SleepStep, Amnil.AccessControlManagementSystem.Application",`

  `"NextStepId": "NextStepId",`

  `"Inputs": {`

    `"Period": "00:00:30"`

  `},`

  `"Outputs": {}`

`}`

### 

### 

### **6\. StartWorkflowInstanceStep.cs** {#6.-startworkflowinstancestep.cs}

#### **Purpose:** {#purpose:-5}

Starts a new workflow instance for a provided application.

#### **Input:** {#input:-5}

* `ApplicationWorkflowInstanceId` (string): The ID of the application workflow instance.

#### **Output:** {#output:-5}

* `WorkflowInstanceId` (Guid): The ID of the newly created workflow instance.

#### **Example Workflow JSON:** {#example-workflow-json:-5}

`{`

  `"Id": "StartWorkflowInstanceStep",`

  `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.StartWorkflowInstanceStep, Amnil.AccessControlManagementSystem.Application",`

  `"NextStepId": "NextStepId",`

  `"Inputs": {`

    `"ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]"`

  `},`

  `"Outputs": {`

    `"WorkflowInstanceId": "step.WorkflowInstanceId"`

  `}`

`}`

### 

### **7\. UpdateApplicationTaskStageStep.cs** {#7.-updateapplicationtaskstagestep.cs}

#### **Purpose:** {#purpose:-6}

Updates the stage of an application task within the workflow.

#### **Input:** {#input:-6}

* `ApplicationWorkflowInstanceId` (string): The ID of the application workflow instance.

* `StageName` (string): The name of the stage (e.g., "Requested", "In Progress").

* `SubStageName` (string, optional): The name of the sub-stage (e.g., "Review").

* `Remarks` (string, optional): Additional details about the stage.

#### **Output:** {#output:-6}

* No direct output.

#### **Example Workflow JSON:** {#example-workflow-json:-6}

`{`

  `"Id": "UpdateApplicationTaskStageStep",`

  `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",`

  `"NextStepId": "NextStepId",`

  `"Inputs": {`

    `"ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",`

    `"StageName": "Requested",`

    `"SubStageName": "Approval Requested",`

    `"Remarks": "Approval Requested for task id: data[\"applicationWorkflowInstanceId\"]"`

  `},`

  `"Outputs": {}`

`}`

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### **8\. UpdateOperationTaskStageStep.cs** {#8.-updateoperationtaskstagestep.cs}

#### **Purpose:** {#purpose:-7}

Updates the stage of an operation task in the workflow.

#### **Input:** {#input:-7}

* `OperationWorkflowInstanceId` (string): The ID of the operation workflow instance.

* `ApplicationWorkflowInstanceId` (string): The ID of the application workflow instance.

* `Remarks` (string, optional): Additional remarks.

* `CurrentUserId` (string, optional): The ID of the current user.

#### **Output:** {#output:-7}

* `OperationStatus` (string): The status of the operation after the update.

#### **Example Workflow JSON:** {#example-workflow-json:-7}

`{`

  `"Id": "UpdateOperationTaskStageStep",`

  `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateOperationTaskStageStep, Amnil.AccessControlManagementSystem.Application",`

  `"NextStepId": "NextStepId",`

  `"Inputs": {`

    `"OperationWorkflowInstanceId": "data[\"operationWorkflowInstanceId\"]",`

    `"ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",`

    `"Remarks": "Operation Workflow stage changed to processing"`

  `},`

  `"Outputs": {`

    `"OperationStatus": "step.OperationStatus"`

  `}`

`}`

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### **9\. UpdateWorkflowEventStatusStep.cs** {#9.-updateworkfloweventstatusstep.cs}

#### **Purpose:** {#purpose:-8}

Updates the status of a workflow event.

#### **Input:** {#input:-8}

* `WorkflowEventId` (string): The ID of the workflow event to update.

* `EventData` (JObject): The data to update the event with.

#### **Output:** {#output:-8}

* No direct output.

#### **Example Workflow JSON:** {#example-workflow-json:-8}

`{`

  `"Id": "UpdateWorkflowEventStatusStep",`

  `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateWorkflowEventStatusStep, Amnil.AccessControlManagementSystem.Application",`

  `"NextStepId": "NextStepId",`

  `"Inputs": {`

    `"WorkflowEventId": "data[\"workflowEventId\"]",`

    `"EventData": "{ \"status\": \"completed\" }"`

  `},`

  `"Outputs": {}`

`}`

### 

### **10\. ValidateRulesStep.cs** {#10.-validaterulesstep.cs}

#### **Purpose:** {#purpose:-9}

Validates a rule using a rules engine.

#### **Input:** {#input:-9}

* `RuleName` (string): The name of the rule to validate.

* `Inputs` (array of objects): The data to validate against the rule.

#### **Output:** {#output:-9}

* `Response` (JObject): The result of the validation, typically containing whether the validation passed and any validation messages.

#### **Example Workflow JSON:** {#example-workflow-json:-9}

`{`

  `"Id": "ValidateRulesStep",`

  `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.ValidateRulesStep, Amnil.AccessControlManagementSystem.Application",`

  `"NextStepId": "NextStepId",`

  `"Inputs": {`

    `"RuleName": "SomeRuleName",`

    `"Inputs": "data[\"applicationDetails\"]"`

  `},`

  `"Outputs": {`

    `"Response": "step.Response"`

  `}`

`}`

### **11\. PrintMessageStep.cs** {#11.-printmessagestep.cs}

#### **Purpose:** {#purpose:-10}

Logs a custom message to provide helpful information or status updates at any point in the workflow.

#### **Input:** {#input:-10}

* `Message` (string): The message to be printed. Typically, it may include data from previous steps or variables (e.g., task IDs).

#### **Output:** {#output:-10}

* There is no output; this step simply logs information.

#### **Example Workflow JSON:** {#example-workflow-json:-10}

`{`

  `"Id": "PrintTaskId",`

  `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",`

  `"NextStepId": "UpdateRequestedWorkflowStageStep",`

  `"Inputs": {`

    `"Message": "\"Requested - Task Id: \" + data[\"applicationWorkflowInstanceId\"]"`

  `}`

`}`

### 

### 

### 

### 

### **12\. PublishWorkflowEventStep.cs** {#12.-publishworkfloweventstep.cs}

#### **Purpose:** {#purpose:-11}

Publishes a workflow event with the provided event data.

#### **Input:** {#input:-11}

* `EventName` (string): The name of the event to publish.

* `EventKey` (string): The event key.

* `EventData` (JObject): Data to be sent with the event.

#### **Output:** {#output:-11}

* No direct output.

#### **Example Workflow JSON:** {#example-workflow-json:-11}

`{`

  `"Id": "PublishWorkflowEventStep",`

  `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PublishWorkflowEventStep, Amnil.AccessControlManagementSystem.Application",`

  `"NextStepId": "NextStepId",`

  `"Inputs": {`

    `"EventName": "EventStart",`

    `"EventKey": "key1",`

    `"EventData": "{ \"key\": \"value\" }"`

  `},`

  `"Outputs": {}`

`}`

### 

### **13\. SendEmailNotificationStep.cs** {#13.-sendemailnotificationstep.cs}

#### **Purpose:** {#purpose:-12}

Sends an email notification with the provided content.

#### **Input:** {#input:-12}

* `Email` (string): The recipient email address.

* `Subject` (string): The subject of the email.

* `Body` (string): The body content of the email.

#### **Output:** {#output:-12}

* No direct output.

#### **Example Workflow JSON:** {#example-workflow-json:-12}

`{`

  `"Id": "SendEmailNotificationStep",`

  `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.SendEmailNotificationStep, Amnil.AccessControlManagementSystem.Application",`

  `"NextStepId": "NextStepId",`

  `"Inputs": {`

    `"Email": "test@example.com",`

    `"Subject": "Task Complete",`

    `"Body": "Your task is complete"`

  `},`

  `"Outputs": {}`

`}`

### 

### **14\. SetVariableStep.cs** {#14.-setvariablestep.cs}

#### **Purpose:** {#purpose:-13}

Sets or updates a variable within the workflow instance.

#### **Input:** {#input:-13}

* `ApplicationWorkflowInstanceId` (string): The ID of the application workflow instance.

* `VariableName` (string): The name of the variable to set.

* `VariableValue` (object): The value to assign to the variable.

#### **Output:** {#output:-13}

* No direct output.

#### **Example Workflow JSON:** {#example-workflow-json:-13}

`{`

  `"Id": "SetVariableStep",`

  `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.SetVariableStep, Amnil.AccessControlManagementSystem.Application",`

  `"NextStepId": "NextStepId",`

  `"Inputs": {`

    `"ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",`

    `"VariableName": "Status",`

    `"VariableValue": "Completed"`

  `},`

  `"Outputs": {}`

`}`

### **15\. SleepStep.cs** {#15.-sleepstep.cs}

#### **Purpose:** {#purpose:-14}

Pauses the workflow for a specified duration.

#### **Input:** {#input:-14}

* `Period` (TimeSpan): The duration to pause the workflow.

#### **Output:** {#output:-14}

* No direct output.

#### **Example Workflow JSON:** {#example-workflow-json:-14}

`{`

  `"Id": "SleepStep",`

  `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.SleepStep, Amnil.AccessControlManagementSystem.Application",`

  `"NextStepId": "NextStepId",`

  `"Inputs": {`

    `"Period": "00:00:30"`

  `},`

  `"Outputs": {}`

`}`

### 

### **16\. StartWorkflowInstanceStep.cs** {#16.-startworkflowinstancestep.cs}

#### **Purpose:** {#purpose:-15}

Starts a new workflow instance for a provided application.

#### **Input:** {#input:-15}

* `ApplicationWorkflowInstanceId` (string): The ID of the application workflow instance.

#### **Output:** {#output:-15}

* `WorkflowInstanceId` (Guid): The ID of the newly created workflow instance.

#### **Example Workflow JSON:** {#example-workflow-json:-15}

`{`

  `"Id": "StartWorkflowInstanceStep",`

  `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.StartWorkflowInstanceStep, Amnil.AccessControlManagementSystem.Application",`

  `"NextStepId": "NextStepId",`

  `"Inputs": {`

    `"ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]"`

  `},`

  `"Outputs": {`

    `"WorkflowInstanceId": "step.WorkflowInstanceId"`

  `}`

`}`

### **17\. UpdateApplicationTaskStageStep.cs** {#17.-updateapplicationtaskstagestep.cs}

#### **Purpose:** {#purpose:-16}

Updates the stage of an application task within the workflow.

#### **Input:** {#input:-16}

* `ApplicationWorkflowInstanceId` (string): The ID of the application workflow instance.

* `StageName` (string): The name of the stage (e.g., "Requested", "In Progress").

* `SubStageName` (string, optional): The name of the sub-stage (e.g., "Review").

* `Remarks` (string, optional): Additional details about the stage.

#### **Output:** {#output:-16}

* No direct output.

#### **Example Workflow JSON:** {#example-workflow-json:-16}

**`{`**

  **`"Id": "UpdateApplicationTaskStageStep",`**

  **`"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",`**

  **`"NextStepId": "NextStepId",`**

  **`"Inputs": {`**

    **`"ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",`**

    **`"StageName": "Requested",`**

    **`"SubStageName": "Approval Requested",`**

    **`"Remarks": "Approval Requested for task id: data[\"applicationWorkflowInstanceId\"]"`**

  **`},`**

  **`"Outputs": {}`**

**`}`**

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### **18\. UpdateOperationTaskStageStep.cs** {#18.-updateoperationtaskstagestep.cs}

#### **Purpose:** {#purpose:-17}

Updates the stage of an operation task in the workflow.

#### **Input:** {#input:-17}

* `OperationWorkflowInstanceId` (string): The ID of the operation workflow instance.

* `ApplicationWorkflowInstanceId` (string): The ID of the application workflow instance.

* `Remarks` (string, optional): Additional remarks.

* `CurrentUserId` (string, optional): The ID of the current user.

#### **Output:** {#output:-17}

* `OperationStatus` (string): The status of the operation after the update.

#### **Example Workflow JSON:** {#example-workflow-json:-17}

`{`

  `"Id": "UpdateOperationTaskStageStep",`

  `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateOperationTaskStageStep, Amnil.AccessControlManagementSystem.Application",`

  `"NextStepId": "NextStepId",`

  `"Inputs": {`

    `"OperationWorkflowInstanceId": "data[\"operationWorkflowInstanceId\"]",`

    `"ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",`

    `"Remarks": "Operation Workflow stage changed to processing"`

  `},`

  `"Outputs": {`

    `"OperationStatus": "step.OperationStatus"`

  `}`

`}`

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### 

### **19\. UpdateWorkflowEventStatusStep.cs** {#19.-updateworkfloweventstatusstep.cs}

#### **Purpose:** {#purpose:-18}

Updates the status of a workflow event.

#### **Input:** {#input:-18}

* `WorkflowEventId` (string): The ID of the workflow event to update.

* `EventData` (JObject): The data to update the event with.

#### **Output:** {#output:-18}

* No direct output.

#### **Example Workflow JSON:** {#example-workflow-json:-18}

`{`

  `"Id": "UpdateWorkflowEventStatusStep",`

  `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateWorkflowEventStatusStep, Amnil.AccessControlManagementSystem.Application",`

  `"NextStepId": "NextStepId",`

  `"Inputs": {`

    `"WorkflowEventId": "data[\"workflowEventId\"]",`

    `"EventData": "{ \"status\": \"completed\" }"`

  `},`

  `"Outputs": {}`

`}`

### 

### **20\. ValidateRulesStep.cs** {#20.-validaterulesstep.cs}

#### **Purpose:** {#purpose:-19}

Validates a rule using a rules engine.

#### **Input:** {#input:-19}

* `RuleName` (string): The name of the rule to validate.

* `Inputs` (array of objects): The data to validate against the rule.

#### **Output:** {#output:-19}

* `Response` (JObject): The result of the validation, typically containing whether the validation passed and any validation messages.

#### **Example Workflow JSON:** {#example-workflow-json:-19}

`{`

  `"Id": "ValidateRulesStep",`

  `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.ValidateRulesStep, Amnil.AccessControlManagementSystem.Application",`

  `"NextStepId": "NextStepId",`

  `"Inputs": {`

    `"RuleName": "SomeRuleName",`

    `"Inputs": "data[\"applicationDetails\"]"`

  `},`

  `"Outputs": {`

    `"Response": "step.Response"`

  `}`

`}`

### 

### **21\. AddNocoDBRecordStep**

#### **Purpose:**

Adds record to NocoDB table.

#### **Input:**

* `TableName`(string): The name of the NocoDB table.

* `Data`(JObject): The data of the  NocoDB table.

#### **Output:**

* `Id` (string): Id of insert record.

#### **Example Workflow JSON:**

`{`

  `"Id": "NocoDBRecordStep",`

  `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.AddNocoDBRecordStep, Amnil.AccessControlManagementSystem.Application",`

  `"Inputs": {`

    `"TableName": "NocoDB Table Name",`

    `"@Data": {`

`“ApplicationName”: “Finacle”`

`}`

  `},`

  `"Outputs": {`

    `"Id": "step.Id"`

  `}`

`}`

**22\. CallApiStep.cs**

**Purpose:**  
Executes an HTTP API call using a specified dynamic HTTP client within the workflow.

**Input:**

* ApiRequest (JObject, optional): The JSON object representing the API request payload and metadata (e.g., URL, headers, body).

* ApiClientName (string): The name of the API client configuration to use for the request.

**Output:**

* Response (JObject): The raw response received from the API call.

**Example Workflow JSON:**

`{`

  `"Id": "FinancleRoleChangeApiRequestsWorkflow",`

  `"Version": 3,`

  `"DataType": "Amnil.AccessControlManagementSystem.Workflows.DynamicData, Amnil.AccessControlManagementSystem.Application.Contracts",`

  `"DefaultErrorBehavior": "Terminate",`

  `"Steps": [`

    `{`

    `"Id": "PrintTaskId",`

      `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",`

      `"NextStepId": "ApplicationInprogressStage",`

      `"Inputs": {`

        `"Message": "\"Operation Retry for the application task Id \" + data[\"applicationWorkflowInstanceId\"]"`

    `}`

    `},`

    `{`

    `"Id": "ApplicationInprogressStage",`

      `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",`

      `"NextStepId": "ApiStep",`

      `"Inputs": {`

        `"ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",`

        `"StageName": "\"PROCESSING\"",`

        `"SubStageName": "\"APPLICATION_ACTION_JOB_IN_PROGRESS\""`

    `}`

    `},`

    `{`

    `"Id": "ApiStep",`

      `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.CallApiStep, Amnil.AccessControlManagementSystem.Application",`

      `"NextStepId": "FinancleRoleChangeApiRequests",`

      `"Inputs": {`

        `"ApiClientName": "\"GET_MBL_APPLICATIONS_API_DUMMY_TEST\"",`

        `"ApiRequest": {`

          `"@employeeName": "data[\"operationFormData\"].operationForm.employeeName",`

          `"@roleCode": "data[\"applicationFormData\"].roleChange.roleCode",`

          `"@roleName": "data[\"applicationFormData\"].roleChange.roleName"`

        `}`

    `},`

      `"Outputs": {`

        `"RoleChangeApiResponse": "step.Response"`

    `}`

    `},`

    `{`

    `"Id": "FinancleRoleChangeApiRequests",`

      `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.AddNocoDBRecordStep, Amnil.AccessControlManagementSystem.Application",`

      `"NextStepId": "PrintApplicationTemplate",`

      `"Inputs": {`

        `"TableName": "\"FinancleRoleChangeApiRequests\"",`

        `"Data": {`

          `"ApiClientName": "GET_MBL_APPLICATIONS_API_DUMMY_TEST",`

          `"@AppTaskWorkflowId": "data[\"applicationWorkflowInstanceId\"]",`

          `"@EmployeeName": "data[\"operationFormData\"].operationForm.employeeName",`

          `"@TargetRoleCode": "data[\"applicationFormData\"].roleChange.roleCode",`

          `"@TargetRoleName": "data[\"applicationFormData\"].roleChange.roleName",`

          `"@Status": "data[\"RoleChangeApiResponse\"].success",`

          `"@ErrorMessage": "Convert.ToBoolean(data[\"RoleChangeApiResponse\"].success)? \"\":data[\"RoleChangeApiResponse\"].error"`

        `}`

    `},`

      `"Outputs": {`

        `"Id": "step.Id"`

    `}`

    `},`

    `{`

    `"Id": "PrintApplicationTemplate",`

      `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",`

      `"NextStepId": "ApplicationPublishCompleted",`

      `"Inputs": {`

        `"Message": "\"Data \" + data[\"Data\"]"`

    `}`

    `},`

    `{`

    `"Id": "ApplicationPublishCompleted",`

      `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",`

      `"NextStepId": "UpdateOperationStage",`

      `"Inputs": {`

        `"ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",`

        `"StageName": "\"COMPLETED\"",`

        `"SubStageName": "\"APPLICATION_ACTION_SUCCESS\"",`

        `"Remarks": "\"Application Data passed for application Id: \" + data[\"applicationWorkflowInstanceId\"]"`

    `}`

    `},`

    `{`

    `"Id": "UpdateOperationStage",`

      `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateOperationTaskStageStep, Amnil.AccessControlManagementSystem.Application",`

      `"NextStepId": "EndWorkflow",`

      `"Inputs": {`

        `"OperationWorkflowInstanceId": "data[\"operationWorkflowInstanceId\"]",`

        `"ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",`

        `"Remarks": "\"Operation Workflow has completed\""`

    `}`

    `},`

    `{`

    `"Id": "EndWorkflow",`

      `"StepType": "WorkflowCore.Primitives.EndStep, WorkflowCore"`

    `}`

  `]`

`}`

**23.CreateWorkflowEventStep.cs**

**Purpose:**  
Creates a workflow event tied to a specific application and optionally an operation workflow instance.

**Input:**

* ApplicationWorkflowInstanceId (string): The ID of the application workflow instance.

* OperationWorkflowInstanceId (string, optional): The ID of the operation workflow instance, if applicable.

* EventName (string): The name of the event to be created.

* EventData (JObject, optional): Additional data associated with the workflow event.

**Output:**

* WorkflowEventId (string): The unique ID of the created workflow event.

 

**24\. DeleteRecordOnNocoDBStep.cs**

 **Purpose:**  
 Deletes a specific record from a NocoDB table based on the provided ID.

**Input:**

* TableName (string): The name of the NocoDB table from which the record should be deleted.

* Id (string): The unique identifier of the record to be deleted.

**Output:**  
 *None.*

**25\. GetRecordByIdOnNocoDBStep.cs**

**Purpose:**  
Retrieves a single record from a NocoDB table by its unique identifier.

**Input:**

* TableName (string): The name of the NocoDB table from which the record should be fetched.

* Id (string): The ID of the record to retrieve.

**Output:**

* Data (JObject): The record data retrieved from NocoDB, returned as a JSON object.

**Example Workflow json**  
 `{`

  `"Id": "GetRecordByIdOnNocoDB",`

  `"Version": 3,`

  `"DataType": "Amnil.AccessControlManagementSystem.Workflows.DynamicData, Amnil.AccessControlManagementSystem.Application.Contracts",`

  `"DefaultErrorBehavior": "Terminate",`

  `"Steps": [`

    `{`

    `"Id": "NocoDBRecordStep",`

      `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GetRecordByIdOnNocoDBStep, Amnil.AccessControlManagementSystem.Application",`

      `"NextStepId": "PrintApplicationTemplate",`

      `"Inputs": {`

        `"TableName": "\"RPAJobs\"",`

        `"Id": "5g"`

    `},`

      `"Outputs": {`

        `"Data": "step.Data"`

    `}`

    `},`

    `{`

    `"Id": "PrintApplicationTemplate",`

      `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",`

      `"NextStepId": "EndWorkflow",`

      `"Inputs": {`

        `"Message": "\"Data \" + data[\"Data\"]"`

    `}`

    `},`

    `{`

    `"Id": "EndWorkflow",`

      `"StepType": "WorkflowCore.Primitives.EndStep, WorkflowCore"`

    `}`

  `]`

`}`

 

**26\. GetRecordOnNocoDBStep.cs**  
 

**Purpose:**  
Fetches records from a specified NocoDB table using custom filter parameters.

**Input:**

* TableName (string): The name of the NocoDB table from which to retrieve records.

* NocoDbFilterParams (NocoDbFilterParams): The filtering parameters used to query the records from NocoDB. This can include filters, sorting, pagination, and other query options.

**Output:**

* Data (JObject): A JSON object containing the list of retrieved records from NocoDB.

**Example Workflow JSON:**

`{`

  `"Id": "GetRecordOnNocoDB",`

  `"Version": 1,`

  `"DataType": "Amnil.AccessControlManagementSystem.Workflows.DynamicData, Amnil.AccessControlManagementSystem.Application.Contracts",`

  `"DefaultErrorBehavior": "Terminate",`

  `"Steps": [`

    `{`

    `"Id": "NocoDBRecordStep",`

      `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GetRecordOnNocoDBStep, Amnil.AccessControlManagementSystem.Application",`

      `"NextStepId": "PrintApplicationTemplate",`

      `"Inputs": {`

        `"TableName": "\"RPAJobs\"",`

        `"NocoDbFilterParams": {`

          `"fields": null,`

          `"where": "",`

          `"offset": "",`

          `"limit": "",`

          `"sort": "",`

          `"viewId": ""`

        `}`

    `},`

      `"Outputs": {`

        `"Data": "step.Data"`

    `}`

    `},`

    `{`

    `"Id": "PrintApplicationTemplate",`

      `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",`

      `"NextStepId": "EndWorkflow",`

      `"Inputs": {`

        `"Message": "\"Data \" + data[\"Data\"]"`

    `}`

    `},`

    `{`

    `"Id": "EndWorkflow",`

      `"StepType": "WorkflowCore.Primitives.EndStep, WorkflowCore"`

    `}`

  `]`

`}`

**27\. GetWorkflowEventStep.cs**  
 

**Purpose:**  
Retrieves all workflow events associated with a given OperationWorkflowInstanceId.

**Input:**

* OperationWorkflowInstanceId (string): The unique identifier of the operation workflow instance to retrieve events for.

**Output:**

* Response (JObject): A JSON object containing the list of workflow events and their total count.

`{`

  `"Id": "GetEventWorkflow",`

  `"Version": 14,`

  `"DataType": "Amnil.AccessControlManagementSystem.Workflows.DynamicData, Amnil.AccessControlManagementSystem.Application.Contracts",`

  `"DefaultErrorBehavior": "Compensate",`

  `"Steps": [`

    `{`

    `"Id": "PrintTaskId",`

      `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",`

      `"NextStepId": "UpdateRequestedWorkflowStageStep",`

      `"Inputs": {`

        `"Message": "\"Requested - Task Id: \" + data[\"applicationWorkflowInstanceId\"]"`

    `}`

    `},`

    `{`

    `"Id": "UpdateRequestedWorkflowStageStep",`

      `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",`

      `"NextStepId": "UpdateInitialOperationStage",`

      `"Inputs": {`

        `"ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",`

        `"StageName": "\"REQUESTED\"",`

        `"SubStageName": "\"APPROVAL_REQUESTED\"",`

        `"Remarks": "\"Approval Requested for task id: \" + data[\"applicationWorkflowInstanceId\"]"`

    `}`

    `},`

    `{`

    `"Id": "UpdateInitialOperationStage",`

      `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateOperationTaskStageStep, Amnil.AccessControlManagementSystem.Application",`

      `"NextStepId": "GetApplicationListEvent",`

      `"Inputs": {`

        `"OperationWorkflowInstanceId": "data[\"operationWorkflowInstanceId\"]",`

        `"ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",`

        `"Remarks": "\"Operation Workflow stage changed to processing\""`

    `},`

      `"Outputs": {`

        `"OperationStatus": "step.OperationStatus"`

    `}`

    `},`

    `{`

    `"Id": "GetApplicationListEvent",`

      `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.GetWorkflowEventStep, Amnil.AccessControlManagementSystem.Application",`

      `"NextStepId": "CheckEventResponse",`

      `"Inputs": {`

        `"OperationWorkflowInstanceId": "data[\"operationWorkflowInstanceId\"]"`

    `},`

      `"Outputs": {`

        `"applicationCount": "step.Response[\"totalCount\"]",`

        `"applicationDetails": "step.Response[\"data\"]"`

    `}`

    `},`

    `{`

    `"Id": "CheckEventResponse",`

      `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateApplicationTaskStageStep, Amnil.AccessControlManagementSystem.Application",`

      `"NextStepId": "EndWorkflow",`

      `"Inputs": {`

        `"ApplicationWorkflowInstanceId": "data[\"applicationWorkflowInstanceId\"]",`

        `"StageName": "\"FAILED\"",`

        `"SubStageName": "\"APPLICATION_ACTION_FAILED\"",`

        `"Remarks": "\"Sol API Failed for task id: \" + data[\"applicationDetails\"]"`

    `}`

    `},`

    `{`

    `"Id": "EndWorkflow",`

      `"StepType": "WorkflowCore.Primitives.EndStep, WorkflowCore"`

    `}`

  `]`

`}`

**28\. IncrementStep.cs**

**Purpose:**  
Performs a basic arithmetic operation by incrementing an integer value.

**Input:**

* Value1 (int): The input value to be incremented.

**Output:**

* Value2 (int): The result of Value1 \+ 1\.

**29\. PublishWorkflowEventStep.cs**  
 

**Purpose:**  
Publishes a workflow event using the IWorkflowHost to notify other workflows waiting on the specified event.

**Input:**

* EventName (string): The name of the event to publish.

* EventKey (string): The key used to correlate the event to the correct workflow instance(s).

* EventData (JObject): The payload of the event to be published.

**Output:**

* None.

**30\. RenderTemplateStep.cs**

**Purpose:**  
Renders a template with dynamic data using the ITemplateService.

**Input:**

* TemplateName (string): The name of the template to render. This is required and must not be null or empty.

* Model (JObject): A JSON object representing the dynamic model to be passed into the template.

**Output:**

* Response (string): The rendered output of the template as a string.

 

**31\. UpdateRecordOnNocoDBStep.cs**

**Purpose:**  
Updates an existing record in a NocoDB table using the IDynamicTableProxyAppService.

**Inputs:**

* TableName (string): The name of the NocoDB table to update.

* Data (JObject): A JSON object representing the data to update. Must contain the ID or key for the existing record.

**Output:**

* Id (string): The ID of the updated record.

 

`{`

  `"Id": "UpdateNocoDBData",`

  `"Version": 1,`

  `"DataType": "Amnil.AccessControlManagementSystem.Workflows.DynamicData, Amnil.AccessControlManagementSystem.Application.Contracts",`

  `"DefaultErrorBehavior": "Terminate",`

  `"Steps": [`

    `{`

    `"Id": "UpdateNocoDBRecordStep",`

      `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.UpdateRecordOnNocoDBStep, Amnil.AccessControlManagementSystem.Application",`

      `"NextStepId": "PrintApplicationTemplate",`

      `"Inputs": {`

        `"TableName": "\"FinancleRoleChangeApiRequests\"",`

        `"Data": {`

          `"@ApiClientName": "\"GET_MBL_APPLICATIONS_API_DUMMY_TEST\"",`

          `"@WorkflowId": "",`

          `"@AppTaskWorkflowId": "data[\"applicationWorkflowInstanceId\"]",`

          `"@Status": true`

        `}`

    `},`

      `"Outputs": {`

        `"Id": "step.Id"`

    `}`

    `},`

    `{`

    `"Id": "PrintApplicationTemplate",`

      `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.PrintMessageStep, Amnil.AccessControlManagementSystem.Application",`

      `"NextStepId": "EndWorkflow",`

      `"Inputs": {`

        `"Message": "\"Id \" + data[\"Id\"]"`

    `}`

    `},`

    `{`

    `"Id": "EndWorkflow",`

      `"StepType": "WorkflowCore.Primitives.EndStep, WorkflowCore"`

    `}`

  `]`

`}`

 **32\. AddReversalOperationRequestStep**

**Purpose:** Step for temporary transfer.

**Inputs:**

* OperationWorkflowInstanceId(string): The name of the NocoDB table to update.

* OperationForms(JObject): A JSON object representing the data to update.

* ApplicationForms(JObject): A JSON object representing the data to update

* CurrentUserDetail(JObject)


**Output:**

* Id (string): The ID of the created record.

 `{`

`Example:`

`{`

  `"Id": "OperationRequesTesting",`

  `"Version": 1,`

  `"DataType": "Amnil.AccessControlManagementSystem.Workflows.DynamicData, Amnil.AccessControlManagementSystem.Application.Contracts",`

  `"Steps": [`

    `{`

      `"Id": "AddOperationRequest",`

      `"StepType": "Amnil.AccessControlManagementSystem.Workflows.Steps.AddReversalOperationRequestStep, Amnil.AccessControlManagementSystem.Application",`

      `"Inputs": {`

        `"OperationWorkflowInstanceId": "\"3a1ab774-ae5f-1d99-9cb9-e280c17670ac\"",`

        `"operationForms": {`

          `"userAccountForm": {`

            `"userAccountIdentifier": "7002"`

          `}`

        `},`

        `"applicationForms": {`

          `"applicationWorkflowInstanceId": "1224-fae3-1224-fae3",`

          `"applicationForms": {`

            `"userAccountForm": {`

              `"userIdentifier": "min@yopmail.com"`

            `}`

          `}`

        `}`

      `},`

      `"Outputs": {`

        `"OperationWorkflowInstanceId": "step.Response"`

      `}`

    `}`

  `]`

`}`
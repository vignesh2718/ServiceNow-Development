## Business Rules and Use Cases

### Business Rules

A business rule is a piece of logic or functionality implemented within a system to automate processes or enforce policies. In the context of this document, we'll focus on a specific business rule that triggers actions based on changes to the priority of a problem record.

### Use Cases

#### Use Case 1: Priority Change Triggers Problem Task Creation

**Description:**
- When the priority of a problem record changes to "Critical", the system will automatically create two different types of problem tasks: "General" and "Root Cause Analysis".
- Additionally, the short description field of each created task will mention its type.

**Business Rule Implementation:**
```javascript
(function executeRule(current, previous /*null when async*/) {
    var types = ['General', 'Root Cause Analysis'];
    for (var i = 0; i < 2; i++) {
        var gr = new GlideRecord('problem_task');
        gr.initialize();
        gr.problem_task_type = types[i];
        gr.short_description = 'Task Type is ' + types[i];
        gr.problem = current.sys_id;
        gr.insert();
    }
})(current, previous);
```

#### Use Case 2: Custom Actions Based on Priority Change

**Description:**
- Depending on the priority change, different actions can be triggered, such as notifying specific stakeholders, escalating the issue, or updating related records.

**Example:**
- If priority changes from "High" to "Critical", notify the incident manager and escalate the issue to the higher management.

#### Use Case 3: Priority-based Routing of Tasks

**Description:**
- Priority changes can also trigger routing of tasks to different teams or individuals responsible for handling issues of varying urgency.

**Example:**
- If priority changes to "Critical", assign the task to the senior support engineer for immediate attention.

### Conclusion

These use cases illustrate how a business rule can be utilized to automate processes and streamline workflow based on changes in priority within a problem management system. Each use case demonstrates a different aspect of how such a rule can be applied to enhance efficiency and ensure timely resolution of critical issues.
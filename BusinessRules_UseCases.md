## Business Rules and Use Cases

### Business Rules

Business rules are implemented within a system to automate processes or enforce policies. In this document, we'll discuss two specific business rules related to incident and problem management.

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

#### Use Case 2: Syncing Work Notes between Incident and Problem Records

**Description:**
- When the work notes for an incident record change, the same work notes should be updated in the associated problem record as well.

**Business Rule Implementation:**
```javascript
(function executeRule(current, previous /*null when async*/) {
     var gr = new GlideRecord('problem');
	 gr.addQuery('sys_id',current.problem_id);
	 gr.query();
	 if(gr.next()){
		gr.work_notes=current.work_notes.getJournalEntry(1);
	 }
	 gr.update();
})(current, previous);
```

### Conclusion

These use cases demonstrate how business rules can be utilized within incident and problem management systems to automate processes and ensure data consistency between related records. By implementing these rules, organizations can improve efficiency and reduce manual effort in managing incidents and problems effectively.
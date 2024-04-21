## UI Actions Use Cases

### Overview

This readme.md file outlines three use cases for UI Actions in ServiceNow. UI Actions can be executed on both the server side and client side, providing flexibility in implementing various functionalities within ServiceNow forms.

### Use Case 1: Server Side UI Action

**Description:**
- If the priority of the incident is critical and it is assigned to the Network team, a button labeled 'Create Child Incident' will appear in the form.
- Clicking the button will create a child incident assigned to 'Network Cab Managers'.
- The child incident will have the same caller and short description as the parent incident but with a priority of 3.

**Condition in the UI Action:**
```javascript
(current.priority == 1) && (current.assignment_group == gs.getProperty('getNetworkId'))
```

**UI Action Script:**
```javascript
var gr = new GlideRecord('incident');
gr.initialize();
gr.parent_incident = current.sys_id;
gr.caller_id = current.caller_id;
gr.short_description = current.short_description;
gr.assignment_group = gs.getProperty('getNetwork');
action.setRedirectURL(current);
gr.insert();
```


### Conclusion

UI Actions in ServiceNow offer powerful capabilities for customizing and extending form functionalities. By leveraging UI Actions, administrators and developers can implement various actions, validations, and workflows to enhance user experience and streamline processes within ServiceNow instances.
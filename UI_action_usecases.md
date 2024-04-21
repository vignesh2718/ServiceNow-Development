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

### Use Case 2: Client Side UI Action

**Description:**
- Upon clicking a button labeled 'Send Email', a client-side UI Action will validate the email field in the incident form.
- If the email field is empty or invalid, an error message will be displayed to the user.
- If the email field is valid, the system will send an email to the specified recipient.

**Client Side UI Action Script:**
```javascript
function sendEmail() {
    var email = g_form.getValue('u_email');
    if (!email || !validateEmail(email)) {
        alert('Please enter a valid email address.');
    } else {
        // Send email logic here
    }
}

function validateEmail(email) {
    // Email validation logic here
}
```

### Use Case 3: Server and Client Side UI Action

**Description:**
- A button labeled 'Mark as Resolved' will appear in the incident form.
- Clicking the button will change the incident state to 'Resolved' and display a confirmation message to the user.
- This UI Action will run both on the server side to update the incident state and on the client side to display the confirmation message.

**UI Action Script (Both Server and Client Side):**
```javascript
if (gs.getUser().hasRole('itil')) {
    current.state = 6; // Resolved state
    current.update();
    alert('Incident marked as resolved.');
}
```

### Conclusion

UI Actions in ServiceNow offer powerful capabilities for customizing and extending form functionalities. By leveraging UI Actions, administrators and developers can implement various actions, validations, and workflows to enhance user experience and streamline processes within ServiceNow instances.
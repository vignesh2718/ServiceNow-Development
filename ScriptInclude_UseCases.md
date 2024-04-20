## Script Include Complex Use Cases

This readme.md file outlines a complex use case scenario involving a Script Include and a Client Script to create a new field called 'Number of Group Members' in the incident form. When the assignment group is changed on the incident form, it should display the number of group members available for the selected assignment group.

### Use Case Description

**Description:**
- When an incident form is opened and the assignment group is changed, a new field called 'Number of Group Members' should display the count of group members available for the selected assignment group.

### Script Include: `getGroupMember`

The `getGroupMember` Script Include contains a function named `grpMember` that retrieves the number of group members for a given assignment group.

```javascript
grpMember: function() {
    var count = '';
    var groupName = this.getParameter('sysparm_assignment_group');
    var gr = new GlideRecord('sys_user_grmember');
    gr.addQuery('group', groupName);
    gr.query();

    if (gr.next()) {
        count = gr.getRowCount(); 
    } else {
        count = 'There are no group members available';
    }
    return count;
}
```

### Client Script

The Client Script utilizes `GlideAjax` to call the `grpMember` function from the `getGroupMember` Script Include and updates the 'Number of Group Members' field in the incident form.

```javascript
var ga = new GlideAjax('getGroupMember');
ga.addParam('sysparm_name', 'grpMember');
ga.addParam('sysparm_assignment_group', g_form.getValue('assignment_group'));
ga.getXMLAnswer(countMember);

function countMember(response) {
    if (response > 0) {
        g_form.setValue('u_number_of_group_member', response);
    } else {
        alert(response);
    }
}
```


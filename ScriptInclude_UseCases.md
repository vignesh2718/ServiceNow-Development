## Script Include Complex Use Cases

1.This readme.md file outlines a complex use case scenario involving a Script Include and a Client Script to create a new field called 'Number of Group Members' in the incident form. When the assignment group is changed on the incident form, it should display the number of group members available for the selected assignment group.

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


### Use Case Description

2.In the Incident form, whenever a user selects an assignment group, the system should randomly assign the incident to any member from the same assignment group. The assigned user's name should be displayed in the "Assigned To" field.

### Client Script

```javascript
function onChange(control, oldValue, newValue, isLoading, isTemplate) {
   if (isLoading || newValue === '') {
      return;
   }

   var ga = new GlideAjax('getGroupMember');
   ga.addParam('sysparm_name', 'assignMember');
   ga.addParam('sysparm_group_name', g_form.getValue('assignment_group'));
   ga.getXMLAnswer(groupMember);

   function groupMember(response) {
       var member = JSON.parse(response);
       if (member.length > 0) {
           var randomNum = Math.floor(Math.random() * member.length);
           g_form.setValue('assigned_to', member[randomNum].name);
       } else {
           g_form.setValue('assigned_to', '');
       }
   }
}
```

### Script Include

```javascript
var getGroupMember = Class.create();
getGroupMember.prototype = Object.extendsObject(AbstractAjaxProcessor, {
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
    },
    assignMember: function() {
        var grMember = [];
        var groupId = this.getParameter('sysparm_group_name');
        var gr = new GlideRecord('sys_user_grmember');
        gr.addQuery('group', groupId);
        gr.query();

        while (gr.next()) {
            var member = {};
            member.sys_id = gr.user.toString();
            member.name = gr.user.getDisplayValue();
            grMember.push(member);
        }
        return JSON.stringify(grMember);
    },
    type: 'getGroupMember'
});
```

### Conclusion

This complex use case demonstrates how to implement a dynamic assignment mechanism in ServiceNow. By combining a client script and a Script Include, incidents can be randomly assigned to members of a selected assignment group, improving efficiency and streamlining incident management processes.
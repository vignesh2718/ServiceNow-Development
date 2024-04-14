## Script Include (Server Side API)

### Overview

A Script Include in ServiceNow is a powerful tool for storing reusable JavaScript code that runs on the server side. Unlike other types of scripts, such as Business Rules or Client Scripts, Script Includes do not have trigger conditions and are called from other scripting locations. This readme.md file provides an overview of Script Includes, how they work, and their types.

### What is a Script Include?

A Script Include is a container for multiple JavaScript functions or methods that can be reused across various parts of a ServiceNow instance. It serves as a centralized repository for server-side code that can be called from other scripts like Business Rules, Client Scripts, or UI Policies.

### How Script Include Works

1. **Manual Trigger**: Script Include functions/methods do not trigger automatically. They need to be manually called or triggered from other scripts.
2. **Data Exchange**: Script Includes can receive data from the calling script, process it, and execute the necessary code.
3. **Code Execution**: Once triggered, the Script Include executes the specified code or functions.
4. **Return Value**: After executing the code, the Script Include can return a value or result back to the calling script for further processing.

### Types of Script Includes

### Types of Script Includes

1. **OnDemand/Classless Function**: This type of Script Include contains standalone functions or methods without being associated with a class. It can be called from any server-side scripting but cannot be called from the client side.

### Example Use Case

#### Use Case 1: Updating Work Notes for Associated Problem Record

**Description:**
- When the work notes for an incident record are updated, the same work notes should be updated for the associated problem record using a Classless/OnDemand Script Include.

**Script Include:**
```javascript
// Script Include Name: updateWorkNotes
function updateWorkNotes(problemId, worknotes) {
    var gr = new GlideRecord('problem');
    gr.addQuery('sys_id', problemId);
    gr.query();
    if (gr.next()) {
        gr.work_notes = worknotes;
        gr.update();
    }
}
```

**Business Rule:**
```javascript
(function executeRule(current, previous /*null when async*/) {
    var worknotes = current.work_notes.getJournalEntry(1);
    updateWorkNotes(current.problem_id, worknotes);
})(current, previous);
```

2. **Define a New Class**: Script Includes can define a new JavaScript class with its own set of properties and methods.
-It is complex and contains multiple functions
-Name of the class must be matched with the name of script include.
-Can be called from both serve and client side.

#### Use Case: Creating Associated Incident on Critical Problem Record Change

**Description:**
- When the priority of a problem record changes to "Critical", an associated incident will be created for the same problem record.
- The incident will contain the caller name as the logged-in user's name and include the following information in the description:
  i) All the task numbers attached to the current problem record.
  ii) Names of the groups where the assignee of the problem record is part of.

**Script Include:**
```javascript
var defineClass = Class.create();
defineClass.prototype = {
    initialize: function() {
    },
    getProblemTask: function(problem_id){
        var pTask = [];
        var gr = new GlideRecord('problem');
        gr.addQuery('problem', problem_id);
        gr.query();
        if (gr.next()) {
            pTask.push(gr.getDisplayName('number'));
        }
        return pTask;
    },
    getUserGroup: function(assigned_to){
        var gMember = [];
        var gr = new GlideRecord('sys_user_grmember');
        gr.addQuery('user', assigned_to);
        gr.query();
        while (gr.next()) {
            gMember.push(gr.getDisplayName('group'));
        }
        return gMember;
    },
    type: 'defineClass'
};
```

**Business Rule:**
```javascript
(function executeRule(current, previous /*null when async*/) {
    var mainobj = new defineClass();
    if (current.priority == 1) { // Assuming priority 1 represents "Critical"
        var gr = new GlideRecord('incident');
        gr.initialize();
        gr.problem_id = current.sys.id;
        gr.short_description = 'Testing Classbase function';
        gr.caller_id = gs.getUserID();
        gr.description = 'Problem Task are ' + mainobj.getProblemTask(current.sys.id) + '. Groups of assignee are ' + mainobj.getUserGroup(current.assigned_to);
        gr.insert();
    }
})(current, previous);
```


3. **Extend an Existing Class**: Script Includes can also extend an existing JavaScript class to add additional functionality or override existing methods.
### Extending an Existing Class
Extending an existing class allows you to inherit methods and properties from the parent class while adding new functionality in your new Script Include. In this case, we'll extend the `AbstractAjaxProcessor` class, an out-of-the-box (OOB) Script Include in ServiceNow.

### Client Callable Script Include

By extending the `AbstractAjaxProcessor` class, we create a client callable Script Include that can be used to handle AJAX requests from the client side. The `getParameter()` method is used to retrieve information sent from the client script, and the `getXML()` method is used to send information back to the client.

### GlideAjax

`GlideAjax` is a client-side API in ServiceNow used to call client callable Script Includes from client scripts or UI policies. It allows for asynchronous communication between the client and server.

#### How to Define GlideAjax

```javascript
var ga = new GlideAjax('Name_of_the_Script_Include');
ga.addParam('sysparm_name', 'Name_of_the_Method_in_Script_Include');
ga.addParam('sysparm_variable', g_form.getValue('category'));
ga.getXML(callbackFunction);
```

### Example Use Case

**Use Case: Updating Email when Caller Changes**

**Description:**
- When the caller changes on an incident form, the associated email should also be updated.
- This functionality is implemented using a client script and a client callable Script Include.

**Client Script:**
```javascript
function onChange(control, oldValue, newValue, isLoading, isTemplate) {
   if (isLoading || newValue === '') {
      return;
   }

   var ga = new GlideAjax('getProblem');
   ga.addParam('sysparm_name', 'getEmailID');
   ga.addParam('sysparm_user_details', g_form.getValue('caller_id'));
   ga.getXML(emailDetails);

   function emailDetails(response) {
       var emailID = response.responseXML.documentElement.getAttribute('answer');
       g_form.setValue('u_email', emailID);
   }
}
```

**Script Include:**
```javascript
var getProblem = Class.create();
getProblem.prototype = Object.extendsObject(AbstractAjaxProcessor, {
    getEmailID: function() {
        var user = this.getParameter('sysparm_user_details');
        var gr = new GlideRecord('sys_user');
        gr.addQuery('sys_id', user);
        gr.query();
        if (gr.next()) {
            return gr.email;
        }
    },
    type: 'getProblem'
});
```


### Conclusion

Script Includes are a fundamental part of ServiceNow development, providing a means to encapsulate and reuse server-side JavaScript code efficiently. By understanding how Script Includes work and their different types, developers can leverage them effectively to streamline development and improve code maintainability in ServiceNow instances.



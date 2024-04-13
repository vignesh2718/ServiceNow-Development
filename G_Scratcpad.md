# g_scratchpad 

## Overview

`g_scratchpad` is an object used within ServiceNow to pass information from the server to the client side during form loading. It serves as a temporary storage mechanism for data that needs to be accessed and utilized by client-side scripts.

## Properties

The `g_scratchpad` object has properties that hold the information passed from the server. These properties can be accessed and manipulated within client scripts.

## Usage Guidelines

- `g_scratchpad` should be used when you do not expect the data to change dynamically during the user's session.
- It is primarily utilized during form loading to display information retrieved from the server.

## Use Cases

### Use Case 1: Displaying Caller's Email ID on Incident Form Load

#### Business Rule:
```javascript
g_scratchpad.stored_email = current.caller_id.email;
```

#### Client Script:
```javascript
function onLoad() {
    g_form.addInfoMessage('The email id of caller id is ' + g_scratchpad.stored_email);
}
```

### Use Case 2: Populating Fields when Creating a Problem Task from a Problem Record

#### Business Rule:
```javascript
(function executeRule(current, previous /*null when async*/) {
    var gr = new GlideRecord('problem');
    gr.get(current.problem);
    g_scratchpad.parent = current.problem;
    g_scratchpad.short_description = gr.short_description;
    g_scratchpad.description = gr.description;
    g_scratchpad.assigned_to = gr.assigned_to;
})(current, previous);
```

#### Client Script:
```javascript
function onLoad() {
    if (g_scratchpad.parent) {
        g_form.setValue('short_description', g_scratchpad.short_description);
        g_form.setValue('description', g_scratchpad.description);
        g_form.setValue('assigned_to', g_scratchpad.assigned_to);
    }
}
```

## Conclusion

In summary, `g_scratchpad` is a useful tool for passing server-side data to client-side scripts during form loading in ServiceNow. It helps streamline processes and improve user experience by pre-populating fields and displaying relevant information. However, it should be used judiciously and only when data is expected to remain static during the user's session.
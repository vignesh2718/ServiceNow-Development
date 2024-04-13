# Understanding `getReference()` in GlideForm API

## Overview

`getReference()` is a method provided by the GlideForm API in ServiceNow. It's used to retrieve the entire record of a reference field. There are two variations of this method: one with a callback function and one without.

### `getReference('field_name')`

- This method retrieves the record synchronously, meaning the script and processing halt while waiting for the server response.
- **Use with caution**: It can cause processing delays and is generally not recommended without a callback function.
- Usage example: 
    ```javascript
    var userEmail = g_Form.getReference('caller_id').email;
    ```
    Here, the script waits for the reference record to be retrieved from the database before proceeding to fetch the email ID from the server.

### `getReference('field_name', callbackFunction)`

- This variant uses a callback function and executes asynchronously.
- The callback function executes once the server returns the reference value.
- Highly recommended to use with a callback function to prevent processing halts.
- Usage example:
    ```javascript
    g_form.getReference('caller_id', getEmail);

    function getEmail(userEmail) {
        g_form.addInfoMessage(userEmail.email);
    }
    ```
    Here, the callback function `getEmail()` executes once the server returns the reference value, allowing the script to continue without halting.

## Use Case

Consider a scenario where you have an incident form with a field for the caller's email. Whenever the caller changes, you want the email field to update accordingly.

### Client Script

```javascript
function onChange(control, oldValue, newValue, isLoading, isTemplate) {
    if (isLoading || newValue === '') {
        return;
    }

    g_form.getReference('caller_id', getEmail);

    function getEmail(userEmail) {
        g_form.setValue('u_email', userEmail.email);
    }
}
```

In this script, when the caller ID changes, it triggers `getReference()` asynchronously. Once the server returns the reference value (caller's email), the callback function `getEmail()` updates the email field without causing processing halts.

## Drawback of `getReference()`

One significant drawback of using `getReference()` is that it stores all data and can make the page load slower. To mitigate this issue, consider using GlideAjax instead, especially for scenarios where you need to handle large amounts of data.
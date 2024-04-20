## Returning JSON Object from Script Include

### Overview

JSON (JavaScript Object Notation) is a lightweight data interchange format used for data exchange between applications, such as APIs and web services. In ServiceNow, you can return a JSON object from a Script Include, allowing you to send multiple values as key-value pairs.

### What is JSON?

JSON stores data as key-value pairs, making it easy to parse and use in various programming languages. For example:
```json
{
    "Number": "INC00123",
    "Priority": "2 High"
}
```

### Use Case

**Description:**
- When the caller changes in the incident form, the description field should display all the incidents raised by that caller, formatted as JSON objects.

**Client Script:**
```javascript
function onChange(control, oldValue, newValue, isLoading, isTemplate) {
   if (isLoading || newValue === '') {
      return;
   }

   var finalArray = [];
   var ga = new GlideAjax('getIncDetails');
   ga.addParam('sysparm_name', 'getInc');
   ga.addParam('sysparm_user_id', g_form.getValue('caller_id'));
   ga.getXMLAnswer(IncDetail);

   function IncDetail(response){
      var obj = JSON.parse(response);

      for( i=0; i<obj.length; i++){
         finalArray.push('Incident Number: ' + obj[i].number + '\n' +
                         'Priority: ' + obj[i].priority + '\n' +
                         'Short Description: ' + obj[i].short_desc + '\n\n');
      }

      g_form.setValue('description', finalArray.join(''));
   }
}
```

**Script Include:**
```javascript
var getIncDetails = Class.create();
getIncDetails.prototype = Object.extendsObject(AbstractAjaxProcessor, {

    getInc: function() {
        var incArray = [];
        var gr = new GlideRecord('incident');
        gr.addQuery('caller_id', this.getParameter('sysparm_user_id'));
        gr.query();

        while (gr.next()) {
            var incDetails = {};
            incDetails.number = gr.number.toString();
            incDetails.priority = gr.priority.getDisplayValue();
            incDetails.short_desc = gr.short_description.toString();
            incArray.push(incDetails);
        }
        return JSON.stringify(incArray);
    },

    type: 'getIncDetails'
});
```

### Conclusion

Returning a JSON object from a Script Include in ServiceNow enables efficient data exchange between server-side and client-side scripts. By formatting data as key-value pairs, developers can easily process and manipulate the information, enhancing the functionality and usability of ServiceNow applications.
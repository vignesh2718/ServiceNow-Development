### Using GlideForm (g_form)

#### Introduction
In simple terms, this document explains how to use the GlideForm object (g_form) in ServiceNow to modify forms on your website. GlideForm is like a magic wand that allows you to change the appearance and behavior of forms (like those you fill out online) without having to write a lot of complex code.
which includes the onLoad(), onCellEdit(), onSubmit(), and onChange() functions.

#### Function Explanation
The `onLoad()` function is a special function in ServiceNow that automatically runs when a form loads. This means when you open a page with a form, the code inside the `onLoad()` function starts working right away.

#### Code Breakdown
Let's break down the code inside the `onLoad()` function:

1. **Adding Decorations**: 
   - The `addDecoration()` function adds a visual element, like an icon or color, to a specific part of the form. In this case, it's adding a lightbulb icon in yellow color to the 'category' field.

2. **Error Message**: 
   - The `addErrorMessage()` function adds an error message to the form, which alerts users if something is wrong.

3. **Getting and Checking Values**: 
   - The `getDisplayBox()` function gets the value entered into the 'caller_id' field. Then, there's a check to see if the value is 'Abel Tuter'.

4. **Modifying Form Based on Value**:
   - If the value is 'Abel Tuter', certain changes are made to the form:
     - Adding an option 'Tech Issue' to the 'category' field and removing an option 'software'.
     - Clearing all existing options from the 'category' field.
     - Disabling attachments.
     - Making the 'cmdb_ci' field mandatory (meaning it must be filled out).
     - Disabling the 'service_offering' field.
     - Hiding the 'business_service' field.
     - Changing the label of the 'description' field to 'Issue Details'.
     - Hiding the 'incident' related list.
     - Changing the background color of the 'state' field to light green.

#### Conclusion
 This code uses the GlideForm object to make various changes to a form based on certain conditions. It's like customizing a form to fit specific needs or preferences without needing to be a coding expert.
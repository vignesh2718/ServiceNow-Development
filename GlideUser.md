## Glider User

This readme explains a function named `GliderUser` that takes an input parameter `g_User`. It seems to be part of a larger system or software, but we'll break it down in simple terms.

### What Does it Do?

This function, `onLoad`, seems to be triggered when something loads, possibly a webpage or a form. It performs several actions related to the user who is interacting with the system. Let's go through each action:

1. **Display User Information**: 
   - It shows some basic information about the user, such as their first name, last name, user ID, username, and full name.

2. **Set Description Field to Read-Only**: 
   - It makes a field named 'description' read-only, which means users can't edit it directly.

3. **Conditional Read-Only**: 
   - If the user has a specific role named 'demo_1', it allows them to edit the 'description' field.
   - If the user has any of the roles from a list including 'demo_1', 'itil', or 'security_admin', it also allows them to edit the 'description' field.

### How to Use?

To use this function, you need to ensure it's integrated into a system or software where it can be triggered when something loads, such as a webpage or a form. Additionally, make sure you have the necessary access rights and roles configured in the system for the conditional read-only feature to work as expected.

### Important Notes:

- This function relies on a `g_form` object, which likely handles form-related actions.
- It also relies on a `g_user` object, which presumably holds information about the current user.
- The conditions for setting the 'description' field to read-only seem to be based on the user's roles within the system.

```javascript
function onLoad() {
//  g_form.addInfoMessage(g_user.firstName);
//  g_form.addInfoMessage(g_user.lastName);
//  g_form.addInfoMessage(g_user.userID);
//  g_form.addInfoMessage(g_user.userName);
//  g_form.addInfoMessage(g_user.getFullName());
   // g_form.setReadOnly('description',true);
	// if(g_user.hasRole('demo_1')){
	// 	 g_form.setReadOnly('description',false);
	// }
	//if(g_user.hasRoleFromList('demo_1,itil,secuirty_admin')){
	//	g_form.setReadOnly('description',false);
	//}
}
```



### Conclusion:

In simple terms, this function handles user interactions within a system. It displays user information and controls whether users can edit a specific field based on their roles within the system.
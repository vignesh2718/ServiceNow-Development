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

1. **OnDemand/Classless Function**: This type of Script Include contains standalone functions or methods without being associated with a class.
2. **Define a New Class**: Script Includes can define a new JavaScript class with its own set of properties and methods.
3. **Extend an Existing Class**: Script Includes can also extend an existing JavaScript class to add additional functionality or override existing methods.

### Conclusion

Script Includes are a fundamental part of ServiceNow development, providing a means to encapsulate and reuse server-side JavaScript code efficiently. By understanding how Script Includes work and their different types, developers can leverage them effectively to streamline development and improve code maintainability in ServiceNow instances.
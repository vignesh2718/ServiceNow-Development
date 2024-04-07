# GlideRecord SS-API

## Overview

The GlideRecord SS-API is a tool used for managing and manipulating data in ServiceNow's database. Think of it as a way to interact with the information stored in ServiceNow, like accessing records in a spreadsheet.

## What it does

- **Single Table Focus**: GlideRecord deals with records from just one table at a time. Imagine a single sheet within a larger workbook.

- **Scripting Integration**: It's commonly used in ServiceNow scripting environments such as business rules, script includes, UI actions (server-side), and email scripting to perform database operations.

- **Incident Management**: GlideRecord is especially useful for handling incidents and their related actions within ServiceNow.

## Different Methods

GlideRecord offers various methods to perform different tasks:

- **Adding Queries**: Methods like `addQuery()`, `addActiveQuery()`, `addEncodedQuery()`, and `addNotNullQuery()` help specify conditions for selecting records.

- **Executing Queries**: Methods like `query()` perform the actual database query based on the conditions set.

- **Retrieving Data**: Methods like `get()`, `getValue()`, `getDisplayValue()` help retrieve data from the records.

- **Manipulating Data**: Methods like `insert()`, `update()`, `setValue()` are used to modify records.

- **Navigation**: Methods like `next()` and `hasNext()` help in navigating through the result set.

## How to Use

Here's a basic example of how to use GlideRecord:

```javascript
// Creating a GlideRecord object for the 'incident' table
var gr = new GlideRecord('incident');

// Setting up query conditions
gr.addQuery('priority', 1);

// Executing the query
gr.query();

// Iterating through results
while (gr.next()) {
    gs.info('Incident: ' + gr.number + ', Priority: ' + gr.priority);
}
```

In simpler terms, this script sets up a search for incidents with a priority of 1, then loops through each matching incident, printing out its number and priority.

Remember, GlideRecord is like a special tool you use to dig through ServiceNow's data and do things with it, like finding, changing, or showing information about incidents.
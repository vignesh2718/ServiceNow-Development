# WeV Technology: Use Case Overview

## Introduction

WeV is a company specializing in AI-powered devices for construction workers, including safety drones, AR glasses, smart hats, and wearable environmental sensors. They receive orders from construction-based clients through various channels such as calls and emails. Currently, order processing is managed manually using spreadsheets, involving approval from a release management group before device dispatch.

## Current Process

- **Order Placement:** Clients submit orders via calls, emails, or other channels.
- **Order Processing:** Device management manually enters orders into spreadsheets.
- **Approval:** Device Management emails the release management group for approval.
- **Dispatch:** An outsourced team dispatches devices based on approvals.

## Challenges

- Manual order processing using spreadsheets is inefficient and prone to errors.
- Lack of a central system makes it challenging to track device location and maintain real-time client communication.
- Email-based approvals lead to delays in device delivery.
- Difficulty in collecting and analyzing client feedback for product improvement.

## Desired Outcome

- A centralized portal for clients to submit device requests.
- Streamlined and automated order processing system.
- Faster approvals and order fulfillment lead times.
- Automatic email notifications sent to clients.
- Centralized dashboard for managing operations and tracking.

## Steps for Application Development

### Process Flow:

1. **Client Order Placement:** Orders are submitted through an online portal.
2. **Review and Inventory Check:** Device management team reviews orders and checks inventory availability.
3. **Approval Request:** An approval request is sent to the release management group.
4. **Approval and Dispatch:** Upon approval, the application generates a dispatch order for the device.
5. **Client Notification:** Clients receive notifications regarding their order status.
6. **Automated Email Notifications:** Emails are triggered based on different conditions.
7. **Reporting and Dashboard:** Visualization of metrics through reports and dashboards.

### User Roles for Custom Application:

- **External Users (Clients):**
  - Order placement, status updates, and support access with limited permissions.
- **Internal Users:**
  - Device Management
  - Release Management Group (Approvers)
  - Dispatch Management
  - System Administrator (Manages application settings, user permissions, and access controls)

### Benefits to Users from Custom Application:

- **Device Management Team:**
  - Increased efficiency through reduced manual data entry and faster order processing.
  - Improved visibility with real-time device status and location tracking.
- **Release Management Group (Approvers):**
  - Simplified approval process with dynamically assigned and appropriate approvals.
- **Dispatch Management:**
  - Streamlined dispatch process with easy order generation and management.
- **Leadership:**
  - Cost reduction, improved efficiency, and higher client satisfaction.
  - Automation of tasks and real-time visibility through reports and dashboards.

### Interaction with the Application:

- Accessible via both mobile and desktop/laptop devices.
- Intuitive design for user-friendly experience.

### Inputs and Outputs

**Inputs (Data Sources):**
- Existing spreadsheets for order and device data.
- User input through service catalog forms.

**Outputs:**
- Email notifications.
- Reports and scheduled reports for tracking and analysis.

## ServiceNow Studio

It provides a powerfull integrated developement environment IDE for application developers to work on custom application in one centralized location.
-Build Custom Applications: Create workflows , forms. and user interfaces for various business needs. 
-Source control integration: integrate with external Git repositories like GitLab or Github for advanced version control management.
-Perform Code Search - It is a built in feature that enables developers to quickly locate specifi code snippets, classes, functions, variables,or other elements within their application or acorss multiple applications.


## Source Control 
-Source control also known as version control, is a system for tracking and managing chnages made to application files over time.
-Application files refers to database tables, scripts, flows,various configuration changes etc.


## Why source control is better than update set?
-Remote storgae of application files  using repository.
-Create different branches for specific development work.
-you can track changes.
- No need of source instance or XML Files.


## Requirements Part 1
-If the state is delivered then only delivery date field should come up and it would be a mandatory field.
-If quantity is greater than two , then business justification field should become mandatory.

## Requirements Part 2
-Once opening the device request table it should not display the section(Device Details and delivert details ) by default
-Once the device Name field is filled up then these sections should become visible.

## Requirements Part 3
- Once you select the device name, the information in the device details tab should be auto filled up based on the record in the AI devices table.
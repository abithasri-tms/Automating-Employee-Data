# Automating Employee Data — ServiceNow Implementation

A complete ServiceNow-based employee data automation system that imports
employee records from an external file, transforms them into the User table,
and configures the Incident form with department, email, and manager details
using dot walking and dictionary override.

---

## Overview

This project automates the process of loading and managing employee data
inside ServiceNow. It eliminates manual user creation by importing records
from an Excel or CSV file through Import Sets, mapping them to the sys_user
table, and displaying enriched employee information directly on the Incident form.

---

## Prerequisites

- ServiceNow Developer Instance (PDI)
- Admin role access
- Employee data file (Excel / CSV / XML)
- Basic knowledge of ServiceNow Import Sets and Transform Maps

---

## Input File Format

Prepare your external employee data file with these exact columns:

| Column | Description |
|---|---|
| `Name` | Employee full name |
| `Email` | Employee email address |
| `Department` | Department name (IT, HR, Finance...) |
| `Manager` | Manager full name |
| `Manager Email` | Manager's email address |

Supported formats: `.xlsx` `.csv` `.xml`

---

## Implementation Steps

### Step 1 — Prepare Employee Data File
- Create an Excel, CSV, or XML file with the 5 required columns
- Ensure no empty rows, no duplicate emails, and valid email formats
- Save the file ready for upload into ServiceNow

### Step 2 — Load File Using Import Sets
- Navigate to **System Import Sets → Load Data**
- Upload your employee data file
- ServiceNow automatically creates a staging table
- Verify all records are visible in the staging table before proceeding

### Step 3 — Verify Staging Table
- Open the auto-created staging table
- Confirm all 5 columns are present and correctly populated
- Check row count matches your source file

### Step 4 — Create Transform Map
- Navigate to **System Import Sets → Transform Maps**
- Create a new Transform Map targeting the **User (sys_user)** table
- Map each staging field to the corresponding sys_user field:

| Staging Field | sys_user Field |
|---|---|
| Name | Name (name) |
| Email | Email (email) |
| Department | Department (department) |
| Manager | Manager (manager) — Reference field |
| Manager Email | Used to resolve Manager reference |

- For the Manager field, use a reference lookup to match by name or email
- Save and activate the Transform Map

### Step 5 — Execute the Transform
- Run the Transform Map against the staging table
- Monitor the transform log for errors or skipped rows
- Validate that employee records are correctly inserted into the User table
- Navigate to **User Administration → Users** and search for imported employees

### Step 6 — Configure Incident Form with Dot Walking
- Navigate to **Incident → Open a record → Form Layout**
- Use dot walking to add the following fields from the Assigned To reference:
  - `assigned_to.department` → Displays the assignee's department
  - `assigned_to.email` → Displays the assignee's email
  - `assigned_to.manager` → Displays the assignee's manager
- Save the form layout

### Step 7 — Dictionary Override for Priority
- Navigate to **System Definition → Dictionary**
- Find the **Priority** field on the **Incident** table
- Create a Dictionary Override to change the default Priority value
- Ensure the override applies only to the Incident table
- Confirm other Task child tables (Change, Problem) are not affected

### Step 8 — Test the Complete Setup
- Open a new Incident record
- Assign it to one of the imported employees
- Verify that Department, Email, and Manager details display correctly via dot walking
- Confirm the Priority field defaults to the overridden value
- Test with multiple employees to validate consistency

---

## Validation Checklist

- [ ] Employee file prepared with all 5 columns
- [ ] File loaded successfully into ServiceNow Import Set
- [ ] Staging table contains all records correctly
- [ ] Transform Map created and mapped to sys_user table
- [ ] Manager reference field resolved correctly
- [ ] Transform executed with no errors
- [ ] Employee records visible in User table
- [ ] Incident form shows Department, Email, Manager via dot walking
- [ ] Dictionary Override applied to Priority on Incident table only
- [ ] Incidents assigned to imported users display correct manager details
- [ ] Priority defaults to overridden value on new Incident records

---

## Key Concepts Used

| Concept | Description |
|---|---|
| Import Sets | ServiceNow mechanism to load external data into a staging table |
| Transform Map | Maps staging table fields to target table fields |
| sys_user | ServiceNow's built-in User table |
| Dot Walking | Accessing related record fields through a reference field |
| Dictionary Override | Changing field behavior for a specific table without affecting parent or sibling tables |
| Reference Field | A field that points to a record in another table |

---

## Expected Output

After completing all steps:
- All employees imported into ServiceNow User table
- Manager reference correctly linked for each user
- Incident form displays enriched employee information via dot walking
- Priority field defaults to custom value on all new Incident records
- Full end-to-end workflow validated and tested

---

## Built With

- ServiceNow Developer Instance
- Import Sets and Transform Maps
- sys_user Table
- Incident Form Configuration
- Dictionary Override
- Dot Walking

---

## Purpose

This project demonstrates how ServiceNow can be used to automate
employee data management by replacing manual user creation with a
structured import and transformation workflow. It ensures accurate
data population, reduces human errors, and maintains consistency
across employee records within the ServiceNow platform.

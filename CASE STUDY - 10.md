# Experiment 10: Getting Started with Zoho Creator: Account Setup and Building a Form-Based Application

## 1. Aim

To set up a Zoho Creator account and build a simple form-based application (Employee Directory) with data entry, validation, and a basic report.

## 2. Objectives

- Create a Zoho account and access Zoho Creator.
- Understand the Creator workspace: applications, forms, reports, pages, and workflows.
- Build a form using different field types.
- Add field properties and validations.
- Submit records and view them in a report.

## 3. Requirements

| Item | Details |
|---|---|
| Account | Free Zoho account (Zoho Creator offers a free trial; check current plan limits) |
| Browser | Chrome, Edge, or Firefox |
| Internet | Required |

> The Zoho interface is updated regularly. Menu names and positions may differ slightly from those in this guide.

## 4. Theory

### 4.1 Zoho Creator

Zoho Creator is a low-code/no-code platform for building custom business applications with drag-and-drop tools, workflows, and a scripting language called **Deluge**.

### 4.2 Core Components

| Component | Purpose |
|---|---|
| **Application** | Container for all components |
| **Form** | Collects and stores data (each form is a table) |
| **Report** | Displays and manages stored records (list, grid, calendar, etc.) |
| **Page** | Custom layouts and dashboards |
| **Workflow** | Automation triggered by events or schedules |
| **Section / Role** | Navigation grouping and access control |

### 4.3 Common Field Types

Single Line, Multi Line, Number, Decimal, Email, Phone, Date, Date-Time, Dropdown, Radio, Checkbox, Multi Select, Lookup, Image, File Upload, URL, Address, Name, Auto Number, Formula, Decision Box, Subform.

## 5. Procedure

### Part A: Account Setup

1. Go to the Zoho Creator website and select **Sign Up** (or sign in with an existing Zoho account).
2. Enter name, email, and password; verify the email address.
3. Choose the data center region that applies to you if prompted.
4. Sign in to Zoho Creator. The home page shows your applications and a **Create Application** button.

### Part B: Create the Application

1. Click **Create Application**.
2. Choose **Create from scratch**.
3. Name the application **Employee Directory** and click **Create**.
4. You will see the app builder (or Edit mode) with options to add a form, report, or page.

### Part C: Build the Form

1. Click **Create new** or **+ Form**, then **Form > Start from scratch**.
2. Name the form **Employee**.
3. Drag fields from the left palette and set their **names** and **properties**:

| Field Label | Field Type | Properties |
|---|---|---|
| Employee ID | Auto Number | Prefix `EMP-` (optional) |
| Full Name | Name | Required |
| Email | Email | Required, **No duplicate values** |
| Phone | Phone | Optional |
| Department | Dropdown | Choices: HR, Finance, IT, Sales, Operations |
| Designation | Single Line | Required |
| Date of Joining | Date | Required |
| Salary | Currency/Decimal | Optional, minimum 0 |
| Employment Type | Radio | Full-time, Part-time, Contract |
| Skills | Multi Select | e.g., Communication, Python, Excel, Design |
| Photo | Image | Optional |
| Active | Decision Box | Default checked |

4. For each field, open **Field properties** (click the field) and set the **Display name**, **Link name**, **Required**, and **Placeholder** as needed.

### Part D: Add Validation

1. Select **Date of Joining**, open **Field properties > Validation**, and enable **Allow only past or today's dates** (if available), or add a Deluge validation in Part E.
2. Set **Salary** minimum to 0.
3. Mark **Email** as **No duplicate values** to prevent two employees with the same email.

### Part E: Add Script-Based Validation (Introductory)

1. In the form builder, go to **Workflow > Form events > On validate** (names can vary: *On Validate*, in the form's Actions/Workflow area).
2. Add a Deluge script:

```
if(input.Date_of_Joining > zoho.currentdate)
{
    alert "Date of Joining cannot be in the future.";
    cancel submit;
}
```

3. Save the script.

> Field link names (e.g., `Date_of_Joining`) must match your form. Check the **Link name** in each field's properties.

### Part F: Access the Application and Add Records

1. Click **Access Application** (or the **Preview/Live** button).
2. Fill and submit the **Employee** form at least **8 times** with varied departments.
3. Try submitting with a missing required field and a duplicate email to verify that validations work.

### Part G: View and Manage Data

1. A default **report** (for example, *Employee_Report*) is usually created automatically.
2. Open the report and observe the list of records.
3. Use **Search**, **Filter**, and **Sort**.
4. Edit and delete a record.
5. Use **Export** to download the data (CSV/Excel).

### Part H: Customize the Report (Optional)

1. In edit mode, open the report and click **Customize/Settings**.
2. Choose which columns display, set the default sort, and set the records per page.

### Part I: Share the Application (Optional)

1. Go to **Settings > Share** and invite another user to test.
2. Alternatively, publish the form (**Publish > Permalink**) to obtain a public form link. Do this only with non-sensitive test data.

## 6. Observations

| Item | Your Entry |
|---|---|
| Account email / region | |
| Application name | |
| Form name and number of fields | |
| Validations applied | |
| Records submitted | |
| Result of duplicate email test | |
| Result of future-date test | |

### Screenshots to Attach

- Creator home page after sign-in
- Form builder with all fields
- Validation script
- Submitted form and report view

## 7. Result

A Zoho Creator account was set up and a form-based **Employee Directory** application was built with validation, data entry, and a report.

## 8. Conclusion

Zoho Creator lets users build data-collection applications quickly using drag-and-drop forms and built-in reports, with scripting for custom rules when needed.

## 9. Troubleshooting

| Problem | Possible Cause | Fix |
|---|---|---|
| Script error on save | Wrong field link name | Check the link name in field properties |
| Duplicate check not working | Setting not enabled | Enable *No duplicate values* on the field |
| Cannot find a menu | Interface updated | Use the search option or check the current docs |

## 10. Viva Questions

1. What is Zoho Creator and who is it designed for?
2. What are forms, reports, and pages?
3. What is a field link name and why does it matter in scripts?
4. How can you prevent duplicate records?
5. What is the purpose of the *On validate* event?

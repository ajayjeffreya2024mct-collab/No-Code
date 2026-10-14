# Experiment 11: Designing Pages and Navigation for a Multi-Page Business Application in Zoho Creator

## 1. Aim

To design a multi-page business application in Zoho Creator (Leave and Asset Management) with multiple forms, custom pages, and a structured navigation menu.

## 2. Objectives

- Design an application with several related forms.
- Link forms using lookup fields.
- Create custom pages (home page, about/help page, summary page).
- Organize navigation using sections and menus.
- Control what each user role can see.

## 3. Requirements

| Item | Details |
|---|---|
| Account | Zoho Creator account from Experiment 10 |
| Starting point | Application from Experiment 10 (Employee Directory) can be extended, or create a new app named **Business Hub** |
| Browser | Chrome, Edge, or Firefox |

> The Zoho interface changes over time. If a menu or option name differs, check the in-product search or the current Zoho Creator help documentation.

## 4. Theory

### 4.1 Application Structure

A multi-page business application typically contains:

| Element | Role |
|---|---|
| Forms | Data entry (Employee, Leave Request, Asset, Department) |
| Reports | Views of data from forms |
| Pages | Custom layouts: landing page, instructions, dashboards, embedded forms/reports |
| Sections | Groups of components in the navigation menu |
| Roles / Profiles | Control access and visible menu items |

### 4.2 Navigation Design Principles

- Group related items under clear section names.
- Keep the most-used items at the top.
- Use a landing page with quick links.
- Hide admin-only sections from regular users.
- Use consistent naming (nouns for data, verbs for actions).

### 4.3 Lookup Fields

A **lookup** field links a record in one form to a record in another form (for example, each Leave Request refers to an Employee), enforcing consistency and enabling relational data.

## 5. Application Design

### 5.1 Planned Components

| Component | Type | Purpose |
|---|---|---|
| Department | Form | List of departments |
| Employee | Form | Employee master (from Experiment 10) |
| Leave Request | Form | Employees apply for leave |
| Asset | Form | Company assets (laptops, phones) |
| Asset Assignment | Form | Allocate assets to employees |
| Home | Page | Landing page with quick links |
| Help | Page | Instructions and contacts |
| Reports | Reports | One per form |

### 5.2 Navigation Plan

```
Business Hub
|-- Home (page)
|-- People
|     |-- Employees (report)
|     |-- Departments (report)
|-- Leave
|     |-- Apply for Leave (form)
|     |-- Leave Requests (report)
|-- Assets
|     |-- Assets (report)
|     |-- Assign Asset (form)
|     |-- Assignments (report)
|-- Help (page)
```

## 6. Procedure

### Part A: Create the Supporting Forms

1. Open (or create) the application **Business Hub**.
2. Create the form **Department** with fields:

| Field | Type | Notes |
|---|---|---|
| Department Name | Single Line | Required, no duplicates |
| Head of Department | Single Line | Optional |

3. Edit the **Employee** form (from Experiment 10) and change **Department** from a dropdown to a **Lookup** of the **Department** form (or keep the dropdown if you prefer a simpler version).
4. Create the form **Leave Request**:

| Field | Type | Notes |
|---|---|---|
| Employee | Lookup (Employee) | Required |
| Leave Type | Dropdown | Casual, Sick, Earned, Unpaid |
| From Date | Date | Required |
| To Date | Date | Required |
| Number of Days | Formula/Number | Calculated (see below) |
| Reason | Multi Line | Required |
| Status | Dropdown | Pending (default), Approved, Rejected |

5. Calculate **Number of Days** with a workflow on **On user input** of **To Date**, or on submit:

```
if(input.To_Date != null && input.From_Date != null)
{
    input.Number_of_Days = (input.To_Date - input.From_Date).toDay() + 1;
}
```

6. Add validation on **On validate**:

```
if(input.To_Date < input.From_Date)
{
    alert "To Date cannot be before From Date.";
    cancel submit;
}
```

7. Create the form **Asset**:

| Field | Type |
|---|---|
| Asset Tag | Auto Number |
| Asset Name | Single Line |
| Category | Dropdown (Laptop, Phone, Monitor, Other) |
| Purchase Date | Date |
| Condition | Radio (New, Good, Needs Repair) |

8. Create the form **Asset Assignment**:

| Field | Type |
|---|---|
| Asset | Lookup (Asset) |
| Employee | Lookup (Employee) |
| Assigned On | Date (default today) |
| Returned On | Date |

### Part B: Add Sample Data

1. Add at least 3 departments, 8 employees, 6 assets, 5 leave requests, and 4 assignments.

### Part C: Create the Home Page

1. Click **Create new > Page**, name it **Home**.
2. The page builder opens. Add elements from the palette:
   - **Text/Heading** element: "Welcome to Business Hub"
   - **Buttons** linking to forms (Apply for Leave, Assign Asset)
   - **HTML** snippet or **Embed** element for a simple banner (optional)
3. Add **buttons** with actions *Open form* or *Open URL* (use the application link or form permalink).
4. Save and publish the page.

Optional simple HTML snippet for quick links:

```html
<div style="padding:20px;font-family:Arial;">
  <h2>Welcome to Business Hub</h2>
  <p>Select an option from the menu or use the quick links below.</p>
</div>
```

### Part D: Create the Help Page

1. Create a page named **Help**.
2. Add headings and text describing how to apply for leave, request assets, and contact HR/IT.

### Part E: Arrange Navigation

1. In the app builder, open **Settings > Navigation** (or edit the **Application menu**, in the *Edit/Layout* area).
2. Create sections **People**, **Leave**, **Assets**.
3. Move components into sections following the navigation plan:
   - People: Employee report, Department report
   - Leave: Leave Request form, Leave Request report
   - Assets: Asset report, Asset Assignment form and report
4. Place **Home** at the top and **Help** at the bottom.
5. Set **Home** as the **default landing page** (look for the application's *Landing page* or *Home page* setting).
6. Rename menu items to user-friendly labels (for example, "Apply for Leave" instead of "Leave_Request").

### Part F: Control Access with Roles/Profiles

1. Open **Settings > Users & Permissions > Profiles/Roles**.
2. Create profiles such as **Admin**, **Manager**, **Employee**.
3. For each profile, set which sections/components are visible:

| Component | Admin | Manager | Employee |
|---|---|---|---|
| Home, Help | Yes | Yes | Yes |
| Employees report | Yes | Yes | No |
| Departments report | Yes | No | No |
| Apply for Leave form | Yes | Yes | Yes |
| Leave Requests report | Yes | Team only | Own only |
| Assets and Assignments | Yes | No | No |

4. Where supported, restrict data with criteria (for example, Employees see only their own leave requests).
5. Invite a test user to each profile, or use the preview-as feature if available, and confirm visibility.

### Part G: Test the Experience

1. Use **Access Application** and navigate through every menu item.
2. Verify the lookups, validations, and navigation links.
3. Test on a mobile browser or the Zoho Creator mobile app to see responsive behavior.

## 7. Observations

| Item | Your Entry |
|---|---|
| Number of forms created | |
| Lookups configured | |
| Pages created | |
| Sections in navigation | |
| Landing page set | Yes / No |
| Profiles created | |

### Screenshots to Attach

- Form relationships (lookups)
- Home page design
- Navigation menu (as user sees it)
- Role-based view differences

## 8. Result

A multi-page business application with multiple linked forms, custom pages, structured navigation, and role-based access was designed in Zoho Creator.

## 9. Conclusion

Good page and navigation design makes applications easy to use and safe to share. Lookups connect data, pages provide friendly entry points, and profiles ensure each user sees only what they need.

## 10. Viva Questions

1. What is the purpose of a lookup field?
2. How do pages differ from forms and reports?
3. How are sections used to organize navigation?
4. How do you set a default landing page?
5. How can you ensure employees only see their own leave records?

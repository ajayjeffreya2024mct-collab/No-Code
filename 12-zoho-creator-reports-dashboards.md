# Experiment 12: Creating Reports and Dashboards for Data Visualization in Zoho Creator

## 1. Aim

To create different types of reports and an interactive dashboard in Zoho Creator for visualizing business data.

## 2. Objectives

- Create list, grid, summary, and calendar reports.
- Apply filters, grouping, sorting, and quick-view customizations.
- Build charts and KPI tiles.
- Compose a dashboard page that combines charts, KPIs, and reports.

## 3. Requirements

| Item | Details |
|---|---|
| Account | Zoho Creator account |
| Application | **Business Hub** from Experiment 11 (Employee, Leave Request, Asset forms with sample data). Alternatively, use any application that has at least 30 sample records |
| Browser | Chrome, Edge, or Firefox |

> The Zoho Creator interface is updated frequently. Use the in-product search or help documentation if a menu differs from the steps below.

## 4. Theory

### 4.1 Report Types

| Report Type | Best For |
|---|---|
| **List** | Browsing and editing records in rows |
| **Grid** | Spreadsheet-like view with grouping and inline editing |
| **Summary** | Aggregations (count, sum, average) grouped by fields |
| **Pivot / Table** | Cross-tabulated analysis |
| **Calendar** | Date-based records (leaves, appointments) |
| **Kanban** | Status-based boards (Pending, Approved, Rejected) |
| **Map / Timeline** | Location or chronological views (where supported) |

### 4.2 Charts

Common chart types: bar/column, line, area, pie/donut, funnel, scatter. Choose the chart that matches the question:

| Question | Chart |
|---|---|
| Compare categories | Bar/column |
| Show a trend over time | Line |
| Show share of a whole | Pie/donut (few categories) |
| Show process drop-off | Funnel |

### 4.3 Dashboards

A dashboard is a **page** combining multiple components: KPI tiles, charts, and reports. It should answer key questions at a glance, use consistent colors, and limit clutter.

## 5. Procedure

### Part A: Prepare Data

1. Open **Leave Request** and add at least 30 records spread over several employees, leave types, months, and statuses.
2. Make sure the **Number of Days** field has values.
3. Optionally use **Import data** (CSV/Excel) to load bulk sample data.

### Part B: Build Reports

**1. List report with filter**

1. In edit mode, select **Create new > Report > List Report** (or Report > From scratch) on the **Leave Request** form. Name it `Pending_Leaves`.
2. Choose the columns: Employee, Leave Type, From Date, To Date, Number of Days, Status.
3. Under **Filters/Criteria**, set **Status equals Pending**.
4. Save and open the report in access mode.

**2. Grid report with grouping**

1. Create a **Grid report** named `Leaves_by_Type`.
2. In report settings, **Group by Leave Type**.
3. Enable sorting by From Date (descending).

**3. Summary report**

1. Create a **Summary report** named `Leave_Summary`.
2. Group by **Employee** and add aggregates: **Count of records** and **Sum of Number of Days**.
3. Add a second grouping by **Leave Type** to see a breakdown.

**4. Calendar report**

1. Create a **Calendar report** named `Leave_Calendar`.
2. Set the **Start Date** to **From Date** and the **End Date** to **To Date**; use Employee as the title.
3. View by month and week.

**5. Kanban report (optional)**

1. Create a **Kanban report** named `Leave_Board`, using **Status** as the lane field.
2. Drag cards between lanes to test (this updates the Status field).

### Part C: Quick View and Customization

1. Set up **quick view** layouts so that clicking a record shows a clean summary.
2. Configure **column colors** or conditional formatting (for example, red for Rejected, green for Approved) where available.
3. Enable **Search, Filter, Export** options for end users.

### Part D: Create Charts

Create charts from the **Leave Request** form data (use **Create new > Page > Dashboard/Page** and add charts, or use the Chart Builder from a report):

| Chart | Type | Dimension (X) | Measure (Y) |
|---|---|---|---|
| Leaves by Type | Bar | Leave Type | Count |
| Monthly Leave Trend | Line | From Date (by Month) | Sum of Number of Days |
| Status Share | Donut | Status | Count |
| Top Employees by Days Taken | Bar (horizontal) | Employee | Sum of Number of Days |

Steps for each chart:

1. Add a **Chart** component in the page builder.
2. Select the **form/report** as the data source.
3. Choose the chart type, X-axis (dimension), and Y-axis (measure with aggregation).
4. Apply filters where needed (e.g., current year).
5. Format title, colors, and labels; save.

### Part E: Create KPI Tiles

1. Add **KPI** or **Number** components to the page.
2. Create these KPIs:

| KPI | Calculation |
|---|---|
| Total leave requests | Count of all records |
| Pending requests | Count where Status = Pending |
| Total days taken (approved) | Sum of Number of Days where Status = Approved |
| Approval rate | Approved / Total x 100 |

If the page builder does not offer a calculated KPI directly, compute the value with a Deluge snippet in a **Page** (HTML/Deluge) element or use an aggregate report. Example Deluge:

```
total = Leave_Request[ID != 0].count();
pending = Leave_Request[Status == "Pending"].count();
approved = Leave_Request[Status == "Approved"].count();
rate = 0;
if(total > 0)
{
    rate = (approved * 100.0 / total).round(1);
}
info "Approval rate: " + rate + "%";
```

> Replace `Leave_Request` and `Status` with your form and field **link names**.

### Part F: Compose the Dashboard

1. Create a page named **HR Dashboard**.
2. Arrange components in a grid:

```
+----------------------------------------------------------+
| KPI: Total | KPI: Pending | KPI: Days Taken | KPI: Rate   |
+----------------------------------------------------------+
| Bar: Leaves by Type        | Donut: Status Share         |
+----------------------------------------------------------+
| Line: Monthly Leave Trend  | Bar: Top Employees          |
+----------------------------------------------------------+
| Report: Pending Leaves (list, embedded)                  |
+----------------------------------------------------------+
```

3. Add **page-level filters** (for example, Year, Department) so charts update together, where supported.
4. Test interactivity: click chart segments (drill-down) and apply filters.
5. Add the dashboard to the **navigation** and set role permissions (Admin and HR only).

### Part G: Share and Export

1. Export a report to **PDF/CSV/Excel**.
2. Schedule a report email (if supported on your plan) or generate a PDF of the dashboard.

## 6. Observations

| Report / Chart | Type | Insight Gained |
|---|---|---|
| Pending_Leaves | List | |
| Leaves_by_Type | Grid | |
| Leave_Summary | Summary | |
| Leave_Calendar | Calendar | |
| Leaves by Type | Bar | |
| Monthly Leave Trend | Line | |
| Status Share | Donut | |

### Dashboard Review

| Question | Answer |
|---|---|
| Which leave type is most used? | |
| Which month has most leaves? | |
| How many requests are pending? | |
| Who took the most leave days? | |

### Screenshots to Attach

- Each report type
- Chart builder settings
- Final HR Dashboard

## 7. Result

Multiple report types, charts, and a consolidated dashboard were created in Zoho Creator to visualize leave data.

## 8. Conclusion

Reports and dashboards turn raw data into actionable insight. Choosing appropriate report and chart types, adding filters, and keeping the layout simple make data easier to understand and decisions faster.

## 9. Design Tips

- Put the most important KPIs at the top.
- Use few colors and consistent meaning (e.g., red for rejected).
- Avoid pie charts with many categories.
- Label axes and add titles.
- Test with real users and iterate.

## 10. Viva Questions

1. Differentiate list, grid, and summary reports.
2. When would you use a calendar or Kanban report?
3. Which chart type suits trends over time?
4. What is a KPI and how is it calculated here?
5. How do filters improve a dashboard?
6. How can dashboard access be restricted?

# Experiment 14: Introduction to Deluge Scripting: Writing Custom Functions and Basic Programs

## 1. Aim

To learn the basics of Deluge, Zoho's scripting language, and to write custom functions and simple programs in Zoho Creator.

## 2. Objectives

- Understand Deluge syntax, data types, and operators.
- Use variables, conditions, loops, lists, and maps.
- Work with built-in functions and string, date, and number operations.
- Fetch, insert, update, and delete records.
- Write custom functions and call them from workflows.
- Debug scripts using `info` statements and logs.

## 3. Requirements

| Item | Details |
|---|---|
| Account | Zoho Creator account |
| Application | **Business Hub** (Employee, Leave Request) or any application with sample data |
| Where to run code | Creator's Deluge editor in **Workflow > Functions** (standalone functions), form workflows, or the Deluge **Script/Console** option if available |

> Deluge syntax and the editor evolve. Use the editor's autocomplete and error messages, and consult the current Zoho Deluge documentation for exact function signatures.

## 4. Theory

### 4.1 What Is Deluge?

Deluge (Data Enriched Language for the Universal Grid Environment) is Zoho's scripting language used across Creator and other Zoho products. It uses a readable, English-like syntax and has built-in support for database operations, email, integrations, and APIs.

### 4.2 Data Types

| Type | Example |
|---|---|
| Text (string) | `"Hello"` |
| Number (int) | `25` |
| Decimal | `99.5` |
| Boolean | `true`, `false` |
| Date / Date-Time | `'01-Jan-2026'`, `zoho.currentdate`, `zoho.currenttime` |
| List | `{1, 2, 3}` or `List()` |
| Map (key-value) | `Map()` |
| Collection (records) | Result of a fetch |

### 4.3 Operators

| Category | Operators |
|---|---|
| Arithmetic | `+  -  *  /  %` |
| Comparison | `==  !=  <  >  <=  >=` |
| Logical | `&&  ||  !` |
| String concatenation | `+` |

### 4.4 Variables and Comments

```
// This is a single-line comment
name = "Asha";          // text variable
age = 25;               // number
isActive = true;        // boolean
```

### 4.5 Commonly Used System Variables

| Variable | Meaning |
|---|---|
| `zoho.currentdate` | Current date |
| `zoho.currenttime` | Current date-time |
| `zoho.loginuser` | Name/ID of the logged-in user |
| `zoho.loginuserid` | Email of the logged-in user |
| `zoho.adminuserid` | Admin email of the account |
| `input.<FieldLinkName>` | Value of a form field in form workflows |

## 5. Procedure

### Part A: First Program: Display Output

Create a **standalone function** (Workflow > Functions > Create function) and run it from the editor's **Run/Execute** option.

```
void helloWorld()
{
    info "Hello, Deluge!";
}
```

`info` prints values to the execution log, which is useful for debugging.

### Part B: Variables, Operators, and Conditions

```
void checkNumber()
{
    num = 15;

    if(num % 2 == 0)
    {
        info num + " is even";
    }
    else
    {
        info num + " is odd";
    }

    if(num > 10 && num < 20)
    {
        info "Number is between 10 and 20";
    }
}
```

### Part C: Loops

**For each over a list**

```
void listDemo()
{
    fruits = {"Apple", "Banana", "Mango"};

    for each fruit in fruits
    {
        info fruit;
    }
}
```

**Looping over a range of numbers**

```
void sumNumbers()
{
    total = 0;

    for each n in {1, 2, 3, 4, 5}
    {
        total = total + n;
    }

    info "Sum = " + total;
}
```

**Build a list dynamically**

```
void buildList()
{
    numbers = List();

    for each i in {1, 2, 3, 4, 5}
    {
        numbers.add(i * i);
    }

    info numbers;
    info "Count: " + numbers.size();
}
```

### Part D: Maps

```
void mapDemo()
{
    student = Map();
    student.put("Name", "Ravi");
    student.put("Marks", 87);

    info student.get("Name");
    info student.get("Marks");
    info student;
}
```

### Part E: Working with Text, Numbers, and Dates

```
void builtInDemo()
{
    text = "  Zoho Creator  ";
    info text.trim();
    info text.trim().toUpperCase();
    info text.trim().length();
    info text.contains("Creator");
    info text.replaceAll("Zoho", "My");
    info text.trim().subString(0, 4);

    amount = 1234.5678;
    info amount.round(2);

    today = zoho.currentdate;
    info today;
    info today.addDay(7);
    info today.getDay();
    info today.getMonth();
    info today.getYear();
    info today.toString("dd-MMM-yyyy");
}
```

### Part F: Custom Functions with Parameters and Return Values

**Function that returns a value**

```
int addNumbers(int a, int b)
{
    return a + b;
}
```

**Function that returns text**

```
string getGrade(int marks)
{
    grade = "F";

    if(marks >= 90)
    {
        grade = "A+";
    }
    else if(marks >= 75)
    {
        grade = "A";
    }
    else if(marks >= 60)
    {
        grade = "B";
    }
    else if(marks >= 40)
    {
        grade = "C";
    }

    return grade;
}
```

**Calling a function from another script**

```
result = thisapp.addNumbers(10, 20);
info result;

grade = thisapp.getGrade(82);
info grade;
```

(In Creator, custom functions are called through the `thisapp` namespace. Confirm the namespace shown in your editor.)

### Part G: Database Operations (Fetch, Insert, Update, Delete)

Use your own form and field **link names**. The examples assume forms `Employee` (fields `Full_Name`, `Email`, `Department`, `Salary`) and `Leave_Request`.

**Fetch records**

```
void fetchDemo()
{
    // all employees in IT
    itStaff = Employee[Department == "IT"];
    info "IT employees: " + itStaff.count();

    for each emp in itStaff
    {
        info emp.Full_Name + " - " + emp.Email;
    }

    // single record by criteria
    one = Employee[Email == "asha@example.com"];
    info one.Full_Name;
}
```

**Aggregate functions**

```
void aggregateDemo()
{
    total = Employee[ID != 0].count();
    totalSalary = Employee[ID != 0].sum(Salary);
    maxSalary = Employee[ID != 0].maximum(Salary);

    info "Employees: " + total;
    info "Total salary: " + totalSalary;
    info "Highest salary: " + maxSalary;
}
```

**Insert a record**

```
void insertDemo()
{
    insert into Employee
    [
        Full_Name = "Test User"
        Email = "test.user@example.com"
        Department = "Sales"
        Salary = 30000
        Added_User = zoho.loginuser
    ]
}
```

**Update records**

```
void updateDemo()
{
    for each emp in Employee[Department == "Sales"]
    {
        emp.Salary = emp.Salary * 1.05;
    }
}
```

**Delete records**

```
void deleteDemo()
{
    delete from Employee[Email == "test.user@example.com"];
}
```

> Be careful with delete and update scripts: always test with a narrow criteria first, and verify results before running on all data.

### Part H: Form Workflow Examples

**Validation (form On validate)**

```
if(input.Salary < 0)
{
    alert "Salary cannot be negative.";
    cancel submit;
}
```

**Set a default after submit (On create > On success)**

```
input.Status = "Pending";
```

**Send an email**

```
sendmail
[
    from: zoho.adminuserid
    to: input.Email
    subject: "Welcome " + input.Full_Name
    message: "Your employee record has been created."
]
```

**Show a message to the user**

```
openUrl("#Report:Employee_Report", "same window");
```

### Part I: Practice Programs

Write and run the following as functions. Record your code and output.

| # | Program |
|---|---|
| 1 | Print the multiplication table of a number (use a loop) |
| 2 | Check whether a number is prime |
| 3 | Reverse a text string |
| 4 | Find the largest number in a list |
| 5 | Count vowels in a text string |
| 6 | Function `calculateTax(salary)` returning 10% tax if salary > 50,000, else 5% |
| 7 | Count employees per department using a Map |
| 8 | Calculate the age from a date of birth |

**Sample solution (Program 1)**

```
void multiplicationTable(int n)
{
    for each i in {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
    {
        info n + " x " + i + " = " + (n * i);
    }
}
```

**Sample solution (Program 6)**

```
decimal calculateTax(decimal salary)
{
    rate = 0.05;

    if(salary > 50000)
    {
        rate = 0.10;
    }

    return salary * rate;
}
```

**Sample solution (Program 7: employees per department)**

```
void employeesPerDepartment()
{
    counts = Map();

    for each emp in Employee[ID != 0]
    {
        dept = emp.Department;

        if(counts.containsKey(dept))
        {
            counts.put(dept, counts.get(dept) + 1);
        }
        else
        {
            counts.put(dept, 1);
        }
    }

    info counts;
}
```

### Part J: Debugging

1. Use `info` to print intermediate values.
2. Read the **error line** and message in the editor; fix missing semicolons, braces, or incorrect link names.
3. Use the platform's **Logs** or **Execution history** to review run results.
4. Test with small data before running on full data.
5. Use **comments** to disable parts of code while testing.

## 6. Observations

| Program | Input | Output | Status |
|---|---|---|---|
| helloWorld | none | | |
| checkNumber | 15 | | |
| addNumbers | 10, 20 | | |
| getGrade | 82 | | |
| fetchDemo | | | |
| Practice 1 to 8 | | | |

### Errors Encountered

| Error Message | Cause | Fix |
|---|---|---|
| | | |

## 7. Result

Deluge scripting fundamentals were practiced: variables, conditions, loops, lists, maps, built-in functions, database operations, workflows, and custom functions.

## 8. Conclusion

Deluge extends no-code applications with custom logic that visual configuration cannot cover. Understanding its basics lets builders validate data, automate processes, integrate systems, and reuse logic through custom functions.

## 9. Viva Questions

1. What is Deluge and where is it used?
2. How do you declare variables and write comments in Deluge?
3. What is the difference between a list and a map?
4. How do you fetch and update records?
5. What does `cancel submit` do?
6. How do you write and call a custom function?
7. How can you debug a Deluge script?
8. Why should you test delete and update scripts on a small set of records first?

## 10. References

- Zoho Deluge documentation: https://www.zoho.com/deluge/help/
- Zoho Creator help: https://help.zoho.com/portal/en/community/creator

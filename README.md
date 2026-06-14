# Employee Management System
A console-based Java application for managing employee records using ArrayList, HashMap, file persistence, and full CRUD operations.

---

## Project Overview
This system lets you add, view, search, update, and delete employee records through a numbered menu. Data is saved to disk automatically after every change, so nothing is lost when you close the program.

**Key concepts demonstrated:**
- `ArrayList` — ordered list of employees for iteration and display
- `HashMap<String, Employee>` — fast O(1) employee lookup by ID
- Object Serialization — save/load data with `ObjectOutputStream` / `ObjectInputStream`
- Exception handling — invalid input, file errors, number format errors
- Multi-class design — each class has a single responsibility

---

## Project Structure
```
EmployeeManagementSystem/
├── src/
│   └── employeems/
│       ├── Main.java                    ← Entry point
│       ├── Employee.java                ← Employee data class (Serializable)
│       ├── EmployeeManagementSystem.java← CRUD, search, menu logic
│       ├── EmployeeFileHandler.java     ← File save/load/export
│       └── EmployeeReportGenerator.java ← All reporting features
├── data/
│   └── employees.dat                    ← Auto-created binary data file
├── reports/
│   └── employee_report_YYYYMMDD.txt     ← Exported text reports
├── docs/
│   └── DATA_FORMAT.md                   ← Data format specification
└── README.md
```

---

## Setup & Running

### Prerequisites
- Java JDK 8 or higher installed
- Command Prompt (Windows) or Terminal (Mac/Linux)

### Step 1 — Compile
Open Command Prompt inside the `EmployeeManagementSystem` folder and run:
```
javac -d out src/employeems/*.java
```
This compiles all `.java` files and puts the `.class` files into the `out/` folder.

### Step 2 — Run
```
java -cp out employeems.Main
```

### Step 3 — Use the menu
```
============================================================
         EMPLOYEE MANAGEMENT SYSTEM
============================================================
  1.  Add New Employee
  2.  View All Employees
  3.  Search Employee
  4.  Update Employee
  5.  Delete Employee
  6.  Generate Reports
  7.  Save to File
  8.  Load from File
  9.  Export Report to Text File
  10. Exit
```

---

## Features

### CRUD Operations
| Operation | Description |
|-----------|-------------|
| Create    | Add a new employee with ID, name, department, position, salary, and join date |
| Read      | View all employees in a formatted table |
| Update    | Edit any field of an existing employee by ID |
| Delete    | Remove an employee after confirmation |

### Search (5 modes)
- By **ID** — exact match using HashMap (instant lookup)
- By **Name** — partial, case-insensitive match
- By **Department** — partial, case-insensitive match
- By **Position** — partial, case-insensitive match
- By **Salary Range** — enter min and max

### Reports (6 options)
- Salary statistics (total, average, highest, lowest)
- Department-wise summary (count + average salary per department)
- Position-wise employee count
- Employees ranked by salary (descending)
- Recently joined employees (top N)
- Full report (all of the above)

### File Persistence
- Data auto-saves to `data/employees.dat` after every Add, Update, Delete
- Auto-loads on startup if the file exists
- Text report export to `reports/` folder with timestamp in filename

---

## Sample Output

**Adding an employee:**
```
=== ADD NEW EMPLOYEE ===
Enter Employee ID (e.g. E001): E001
Enter Name: Alice Johnson
Enter Department: Engineering
Enter Position: Software Developer
Enter Salary (Rs.): 85000
Enter Join Date (yyyy-MM-dd): 2024-01-15

[OK] Employee added successfully!
[OK] Data saved successfully to 'data/employees.dat'.
```

**View all employees:**
```
#    ID       Name                 Department      Position           Salary           Join Date
----------------------------------------------------------------------------------------------------
1    E001     Alice Johnson        Engineering     Software Developer Rs.85,000.00     2024-01-15
2    E002     Bob Wilson           Marketing       Manager            Rs.95,000.00     2024-01-10
3    E003     Carol Davis          HR              Specialist         Rs.75,000.00     2024-01-05
4    E004     David Brown          Engineering     Senior Developer   Rs.105,000.00    2024-01-12
```

**Salary report:**
```
SALARY STATISTICS
Total Employees  : 4
Total Salary     : Rs.360,000.00
Average Salary   : Rs.90,000.00
Highest Salary   : Rs.105,000.00  (David Brown)
Lowest Salary    : Rs.75,000.00  (Carol Davis)
```

---

## Exception Handling
| Scenario | How it's handled |
|----------|-----------------|
| Non-numeric salary input | Caught with `NumberFormatException`, user re-prompted |
| Duplicate employee ID | Checked against HashMap before insert |
| Invalid date format | Caught with `ParseException`, user re-prompted |
| File not found on load | Graceful message, fresh start |
| Corrupted data file | Caught with `IOException` / `ClassNotFoundException` |
| Menu choice out of range | Loop re-prompts until valid |

---

## Technologies Used
- Java SE (JDK 8+)
- `java.util.ArrayList`, `java.util.HashMap`
- `java.io.ObjectOutputStream` / `ObjectInputStream` (Serialization)
- `java.io.PrintWriter` (text export)
- `java.util.Scanner` (console input)
- `java.text.SimpleDateFormat` (date formatting/parsing)

# Faculty Management Database Schema

## METADATA
```json
{
  "database_name": "faculty_management_db",
  "schemas": [
    {
      "schema_name": "FACULTY_MANAGEMENT",
      "tables": [
        {
          "table_name": "EMPLOYEE",
          "columns": [
            { "column_name": "Ssn", "data_type": "CHAR(9)", "constraints": ["PRIMARY KEY"] },
            { "column_name": "Fname", "data_type": "VARCHAR(30)", "constraints": [] },
            { "column_name": "Minit", "data_type": "CHAR(1)", "constraints": [] },
            { "column_name": "Lname", "data_type": "VARCHAR(30)", "constraints": [] },
            { "column_name": "Bdate", "data_type": "DATE", "constraints": [] },
            { "column_name": "Address", "data_type": "VARCHAR(50)", "constraints": [] },
            { "column_name": "Salary", "data_type": "NUMERIC(10, 2)", "constraints": [] },
            { "column_name": "Sex", "data_type": "CHAR(1)", "constraints": [] },
            { "column_name": "Supervisor", "data_type": "CHAR(9)", "constraints": ["FOREIGN KEY (Supervisor) REFERENCES EMPLOYEE(Ssn)"] }
          ],
          "table_constraints": ["PRIMARY KEY (Ssn)", "FOREIGN KEY (Supervisor) REFERENCES EMPLOYEE(Ssn)"]
        },
        {
          "table_name": "DEPARTMENT",
          "columns": [
            { "column_name": "Number", "data_type": "INT", "constraints": ["PRIMARY KEY"] },
            { "column_name": "Name", "data_type": "VARCHAR(30)", "constraints": [] },
            { "column_name": "Locations", "data_type": "VARCHAR(100)", "constraints": [] }
          ],
          "table_constraints": ["PRIMARY KEY (Number)"]
        },
        {
          "table_name": "PROJECT",
          "columns": [
            { "column_name": "Number", "data_type": "INT", "constraints": ["PRIMARY KEY"] },
            { "column_name": "Name", "data_type": "VARCHAR(30)", "constraints": [] },
            { "column_name": "Location", "data_type": "VARCHAR(50)", "constraints": [] }
          ],
          "table_constraints": ["PRIMARY KEY (Number)"]
        },
        {
          "table_name": "DEPENDENT",
          "columns": [
            { "column_name": "Name", "data_type": "VARCHAR(30)", "constraints": ["PRIMARY KEY"] },
            { "column_name": "Employee_Ssn", "data_type": "CHAR(9)", "constraints": ["FOREIGN KEY (Employee_Ssn) REFERENCES EMPLOYEE(Ssn)"] },
            { "column_name": "Sex", "data_type": "CHAR(1)", "constraints": [] },
            { "column_name": "Birth_date", "data_type": "DATE", "constraints": [] },
            { "column_name": "Relationship", "data_type": "VARCHAR(20)", "constraints": [] }
          ],
          "table_constraints": ["PRIMARY KEY (Name, Employee_Ssn)", "FOREIGN KEY (Employee_Ssn) REFERENCES EMPLOYEE(Ssn)"]
        },
        {
          "table_name": "SUPERVISION",
          "columns": [
            { "column_name": "Supervisor", "data_type": "CHAR(9)", "constraints": ["FOREIGN KEY (Supervisor) REFERENCES EMPLOYEE(Ssn)"] },
            { "column_name": "Supervisee", "data_type": "CHAR(9)", "constraints": ["FOREIGN KEY (Supervisee) REFERENCES EMPLOYEE(Ssn)"] }
          ],
          "table_constraints": ["PRIMARY KEY (Supervisor, Supervisee)", "FOREIGN KEY (Supervisor) REFERENCES EMPLOYEE(Ssn)", "FOREIGN KEY (Supervisee) REFERENCES EMPLOYEE(Ssn)"]
        },
        {
          "table_name": "WORKS_ON",
          "columns": [
            { "column_name": "Employee_Ssn", "data_type": "CHAR(9)", "constraints": ["FOREIGN KEY (Employee_Ssn) REFERENCES EMPLOYEE(Ssn)"] },
            { "column_name": "Project_Number", "data_type": "INT", "constraints": ["FOREIGN KEY (Project_Number) REFERENCES PROJECT(Number)"] },
            { "column_name": "Hours", "data_type": "NUMERIC(5, 2)", "constraints": [] }
          ],
          "table_constraints": ["PRIMARY KEY (Employee_Ssn, Project_Number)", "FOREIGN KEY (Employee_Ssn) REFERENCES EMPLOYEE(Ssn)", "FOREIGN KEY (Project_Number) REFERENCES PROJECT(Number)"]
        },
        {
          "table_name": "MANAGES",
          "columns": [
            { "column_name": "Employee_Ssn", "data_type": "CHAR(9)", "constraints": ["FOREIGN KEY (Employee_Ssn) REFERENCES EMPLOYEE(Ssn)"] },
            { "column_name": "Department_Number", "data_type": "INT", "constraints": ["FOREIGN KEY (Department_Number) REFERENCES DEPARTMENT(Number)"] },
            { "column_name": "Start_date", "data_type": "DATE", "constraints": [] }
          ],
          "table_constraints": ["PRIMARY KEY (Employee_Ssn, Department_Number)", "FOREIGN KEY (Employee_Ssn) REFERENCES EMPLOYEE(Ssn)", "FOREIGN KEY (Department_Number) REFERENCES DEPARTMENT(Number)"]
        },
        {
          "table_name": "WORKS_FOR",
          "columns": [
            { "column_name": "Employee_Ssn", "data_type": "CHAR(9)", "constraints": ["FOREIGN KEY (Employee_Ssn) REFERENCES EMPLOYEE(Ssn)"] },
            { "column_name": "Department_Number", "data_type": "INT", "constraints": ["FOREIGN KEY (Department_Number) REFERENCES DEPARTMENT(Number)"] },
            { "column_name": "Start_date", "data_type": "DATE", "constraints": [] }
          ],
          "table_constraints": ["PRIMARY KEY (Employee_Ssn, Department_Number)", "FOREIGN KEY (Employee_Ssn) REFERENCES EMPLOYEE(Ssn)", "FOREIGN KEY (Department_Number) REFERENCES DEPARTMENT(Number)"]
        },
        {
          "table_name": "DEPENDENTS_OF",
          "columns": [
            { "column_name": "Employee_Ssn", "data_type": "CHAR(9)", "constraints": ["FOREIGN KEY (Employee_Ssn) REFERENCES DEPENDENT(Employee_Ssn)"] },
            { "column_name": "Dependent_Name", "data_type": "VARCHAR(30)", "constraints": ["FOREIGN KEY (Dependent_Name) REFERENCES DEPENDENT(Name)"] }
          ],
          "table_constraints": ["PRIMARY KEY (Employee_Ssn, Dependent_Name)", "FOREIGN KEY (Employee_Ssn, Dependent_Name) REFERENCES DEPENDENT(Employee_Ssn, Name)"]
        },
        {
          "table_name": "CONTROLS",
          "columns": [
            { "column_name": "Department_Number", "data_type": "INT", "constraints": ["FOREIGN KEY (Department_Number) REFERENCES DEPARTMENT(Number)"] },
            { "column_name": "Project_Number", "data_type": "INT", "constraints": ["FOREIGN KEY (Project_Number) REFERENCES PROJECT(Number)"] }
          ],
          "table_constraints": ["PRIMARY KEY (Department_Number, Project_Number)", "FOREIGN KEY (Department_Number) REFERENCES DEPARTMENT(Number)", "FOREIGN KEY (Project_Number) REFERENCES PROJECT(Number)"]
        }
      ]
    }
  ]
}
```

## OVERVIEW

### 1. EMPLOYEE
- **Ssn**: Employee's unique Social Security Number (Primary Key).
- **Fname**: First name of the employee.
- **Minit**: Middle initial of the employee.
- **Lname**: Last name of the employee.
- **Bdate**: Birth date of the employee.
- **Address**: Residential address of the employee.
- **Salary**: Employee's salary in numeric format.
- **Sex**: Gender of the employee (M/F).
- **Supervisor**: Employee's supervisor's Ssn (Foreign Key).

**Purpose**: Stores personal and employment details of each employee, including supervisory relationships.

### 2. DEPARTMENT
- **Number**: Department's unique identifier (Primary Key).
- **Name**: Name of the department.
- **Locations**: Location(s) of the department's operations.

**Purpose**: Manages data related to the different departments in the organization.

### 3. PROJECT
- **Number**: Unique project identifier (Primary Key).
- **Name**: Name of the project.
- **Location**: Location where the project is being executed.

**Purpose**: Holds data about various projects run by the organization.

### 4. DEPENDENT
- **Name**: Name of the dependent (Primary Key, together with Employee_Ssn).
- **Employee_Ssn**: Employee's Ssn to whom the dependent belongs (Foreign Key).
- **Sex**: Gender of the dependent (M/F).
- **Birth_date**: Birth date of the dependent.
- **Relationship**: Relationship to the employee (e.g., spouse, child).

**Purpose**: Stores information about employees' dependents.

### 5. SUPERVISION
- **Supervisor**: Ssn of the employee who is the supervisor (Foreign Key).
- **Supervisee**: Ssn of the employee being supervised (Foreign Key).

**Purpose**: Tracks the supervision relationships between employees.

### 6. WORKS_ON
- **Employee_Ssn**: Employee's Ssn working on a project (Foreign Key).
- **Project_Number**: Project number being worked on (Foreign Key).
- **Hours**: Number of hours the employee has worked on the project.

**Purpose**: Links employees to the projects they are working on and tracks their hours.

### 7. MANAGES
- **Employee_Ssn**: Ssn of the employee managing a department (Foreign Key).
- **Department_Number**: Department being managed (Foreign Key).
- **Start_date**: Date the employee started managing the department.

**Purpose**: Manages the relationship between employees and the departments they manage.

### 8. WORKS_FOR
- **Employee_Ssn**: Employee's Ssn (Foreign Key).
- **Department_Number**: Department number where the employee works (Foreign Key).
- **Start_date**: Date the employee started working for the department.

**Purpose**: Tracks which department an employee works for.

### 9. DEPENDENTS_OF
- **Employee_Ssn**: Ssn of the employee (Foreign Key).
- **Dependent_Name**: Name of the dependent (Foreign Key).

**Purpose**: Establishes a relationship between employees and their dependents.

### 10. CONTROLS
- **Department_Number**: Department controlling the project (Foreign Key).
- **Project_Number**: Project being controlled (Foreign Key).

**Purpose**: Links departments with the projects they are responsible for managing.


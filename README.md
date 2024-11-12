# Faculty Management Database Schema

## DATABASE DESCRIPTION
## PostgreSQL Database: `faculty_management_db`

The **PostgreSQL database** named `faculty_management_db` is a robust and comprehensive database schema designed to manage and organize the faculty and administrative information of an institution. Below is a detailed description of its structure and components, including schemas, tables, and relationships.

---

### Schema Overview: `FACULTY_MANAGEMENT`

This schema serves as the central framework of the `faculty_management_db`, housing all the tables necessary to manage employee information, department details, projects, and their interrelations. It emphasizes data consistency, integrity, and adherence to business rules via well-defined constraints.

---

## Tables and Their Structure

#### 1. `EMPLOYEE` Table

The `EMPLOYEE` table is the backbone of the schema, containing critical details about employees.

- **Columns:**
  - `Ssn` (`CHAR(9)`): A unique identifier for employees; serves as the primary key.
  - `Fname` (`VARCHAR(30)`): First name of the employee.
  - `Minit` (`CHAR(1)`): Middle initial of the employee.
  - `Lname` (`VARCHAR(30)`): Last name of the employee.
  - `Bdate` (`DATE`): Birthdate of the employee.
  - `Address` (`VARCHAR(50)`): Residential address.
  - `Salary` (`NUMERIC(10, 2)`): Salary of the employee.
  - `Sex` (`CHAR(1)`): Gender of the employee.
  - `Supervisor` (`CHAR(9)`): SSN of the supervising employee, a foreign key referencing `EMPLOYEE(Ssn)`.

- **Constraints:**
  - Primary Key: `Ssn`.
  - Foreign Key: `Supervisor` references `EMPLOYEE(Ssn)`.

---

#### 2. `DEPARTMENT` Table

The `DEPARTMENT` table contains details about the various departments within the institution.

- **Columns:**
  - `Number` (`INT`): Unique identifier for departments; serves as the primary key.
  - `Name` (`VARCHAR(30)`): Name of the department.
  - `Locations` (`VARCHAR(100)`): Locations where the department operates.

- **Constraints:**
  - Primary Key: `Number`.

---

#### 3. `PROJECT` Table

The `PROJECT` table tracks various projects being undertaken by the departments.

- **Columns:**
  - `Number` (`INT`): Unique identifier for projects; serves as the primary key.
  - `Name` (`VARCHAR(30)`): Name of the project.
  - `Location` (`VARCHAR(50)`): Location where the project is executed.

- **Constraints:**
  - Primary Key: `Number`.

---

#### 4. `DEPENDENT` Table

This table stores information about the dependents of employees.

- **Columns:**
  - `Name` (`VARCHAR(30)`): Name of the dependent; part of the primary key.
  - `Employee_Ssn` (`CHAR(9)`): SSN of the employee; part of the primary key and foreign key referencing `EMPLOYEE(Ssn)`.
  - `Sex` (`CHAR(1)`): Gender of the dependent.
  - `Birth_date` (`DATE`): Birthdate of the dependent.
  - `Relationship` (`VARCHAR(20)`): Relationship to the employee.

- **Constraints:**
  - Primary Key: `Name, Employee_Ssn`.
  - Foreign Key: `Employee_Ssn` references `EMPLOYEE(Ssn)`.

---

#### 5. `SUPERVISION` Table

This table maps supervisory relationships between employees.

- **Columns:**
  - `Supervisor` (`CHAR(9)`): SSN of the supervisor; foreign key referencing `EMPLOYEE(Ssn)`.
  - `Supervisee` (`CHAR(9)`): SSN of the supervisee; foreign key referencing `EMPLOYEE(Ssn)`.

- **Constraints:**
  - Primary Key: `Supervisor, Supervisee`.
  - Foreign Keys: `Supervisor` and `Supervisee` reference `EMPLOYEE(Ssn)`.

---

#### 6. `WORKS_ON` Table

The `WORKS_ON` table links employees to the projects they are working on.

- **Columns:**
  - `Employee_Ssn` (`CHAR(9)`): SSN of the employee; foreign key referencing `EMPLOYEE(Ssn)`.
  - `Project_Number` (`INT`): Project number; foreign key referencing `PROJECT(Number)`.
  - `Hours` (`NUMERIC(5, 2)`): Number of hours worked on the project.

- **Constraints:**
  - Primary Key: `Employee_Ssn, Project_Number`.
  - Foreign Keys: `Employee_Ssn` references `EMPLOYEE(Ssn)`, `Project_Number` references `PROJECT(Number)`.

---

#### 7. `MANAGES` Table

This table records managerial assignments to departments.

- **Columns:**
  - `Employee_Ssn` (`CHAR(9)`): SSN of the managing employee; foreign key referencing `EMPLOYEE(Ssn)`.
  - `Department_Number` (`INT`): Department number; foreign key referencing `DEPARTMENT(Number)`.
  - `Start_date` (`DATE`): Start date of the managerial role.

- **Constraints:**
  - Primary Key: `Employee_Ssn, Department_Number`.
  - Foreign Keys: `Employee_Ssn` references `EMPLOYEE(Ssn)`, `Department_Number` references `DEPARTMENT(Number)`.

---

#### 8. `WORKS_FOR` Table

This table tracks departmental affiliations of employees.

- **Columns:**
  - `Employee_Ssn` (`CHAR(9)`): SSN of the employee; foreign key referencing `EMPLOYEE(Ssn)`.
  - `Department_Number` (`INT`): Department number; foreign key referencing `DEPARTMENT(Number)`.
  - `Start_date` (`DATE`): Start date of the association.

- **Constraints:**
  - Primary Key: `Employee_Ssn, Department_Number`.
  - Foreign Keys: `Employee_Ssn` references `EMPLOYEE(Ssn)`, `Department_Number` references `DEPARTMENT(Number)`.

---

#### 9. `DEPENDENTS_OF` Table

This table maps dependents to their respective employees.

- **Columns:**
  - `Employee_Ssn` (`CHAR(9)`): SSN of the employee; foreign key referencing `DEPENDENT(Employee_Ssn)`.
  - `Dependent_Name` (`VARCHAR(30)`): Name of the dependent; foreign key referencing `DEPENDENT(Name)`.

- **Constraints:**
  - Primary Key: `Employee_Ssn, Dependent_Name`.
  - Foreign Keys: Composite key referencing `DEPENDENT(Employee_Ssn, Name)`.

---

#### 10. `CONTROLS` Table

This table establishes control relationships between departments and projects.

- **Columns:**
  - `Department_Number` (`INT`): Department number; foreign key referencing `DEPARTMENT(Number)`.
  - `Project_Number` (`INT`): Project number; foreign key referencing `PROJECT(Number)`.

- **Constraints:**
  - Primary Key: `Department_Number, Project_Number`.
  - Foreign Keys: `Department_Number` references `DEPARTMENT(Number)`, `Project_Number` references `PROJECT(Number)`.

---

### Relationships and Data Integrity

1. **Hierarchy:** The schema emphasizes hierarchy through relationships like supervision (`SUPERVISION`) and management (`MANAGES`).
2. **Department-Project Association:** Departments control projects via the `CONTROLS` table.
3. **Employee Associations:** Employees are linked to departments, projects, and dependents through respective tables.
4. **Self-referential Integrity:** The `EMPLOYEE` table's `Supervisor` column maintains a self-referential foreign key, ensuring valid hierarchical relationships.

---

### Use Cases

- **Employee Management:** Track employee details, including personal and employment-related data.
- **Project Assignments:** Allocate employees to projects and monitor their contributions.
- **Departmental Oversight:** Manage departments and their locations, along with managerial responsibilities.
- **Dependents Tracking:** Maintain information about employees' dependents.
- **Control Structures:** Map interrelations between departments and projects to ensure organizational accountability.

This schema provides a comprehensive framework for efficiently managing faculty-related data while ensuring data integrity and consistency through well-defined constraints and relationships.

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


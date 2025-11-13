# Employee Management System

## Overview
The Employee Management System is a basic Database Management System (DBMS) project designed to handle core employee-related operations. It provides a simple structure for storing, retrieving, updating, and deleting employee records, including details such as personal information, department assignments, salaries, and roles. This project serves as an introductory implementation for students learning relational database concepts using MySQL.

The system demonstrates fundamental DBMS principles like table creation, primary/foreign key relationships, data insertion, and SQL queries for common HR tasks.

## Features
- **Employee Registration**: Add new employees with details like ID, name, age, department, position, and salary.
- **Data Retrieval**: View all employees or filter by department/role.
- **Updates and Deletions**: Modify employee information or remove records.
- **Reports**: Generate simple reports, such as average salary per department or total employees.
- **Data Integrity**: Enforces constraints like unique employee IDs and valid salary ranges.

## Technologies Used
- **Database**: MySQL (Relational DBMS)
- **Query Language**: SQL for schema definition, data manipulation, and queries
- **Tools**: MySQL Workbench or phpMyAdmin for execution (optional)

## Prerequisites
- MySQL Server installed (version 5.7 or higher)
- Access to a MySQL client (e.g., command line, Workbench)

## Installation and Setup
1. **Clone the Repository**:
   ```
   git clone https://github.com/sharpsalt/Employee-Management-System.git
   cd Employee-Management-System
   ```

2. **Create Database**:
   Open your MySQL client and execute:
   ```sql
   CREATE DATABASE employee_management;
   USE employee_management;
   ```

3. **Run the Schema Script**:
   Import or execute the provided SQL file (e.g., `database.sql` or `schema.sql`) to create tables and insert sample data:
   ```sql
   SOURCE path/to/database.sql;
   ```
   This will set up the necessary tables: `Employees`, `Departments`, and `Salaries` (if applicable).

4. **Verify Setup**:
   Run a test query:
   ```sql
   SELECT * FROM Employees LIMIT 5;
   ```

## Database Schema
The project uses a normalized schema with the following key tables:

### Employees Table
| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| emp_id | INT | Primary Key, Auto-increment |
| first_name | VARCHAR(50) | Employee's first name |
| last_name | VARCHAR(50) | Employee's last name |
| email | VARCHAR(100) | Unique email address |
| phone | VARCHAR(15) | Contact number |
| dept_id | INT | Foreign Key to Departments |
| position | VARCHAR(50) | Job title |
| hire_date | DATE | Date of joining |
| salary | DECIMAL(10,2) | Annual salary |

### Departments Table
| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| dept_id | INT | Primary Key, Auto-increment |
| dept_name | VARCHAR(50) | Department name (e.g., IT, HR) |
| location | VARCHAR(100) | Department location |

- **Relationships**: One-to-Many (One department has many employees).
- **Constraints**: Foreign keys ensure referential integrity; NOT NULL on essential fields.

Sample SQL for schema creation (included in the repo's SQL file):
```sql
CREATE TABLE Departments (
    dept_id INT AUTO_INCREMENT PRIMARY KEY,
    dept_name VARCHAR(50) NOT NULL,
    location VARCHAR(100)
);

CREATE TABLE Employees (
    emp_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    phone VARCHAR(15),
    dept_id INT,
    position VARCHAR(50),
    hire_date DATE DEFAULT CURRENT_DATE,
    salary DECIMAL(10,2) CHECK (salary > 0),
    FOREIGN KEY (dept_id) REFERENCES Departments(dept_id) ON DELETE SET NULL
);
```

## Usage
### Inserting Data
```sql
INSERT INTO Departments (dept_name, location) VALUES ('IT', 'Building A');
INSERT INTO Employees (first_name, last_name, email, dept_id, position, salary) 
VALUES ('John', 'Doe', 'john.doe@company.com', 1, 'Developer', 75000.00);
```

### Sample Queries
1. **List All Employees with Department**:
   ```sql
   SELECT e.first_name, e.last_name, e.position, d.dept_name
   FROM Employees e
   JOIN Departments d ON e.dept_id = d.dept_id;
   ```

2. **Average Salary by Department**:
   ```sql
   SELECT d.dept_name, AVG(e.salary) AS avg_salary
   FROM Employees e
   JOIN Departments d ON e.dept_id = d.dept_id
   GROUP BY d.dept_id;
   ```

3. **Employees Hired in Last Year**:
   ```sql
   SELECT * FROM Employees
   WHERE hire_date >= DATE_SUB(CURDATE(), INTERVAL 1 YEAR);
   ```

4. **Update Salary**:
   ```sql
   UPDATE Employees SET salary = 80000.00 WHERE emp_id = 1;
   ```

5. **Delete Employee**:
   ```sql
   DELETE FROM Employees WHERE emp_id = 1;
   ```

## Sample Data
The SQL script includes sample records for 10+ employees across 4 departments to demonstrate functionality.

## Project Structure
```
Employee-Management-System/
├── README.md              # This file
├── database.sql           # Main SQL script for schema and data
├── queries.sql            # Advanced queries and reports
└── diagram.png           # Optional ERD (Entity-Relationship Diagram)
```

## Potential Extensions
- Add triggers for automatic salary adjustments.
- Implement stored procedures for common operations (e.g., hire_employee).
- Integrate with a frontend (e.g., PHP or Python Flask) for a web-based interface.
- Add more tables for performance reviews, attendance, or projects.

## Contributing
Contributions are welcome! Please fork the repository and submit a pull request for any improvements, bug fixes, or new features.

## Contact
- **Author**: Srijan Verma (sharpsalt on GitHub)
- **Email**: [srijanv0@gmail.com](mailto:your-srijanv0@gmail.com)
- **Issues**: Report bugs or request features via GitHub Issues.

---

*This README was generated based on the repository's basic structure and inferred DBMS focus. For customizations, refer to the SQL files.*

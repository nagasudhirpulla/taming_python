# VS Code erd-editor plugin

## Introduction

The ERD Editor VS Code extension helps to develop and edit database schemas as interactive diagrams, allowing for simultaneous design and documentation

![erd-editor%20demo.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/erd-editor%20demo.png?raw=true)

## Key features

- **Native VS Code Integration:** Manage database design as `.erd.json` or `.json` files in a project.
- **Visual Schema Management:** Create and edit tables, columns, and indexes through an intuitive graphical interface. Automatically visualize cardinality (One-to-Many, etc.) via foreign key constraints.
- **SQL Import**: Parses the DDL statements from a `.sql` file (including tables, keys, and indexes) and imports it.

![erd-editor%20import%20sql.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/erd-editor%20import%20sql.png?raw=true)

- **Flexible Exports:** Generate SQL DDL or ORM objects directly from the design.
- **Multi-Engine Support:** Design for various dialects including MySQL, PostgreSQL, SQLite, and Oracle.
- **Intelligent Auto-Layout:** Keep your diagrams tidy and readable with automated table positioning.

## Using the tool

1. **Launch the Editor:** Open an `.erd.json` file with VS code
2. **Add a Table:** Right-click the canvas and select **Add Table** to start building a schema.
3. **Define Columns:** Use the table UI to add columns; toggle checkboxes for **Primary Keys (PK)** and **Not Null (NN)** constraints.
4. **Establish Foreign Keys:** Drag from one table's Primary Key to another table's column to instantly create a **One-to-Many** relationship.
5. Remember to zoom in to view the table columns
6. **Enable Auto-Layout:** Click the **Automatic Layout** button in the toolbar to snap your tables into an organized, readable grid.
7. **Customize Visualization:** Use the sidebar to toggle "Mini Map" or "Relationship Lines" for better navigation of large schemas.

## **Export SQL or ORM Objects**

A design can be exported as

- **SQL** that contains the DDL scripts for executing in the database
- **ORM Code** **objects** for popular languages like C#, Java, Typescript, GraphQL

![erd-editor%20code%20generation.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/erd-editor%20code%20generation.png?raw=true)

## Example SQL for demo

- Import the SQL into the erd-editor tool by right clicking on the canvas to play around with the tool

```sql
CREATE TABLE regions (
	region_id INT (11) AUTO_INCREMENT PRIMARY KEY,
	region_name VARCHAR (25) DEFAULT NULL
);

CREATE TABLE countries (
	country_id CHAR (2) PRIMARY KEY,
	country_name VARCHAR (40) DEFAULT NULL,
	region_id INT (11) NOT NULL,
	FOREIGN KEY (region_id) REFERENCES regions (region_id)
);

CREATE TABLE locations (
	location_id INT (11) AUTO_INCREMENT PRIMARY KEY,
	street_address VARCHAR (40) DEFAULT NULL,
	postal_code VARCHAR (12) DEFAULT NULL,
	city VARCHAR (30) NOT NULL,
	state_province VARCHAR (25) DEFAULT NULL,
	country_id CHAR (2) NOT NULL,
	FOREIGN KEY (country_id) REFERENCES countries (country_id)
);

CREATE TABLE jobs (
	job_id INT (11) AUTO_INCREMENT PRIMARY KEY,
	job_title VARCHAR (35) NOT NULL,
	min_salary DECIMAL (8, 2) DEFAULT NULL,
	max_salary DECIMAL (8, 2) DEFAULT NULL
);

CREATE TABLE departments (
	department_id INT (11) AUTO_INCREMENT PRIMARY KEY,
	department_name VARCHAR (30) NOT NULL,
	location_id INT (11) DEFAULT NULL,
	FOREIGN KEY (location_id) REFERENCES locations (location_id)
);

CREATE TABLE employees (
	employee_id INT (11) AUTO_INCREMENT PRIMARY KEY,
	first_name VARCHAR (20) DEFAULT NULL,
	last_name VARCHAR (25) NOT NULL,
	email VARCHAR (100) NOT NULL,
	phone_number VARCHAR (20) DEFAULT NULL,
	hire_date DATE NOT NULL,
	job_id INT (11) NOT NULL,
	salary DECIMAL (8, 2) NOT NULL,
	manager_id INT (11) DEFAULT NULL,
	department_id INT (11) DEFAULT NULL,
	FOREIGN KEY (job_id) REFERENCES jobs (job_id),
	FOREIGN KEY (department_id) REFERENCES departments (department_id),
	FOREIGN KEY (manager_id) REFERENCES employees (employee_id)
);

CREATE TABLE dependents (
	dependent_id INT (11) AUTO_INCREMENT PRIMARY KEY,
	first_name VARCHAR (50) NOT NULL,
	last_name VARCHAR (50) NOT NULL,
	relationship VARCHAR (25) NOT NULL,
	employee_id INT (11) NOT NULL,
	FOREIGN KEY (employee_id) REFERENCES employees (employee_id)
);
```

## References

- ERD Editor VS Code extension - [https://marketplace.visualstudio.com/items?itemName=dineug.vuerd-vscode](https://marketplace.visualstudio.com/items?itemName=dineug.vuerd-vscode)
- ERD Editor docs - [https://docs.erd-editor.io/](https://docs.erd-editor.io/)
- ERD Editor online app - [https://erd-editor.io/](https://erd-editor.io/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzI1NzY4OTMyXX0=
-->
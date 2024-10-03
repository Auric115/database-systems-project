
# Phase 1 Report

## 1. Project Details
**Project Name**: Secure Medical Records Database  
**Developer**: BJ Anderson 
LinkedIn: https://www.linkedin.com/in/bj-/
GitHub: https://github.com/Auric115


## 2. Problem Statement

In today's digital age, the healthcare industry deals with vast amounts of sensitive patient data. A simple spreadsheet such as an Excel document does not provide the security or scalability necessary to manage such data. Our **Secure Medical Records Database** will address these issues by providing a structured and secure solution for storing, accessing, and managing patient data.

This system will allow medical professionals to securely access patient records, update medical histories, and manage treatment details, all while ensuring that sensitive data like Social Security Numbers (SSNs) and medical information are encrypted both at rest and in transit. With role-based access control (RBAC), different levels of users will have different access privileges to ensure data privacy and integrity.

An Excel sheet lacks built-in encryption, role management, auditing, and security measures, making it unsuitable for handling sensitive information. By using a MySQL database, we gain the advantages of structured data storage, better querying capabilities, and most importantly, data security mechanisms such as encryption, authentication, and logging.

## 3. Target User

The database will be accessed by:
- **Doctors and Nurses**: They will be able to view and update patient records based on their roles.
- **Administrative Staff**: They will have access to manage user roles and audit logs but cannot modify patient records.
- **Patients**: Patients will be able to view their medical history and personal information, but they will not have access to modify it.

**Real-World Example**: In a hospital or clinic setting, a system like this can be used to securely store patient data, ensuring compliance with healthcare privacy regulations such as HIPAA (Health Insurance Portability and Accountability Act). 

## 4. List of Relations

We plan to create at least four key relations (tables) for this project:
1. **Users**: This table will store information about users of the system, including doctors, nurses, administrators, and patients.  
   - **Schema**: `user_id INT PRIMARY KEY`, `username VARCHAR(255) UNIQUE`, `password_hash VARCHAR(255)`, `role ENUM('doctor', 'nurse', 'admin', 'patient')`, `last_login TIMESTAMP`
  
2. **Patients**: This table will store patient-specific information. Sensitive fields such as SSN will be encrypted.
   - **Schema**: `patient_id INT PRIMARY KEY`, `name VARCHAR(255)`, `address VARCHAR(255)`, `ssn VARBINARY(255)`, `date_of_birth DATE`
   
3. **Medical_Records**: This table will contain the medical history of patients. It will link to both patients and doctors.
   - **Schema**: `record_id INT PRIMARY KEY`, `patient_id INT FOREIGN KEY`, `doctor_id INT FOREIGN KEY`, `treatment TEXT`, `notes TEXT`
   
4. **Audit_Logs**: This table will track every modification made to the patient or medical records, essential for security monitoring.
   - **Schema**: `log_id INT PRIMARY KEY`, `user_id INT FOREIGN KEY`, `action VARCHAR(255)`, `timestamp TIMESTAMP`, `record_id INT FOREIGN KEY`

## 5. Web Interface

The web interface will consist of several forms, allowing users to interact with the database based on their role:
- **Login Form**: A simple login form that validates user credentials. It will include fields like `username` and `password`, and will redirect users to the appropriate dashboard based on their role.
- **Patient Dashboard**: Patients will have a view-only interface to check their medical history and personal details.
- **Doctor Dashboard**: Doctors will be able to search for and update patient records using this interface. There will be forms for entering new treatments and updating medical records.
- **Admin Dashboard**: Administrators will have access to a secure form for managing user roles and viewing audit logs. They can query the database for any suspicious activity in the logs.

All forms will be designed with security in mind, ensuring proper input validation and protection against common attacks like SQL injection.

## 6. Data

To populate the relations, we will generate synthetic data, which will include dummy patient records, user credentials for doctors, nurses, and patients, and medical histories. 

For the **Patients** and **Medical_Records** tables, we will create fictional patients and their corresponding medical histories using data generators or manually created data. For sensitive fields like SSN, we will apply encryption techniques to ensure that even in the database, the sensitive information remains secure.

Audit logs will be generated based on simulated user actions, including login attempts and record modifications, to demonstrate how the system tracks changes over time.

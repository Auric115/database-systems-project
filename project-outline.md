# Phase 1 Report

## 1. Project Details
**Project Name**: Secure Banking System  
**Developer**: BJ Anderson  
LinkedIn: [BJ Anderson](https://www.linkedin.com/in/bj-/)  
GitHub: [Auric115](https://github.com/Auric115)

## 2. Problem Statement

In the current digital era, the banking sector manages enormous amounts of sensitive financial data. A simple spreadsheet such as an Excel document lacks the security, scalability, and control necessary for handling this information effectively. Our **Secure Banking System** aims to address these shortcomings by providing a structured, secure solution for storing, accessing, and managing financial data.

This system will allow banking professionals to securely handle customer financial records, transaction histories, and account management while ensuring that sensitive data, such as Social Security Numbers (SSNs), account numbers, and transaction details, are encrypted both at rest and in transit. With role-based access control (RBAC), different users such as customers, tellers, and administrators will have varying access privileges to maintain data privacy and integrity.

A simple Excel sheet lacks built-in encryption, auditing, and role management, making it insufficient for secure financial management. By implementing a MySQL database, we gain advantages like structured data storage, advanced querying, and crucial security features such as encryption, authentication, and transaction logging.

## 3. Target User

The database will be accessed by:
- **Bank Tellers**: Responsible for managing transactions and updating customer records.
- **Bank Administrators**: Will handle user roles, monitor audit logs, and have restricted access to financial data.
- **Customers**: Customers will have access to view their account details and transaction history, but they will not have permissions to alter any data.
  
**Real-World Example**: In a banking institution, this system can be used to securely store customer financial data and transaction records while complying with banking industry regulations like the Gramm-Leach-Bliley Act (GLBA) and Payment Card Industry Data Security Standard (PCI-DSS).

## 4. List of Relations

We plan to create at least four key relations (tables) for this project:
1. **Users**: This table will store user information, including tellers, administrators, and customers.
   - **Schema**: `user_id INT PRIMARY KEY`, `username VARCHAR(255) UNIQUE`, `password_hash VARCHAR(255)`, `role ENUM('teller', 'admin', 'customer')`, `last_login TIMESTAMP`
  
2. **Accounts**: This table will hold customer account details, with sensitive fields encrypted.
   - **Schema**: `account_id INT PRIMARY KEY`, `user_id INT FOREIGN KEY`, `account_number VARBINARY(255)`, `balance DECIMAL(10, 2)`, `account_type ENUM('savings', 'checking')`, `creation_date TIMESTAMP`
   
3. **Transactions**: This table will contain records of financial transactions, linked to accounts.
   - **Schema**: `transaction_id INT PRIMARY KEY`, `account_id INT FOREIGN KEY`, `amount DECIMAL(10, 2)`, `transaction_date TIMESTAMP`, `transaction_type ENUM('deposit', 'withdrawal', 'transfer')`, `description TEXT`
   
4. **Audit_Logs**: This table will track every modification to accounts or transaction records, essential for monitoring security.
   - **Schema**: `log_id INT PRIMARY KEY`, `user_id INT FOREIGN KEY`, `action VARCHAR(255)`, `timestamp TIMESTAMP`, `affected_table VARCHAR(255)`, `record_id INT`

## 5. Web Interface

The web interface will consist of several forms, allowing users to interact with the database securely:
- **Login Form**: A login form that verifies credentials and directs users to their respective dashboards (teller, admin, customer).
- **Customer Dashboard**: Customers will have a read-only interface to view their account balance and transaction history.
- **Teller Dashboard**: Tellers will use this interface to manage transactions, including deposits, withdrawals, and transfers. 
- **Admin Dashboard**: Administrators will have access to user management and the audit logs, monitoring for any suspicious activity in the system.

All forms will be designed with security best practices, including input validation, and will protect against SQL injection and other common attacks.

## 6. Data

To populate the relations, synthetic data will be generated, including dummy customer accounts, transaction records, and user credentials for tellers, admins, and customers.

For the **Accounts** and **Transactions** tables, we will create fictional accounts and financial transactions, encrypting sensitive fields such as account numbers. Audit logs will simulate user actions, including login attempts, and account or transaction modifications, to demonstrate the system’s ability to track changes securely.

# Bank Management System

A simple command-line-based Bank Management System using Python and MySQL.

## Features:
- **User Authentication**: Sign-In, Sign-Up, and Forgot Password functionality.
- **Password Security**: Uses SHA-256 hashing to store passwords securely.
- **Account Types**: Supports Saving and Current accounts.
- **OTP-Based Password Reset**: Allows users to reset passwords using OTP.

## Technologies Used:
- Python
- MySQL
- hashlib (for password hashing)
- random (for OTP generation)

## Prerequisites:
1. Install MySQL and create a database named `Bank_Management`.
2. Create the following tables:

```sql
CREATE TABLE saving_account (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    age INT,
    father_name VARCHAR(255),
    account_no INT UNIQUE,
    balance INT,
    password VARCHAR(255)
);

CREATE TABLE current_account (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    age INT,
    company_name VARCHAR(255),
    account_no INT UNIQUE,
    balance INT,
    password VARCHAR(255)
);


git clone https://github.com/yourusername/Bank-Management-System.git

cd Bank-Management-System

python bank_management.py

# Banking-System-with-Secure-Authentication

## Overview

This is a **Python-based banking system** that uses **MySQL** for data storage. It includes security features like **password protection** and **OTP-based password recovery**.

## Features

✅ **User Authentication** – Users must enter a password to log in.\
✅ **Secure Password Storage** – Uses **SHA-256 hashing** for security.\
✅ **OTP-Based Password Recovery** – Users can reset their password if they forget it.\
✅ **Account Management** – Deposit, Withdraw, and Transfer money securely.\
✅ **Transaction History** – View past transactions for better tracking.

## Database Setup

Before running the code, set up your MySQL database:

```sql
CREATE DATABASE Bank_Management;
USE Bank_Management;

CREATE TABLE saving_account (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    father_name VARCHAR(100),
    account_no INT UNIQUE,
    balance FLOAT,
    password VARCHAR(255)
);

CREATE TABLE current_account (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    company_name VARCHAR(100),
    account_no INT UNIQUE,
    balance FLOAT,
    password VARCHAR(255)
);
```

## Installation

1. Install **Python** (if not already installed).
2. Install required dependencies:
   ```sh
   pip install mysql-connector-python
   ```
3. Update **database credentials** in the Python script.
4. Run the script:
   ```sh
   python banking_system.py
   ```

## Usage

### 1️⃣ Sign-Up

- Select **Saving** or **Current Account**.
- Enter details and set a strong password.
- The system generates a **unique account number**.

### 2️⃣ Sign-In

- Enter your **account number** and **password**.
- If credentials match, access banking services.

### 3️⃣ Banking Services

- **Deposit Money** – Add funds to your account.
- **Withdraw Money** – Withdraw funds securely.
- **Transfer Money** – Send money to another account.
- **View Transactions** – Check transaction history.

### 4️⃣ Forgot Password (OTP-Based Recovery)

- Enter your account number.
- The system generates a **6-digit OTP** (displayed for now).
- Enter the OTP to reset your password securely.

## Security Measures

🔒 **Hashed Passwords** – Uses **SHA-256** hashing for storage.\
🔒 **OTP Verification** – Prevents unauthorized password resets.\
🔒 **SQL Injection Protection** – Uses parameterized queries.

## Future Enhancements

🚀 **Email/SMS OTP Delivery**\
🚀 **Graphical User Interface (GUI)**\
🚀 **Admin Panel for Account Management**

## License

This project is open-source and available under the **MIT License**.

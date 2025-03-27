# Bank_Management_via_MySQL

import mysql.connector
import random
import hashlib

# Function to hash passwords
def hash_password(password):
    return hashlib.sha256(password.encode()).hexdigest()

# Function to generate OTP
def generate_otp():
    return str(random.randint(100000, 999999))

# Database Connection
try:
    mycon = mysql.connector.connect(
        host="localhost",
        user="root",
        password="password",
        database="Bank_Management"
    )
    print("Connected to Database:", mycon)
    mycursor = mycon.cursor()
except mysql.connector.Error as err:
    print("Error connecting to database:", err)
    exit()

print("------Welcome to SAGAR'S BANK-----")
print("Press 1 for SignIN ")
print("Press 2 for SignUP")
print("Press 3 for Forgot Password")

a = input().strip()

if a == "1":  # Sign-In
    account_no = input("Enter Your Registered Account Number: ").strip()
    password = input("Enter Your Password: ").strip()
    hashed_password = hash_password(password)

    mycursor.execute("SELECT name, balance, password FROM saving_account WHERE account_no = %s", (account_no,))
    user = mycursor.fetchone()
    account_type = "saving_account"

    if not user:
        mycursor.execute("SELECT name, balance, password FROM current_account WHERE account_no = %s", (account_no,))
        user = mycursor.fetchone()
        account_type = "current_account"

    if user:
        if user[2] == hashed_password:
            print(f"Welcome {user[0]}! Your current balance is ₹{user[1]}")
        else:
            print("Incorrect Password! Access Denied.")
    else:
        print("Invalid Account Number! Please check and try again.")

elif a == "2":  # Sign-Up
    print("Thank you For Choosing Our Bank")
    acc_type = input("Press 1 for Saving Account.\nPress 2 for Current Account.\n").strip()

    name = input("Please Enter Your Name: ").strip()
    age = int(input("Please Enter Your Age: ").strip())
    password = input("Set a strong password: ").strip()
    hashed_password = hash_password(password)

    if acc_type == "1":
        father = input("Please Enter Your Father's Name: ").strip()
        account = random.randint(1000, 9999)
        balance = int(input("Enter The Amount That You Want To Deposit: ").strip())

        sql = "INSERT INTO saving_account (name, age, father_name, account_no, balance, password) VALUES (%s, %s, %s, %s, %s, %s)"
        values = (name, age, father, account, balance, hashed_password)

    elif acc_type == "2":
        company = input("Please Enter Your Company Name: ").strip()
        account = random.randint(100000, 999999)
        balance = int(input("Enter The Amount That You Want To Deposit: ").strip())

        sql = "INSERT INTO current_account (name, age, company_name, account_no, balance, password) VALUES (%s, %s, %s, %s, %s, %s)"
        values = (name, age, company, account, balance, hashed_password)

    else:
        print("Invalid Selection! Try again.")
        exit()

    mycursor.execute(sql, values)
    mycon.commit()
    print(f"Account Created Successfully! Your Account Number is {account}")

elif a == "3":  # Forgot Password
    account_no = input("Enter Your Registered Account Number: ").strip()

    mycursor.execute("SELECT name FROM saving_account WHERE account_no = %s", (account_no,))
    user = mycursor.fetchone()
    account_type = "saving_account"

    if not user:
        mycursor.execute("SELECT name FROM current_account WHERE account_no = %s", (account_no,))
        user = mycursor.fetchone()
        account_type = "current_account"

    if user:
        otp = generate_otp()
        print(f"Your OTP for password reset is: {otp}")  # Ideally, send via SMS or Email

        entered_otp = input("Enter the OTP: ").strip()
        if entered_otp == otp:
            new_password = input("Enter your new password: ").strip()
            hashed_new_password = hash_password(new_password)

            mycursor.execute(f"UPDATE {account_type} SET password = %s WHERE account_no = %s", (hashed_new_password, account_no))
            mycon.commit()

            print("Password reset successful! You can now log in with your new password.")
        else:
            print("Incorrect OTP! Password reset failed.")
    else:
        print("Account not found! Please check the account number.")

# Close the database connection
mycursor.close()
mycon.close()

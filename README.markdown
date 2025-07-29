# Enigma Password Manager

## Overview

Enigma Password Manager is a secure and user-friendly application designed to help users manage their website credentials safely. Built with Python, it uses MySQL for data storage and implements OTP-based email verification for enhanced security. The application allows users to generate strong passwords, store website credentials, modify existing entries, and securely manage their accounts.

## Features

- **User Authentication**: Sign up and log in with email and a strong master password (8-16 characters, including uppercase, lowercase, numbers, and symbols).
- **OTP Verification**: Secure account creation and password reset with email-based OTP verification.
- **Password Generation**: Generate strong, random passwords of 8-16 characters.
- **Credential Management**:
  - Add website details (website, username, password, email, phone number).
  - Modify existing credentials (username, email, password, or phone number).
  - View all stored credentials in a tabulated format.
- **Account Deletion**: Option to permanently delete your account with a 5-minute recovery window.
- **Security**:
  - Validates strong passwords and checks against a list of common weak passwords.
  - Prevents duplicate entries for the same website and username.
  - Sends alerts for unauthorized login attempts.

## Prerequisites

- **Python**: Version 3.x
- **MySQL**: A running MySQL server with a configured database.
- **Python Libraries**:
  - `mysql-connector-python`
  - `tabulate`
  - `smtplib` (included in Python standard library)
- **Gmail Account**: For sending OTP emails (requires an App Password for SMTP).
- **Common Roots File**: A `common_roots.txt` file containing weak passwords to avoid.

## Installation

1. **Install Python**: Ensure Python 3.x is installed on your system.
2. **Install Required Libraries**:

   ```bash
   pip install mysql-connector-python tabulate
   ```
3. **Set Up MySQL**:
   - Create a database (e.g., `enigma_db`).
   - Create two tables: `signup7` and `userinfo` with the following schema:

     ```sql
     CREATE TABLE signup7 (
         id INT AUTO_INCREMENT PRIMARY KEY,
         email VARCHAR(255) NOT NULL,
         name VARCHAR(255) NOT NULL,
         masterpassword VARCHAR(255) NOT NULL
     );
     
     CREATE TABLE userinfo (
         id INT,
         website VARCHAR(255) NOT NULL,
         webpassword VARCHAR(255) NOT NULL,
         username VARCHAR(255) NOT NULL,
         usermail VARCHAR(255) NOT NULL,
         userph BIGINT NOT NULL,
         FOREIGN KEY (id) REFERENCES signup7(id)
     );
     ```
4. **Configure Email**:
   - Replace placeholders in the `mail()` function with your Gmail address and App Password.
5. **Prepare** `common_roots.txt`:
   - Create a text file named `common_roots.txt` in the same directory as the script, containing a list of weak passwords to avoid.

## Configuration

Update the following placeholders in the script:

- **Database Connection**:

  ```python
  return mysql.connector.connect(
      host="localhost",
      user="your_mysql_username",
      password="your_mysql_password",
      database="your_database_name"
  )
  ```
- **Email Settings**:

  ```python
  from_email = "your_gmail@gmail.com"
  password = "your_gmail_app_password"
  ```

## Usage

1. **Run the Script**:

   ```bash
   python enigma_pwd_manager.py
   ```
2. **Main Menu**:
   - **1. Login**: Log in with your email and master password. Use `forgotpwd` to reset your password.
   - **2. Signup**: Create a new account with email verification.
   - **3. Generate Password**: Generate a random, strong password.
   - **4. How to Use**: View a quick guide on using the application.
   - **5. Exit**: Exit the application.
3. **Logged-in Menu**:
   - Add, modify, or view website credentials.
   - Delete your account (with a 5-minute recovery period).
   - Exit the logged-in session.

## Security Notes

- **Master Password**: Must be 8-16 characters, include uppercase, lowercase, numbers, and symbols, and not be in `common_roots.txt`.
- **OTP**: Valid for 5 minutes with up to 5 attempts.
- **Email Validation**: Ensures valid email formats for sign-up and credential storage.
- **Duplicate Entries**: Prevents adding duplicate website-username combinations.
- **Unauthorized Access**: Alerts users via email after 5 failed login attempts.

## Limitations

- Requires a stable internet connection for sending OTP emails.
- Phone number input is stored as an integer, limiting formats.
- Relies on `common_roots.txt` for weak password checks, which must be maintained.
- No GUI; operates via command-line interface.

## Future Improvements

- Add a graphical user interface (GUI) for better user experience.
- Support additional email providers for OTP.
- Implement password encryption for enhanced security.
- Add multi-factor authentication options.

## Authors

- Yashwant Gokul P
- Sankara Narayanan S
- S Haridev
- Charulatha S
# Linux User and Group Administration - Complete Study Notes

> Based on Class-03 with additional explanations, practical examples, and Linux administration best practices.

---

# Table of Contents

1. Introduction
2. What is a User?
3. Types of Linux Users
4. User ID (UID) and Group ID (GID)
5. The `/etc/passwd` File
6. Understanding `/etc/passwd` Fields
7. Creating Users
8. The `/etc/shadow` File
9. Understanding `/etc/shadow` Fields
10. Setting and Changing Passwords
11. Viewing User Information
12. Renaming Users
13. Useful User Management Commands
14. Best Practices
15. Summary

---

# 1. Introduction

Linux is a **multi-user operating system**, meaning multiple users can use the same system simultaneously.

Each user has their own:

- Username
- Password
- Home directory
- Permissions
- Files
- Environment

Proper user and group management is one of the most important responsibilities of a Linux system administrator.

---

# 2. What is a User?

A **user** is an account that allows someone (or a system service) to log in and interact with the Linux operating system.

Examples:

```
ashiqur
student
developer
admin
```

Every user has:

- A unique username
- A User ID (UID)
- A Primary Group ID (GID)
- A home directory
- A login shell

---

# 3. Types of Linux Users

Linux mainly has **three types of users**.

---

## Root User

The **root** user is the system administrator (superuser).

Characteristics:

- Has complete control over the system.
- Can read, modify, or delete any file.
- Can install or remove software.
- Can manage users and services.

UID:

```
0
```

Example:

```bash
root
```

> ⚠️ Be careful when working as `root`, as incorrect commands can affect the entire system.

---

## System Users

System users are created automatically for running services and applications.

Examples:

```
mysql
nginx
www-data
postfix
daemon
```

Characteristics:

- Usually cannot log in interactively.
- Used by background services.
- Improve security by isolating services.

Typical UID range:

```
1–999
```

(The exact range may vary depending on the Linux distribution.)

---

## Regular Users

Regular users are normal human accounts used for daily work.

Examples:

```
student
developer
hasan
john
```

Characteristics:

- Can log in to the system.
- Usually have their own home directory.
- Limited permissions unless granted `sudo` access.

Typical UID:

```
1000 and above
```

---

# 4. User ID (UID) and Group ID (GID)

Every user has two important identifiers.

## UID (User ID)

A unique numeric identifier assigned to each user.

Example:

```
1001
```

Linux internally uses the UID rather than the username for permission checks.

---

## GID (Group ID)

Each user belongs to at least one group.

The **primary group** is identified by its GID.

Example:

```
1001
```

Groups help manage permissions for multiple users efficiently.

---

# 5. The `/etc/passwd` File

The file:

```text
/etc/passwd
```

contains basic information about every user account.

View it using:

```bash
cat /etc/passwd
```

Example entry:

```text
azam:x:1001:1001::/home/azam:/bin/bash
```

---

# 6. Understanding `/etc/passwd` Fields

Each line is divided into seven fields separated by colons (`:`).

Example:

```text
azam:x:1001:1001::/home/azam:/bin/bash
```

| Field | Value | Description |
|-------|------|-------------|
| Username | azam | Login name |
| Password Placeholder | x | Actual password is stored in `/etc/shadow` |
| UID | 1001 | User ID |
| GID | 1001 | Primary Group ID |
| Comment | *(empty)* | Full name or description |
| Home Directory | /home/azam | User's personal directory |
| Login Shell | /bin/bash | Default shell |

---

## Password Placeholder (`x`)

Modern Linux systems do **not** store passwords inside `/etc/passwd`.

Instead, the actual encrypted password is stored in:

```text
/etc/shadow
```

This improves security because `/etc/passwd` is readable by all users, while `/etc/shadow` is restricted.

---

# 7. Creating Users

Create a new user:

```bash
sudo useradd hasan
```

This creates the account but does **not** set a password.

---

## Create a User with a Comment

You can add a descriptive comment:

```bash
sudo useradd -c "Hasan Rahman" hasan
```

The comment is often used to store the user's full name.

---

# 8. The `/etc/shadow` File

The file:

```text
/etc/shadow
```

stores encrypted passwords and password aging information.

Only the root user can access it.

View it:

```bash
sudo cat /etc/shadow
```

Example:

```text
azam:$y$j9T$swPH1ValHz2H2g5/...:20641:0:99999:7:::
```

---

# 9. Understanding `/etc/shadow` Fields

Example:

```text
azam:$y$j9T$swPH1ValHz2H2g5/...:20641:0:99999:7:::
```

| Field | Description |
|--------|-------------|
| Username | User's login name |
| Encrypted Password | Securely hashed password |
| Last Password Change | Days since Unix Epoch (1 January 1970) |
| Minimum Password Age | Minimum days before changing password again |
| Maximum Password Age | Maximum password validity period |
| Warning Period | Days before password expiry to warn the user |
| Inactive Period | Days after password expiry before account becomes inactive |
| Account Expiration | Date when the account expires |
| Reserved | Reserved for future use |

---

## Password Aging Example

```
20641
```

This means the password was last changed **20,641 days after 1 January 1970 (Unix Epoch).**

---

## Warning Period

```
7
```

The user starts receiving password expiration warnings **7 days before the password expires**.

---

# 10. Setting and Changing Passwords

Assign or change a password:

```bash
sudo passwd hasan
```

Example output:

```text
New password:
Retype new password:
passwd: password updated successfully
```

---

# 11. Viewing User Information

Display user details:

```bash
id hasan
```

Example:

```text
uid=1001(hasan)
gid=1001(hasan)
groups=1001(hasan)
```

This command shows:

- UID
- GID
- Supplementary groups

---

# 12. Renaming a User

Rename an existing user:

```bash
sudo usermod -l hasan1 hasan
```

Explanation:

- `-l` → New login name
- `hasan1` → New username
- `hasan` → Current username

> Note: Renaming the user does **not** automatically rename the home directory. Use `usermod -d` and `-m` if you also want to move the home directory.

Example:

```bash
sudo usermod -d /home/hasan1 -m hasan1
```

---

# 13. Useful User Management Commands

## Display Current User

```bash
whoami
```

---

## Display Current User ID

```bash
id
```

---

## List Logged-in Users

```bash
who
```

or

```bash
w
```

---

## List All Users

```bash
cat /etc/passwd
```

---

## Check User Details

```bash
id username
```

---

## Lock a User Account

```bash
sudo passwd -l username
```

---

## Unlock a User Account

```bash
sudo passwd -u username
```

---

## Delete a User

Keep the home directory:

```bash
sudo userdel username
```

Delete the user and home directory:

```bash
sudo userdel -r username
```

---

# 14. Best Practices

- Avoid logging in directly as `root`; use a regular user with `sudo` instead.
- Use strong, unique passwords.
- Regularly review user accounts and remove unused ones.
- Lock inactive or temporary accounts when they are no longer needed.
- Grant the minimum permissions required for each user (principle of least privilege).
- Monitor `/etc/passwd` and `/etc/shadow` for unexpected changes.
- Keep sensitive files such as `/etc/shadow` accessible only to root.

---

# Summary

Linux is a multi-user operating system where every user has a unique identity, home directory, and permissions.

Key points:

- **Root User**: Full administrative privileges (UID 0).
- **System Users**: Used by services and applications.
- **Regular Users**: Human accounts for everyday tasks.
- **`/etc/passwd`**: Stores basic account information.
- **`/etc/shadow`**: Stores encrypted passwords and password aging information.
- **`useradd`**: Creates new users.
- **`passwd`**: Sets or changes passwords.
- **`id`**: Displays user and group information.
- **`usermod`**: Modifies user properties, including renaming accounts.

Proper user management is fundamental to maintaining a secure, organized, and well-administered Linux system.
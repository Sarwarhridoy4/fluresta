# Module 3: User and Group Administration (Part 2)

**Fluresta Cloud And Networking Institute (FCNI)**
📱 WhatsApp: +88 01553207425 · 🌐 fcni.com.bd

---

## Table of Contents

1. [Creating, Modifying, and Deleting Users](#1-creating-modifying-and-deleting-users)
2. [User Modification](#2-user-modification)
3. [Locking and Expiring Accounts](#3-locking-and-expiring-accounts)
4. [Group Administration](#4-group-administration)
5. [Granting Administrator (sudo) Access](#5-granting-administrator-sudo-access)
6. [Why Use `sudo`?](#6-why-use-sudo)
7. [Advantages of Being in the `sudo` Group](#7-advantages-of-being-in-the-sudo-group)
8. [Disadvantages / Risks of the `sudo` Group](#8-disadvantages--risks-of-the-sudo-group)
9. [Best Practices](#9-best-practices)

---

## 1. Creating, Modifying, and Deleting Users

### Basic User Creation

To create a new user, you can use either of the following commands:

```bash
sudo useradd rahat
```

or

```bash
sudo adduser rahat
```

> **Example Output:**
> ```
> ripon@CentOS:~$ sudo useradd rahat
> ripon@CentOS:~$ id rahat
> uid=1005(rahat) gid=1005(rahat) groups=1005(rahat)
> ```

### Setting a Password for the New User

```bash
sudo passwd rahat
```

> **Example Output:**
> ```
> ripon@CentOS:~$ sudo passwd rahat
> New password:
> BAD PASSWORD: The password is shorter than 8 characters
> Retype new password:
> passwd: password updated successfully
> ```

---

## 2. User Modification

| Command | Work / Description |
|---|---|
| `sudo usermod -c "rahat Islam" rahat` | Changes the user's full name (check in `/etc/passwd`) |
| `sudo usermod -s /bin/zsh rahat` | Changes the user's default shell — verify/change with `cat /etc/shells`, `echo $SHELL`, or `chsh -s /bin/zsh` |
| `sudo usermod -aG developers rahat` | Adds the user to a new group (`-a` means *append*, existing groups remain intact) |

> **Example (terminal output):**
> ```
> ripon@CentOS:~$ id rahat
> uid=1005(rahat) gid=1005(rahat) groups=1005(rahat)
> ripon@CentOS:~$ sudo usermod -aG developer rahat
> ripon@CentOS:~$ id rahat
> uid=1005(rahat) gid=1005(rahat) groups=1005(rahat),1007(developer)
> ```

> ⚠️ **Warning:** Always use `-aG`. Using only `-G` will remove all existing group memberships and replace them with only the new group.

---

## 3. Locking and Expiring Accounts

### Locking an Account

```bash
sudo usermod -L rahat
```

`usermod -L` actually locks the user's **password**. In this state, login with a password is not possible. However, if SSH key, Kerberos, or any other authentication method is active, login may still be possible through those methods.

To check the user's current status:

```bash
sudo passwd -S rahat
```

### Fully Locking an Account from All Methods

If you want to block the account from all authentication methods:

```bash
sudo usermod -s /sbin/nologin rahat
```

or

```bash
sudo usermod -s /bin/false rahat
```

### Restoring Login Access

```bash
sudo usermod -s /bin/bash rahat
```

### Locking via Account Expiry

```bash
sudo usermod -e 1 rahat
sudo usermod -e 2026-12-31 rahat
```

**To unlock (remove expiry):**

```bash
sudo usermod -e "" rahat
```

If no expiration date is provided to the `-e` option, the account's expiration date is removed and the account will no longer expire.

### Password Unlock

```bash
sudo usermod -U rahat
```

### Changing Username

```bash
sudo usermod -l newname oldname
```

> `-l` means *login name*.

### Changing Home Directory (with file move)

```bash
sudo usermod -d /home/newhome -m rahat
```

| Option | Meaning |
|---|---|
| `-d` | Specifies the new directory |
| `-m` | Moves all data from the old home directory to the new home directory |

> 💡 When using `-m` with `usermod -d`, if the new directory doesn't exist, `usermod` automatically creates it and moves the contents from the old home directory.

### Creating a User with Home Directory and Groups in One Step

```bash
sudo useradd -m -G sudo,developers -s /bin/bash rahat    # Debian (sudo group)
sudo useradd -m -G wheel,developers -s /bin/bash rahat   # RedHat (wheel group)
```

---

## 4. Group Administration

### Creating a Group

```bash
sudo groupadd developers1     # Verify with cat /etc/group
sudo groupadd developers2     # Verify with cat /etc/group
sudo groupadd -g 2000 developers1    # Create with a specific GID
```

### Adding a User to Groups

```bash
sudo usermod -aG developers1,developers2 rahat   # Add user to multiple groups
```

### Removing a User from a Group / Making a User Group Admin

```bash
sudo gpasswd -d rahat developers    # Remove user from group
sudo gpasswd -A rahat developers    # Make rahat a group admin
```

### Checking Group Information

```bash
getent group developers
cat /etc/group | grep developers
groups rahat                        # Check which groups rahat belongs to
```

### Deleting a Group

```bash
sudo groupdel developers
```

---

## 5. Granting Administrator (`sudo`) Access

No user can become root directly, but specific users can be granted Administrator permissions.

### On Debian-based OS

```bash
sudo usermod -aG sudo student01
sudo visudo
```

### On RedHat-based OS

```bash
sudo usermod -aG wheel student01
```

or

```bash
sudo visudo
```

---

## 6. Why Use `sudo`?

**`sudo` = Super User DO** — it allows a user to run a specific command with root privileges.

### Why use `sudo`?

Suppose you have 10 Linux administrators in your company. Would you give the root password to everyone's hand?

**No.**

Because someone might accidentally damage the server, and the root password could be compromised. So everyone gets their own user account, and when an administrator needs to perform administrative tasks, they use the `sudo` command.

---

## 7. Advantages of Being in the `sudo` Group

1. **No need to know the Root Password** — Users can perform administrative tasks using their own password.
   > Example: `sudo reboot`

2. **Reduced need for Root Login** — No need to log in directly as the Root user. This is a Linux Security Best Practice.

3. **Audit Logs are Maintained** — Who ran which command and when is recorded in the logs.
   > Examples:
   > ```bash
   > sudo cat /var/log/auth.log        # Debian
   > sudo journalctl | grep sudo       # RHEL / Rocky / AlmaLinux
   > sudo grep sudo /var/log/secure    # or
   > ```

4. **Separate Accounts, Clear Accountability** — Everyone has a separate account, so if something goes wrong, it's easy to see who did it. If everyone uses root, it's impossible to tell.

5. **Permission Control** — For example:
   - Student A can only restart services
   - Student B can only create users
   - Student C can run all commands

   These can all be controlled with `sudo`.

6. **Specific Commands Can Be Authorized**

   ```
   Cmnd_Alias SERVICES = /usr/bin/systemctl restart *
   student01 ALL=(ALL) SERVICES
   ```

   Here, `sudo systemctl restart ssh` will work, but `sudo rm -rf /` will not.

7. **Safe for Production Environments** — Google, Facebook, Amazon, Microsoft, and almost all Linux servers use `sudo` instead of Root Login.

---

## 8. Disadvantages / Risks of the `sudo` Group

1. **Gaining Full Administrator Capabilities** — If the rule is:

   ```
   %sudo ALL=(ALL:ALL) ALL
   ```

   Then the user can do almost everything root can do.

2. **Accidental Commands Can Cause Major Damage**

   ```bash
   sudo rm -rf /important-data
   sudo systemctl stop ssh
   sudo userdel -r admin
   ```

   These commands can cause major problems on the server.

3. **Malware Risk** — If a user's account is hacked and they are in the `sudo` group, the attacker will try to gain root privileges.

4. **Principle of Least Privilege** — An important security principle is to give only as much permission as needed. If a developer only needs to restart services, giving them full `sudo` is not advisable.

---

## 9. Best Practices

- ✅ Do not log in directly as root.
- ✅ Each administrator should have a separate user account.
- ✅ Use the `sudo` or `wheel` group.
- ✅ Whenever possible, do not grant full `sudo` — instead grant permission for specific commands (using `Cmnd_Alias` or specific command rules).
- ✅ Do not edit the `/etc/sudoers` file directly — use `visudo`.
- ✅ Or use the `/etc/sudoers.d/` directory.

---

<div align="center">

**Fluresta Cloud And Networking Institute (FCNI)**
📱 +88 01553207425 · 🌐 fcni.com.bd

</div>

## Class 01 - Linux System Administration Introduction & Linux Fundamentals

### Learning Outcomes

- Understand the role of an operating system and its core responsibilities including process, memory, filesystem, device, user, and network management
- Explain the historical development of UNIX, the birth of Linux by Linus Torvalds, and the relationship between the Linux kernel and GNU tools
- Differentiate between Linux distributions and identify major distribution families (Red Hat, Debian, Arch, SUSE, Gentoo, Slackware) along with their package formats and managers
- Describe the Red Hat ecosystem progression from Fedora to CentOS Stream to RHEL, and compare RHEL with CentOS Stream
- Identify use cases for embedded systems and virtualization, including differences between Type 1 and Type 2 hypervisors

### Summary

This class introduces Linux as a powerful, open-source operating system built around the Linux kernel and commonly paired with GNU tools. It covers the history of UNIX and Linux, the GNU Project's contribution, and the distinction between the kernel and a complete distribution. Students learn about major Linux families, their package formats and managers, the Red Hat ecosystem, embedded systems, and virtualization basics including Type 1 and Type 2 hypervisors.

---

## Class 02 - Linux Shell & Basic Text Processing

### Learning Outcomes

- Understand the role of the Linux shell as a command-line interpreter bridging users and the Linux kernel
- Identify and compare popular shells including Bash, Zsh, Fish, Korn Shell, and Csh/Tcsh
- Switch between shells temporarily and permanently using commands like `chsh`, and apply shell changes without rebooting
- Create, display, and delete temporary and persistent environment variables using `export` and shell configuration files like `.bashrc`
- Use essential text-processing commands (`cat`, `echo`, `head`, `tail`, `less`, `grep`, `wc`) and understand their practical applications including log monitoring with `tail -f`

### Summary

This class covers the Linux shell as the interface between users and the kernel, exploring popular shells and how to manage shell environments. Students learn to install and switch between shells, manage environment variables, and master essential text-processing tools like `cat`, `grep`, `wc`, `head`, `tail`, and `less`. The class also introduces the EPEL repository for additional Enterprise Linux packages.

---

## Class 03 - Linux User and Group Administration

### Learning Outcomes

- Understand Linux as a multi-user operating system and identify the three types of users: root, system users, and regular users
- Interpret the fields in `/etc/passwd` and `/etc/shadow` files, including UID, GID, home directory, login shell, and password aging information
- Create new user accounts using `useradd`, set and change passwords with `passwd`, and view user information using `id`
- Rename users with `usermod`, and perform user account management tasks including locking, unlocking, and deleting users
- Apply security best practices such as avoiding direct root login, using strong passwords, and following the principle of least privilege

### Summary

This class focuses on Linux user and group administration, covering the three user types (root, system, regular) and their UID/GID ranges. Students learn to read and interpret `/etc/passwd` and `/etc/shadow`, create and manage user accounts with `useradd`, `passwd`, and `usermod`, and view user details with `id`. The class emphasizes security best practices including the principle of least privilege and proper use of `sudo`.

---

## Class 04 - SSH Complete Study Notes

### Learning Outcomes

- Understand SSH as a secure network protocol for remote login, command execution, file transfer, port forwarding, and Git authentication
- Install and manage the OpenSSH server on both Debian/Ubuntu and RHEL/Rocky/AlmaLinux systems using `systemctl`
- Generate SSH key pairs using `ssh-keygen` with the Ed25519 algorithm, and upload public keys to servers using `ssh-copy-id`
- Configure passwordless SSH login using `~/.ssh/config` with host aliases, identity files, and keepalive settings
- Apply SSH security best practices including using Ed25519 keys, protecting private keys with passphrases, disabling password authentication, and restricting root login

### Summary

This class provides a comprehensive study of SSH (Secure Shell) as a secure alternative to Telnet for remote server access. Students learn to install OpenSSH server, generate and deploy SSH key pairs for passwordless authentication, configure SSH client settings with host aliases, and implement security best practices. The class also covers Windows SSH setup and cross-platform key management.

---

## Class 04 - SSH (Secure Shell) — Updated

### Learning Outcomes

- Understand SSH as an encrypted network protocol and compare it with unencrypted alternatives like Telnet
- Install and configure the OpenSSH server on both Debian-based and Red Hat-based systems, and verify the service status with `systemctl`
- Set up SSH key-based authentication using `ssh-keygen` and `ssh-copy-id`, and configure passwordless login via `~/.ssh/config` aliases
- Customize the SSH port by editing `/etc/ssh/sshd_config`, validate the configuration with `sshd -t`, and configure UFW firewall rules to secure the new port
- Apply SSH security hardening practices including the use of Ed25519 keys, `IdentitiesOnly yes`, keepalive settings, and UFW firewall configuration

### Summary

This updated class covers SSH fundamentals, secure key-based authentication setup, and advanced server hardening. Students learn to generate SSH keys, configure passwordless login with custom host aliases, and customize the default SSH port on Ubuntu Server using UFW. The class also provides a reference for the Linux directory structure and emphasizes cross-platform SSH usage including Windows clients.

---

## Class 05 - User and Group Administration (Part-02)

### Learning Outcomes

- Modify existing user accounts using `usermod` to change full names, login shells, group memberships, home directories, and usernames
- Manage user account security and expiration using `usermod -L`, `usermod -U`, `usermod -e`, and `usermod -s /sbin/nologin`
- Create and administer groups using `groupadd`, `gpasswd`, and `getent`, including setting group administrators and managing GIDs
- Configure sudo privileges by adding users to the `sudo` or `wheel` group and managing policies with `visudo`
- Apply sudo security best practices including the principle of least privilege, specific command authorization with `Cmnd_Alias`, and using `/etc/sudoers.d/` instead of editing `/etc/sudoers` directly

### Summary

This class covers advanced user and group administration tasks including modifying existing user accounts with `usermod` for attributes like full name, shell, and group membership, as well as account locking and expiration management. Students learn group administration commands (`groupadd`, `gpasswd`, `getent`) and how to configure sudo access for administrators on both Debian and Red Hat-based systems. The class emphasizes sudo security best practices including the principle of least privilege, fine-grained command authorization using `Cmnd_Alias`, and proper sudoers file management with `visudo`.

---

## Class 06 - User and Group Administration (Part-02)

### Learning Outcomes

- Modify existing user accounts using `usermod` to change full names, login shells, group memberships, home directories, and usernames
- Manage user account security and expiration using `usermod -L`, `usermod -U`, `usermod -e`, and `usermod -s /sbin/nologin`
- Create and administer groups using `groupadd`, `gpasswd`, and `getent`, including setting group administrators and managing GIDs
- Configure sudo privileges by adding users to the `sudo` or `wheel` group and managing policies with `visudo`
- Apply sudo security best practices including the principle of least privilege, specific command authorization with `Cmnd_Alias`, and using `/etc/sudoers.d/` instead of editing `/etc/sudoers` directly

### Summary

This class covers advanced user and group administration tasks including modifying existing user accounts with `usermod` for attributes like full name, shell, and group membership, as well as account locking and expiration management. Students learn group administration commands (`groupadd`, `gpasswd`, `getent`) and how to configure sudo access for administrators on both Debian and Red Hat-based systems. The class emphasizes sudo security best practices including the principle of least privilege, fine-grained command authorization using `Cmnd_Alias`, and proper sudoers file management with `visudo`.

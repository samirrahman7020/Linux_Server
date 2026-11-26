### <h1 style="color: #3498db;">Linux Server Project Overview</h1>
> [!IMPORTANT]
> * This file will be used to document the changes, projects and features that are present in this server.

## 1. 20/11/2026

 * This document tracks the configuration and security that has been implemented into the server. In this section of the project, I learned how to install and manage security through a variety of features.

# Initial Setup
**Status:** <span style="color:green"> Complete</span>

 - [x] Ubuntu Server Installation : Installed Ubuntu 26.04.1 LTS 
 - [x] Package Updates : Updated and Upgraded packages within my Server by creating a custom alias. This reduced the time to update packages as only one command is now required
 - [x] SSH Installation : Installed the OpenSSH (sshd) server, allowing remote access.

![Server Info](./Images/Setup_and_Security/server_info.png "Server Info")

## 2. 24/11/2026

# Security
**Status:** <span style="color:green"> Complete</span>
 
 *  Security was a priority when configuring this server. Linux servers can be targeted by automated bots which may try to gain unauthorised access through repeated login attempts. Although having a strong password is a counter measure, other precautions should be put in place.

2.1 SSH Key Authentication
SSH Keys were used to restrict access to unauthorised users. This ensures secure remote access.
 - [x] Generate an Ed25519 key using:
```bash
       ssh-keygen -t ed25519
```
 - [x] Transfer the public key using:
```bash
       ssh-copy-id username@server_address
 ```
 - [x] Confirm the public key is stored in:
```bash
       ~/.ssh/authorized_keys
```

2.2 SSH Configuration
For extra security measures, the following settings were configured:
Within 
```bash
       /etc/ssh/sshd_config
```
Set:
 - [x] PasswordAuthentication no
 - [x] PermitRootLogin no

This was done to stop bots or attackers trying to log in as Root and ensures greater security by disabling passwords completely.
Run:
```bash
sudo systemctl restart ssh
```
to save the changes
> [!NOTE]
> This is more secure as it blocks brute force attacks AND protects against weak passwords.

2.3 User Privilege

- [x] An admin user was configured with sudo privileges:
```bash
sudo adduser username
sudo usermod -aG sudo username
```
> [!TIP]
> It is safer to grant sudo privileges instead of using the root user through "su". This will limit any damage and allows for accountability; sudo logs which user ran which command.

2.4 Firewall Configuration
UFW was used within the server to control network traffic.

- [x] Allow OpenSSH
```bash
sudo ufw allow OpenSSH
```
- [x] Enable ufw
```bash
sudo ufw enable
```
- [x] Check ufw status
```bash
sudo ufw status verbose
```
> [!WARNING]
> Although this ensures security by limiting which ports can be accessed, ensure any other services that require additional ports are configured. Furthermore, be cautious with the commands used which could lead to self-lockout hazards.

2.5 Port Inspection

Using the following command, I was able to identify any open ports. Unnecessary services can be disabled to reduce the risk of attackers.

- [x] Check open ports using socket statistics:
```bash
sudo ss -tulpn
```
> [!Note] This command was used over netstat as it is simpler and faster
 - [x] Disable a service using the relevant command
```bash
   sudo systemctl disable --now service_name
```

2.6 Login Monitoring + Intrusion Prevention

- [x] List active users and failed login attempts using commands:
```bash
who
sudo lastb
```

Using this info, Fail2Ban was installed to help prevent against repeated failed attempts.
 - [x] Installation and Status:
```bash
sudo apt install fail2ban
sudo fail2ban-client status sshd
```
> [!TIP]
> Fail2Ban is a very useful tool to have on a server. It monitors server log files and automatically blocks suspicious IP addresses after repeated failed login attempts using firewall rules. This helps prevent attackers from continuously attempting to gain unauthorised access to the server.

2.7 Automatic Security Updates

- [x] Install unattended upgrades:
```bash
sudo apt install unattended-upgrades
```

This ensures security updates are automatically installed, ensuring the server is up to date.

2.8 System and Kernel Maintenance

A custom alias was created called "package_update" it runs the commands below. This was done to simplify package maintenance.

- [x] Create a custom alias to simplify the process:
```bash
sudo apt update
sudo apt upgrade
```
- [x] Update the kernel and reboot:
* Firstly check the kernel version
```bash
   uname -r
```
* Install the updates and perform a reboot
```bash
sudo apt update && sudo apt full-upgrade
sudo reboot
```
You can then verify if the new kernel version has been installed using ``` uname -r ``` again.






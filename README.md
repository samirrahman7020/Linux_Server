<h1> 🖥️ Linux Server Project </h1>

## 📌 Summary
This project involves building and configuring a Linux server using Ubuntu Server, with the aim of developing practical skills in Linux system administration, networking and server security. 

To build this server, an old laptop was installed with the Ubuntu Server Operating system.

The goal is to build a secure and remotely accessible server that can be managed over a network, host services and eventually provide network file sharing between devices.

Throughout this project, I have been developing my understanding of Linux, server administration, network configuration and security by applying these concepts in a practical environment.

>[!IMPORTANT]
> This project is currently in progress and will be updated with further additions and technologies.

## 🛠️ Features 
> [!NOTE]
> | Feature  | Description |
> | ------------- | ------------- |
> | 🐧 Ubuntu Server | Installed and configured Ubuntu Server 26.04.1 LTS |
> | 🔑 SSH Access | Configured remote server access using OpenSSH and Ed25519 SSH keys |
> | 🔒 SSH Hardening | Disabled password authentication and root login within SSH configuration |
> | 🛡️ UFW Firewall | Configured firewall rules to allow SSH connections and block external ports |
> | 🚨 Fail2Ban | Installed Fail2Ban to help protect against repeated failed login attempts and to block suspicious IP's |
> | 🔄 Automatic Updates and Kernel Maintenance | Enabled unattended security updates to keep the server protected and created custom aliases to streamline Linux processes |

## ⚠️ Challenges
>[!WARNING]
> ### 20/11/2026
> The server currently uses WIFI due to no access to an ethernet port. However, when trying to connect to the wireless interface, several issues occurred:
> * The wireless interface wasn't recognised
> * The Netplan configuration was incorrect
>
> Fixing this required me to:
> - [x] Display all network interfaces and locate the wireless interface:
> ```bash
> ip link show  
> ```
> - [x] Locate the correct configuration file and edit it:
> ```bash
> cd /etc/netplan/file_path.yaml
> ls
> ```
> - [x] Change the permissions of the configuration file to ensure security:
> ```bash
> sudo chmod 600 "file_path.yaml"
> ```
> - [x] Use the new configuration and check its status:
> ```bash
> sudo netplan generate
> sudo netplan try
> ```
> If there are no errors run:
> ```bash
> sudo netplay apply
> ```

## 📚 What I Learned
> [!TIP]
> ### 20/11/2026
>  - How Ubuntu Server manages network configuration using NetPlan
>  - How to configure a wireless interface
> - How to troubleshoot network connectivity using Linux Commands


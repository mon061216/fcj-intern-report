---
title: "Week 2 Worklog"
date: 2026-09-28
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:
- Master the Linux Command Line Interface (CLI) – the operating foundation for over 90% of cloud servers today.
- Understand how to manage processes, background services, system permissions, and network configurations (IP, Port, Firewall, SSH) to run an application on a remote server.

### Tasks to Implement This Week:
| Day | Task | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Mon | - Compared core differences between Windows Server and Linux (kernel architecture, command-line interface, permission mechanisms, performance, and licensing costs) <br> - Learned the concepts of **Terminal**, **Shell** (Bash/Zsh), and the standard Linux Filesystem Hierarchy Standard (FHS) (`/etc` for configuration files, `/var/log` for logs, `/home` for user data, `/usr/bin` for user binaries/programs) | 28/09/2026 | 28/09/2026 | Linux Journey |
| Tue | - **Hands-on CLI Practice:** <br>&emsp; + Directory and file management: `ls -la`, `cd`, `pwd`, `mkdir -p`, `cp -r`, `mv`, `rm -rf` <br>&emsp; + Reading and filtering file contents: `cat`, `less`, `head`, `tail -f`, `grep` <br>&emsp; + Managing file and directory permissions with `chmod` (numeric modes like `755`, `644`, `400` and symbolic modes like `u+x`) and changing ownership with `chown` | 29/09/2026 | 29/09/2026 | Ubuntu Documentation |
| Wed | - Distinguished between a **Program** (executable file stored on disk), a **Process** (running instance loaded into RAM with a unique PID), and a **Service** (background process managed by `systemd`) <br> - Practiced inspecting system resources with `ps aux`, `top`/`htop`, `kill -9`, and managing services via `systemctl status/start/stop/enable` <br> - Distinguished between **Foreground** execution (occupies the terminal, prints logs directly) and **Background** execution (runs silently, writes logs to files or `journalctl`) | 30/09/2026 | 30/09/2026 | Linux Journey |
| Thu | - Researched server networking architecture: <br>&emsp; + Differences between **Public IP** (routable over the Internet) and **Private IP** (internal network ranges per RFC 1918 such as `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`) <br>&emsp; + Calculating the number of usable IP addresses from **CIDR** notation (e.g., `/16`, `/24`), and understanding the roles of **Subnets** and **Default Gateways** <br>&emsp; + Packet filtering mechanisms of **Firewalls** (`ufw` / `iptables`) based on source IP, protocol (TCP/UDP), and destination Port | 01/10/2026 | 01/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Fri | - Studied the asymmetric encryption mechanism of the **SSH** protocol (Port 22) using a **Public Key** (stored on the server at `~/.ssh/authorized_keys`) and a **Private Key** (kept secret on the client machine) <br> - **Hands-on Practice:** Generated an RSA/Ed25519 key pair using `ssh-keygen`, set `chmod 400` permissions on the Private Key, and successfully established an SSH connection to a Linux virtual machine | 02/10/2026 | 02/10/2026 | Hands-on Practice |

### Week 2 Achievements:
- Mastered essential Linux commands for file administration, error log inspection, and server security permissions.
- Understood the full lifecycle of an application on Linux: from manual execution as a Process to packaging it as a Service that automatically recovers upon server reboot.
- Grasped the prerequisites for a client to connect to an application on a server: the server must have a Public IP, the application must listen on the correct Port, and the Firewall must allow traffic (Inbound Rule) for that Port.

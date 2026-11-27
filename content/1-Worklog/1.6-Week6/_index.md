---
title: "Week 6 Worklog"
date: 2026-10-26
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:
- Master the build, packaging (publish), and deployment process of a production **ASP.NET Core Web API** to a Linux server on AWS.
- Configure the application to run reliably as a Linux `systemd` service and expose API documentation (Swagger UI) over the Internet.

### Tasks to Implement This Week:
| Day | Task | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Mon | - Built a basic **Todo API** using ASP.NET Core (implementing `GET`, `POST`, `PUT`, `DELETE` endpoints and Swagger UI) <br> - Tested the API locally and ran `dotnet publish -c Release -o ./publish` to generate optimized production binaries | 26/10/2026 | 26/10/2026 | Microsoft .NET Docs |
| Tue | - Launched a new **Ubuntu EC2 instance** on AWS and connected via SSH <br> - Installed the matching **ASP.NET Core Runtime** on Ubuntu and verified installation via `dotnet --info` | 27/10/2026 | 27/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Wed | - Transferred the `./publish` directory from local machine to `/var/www/todoapi` on EC2 using `scp` <br> - Ran the application in the **foreground** (`dotnet TodoApi.dll --urls "http://0.0.0.0:5000"`) to inspect startup logs and detect missing dependencies | 28/10/2026 | 28/10/2026 | Personal Practice |
| Thu | - Created a service definition file at `/etc/systemd/system/todoapi.service` configuring `WorkingDirectory`, `ExecStart`, `Restart=always`, and `User=www-data` <br> - Activated and started the service with `sudo systemctl daemon-reload`, `enable`, and `start todoapi` for persistent background execution | 29/10/2026 | 29/10/2026 | Linux Systemd Docs |
| Fri | - Updated the EC2 **Security Group** to allow inbound traffic on custom TCP port 5000 <br> - Navigated to `http://<EC2-Public-IP>:5000/swagger` in a web browser and successfully tested create/read/delete API requests | 30/10/2026 | 30/10/2026 | Personal Practice |

### Week 6 Key Outcomes:
- Successfully deployed an ASP.NET Core Web API from local development to production on AWS EC2.
- Ensured process resilience and automated recovery on server reboot via `systemd` service management.
- Understood network troubleshooting between application listening interfaces (`0.0.0.0` vs. `localhost`) and AWS Security Group inbound filtering.

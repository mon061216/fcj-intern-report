---
title: "Week 8 Worklog"
date: 2026-11-09
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:
- Master containerization with **Docker** to eliminate environment discrepancies between development and production environments.
- Package the ASP.NET Core Web API into an optimized Docker Image and run containerized workloads on AWS EC2.

### Tasks to Implement This Week:
| Day | Task | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Mon | - Studied Docker architecture: distinguishing static layered blueprints (**Docker Images**) from active running instances (**Docker Containers**), and the role of the Docker Daemon and Registry | 09/11/2026 | 09/11/2026 | Docker Documentation |
| Tue | - Authored a multi-stage `Dockerfile` (using `mcr.microsoft.com/dotnet/sdk` for compilation and copying artifacts to a lean `mcr.microsoft.com/dotnet/aspnet` runtime image) <br> - Executed `docker build -t todo-api:v1 .` and tested container execution locally via `docker run` | 10/11/2026 | 10/11/2026 | Microsoft .NET Docker Docs |
| Wed | - Practiced core container management techniques: **Port mapping** (`-p 8080:8080`), persistent data storage (**Volumes** `-v`), and sensitive configuration injection via **Environment Variables** (`-e` or `--env-file`) | 11/11/2026 | 11/11/2026 | Docker Documentation |
| Thu | - Created a `docker-compose.yml` file to declare services, isolated bridge networks, restart policies (`restart: unless-stopped`), and environment parameters connecting to RDS and S3 | 12/11/2026 | 12/11/2026 | Docker Compose Docs |
| Fri | - Installed Docker Engine and Docker Compose plugin on the **Ubuntu EC2 instance** <br> - Deployed the containerized application using `docker compose up -d`, verified operational logs with `docker logs -f`, and confirmed healthy API availability | 13/11/2026 | 13/11/2026 | Personal Practice |

### Week 8 Key Outcomes:
- Mastered writing production-ready `Dockerfile` specifications with minimal image footprints using multi-stage builds.
- Modernized the backend deployment workflow on EC2 to containerization, enabling rolling updates and fast failure recovery with a single command.

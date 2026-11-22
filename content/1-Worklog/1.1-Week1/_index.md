---
title: "Week 1 Worklog"
date: 2026-09-21
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Week 1 Objectives:
- Connect and get acquainted with team members in the First Cloud AI Journey (FCAJ) internship program, and understand the rules and progress reporting procedures.
- Gain a deep understanding of web network communication: how the Client sends requests, how the Backend processes logic, communicates with the Database, and returns responses via HTTP/HTTPS protocols.

### Tasks to Implement This Week:
| Day | Task | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Mon | - Attended the Onboarding session starting September 20, getting to know the mentor and team members <br> - Carefully reviewed internship regulations, how to write worklogs on the Hugo platform, and source code management rules on GitHub | 21/09/2026 | 21/09/2026 | FCAJ Internal Documentation |
| Tue | - Analyzed the 3-tier architecture: Frontend (Presentation), Backend (Business Logic), and Database (Data Storage) <br> - Studied the detailed structure of an **HTTP Request** (Request Line, Headers, Body) and **HTTP Response** (Status Line, Headers, Body) <br> - Researched the **JSON** data structure (Key-Value, Array, Nested Object) used for data exchange between services | 22/09/2026 | 22/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Wed | - Studied **RESTful API** design standards and resource-based URL **Endpoint** naming conventions <br> - Clearly distinguished the semantics and idempotency of HTTP Methods: `GET` (retrieve), `POST` (create), `PUT` (full update), `PATCH` (partial update), `DELETE` (delete) <br> - Systematized **HTTP Status Code** groups: `2xx` (`200 OK`, `201 Created`, `204 No Content`), `4xx` (`400 Bad Request`, `401 Unauthorized`, `403 Forbidden`, `404 Not Found`), `5xx` (`500 Internal Server Error`, `502 Bad Gateway`) <br> - Explored content negotiation mechanisms using the `Content-Type` and `Accept` header pair | 23/09/2026 | 23/09/2026 | MDN Web Docs |
| Thu | - Distinguished between **IP Address** (device identifier on a network), **Domain Name** (human-friendly name resolved via DNS), **Port** (application process identifier), and the local loopback address `localhost` (`127.0.0.1`) <br> - Compared the differences between **HTTP** (plaintext transmission, port 80) and **HTTPS** (encrypted transmission using SSL/TLS certificates, port 443) | 24/09/2026 | 24/09/2026 | MDN Web Docs |
| Fri | - Studied the **12-Factor App** security principle of separating configuration from source code using **Environment Variables** <br> - **Hands-on Practice:** Used Postman and the `curl` CLI tool to send CRUD requests to a sample REST API, inspected Request/Response Headers and JSON Payloads in detail, and drew a data flow diagram from the browser down to the Database | 25/09/2026 | 25/09/2026 | Hands-on Practice |

### Week 1 Achievements:
- Integrated smoothly into the FCAJ working environment, mastering the 12-week roadmap and technical documentation standards.
- Thoroughly explained the lifecycle of a data packet: from a user clicking a button on the Frontend -> DNS resolving the domain to an IP -> opening an HTTPS connection to the Backend Port -> Backend reading environment variables to connect to the Database -> querying data and packaging a JSON response with the corresponding Status Code.
- Proficiently used Postman and `curl` to test APIs and debug errors based on HTTP status codes.

# API TESTING & INTEGRATION QA (Postman & Newman)

## Overview
This portfolio suite models a complete end-to-end API testing progression, transitioning from basic UI assertions in Postman to automated CLI execution, custom reporting, and continuous delivery pipelines.

## Projects Overview
- **Project 1: Functional Assertions & Schema Basics (UI Desktop)**  
  *Focus:* Implementing foundational API assertions in Postman, validating HTTP status codes (`200 OK`), response headers (`Content-Type`), and validating JSON payload data structures.
- **Project 2: Dynamic Environment Variables & Data Pass (UI Desktop)**  
  *Focus:* Dynamic request chaining and data persistence across requests, extracting generated IDs via JavaScript scripts (`pm.environment.set`) and passing them to downstream endpoints.
- **Project 3: Headless Execution & HTML Reporting via Newman CLI**  
  *Focus:* Decoupling collection execution from the Postman desktop app, running automated CLI suites using Newman in PowerShell, and generating HTML execution reports (`htmlextra`).
- **Project 4: Automated Execution Script & CI/CD Pipeline (PowerShell & GitHub Actions)**  
  *Focus:* Automating local suite execution via a custom PowerShell script (`run-tests.ps1`) to streamline headless runs, generate custom-titled HTML audit dashboards, and integrate continuous testing via GitHub Actions (`api-tests.yml`).

---

## Suite Projects
- [Project 1: Functional Assertions & Schema Basics (UI Desktop)](./PROJECT_1.md)
- [Project 2: Dynamic Environment Variables & Data Pass (UI Desktop)](./PROJECT_2.md)
- [Project 3: Headless Execution & HTML Reporting via Newman CLI](./PROJECT_3.md)
- [Project 4: Automated Execution Script & CI/CD Pipeline (PowerShell & GitHub Actions)](./PROJECT_4.md)

---

## Executive Summary: End-to-End API Testing Architecture
The development of these four projects establishes an automated testing architecture for REST APIs and web services, transitioning seamlessly from functional UI validation to headless continuous integration:

- **Functional Validation & Contract Integrity (Project 1):** Implementation of assertions for HTTP status codes, response times, security headers, and dynamic payload schemas to ensure architectural consistency.
- **State Persistence & Dynamic Workflows (Project 2):** Utilization of post-response scripts to capture environment variables dynamically, enabling hands-free endpoint chaining (POST $\rightarrow$ GET).
- **Headless Execution & Reporting (Project 3):** Decoupling test execution from the desktop UI using Newman CLI, facilitating isolated collection runs and generating interactive HTML audit dashboards via `htmlextra`.
- **Local Orchestration & CI/CD Pipelines (Project 4):** Standardization of test execution through a custom PowerShell script (`run-tests.ps1`) for local environments, fully integrated with GitHub Actions (`.github/workflows/api-tests.yml`) for automated artifact delivery across build cycles.

With this ecosystem, the suite is fully prepared for integration into QA/SecOps pipelines, serving as a robust foundation for regression testing, security audits, and API vulnerability assessments.

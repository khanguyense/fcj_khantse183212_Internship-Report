---
title: "Week 11 Worklog"
date: "2025-11-21"
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---
### Week 11 Objectives:

* Complete the remaining FE interface together with the Frontend team.
* Coordinate end-to-end testing between FE and BE.
* Learn the overall deployment workflow of the system (API, FE, database, infrastructure) to gain general understanding, even if not directly responsible.
* Prepare the necessary notes for Week 12 (documentation & final summary).


### Tasks to be carried out this week:
| Day | Task                                                                                                                                                        | Start Date | End Date   | Reference Materials |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | ---------- | ------------------- |
| 2   | - Work with the FE team to complete the remaining UI components <br> - Review API contract alignment between FE and BE                                      | 17/11/2025 | 17/11/2025 |                     |
| 3   | - FE integrates full CRUD API flows <br> - Fix schema, payload, and status code mismatches during FE testing                                                | 18/11/2025 | 18/11/2025 |                     |
| 4   | - Perform full end-to-end testing: List -> Create -> Update -> Delete from FE to BE <br> - Update response models/validations to match FE expectations      | 19/11/2025 | 19/11/2025 | < >                 |
| 5   | - Learn the team’s deployment workflow (CI/CD, API Gateway, Lambda, S3 + CloudFront) <br> - Take notes for Week 12 documentation                            | 20/11/2025 | 20/11/2025 |                     |
| 6   | - Summarize FE and BE issues during the week <br> - Review the entire BE codebase to prepare for deployment environment (even though not the one deploying) | 21/11/2025 | 21/11/2025 |                     |


### Week 11 Achievements:

* Overview:
  * This week, I mainly collaborated with the FE team to finalize UI components and complete API integration. Since the backend was completed in Week 10, I helped fix issues, standardize API contracts, and conduct full end-to-end testing.  
    Additionally, I learned the team’s deployment workflow (Lambda, API Gateway, S3/CloudFront, CI/CD) to prepare documentation for Week 12.

* Theoretical knowledge acquired:
  * How FE calls CRUD APIs and debugs requests.
  * API Contract: input/output schemas, error formats, status codes.
  * Deployment workflow: .NET -> Lambda, API Gateway routing, FE build -> S3/CloudFront.
  * Overview of CI/CD pipeline and how to prepare code for deployment (configs, logging).

* Practical work / Deliverables:
  * Collaborated with FE to complete List/Create/Update/Delete screens.
  * Adjusted backend according to FE requirements (schema, validation, status codes).
  * Conducted full end-to-end testing between FE ↔ BE on local environment.
  * Documented deployment workflow for use in Week 12.
  * Compiled FE and BE issues and updated the team backlog.

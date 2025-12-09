---
title: "Week 10 Worklog"
date: "2025-11-14"
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---
### Week 10 Objectives:

* Complete 100% of the Backend CRUD using .NET running on Aspire AppHost.
* Build and test the DynamoDB data model on the local environment (Docker).
* Integrate DynamoDB Local with NoSQL Workbench to validate the data model.
* Collaborate with the FE team to complete the basic UI and connect to local APIs.
* Prepare a solid foundation before moving into Week 11 (migrating code to Lambda + API Gateway).


### Tasks to be carried out this week:
| Day | Task                                                                                                                                                     | Start Date | End Date   | Reference Materials |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | ---------- | ------------------- |
| 2   | - Verify & reinstall BE environment: .NET SDK, Docker Desktop, NoSQL Workbench <br> - Understand system architecture diagram and backend processing flow | 10/11/2025 | 10/11/2025 |                     |
| 3   | - Set up DynamoDB Local using Docker <br> - Connect & visualize via NoSQL Workbench, manually test CRUD operations                                       | 11/11/2025 | 11/11/2025 |                     |
| 4   | - Implement DAL/Repository using .NET + AWSSDK.DynamoDBv2 <br> - Integrate DI into Aspire AppHost <br> - Implement business logic in BLL                 | 12/11/2025 | 12/11/2025 |                     |
| 5   | - Build CRUD API Controllers <br> - Perform unit tests & integration tests in the local environment                                                      | 13/11/2025 | 13/11/2025 |                     |
| 6   | - Collaborate with the FE team <br> - Build basic UI (List/Create) <br> - FE connects to Local API and performs end-to-end testing                       | 14/11/2025 | 14/11/2025 |                     |


### Week 10 Achievements:

* Overview:
  * This week, I completed the entire backend running locally using Aspire AppHost, built the DynamoDB data model, tested CRUD operations, and integrated with the frontend. By ensuring a complete and stable local architecture and codebase, I established a strong foundation for transitioning to Lambda/API Gateway in Week 11.

* Theoretical knowledge acquired:
  * DynamoDB data modeling based on Single-Table Design, Access Patterns, PK/SK.
  * Knowledge about DynamoDB Local, NoSQL Workbench, Docker setup.
  * Using AWSSDK.DynamoDBv2 in .NET and integrating Dependency Injection.
  * Backend structure in ASP.NET (Controller -> BLL -> Repository).
  * How FE calls local APIs, handles responses, and renders UI.

* Practical work / Deliverables:
  * Set up DynamoDB Local using Docker and managed schema via NoSQL Workbench.
  * Built Repository + BLL + Controllers using .NET 8 / Aspire AppHost.
  * Completed 5–6 CRUD APIs (POST/GET/PUT/DELETE/List).
  * Wrote unit tests for BLL and integration tests for API.
  * FE team built List + Create UI and successfully tested with local API.

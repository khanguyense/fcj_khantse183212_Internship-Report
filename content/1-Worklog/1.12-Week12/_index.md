---
title: "Worklog"
date: "2025-12-09"
weight: 12
chapter: false
pre: " <b> 12. </b> "
---

*# Week 12 Worklog

## Week 12 Objectives
- Master the deployment process of AWS infrastructure using CDK and understand the relationships between stacks (VPC, RDS, Lambda, S3, API Gateway).
- Complete the backend logic for the admin module, including data processing, analytics, and the archiving mechanism from RDS → S3.
- Optimize the system structure, refactor backend and dashboard code toward a clean business-layer separation – easy to maintain – easy to scale.
- Research and implement improvements for more efficient data processing (checksum, data load limitation, optimized synchronization logic).
- Become proficient in managing AWS resources through CLI and Console, and ensure multiple deployments can run without conflicts.

## Tasks to be carried out this week

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | ---------------- | ------------------ |
| 2 | Refactor the deployment process and comment out unused analytics components.<br>Adjust `app.py` to always deploy VPC, RDS, and DB Init Stack; enable `DashboardStack` with correct dependencies.<br>Comment out all Glue, archive, and analytics resources (Lambda/EventBridge + API) in `dashboard_stack.py`.<br>Reduce RDS instance size (SMALL → MICRO) and set storage = 20GB. | 24/11/2025 | 24/11/2025 |  |
| 3 | Begin deployment of `AppStack`, `DashboardStack`, and `DBInitStack` to support the admin backend.<br>Fix errors caused by setting max AZ = 1 when creating RDS (AWS requires minimum 2 AZ). Although 2 AZ are created, Multi-AZ mode is **not** enabled, only an additional subnet – so no additional cost.<br>Refactor API: handle string body returned from API Gateway, update endpoint paths, improve logging.<br>Update CDK: use correct secret for Lambda, update VPC/subnets, add HTTPS SG rule, comment out unused Bedrock endpoint.<br>Update asset bundling (use `cp -r` instead of `cp -au`).<br>Reorganize the admin business flow: manage appointments, assign consultants to timeslots, and generate daily appointment summaries.<br>Admin uploads SQL file → `ArchiveData` stores it in S3 → future deployments will load from S3 instead of requiring re-upload.<br>Future direction: allow Lambda `index.py` to read schema during deployment and load data from S3 – feasible.<br>Long-term direction: migrate all on-premise data to S3; Lambda will push initial data into RDS upon first deployment; new data updates will be handled by `ArchiveData`. | 25/11/2025 | 25/11/2025 |  |
| 4 | Hardcode schema in `index.py` and remove schema files from the project folder.<br>Process new data and save CSV for future Athena DDL usage.<br>Add dashboard overview API and UI; refactor admin database logic.<br>Add APIs for summary statistics: general overview, customers, consultants, appointments, community programs; update dashboard UI to display these metrics.<br>Refactor `DatabasePage`: remove raw SQL execution feature, focus on schema + analytics.<br>Update CDK + IAM roles for new S3 bucket and proper permissions.<br>Move all admin dashboard business logic to a dedicated service class (`code/services/admin.py`).<br>Rename `AdminStack` → `FrontendStack` to reflect correct responsibility; update all references. | 26/11/2025 | 26/11/2025 |  |
| 5 | Meeting with team to design strategy for loading data from S3 to RDS whenever RDS is started.<br>Requirement: avoid loading the entire dataset every time. Dynamic data (appointments, work schedules) changes frequently → cannot reload everything.<br>Solution: limit the amount of data loaded. Static data (consultant info) should be fully loaded. Dynamic time-based data (appointments) should be conditionally loaded, e.g., load data for the date range relevant to admin operations.<br>Current approach: load data within ±1 day of the current date.<br>Update `vpc_stack` to import the manually created S3 bucket from CLI.<br>CLI command:<br>`aws s3 mb s3://meetassist-data-<account-id>-ap-southeast-1 --region ap-southeast-1`<br>Clean up `DashboardStack`, remove outdated Glue & analytics code.<br>Update APIs for customer and consultant; enhance logging for `AdminManager` Lambda. | 27/11/2025 | 27/11/2025 |  |
| 6 | Manage EventBridge rule for `ArchiveData` Lambda (enable/disable/check status/manual invoke).<br><br>Disable: `aws events disable-rule --name MeetAssist-ArchiveSchedule`<br>Enable: `aws events enable-rule --name MeetAssist-ArchiveSchedule`<br>Check status: `aws events describe-rule --name MeetAssist-ArchiveSchedule`<br>Invoke: `aws lambda invoke --function-name DashboardStack-ArchiveData --payload "{}" --cli-binary-format raw-in-base64-out NUL`<br><br>Fix CSV UTF-8 issue when opening in Excel; `index.py` now supports both UTF-8 and UTF-8 BOM.<br>Implement checksum logic for `ArchiveData` to avoid re-uploading unchanged CSV → reduce S3 PUT cost.<br>Option 1: No checksum (always overwrite) – simple but noisy timestamps and higher cost.<br>Option 2 (recommended): Use checksum (MD5). If unchanged → skip; if different → upload.<br>Create `archive_info.json` in S3 to:<br>- Track archiving status<br>- Store checksums<br>- Record metrics, errors, last update time<br>- Potential future use in the dashboard<br>Implement RDS → S3 archiving mechanism using a scheduled Lambda:<br>- Create `ArchiveService` to export CSV + upload to S3 + write metadata<br>- `archive_handler` runs on schedule (every 5 minutes, disabled by default)<br>- Automatically skip unchanged tables based on checksum<br>Update CDK to deploy Lambda + IAM + EventBridge rule.<br>Improve error handling for consultant/appointment/program workflows.<br>Update `dashboard_handler` docstring to clearly describe the separation between CRUD and archiving flows. | 28/11/2025 | 28/11/2025 |  |

## Week 12 Achievements
- Refactored the entire backend & infrastructure for better optimization and maintainability.
- Gained a solid understanding of deploying and configuring VPC, RDS, S3, Lambda, and EventBridge using CDK.
- Completed all dashboard and admin APIs for analytics and management features.
- Optimized the import & archive workflows between RDS ↔ S3.
- Built a checksum mechanism to reduce S3 cost and improve data processing efficiency.
- Clearly separated business logic into service classes for easier testing and expansion.
- Improved logging, debugging, and API Gateway – Lambda integration structure.
- Completed the data migration process from on-premise to cloud and ensured correct handling on redeployments.


---
title: "Week 3 Worklog"
date: 2025-09-23
weight: 3
chapter: false
pre: " <b> 1.3 </b> "
---

### Week 3 Objectives:

* Deepen understanding of AWS IAM access control: Users, Groups, Policies, and Roles.
* Learn how to design and implement secure access patterns using IAM Roles and least privilege.
* Practice creating IAM Groups, Users, Roles and configuring role switching scenarios.
* Understand core Amazon VPC networking concepts: Subnets, Route Tables, Internet Gateway, NAT Gateway.
* Get hands-on experience with VPC security (Security Groups, Network ACLs) and an introduction to Site-to-Site VPN.

---

### Tasks to be carried out this week:

| Day | Task                                                                                                                                                                                                                                           | Start Date | Completion Date | Reference Material                         |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | ---------------- | ------------------------------------------ |
| 1   | - Study IAM access control overview <br>&emsp; + IAM Users & IAM Groups <br>&emsp; + IAM Policies <br>&emsp; + IAM Roles <br> - Review security objectives and principle of least privilege                                                     | 09/23/2025 | 09/23/2025       | <https://000002.awsstudygroup.com/>        |
| 2   | - **Hands-on IAM (1):** <br>&emsp; + Create Admin IAM Group <br>&emsp; + Create Admin User and add to group <br>&emsp; + Login as Admin User and verify permissions                                                                           | 09/24/2025 | 09/24/2025       | <https://000002.awsstudygroup.com/>        |
| 3   | - **Hands-on IAM (2):** <br>&emsp; + Create Admin Role <br>&emsp; + Create OperatorUser <br>&emsp; + Configure trust relationships for role switching <br>&emsp; + Test “Switch Role” from OperatorUser <br>&emsp; + Review and clean up config | 09/25/2025 | 09/25/2025       | <https://000002.awsstudygroup.com/>        |
| 4   | - Study Amazon VPC fundamentals: <br>&emsp; + Subnets <br>&emsp; + Route Tables <br>&emsp; + Internet Gateway <br>&emsp; + NAT Gateway <br> - Learn VPC security components: <br>&emsp; + Security Groups <br>&emsp; + Network ACLs             | 09/26/2025 | 09/26/2025       | <https://000003.awsstudygroup.com/>        |
| 5   | - **Hands-on VPC & Networking:** <br>&emsp; + Create VPC, Subnets, Internet Gateway, Route Tables, Security Groups <br>&emsp; + Enable VPC Flow Logs <br>&emsp; + Launch EC2 instance in VPC and test connectivity <br>&emsp; + Read through Site-to-Site VPN setup steps | 09/27/2025 | 09/27/2025       | <https://000003.awsstudygroup.com/>        |

---

### Week 3 Achievements:

* Gained a solid understanding of IAM access control concepts:
  * IAM Users and IAM Groups  
  * IAM Policies (permission-based access)  
  * IAM Roles and trust relationships  

* Implemented a basic IAM administrative structure:
  * Created Admin Group and Admin User  
  * Verified permissions using group-based policies  

* Practiced advanced IAM patterns:
  * Created Admin Role and OperatorUser  
  * Configured and tested “Switch Role” flows  
  * Applied the principle of least privilege when assigning permissions  

* Understood Amazon VPC core components:
  * Subnets, Route Tables, Internet Gateway, NAT Gateway  
  * Security Groups vs. Network ACLs  

* Built a small VPC environment:
  * Created VPC, subnets, routing, and security layers  
  * Launched EC2 instance inside VPC and verified connectivity  
  * Enabled VPC Flow Logs for traffic visibility  

* Reviewed the overall steps to set up AWS Site-to-Site VPN for hybrid connectivity.

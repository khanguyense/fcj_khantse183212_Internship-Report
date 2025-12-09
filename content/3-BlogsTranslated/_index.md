---
title: "Translated Blogs"
date: "2025-10-5"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---



**This section will list and introduce the blogs you have translated. For example:**

###  [Blog 1 - Enhance deployment guardrails with inference component rolling updates for Amazon SageMaker AI inference](3.1-Blog1/)
Amazon SageMaker AI now supports rolling updates for inference components, solving key problems of traditional blue/green deployments—like high GPU cost, limited capacity, and risky all-in-one traffic shifts—especially for large LLMs on expensive instances. Inference components already help by right-sizing resources and scaling per model, and rolling updates extend this by updating model copies in configurable batches, temporarily adding just enough capacity for each step, shifting traffic to the new version, and then tearing down the old capacity. You control batch size, timeouts, rollback behavior, and wait intervals through the RollingUpdatePolicy in UpdateInferenceComponent, while CloudWatch alarms can trigger automatic, controlled rollbacks if issues arise. For example, with three single-GPU instances, SageMaker can update one copy at a time by launching a new instance, validating it, then removing one old copy, repeating this until all copies are updated—achieving zero downtime, safer validation, and more cost-efficient, reliable deployments for models of different sizes.

###  [Blog 2 - Empowering bacterial genomics education with Amazon WorkSpaces](3.2-Blog2/)
TSiriraj Medical Research Center’s “Nanopore workshop: bacterial genome bioinformatics series” needed powerful, consistent computing environments for over 60 researchers, but faced big obstacles: participants had very different laptops and operating systems, many too weak for heavy bacterial genome analysis; installing and configuring complex bioinformatics tools like EPI2ME on each personal device was slow and error-prone; and limited on-premise infrastructure made it hard to scale or support hybrid/remote training. By using Amazon WorkSpaces—virtual cloud desktops that can run various Linux or Windows systems and be accessed from many devices— they could centrally provide preconfigured, high-performance environments, avoid hardware procurement and individual setup issues, and deliver smoother, more scalable hands-on bacterial genomics training.

###  [Blog 3 - End of support notifications and enhanced discoverability for Amazon EKS](3.3-Blog3/)
In the rapidly evolving world of containerized applications, maintaining resilience and observability across Kubernetes environments has become a critical challenge. As organizations increasingly adopt Amazon Elastic Kubernetes Service (Amazon EKS) to manage their containerized workloads, the need for cluster version lifecycle management and discovery mechanisms becomes crucial. As Amazon EKS environments grow more complex and span multiple AWS Regions and accounts, users often struggle to track cluster versions, support lifecycles, and overall deployment status.

Proactive monitoring of EKS cluster lifecycles and end of support is crucial to making sure of the security, stability, and compliance of Kubernetes deployments. Furthermore, gaining visibility into EKS cluster deployments across an entire AWS Organization is essential for effective resource management, strategic planning, and maintaining an accurate inventory.



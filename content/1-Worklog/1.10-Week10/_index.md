---
title: "Week 10 Worklog"
date: 2026-06-22
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives:

* Complete the **Minecraft Security Based on AWS** architecture.
* Deploy AWS Global Accelerator to provide static IP addresses and optimize network connectivity.
* Perform end-to-end testing of the entire system.
* Finalize the technical documentation and prepare for project completion.

### Tasks to be completed this week:

| Day | Tasks | Start Date | Completion Date | References |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| Mon | - Learn AWS Global Accelerator and its global traffic routing mechanism<br>- Analyze the benefits of using Global Accelerator for the Minecraft Server | 22/06/2026 | 22/06/2026 | https://www.youtube.com/@AWSStudyGroup https://cloudjourney.awsstudygroup.com/ |
| Tue | - Create an AWS Global Accelerator<br>- Configure a TCP Listener on port 25565<br>- Connect Global Accelerator to the Network Load Balancer | 23/06/2026 | 23/06/2026 | AWS Global Accelerator Documentation |
| Wed | - Test Minecraft Server connectivity using the Global Accelerator static IP addresses<br>- Verify traffic forwarding to the EC2 instance | 24/06/2026 | 24/06/2026 | Personal Project Notes |
| Thu | - Perform end-to-end testing: Player → Global Accelerator → Network Load Balancer → EC2 Minecraft Server<br>- Verify the GuardDuty → EventBridge → Lambda → SNS security automation workflow | 25/06/2026 | 25/06/2026 | Personal Project Notes |
| Fri | - Optimize the overall system configuration<br>- Finalize the architecture diagram, deployment guide, and operational documentation<br>- Review AWS service costs | 26/06/2026 | 26/06/2026 | AWS Well-Architected Framework |
| Sat | - Conduct final system testing<br>- Resolve remaining issues and optimize system performance<br>- Prepare the project demonstration | 27/06/2026 | 27/06/2026 | Personal Project Notes |
| Sun | - Update the project report and documentation<br>- Prepare the project review and completion plan for the following week | 28/06/2026 | 28/06/2026 | Personal Notes |

### Week 10 Achievements:

* Successfully deployed AWS Global Accelerator and integrated it with the Network Load Balancer.
* Enabled players to access the Minecraft Server through Global Accelerator's static IP addresses.
* Successfully validated the complete system workflow, from player connectivity to the automated security response pipeline.
* Finalized the deployment documentation, architecture diagrams, and operational guidelines.
* Completed the **Minecraft Security Based on AWS** project and prepared it for the final review, evaluation, and internship reporting phase.
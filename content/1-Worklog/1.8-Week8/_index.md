---
title: "Week 8 Worklog"
date: 2026-06-08
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:

* Implement a monitoring and threat detection system for the Minecraft Server.
* Integrate Amazon GuardDuty with Amazon EventBridge and AWS Lambda.
* Automatically send security alerts using Amazon SNS.
* Test the end-to-end AWS security event processing workflow.

### Tasks to be completed this week:

| Day | Tasks | Start Date | Completion Date | References |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| Mon | - Enable Amazon GuardDuty for the AWS account<br>- Learn about GuardDuty Security Findings and threat detection mechanisms | 08/06/2026 | 08/06/2026 | https://www.youtube.com/@AWSStudyGroup https://cloudjourney.awsstudygroup.com/ |
| Tue | - Create an AWS Lambda function to process GuardDuty findings<br>- Configure IAM Roles and permissions for Lambda | 09/06/2026 | 09/06/2026 | https://www.youtube.com/@AWSStudyGroup https://cloudjourney.awsstudygroup.com/ |
| Wed | - Develop the Lambda function to process security findings<br>- Verify execution logs using Amazon CloudWatch Logs | 10/06/2026 | 10/06/2026 | https://www.youtube.com/@AWSStudyGroup https://cloudjourney.awsstudygroup.com/ |
| Thu | - Create an Amazon EventBridge Rule for GuardDuty events<br>- Connect EventBridge with the Lambda function | 11/06/2026 | 11/06/2026 | https://www.youtube.com/@AWSStudyGroup https://cloudjourney.awsstudygroup.com/ |
| Fri | - Create an Amazon SNS Topic and Email Subscription<br>- Test email notifications triggered by security findings | 12/06/2026 | 12/06/2026 | https://www.youtube.com/@AWSStudyGroup https://cloudjourney.awsstudygroup.com/ |
| Sat | - Perform end-to-end testing of the GuardDuty → EventBridge → Lambda → SNS workflow<br>- Optimize the event processing logic | 13/06/2026 | 13/06/2026 | Personal Project Notes |
| Sun | - Update the deployment documentation and architecture diagram<br>- Prepare for implementing AWS Backup and Network Load Balancer in the following week | 14/06/2026 | 14/06/2026 | Personal Notes |

### Week 8 Achievements:

* Successfully enabled Amazon GuardDuty to monitor security threats within the AWS environment.
* Implemented an AWS Lambda function to process GuardDuty security findings.
* Configured Amazon EventBridge to automatically trigger Lambda in response to security events.
* Set up Amazon SNS to deliver email notifications to administrators whenever security threats are detected.
* Completed the automated Security Orchestration, Automation, and Response (SOAR) workflow for the **Minecraft Security Based on AWS** project.
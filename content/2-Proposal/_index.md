---
title: "Project Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Minecraft Security Based on AWS
## A Secure, Monitored, and Automated Incident Response Solution for Minecraft Server on AWS

### 1. Executive Summary

**Minecraft Security Based on AWS** is a cloud security project that deploys a Minecraft server on Amazon Web Services (AWS) and protects it using multiple layers of network security, threat detection, monitoring, automated incident response, and disaster recovery.

The project focuses on transforming a normal Minecraft server into a more secure and resilient game server environment. It addresses common security risks such as port scanning, SSH brute-force attacks, exposure of the origin EC2 public IP address, malicious traffic, data destruction, and possible service disruption.

The solution uses several AWS services, including **Amazon EC2, Amazon VPC, Security Groups, Network ACLs, AWS Systems Manager Session Manager, Amazon GuardDuty, Amazon EventBridge, AWS Lambda, Amazon SNS, Amazon CloudWatch, AWS Backup, Network Load Balancer, and AWS Global Accelerator**.

The key highlight of this project is the implementation of a small-scale **SOAR (Security Orchestration, Automation, and Response)** model. When Amazon GuardDuty detects suspicious activity, Amazon EventBridge triggers an AWS Lambda function to automatically respond to the threat, such as blocking a malicious IP address and sending an email alert to the administrator through Amazon SNS.

---

### 2. Idea & Objectives (Problem Statement)

#### 2.1 Background & Problem

*   **System Purpose:**

    The purpose of this project is to deploy a secure Minecraft server on AWS while applying cloud security best practices. Instead of simply hosting a game server on a virtual machine, the system is designed with proactive security, continuous monitoring, automated response, and backup recovery capabilities.

*   **Target Users:**

    This system is designed for:

    * Minecraft server administrators who want to host a secure game server on the cloud.
    * Students or learners who need a practical AWS Security project.
    * Teams that want to simulate cloud-based threat detection and automated incident response.
    * Minecraft players who need a stable and protected server connection.

*   **Problems to Solve:**

    Public game servers often face several security risks, including:

    * Exposure of the real public IP address of the server.
    * Port scanning and reconnaissance activities.
    * SSH brute-force attacks if port 22 is exposed to the Internet.
    * DDoS or traffic flooding against the game server port.
    * Destruction or corruption of Minecraft world data.
    * Lack of automated alerting and incident response mechanisms.

    This project solves these problems by applying layered security controls, restricting exposed ports, using secure administration through Session Manager, enabling threat detection with GuardDuty, automating response with Lambda, sending alerts with SNS, and performing scheduled backups with AWS Backup.

---

#### 2.2 Specific Objectives

*   **Expected Outputs:**

    * A working Minecraft Server hosted on Amazon EC2.
    * A secure AWS network environment using VPC, Public Subnet, Security Group, and Network ACL.
    * Server administration through **AWS Systems Manager Session Manager** without opening SSH port 22.
    * Threat detection using **Amazon GuardDuty**.
    * Automated incident response using **Amazon EventBridge and AWS Lambda**.
    * Email alerting using **Amazon SNS**.
    * Data backup and recovery using **AWS Backup**.
    * Origin IP protection using **AWS Global Accelerator and Network Load Balancer**.
    * Complete documentation for deployment, operation, demonstration, and resource cleanup.

*   **Success Criteria:**

    * The Minecraft Server can run successfully and allow players to connect through TCP port 25565.
    * The Security Group only allows the required Minecraft port and does not expose SSH publicly.
    * The administrator can access EC2 using AWS Systems Manager Session Manager.
    * GuardDuty can generate findings or sample findings for security demonstration.
    * EventBridge can trigger Lambda when a GuardDuty finding occurs.
    * Lambda can perform an automated response such as logging, blocking an IP address, or sending an alert.
    * SNS can send an email alert to the administrator.
    * AWS Backup can create scheduled backups for the EC2 instance.
    * Global Accelerator provides static IP addresses for players while reducing direct exposure of the EC2 public IP.

---

#### 2.3 Relevance to the Cloud / AWS Program

*   **AWS Security Use Case:**

    This project simulates a realistic cloud security scenario: deploying a public-facing service on the Internet and building a system that can monitor, detect, and automatically respond to suspicious activities.

*   **Cloud-Focused Design:**

    The project demonstrates important cloud principles:

    * **Security:** Protecting the system with Security Groups, IAM, SSM, and GuardDuty.
    * **Monitoring:** Tracking activity with CloudWatch and GuardDuty.
    * **Automation:** Responding automatically with EventBridge and Lambda.
    * **Resilience:** Protecting data through AWS Backup.
    * **Availability:** Improving connectivity with Network Load Balancer and Global Accelerator.
    * **Cost Awareness:** Providing cleanup procedures to avoid unexpected AWS charges.

*   **Proposed Solution:**

    The system consists of the following layers:

    1.  **Game Server Layer:** Amazon EC2 running Ubuntu Server and PaperMC Minecraft Server.
    2.  **Network Security Layer:** Amazon VPC, Public Subnet, Security Groups, and Network ACLs.
    3.  **Secure Administration Layer:** AWS Systems Manager Session Manager for EC2 access without SSH.
    4.  **Threat Detection Layer:** Amazon GuardDuty for identifying suspicious activities.
    5.  **Automated Response Layer:** Amazon EventBridge and AWS Lambda for automated incident response.
    6.  **Notification Layer:** Amazon SNS for sending email alerts.
    7.  **Backup & Recovery Layer:** AWS Backup for scheduled backup and recovery.
    8.  **IP Protection & DDoS Mitigation Layer:** AWS Global Accelerator and Network Load Balancer.

*   **Benefits and ROI:**

    *   **Improved Security:** The server does not expose SSH publicly, reducing brute-force attack risks.
    *   **Fast Response:** Suspicious activities can trigger automated responses instead of relying only on manual action.
    *   **Reduced Downtime:** Scheduled backups help recover Minecraft world data after failures or attacks.
    *   **Easy Demonstration:** GuardDuty Sample Findings can be used to simulate attacks without performing real attacks.
    *   **Cost Optimization:** Resources can be stopped or deleted after the demo to avoid unnecessary costs.

---

### 3. Solution Architecture

The system is designed using a layered security architecture. The Minecraft Server runs on EC2 and is protected by networking, monitoring, automation, alerting, and backup components.

#### 3.1 System Architecture Diagram

![Architecture](/images/2-Proposal/Architecture.png)

#### 3.2 Architecture Flow

Players do not connect directly to the real public IP address of the EC2 instance. Instead, they connect through the static IP addresses provided by **AWS Global Accelerator**. Traffic is then routed to a **Network Load Balancer**, which forwards TCP traffic on port 25565 to the EC2 instance running the Minecraft Server.

For security monitoring, **Amazon GuardDuty** analyzes AWS account activity and network behavior. When GuardDuty detects a finding, **Amazon EventBridge** receives the event and triggers **AWS Lambda**. Lambda then performs an automated response, such as logging the incident, blocking a suspicious IP address, and sending an alert through **Amazon SNS**.

At the same time, **AWS Backup** provides scheduled backup protection for the EC2 instance to support disaster recovery.

---

#### 3.3 AWS Services Used

| Category | AWS Service | Reason for Selection & Role |
| :--- | :--- | :--- |
| **Compute** | Amazon EC2 | Hosts the Minecraft Server on Ubuntu Server. |
| **Game Server** | PaperMC / Minecraft Server | Provides the multiplayer Minecraft environment for players. |
| **Networking** | Amazon VPC | Creates an isolated network environment for the project. |
| **Networking** | Public Subnet | Hosts public-facing components according to the security design. |
| **Security** | Security Group | Allows only TCP port 25565 for Minecraft and does not expose SSH port 22 publicly. |
| **Security** | Network ACL | Adds subnet-level traffic control and can support IP blocking rules. |
| **Administration** | AWS Systems Manager Session Manager | Allows secure EC2 administration through the AWS Console without SSH key pairs. |
| **Identity & Access** | IAM Role | Grants EC2 access to Systems Manager and allows Lambda to perform automated actions. |
| **Threat Detection** | Amazon GuardDuty | Detects suspicious activities such as port scanning, brute-force attempts, and abnormal behavior. |
| **Event Routing** | Amazon EventBridge | Routes GuardDuty findings to Lambda for automated processing. |
| **Automation** | AWS Lambda | Executes automated response actions when a security event occurs. |
| **Notification** | Amazon SNS | Sends email alerts to the administrator. |
| **Monitoring** | Amazon CloudWatch | Stores logs, monitors Lambda execution, and supports demo verification. |
| **Backup** | AWS Backup | Creates scheduled EC2 backups for disaster recovery. |
| **Load Balancing** | Network Load Balancer | Handles TCP traffic on port 25565 and forwards it to the Minecraft Server. |
| **Edge Networking** | AWS Global Accelerator | Provides global static IP addresses and helps protect the origin EC2 IP address. |

---

### 4. Technical Implementation

#### Implementation Phases

The project is implemented in the following phases:

1.  **Secure Network Setup (VPC & Security Group):**

    * Create a dedicated VPC.
    * Create a Public Subnet.
    * Configure an Internet Gateway.
    * Create a Security Group that only allows TCP port 25565.
    * Do not expose SSH port 22 to the Internet.
    * Enable Auto-assign Public IPv4 for the subnet if required.

2.  **Minecraft Server Deployment & Keyless Administration:**

    * Launch an Ubuntu EC2 instance.
    * Proceed without using a traditional key pair.
    * Attach an IAM Role with `AmazonSSMManagedInstanceCore`.
    * Connect to EC2 using AWS Systems Manager Session Manager.
    * Install Java.
    * Download and configure PaperMC Minecraft Server.
    * Create a restricted `minecraft` user to avoid running the server as root.
    * Run the Minecraft Server in the background using `screen`.

3.  **Intrusion Detection Setup:**

    * Enable Amazon GuardDuty.
    * Monitor GuardDuty findings.
    * Use sample findings for demonstration purposes.

4.  **Automated Response with Lambda & EventBridge:**

    * Create a Lambda function to process security events.
    * Grant the required IAM permissions to Lambda.
    * Create an EventBridge Rule for GuardDuty findings.
    * Connect EventBridge to Lambda.
    * Verify Lambda execution through CloudWatch Logs.

5.  **Disaster Recovery Backup with AWS Backup:**

    * Create a Backup Vault.
    * Create a Backup Plan.
    * Configure hourly backups.
    * Assign the Minecraft EC2 instance to the Backup Plan.
    * Configure a retention period to automatically remove old backups.

6.  **Origin IP Protection & DDoS Mitigation with Global Accelerator + NLB:**

    * Create a Target Group for TCP port 25565.
    * Create a Network Load Balancer.
    * Register the Minecraft EC2 instance as a target.
    * Create an AWS Global Accelerator.
    * Attach the Network Load Balancer as an endpoint.
    * Use the static IP addresses from Global Accelerator for player connections.

7.  **Email Notification Setup:**

    * Create an SNS Topic.
    * Create an Email Subscription.
    * Confirm the subscription through email.
    * Update Lambda to publish security alerts to SNS.

8.  **Operation and Resource Cleanup:**

    * Start the Minecraft Server using a secure startup command sequence.
    * Check server status using `screen` or log files.
    * Stop the server safely using the `stop` command.
    * Clean up Global Accelerator, NLB, EC2, Lambda, EventBridge, SNS, GuardDuty, AWS Backup, and custom NACL rules after completing the project.

---

#### Prerequisites

*   **Resources & Tools:**

    * An AWS account with permission to create EC2, VPC, IAM, Lambda, EventBridge, SNS, GuardDuty, CloudWatch, AWS Backup, NLB, and Global Accelerator resources.
    * Minecraft Java Edition installed on a local machine for connection testing.
    * A web browser to access the AWS Console.
    * Basic Linux command-line knowledge.

*   **Required Knowledge:**

    * VPC Networking: Subnets, Route Tables, Internet Gateway, and Security Groups.
    * Amazon EC2 and IAM Roles.
    * AWS Systems Manager Session Manager.
    * Amazon GuardDuty and CloudWatch Logs.
    * AWS Lambda and Amazon EventBridge.
    * Amazon SNS Email Notification.
    * Backup and Disaster Recovery concepts.
    * Basic DDoS mitigation and origin IP protection concepts.

---

### 5. Roadmap & Milestones

*   **Week 1: Core Infrastructure & Minecraft Server Deployment**

    * Design the VPC, Subnet, Internet Gateway, and Security Group.
    * Launch the Ubuntu EC2 instance for Minecraft Server.
    * Configure the IAM Role for Systems Manager.
    * Access EC2 using Session Manager instead of SSH.
    * Install Java and PaperMC.
    * Create the restricted `minecraft` user.
    * Test Minecraft client connection.

*   **Week 2: Security, Monitoring, Automation & Final Validation**

    * Enable Amazon GuardDuty.
    * Create the Lambda function for security event handling.
    * Create the EventBridge Rule to connect GuardDuty with Lambda.
    * Configure SNS email alerts.
    * Configure AWS Backup for EC2.
    * Create the Network Load Balancer and Global Accelerator.
    * Demonstrate GuardDuty Sample Findings.
    * Verify CloudWatch Logs and email alerts.
    * Complete operation, demo, and cleanup documentation.

---

### 6. Budget Estimation

Cost estimation helps evaluate the practical feasibility of deploying the system on the AWS platform. The costs below are calculated based on the reference pricing for the AWS **Asia Pacific (Singapore)** region and are intended for estimation purposes only. Actual costs may vary depending on usage duration, network traffic, and allocated resources.

#### 6.1 Workshop / Tutorial Environment

| No. | AWS Service | Configuration & Pricing Assumptions | Monthly Cost |
| :--- | :--- | :--- | :--- |
| 1 | Amazon EC2 | 1 `t3.medium` Ubuntu instance hosting the Minecraft Server | ~ $30.37 |
| 2 | Amazon EBS | 20GB gp3 SSD Storage | ~ $1.60 |
| 3 | Amazon GuardDuty | CloudTrail, DNS Logs, and VPC Flow Logs analysis at small scale | ~ $3.00 |
| 4 | AWS Lambda | Automated event handling and IP blocking, under 1 million requests/month | ~ $0.00 |
| 5 | Amazon EventBridge | Rule connecting GuardDuty findings to Lambda | ~ $0.00 |
| 6 | Amazon SNS | Email security alerts for the administrator | ~ $0.00 |
| 7 | Amazon CloudWatch | Log storage and monitoring, approximately 5GB logs/month | ~ $2.50 |
| 8 | AWS Backup | Hourly EC2 backup with 7-day retention | ~ $2.50 |
| 9 | Network Load Balancer | 1 TCP Network Load Balancer for port 25565 | ~ $16.20 |
| 10 | AWS Global Accelerator | 1 Accelerator providing global static IP addresses | ~ $18.25 |
| 11 | VPC, IAM, Security Groups, NACL, Systems Manager | Core networking and security administration services | $0.00 |
| **Total** | **Estimated Monthly Cost** | | **~ $74.42** |

*Note:* Cloud infrastructure costs can be significantly reduced to below **$40.00/month** in a learning environment by:

*   Using an EC2 `t3.micro` or `t2.micro` instance instead of `t3.medium` when demonstrating with only a few players.
*   Running EC2 only during lab or demo sessions and stopping the instance when not in use.
*   Disabling AWS Global Accelerator when IP protection or DDoS demonstration is not required.
*   Deleting old backup recovery points after testing.
*   Taking advantage of the AWS Free Tier for Lambda, EventBridge, SNS, and CloudWatch.

#### 6.2 Production Environment

| No. | AWS Service | Configuration & Pricing Assumptions | Monthly Cost |
| :--- | :--- | :--- | :--- |
| 1 | Amazon EC2 | 1 `t3.large` Ubuntu instance running the production Minecraft Server | ~ $60.74 |
| 2 | Amazon EBS | 50GB gp3 SSD Storage | ~ $4.00 |
| 3 | Amazon GuardDuty | Continuous threat detection and monitoring | ~ $10.00 |
| 4 | AWS Lambda | Automated response and malicious IP blocking | ~ $0.50 |
| 5 | Amazon EventBridge | Event routing between GuardDuty and Lambda | ~ $1.00 |
| 6 | Amazon SNS | Email notification service | ~ $0.50 |
| 7 | Amazon CloudWatch | Monitoring, dashboard, and log storage | ~ $8.00 |
| 8 | AWS Backup | Scheduled backup with 30-day retention | ~ $10.00 |
| 9 | Network Load Balancer | 1 Production NLB for Minecraft TCP traffic | ~ $16.20 |
| 10 | AWS Global Accelerator | 1 Production Global Accelerator | ~ $18.25 |
| 11 | VPC, IAM, Security Groups, NACL, Systems Manager | Core networking and security administration services | $0.00 |
| **Total** | **Estimated Monthly Cost** | | **~ $129.19** |

---

### 7. Risk Assessment

#### Risk Matrix

| Identified Risk | Likelihood | Impact | Mitigation & Prevention Strategy |
| :--- | :--- | :--- | :--- |
| **SSH brute-force attack against the server** | Medium | High | Do not expose SSH port 22 publicly. Use AWS Systems Manager Session Manager for administration. |
| **Exposure of the EC2 public IP address** | Medium | High | Use AWS Global Accelerator with Network Load Balancer so players connect through static edge IPs instead of the EC2 public IP. |
| **Port scanning or reconnaissance** | Medium | Medium | Enable Amazon GuardDuty to detect scanning activities and forward findings to EventBridge. |
| **DDoS attack against the Minecraft Server** | Medium | High | Use Global Accelerator and Network Load Balancer to reduce direct exposure of the origin server. |
| **Minecraft world data destruction** | Medium | High | Configure AWS Backup with scheduled backups and a defined retention policy. |
| **Lambda blocks a legitimate IP by mistake** | Low | Medium | Carefully validate the finding-processing logic, log all actions in CloudWatch, and provide a manual recovery process. |
| **Unexpected AWS charges** | Medium | Medium | Stop or delete resources after the demo. Remove Global Accelerator, NLB, EC2, Backup Vault, and disable GuardDuty when not in use. |
| **Running Minecraft Server as root** | Medium | High | Create a dedicated `minecraft` user and run the server with limited privileges. |

---

#### Contingency Plan

*   **In case the Minecraft Server fails or world data is damaged:**

    Use AWS Backup to restore the EC2 instance or Minecraft world data from the latest available backup. With hourly backups, the maximum potential data loss can be limited to less than one hour in the demo environment.

*   **In case a malicious IP is detected:**

    GuardDuty generates a finding, EventBridge triggers Lambda, and Lambda performs the automated response. The administrator receives an SNS email alert and can review details in CloudWatch Logs.

*   **In case the live demo does not produce real findings:**

    Use GuardDuty Sample Findings to simulate attack scenarios. This ensures a stable and repeatable demonstration without depending on real attacks.

*   **In case unexpected costs occur:**

    Follow the cleanup order: Global Accelerator, Network Load Balancer, Target Group, EC2, Lambda, EventBridge, SNS, GuardDuty, AWS Backup, and custom NACL rules.

---

### 8. System Processing Flows & Technical Characteristics

The system applies a layered security architecture combined with automated incident response. The main flows include player connection, secure administration, threat detection, automated response, email alerting, and backup recovery.

#### 8.1 Core Processing Flows

*   **Player Connection Flow:**

    Players connect to the static IP addresses provided by AWS Global Accelerator. TCP traffic on port 25565 is routed to the Network Load Balancer and then forwarded to the EC2 instance running the Minecraft Server. This design reduces direct exposure of the EC2 public IP address.

*   **Secure Administration Flow:**

    The administrator does not use SSH key pairs and does not expose port 22. Instead, EC2 access is performed through AWS Systems Manager Session Manager in the AWS Console. This reduces the risk of SSH brute-force attacks and removes the need to manage `.pem` files.

*   **Threat Detection Flow:**

    Amazon GuardDuty analyzes AWS account activity and network behavior to detect suspicious activities such as port scanning, brute-force attempts, or abnormal behavior. When a finding is generated, GuardDuty sends the event to EventBridge.

*   **Automated Incident Response Flow:**

    EventBridge receives the GuardDuty finding and triggers AWS Lambda. Lambda processes the event, extracts suspicious IP information if available, performs a response action such as logging or blocking the IP, and records the result in CloudWatch Logs.

*   **Email Alert Flow:**

    After Lambda processes the event, Amazon SNS sends an email alert to the administrator. The alert can include the threat type, detection time, source IP address, and response action.

*   **Backup and Recovery Flow:**

    AWS Backup automatically creates scheduled backups for the EC2 instance. If the server fails, is corrupted, or the Minecraft world is damaged, the administrator can restore from the latest backup to minimize data loss.

---

#### 8.2 Architectural Strengths

*   **Defense in Depth:**

    The system does not rely on a single security layer. It combines Security Groups, NACLs, IAM, SSM, GuardDuty, Lambda, SNS, and Backup to improve overall security.

*   **No Public SSH Exposure:**

    Managing EC2 through Session Manager eliminates the need to expose SSH port 22 to the Internet, which significantly reduces a common attack surface.

*   **Automated Incident Response:**

    GuardDuty, EventBridge, and Lambda form a small-scale SOAR workflow. The system can detect security events and automatically respond to them.

*   **Disaster Recovery Capability:**

    AWS Backup protects Minecraft world data against system failures, operational mistakes, and malicious destruction.

*   **Origin IP Protection:**

    Global Accelerator and Network Load Balancer allow players to connect through static IP addresses instead of the EC2 public IP, reducing direct targeting of the origin server.

*   **Demo-Friendly Design:**

    GuardDuty Sample Findings allow the security detection and response flow to be demonstrated reliably during presentation or evaluation.

---

### 9. Expected Outcomes

*   **Technical Improvements:**

    * The Minecraft Server is successfully deployed on Amazon EC2.
    * Players can connect to the server through TCP port 25565.
    * SSH is not exposed publicly, reducing brute-force risk.
    * GuardDuty can detect suspicious activities or generate sample findings.
    * EventBridge can trigger Lambda automatically when a finding occurs.
    * Lambda can process the event, perform a response, and send alerts.
    * SNS can send email alerts to the administrator.
    * AWS Backup can create scheduled recovery points.
    * Global Accelerator and Network Load Balancer help protect the EC2 origin IP address.

*   **Long-Term Value:**

    * The project provides a practical cloud security model that can be extended to other game servers or public-facing services.
    * It applies important AWS Security principles such as Least Privilege, Defense in Depth, Secure Administration, and Automated Incident Response.
    * It creates a foundation for future improvements such as monitoring dashboards, Discord or Telegram alerts, automated Minecraft world snapshots, or container-based deployment using ECS/Fargate.
    * It is suitable for an academic report, cloud computing project, cybersecurity portfolio, or AWS Security learning project.

---
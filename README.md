# aws-devops-mcp-stack
🚀 A production-grade 3-Tier AWS Architecture with Terraform and AI Agents (MCP) for automated auditing


![Terraform](https://img.shields.io/badge/Terraform-v1.5+-623CE4?style=for-the-badge&logo=terraform&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-Cloud-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)
![AI Agents](https://img.shields.io/badge/AI_Agents-MCP_Protocol-00C7B7?style=for-the-badge&logo=google-cloud&logoColor=white)

A production-grade **Infrastructure as Code (IaC)** repository that deploys a secure, auto-scaling **3-Tier Architecture** on AWS. It includes a modern **AI Agent workflow** using the Model Context Protocol (MCP) to audit and manage infrastructure directly from your IDE.

---

## 🏗 Architecture (Mental Model)

This stack creates a **High-Availability Network** with strict isolation between public and private resources.

```mermaid
graph TD
    User((User)) -->|HTTP| ALB[Application Load Balancer]
    Admin((You)) -->|SSH| Bastion[Bastion Host / Jump Box]
    
    subgraph VPC [VPC: 10.0.0.0/16]
        subgraph Public_Zone [Public Subnets]
            ALB
            Bastion
            NAT[Custom NAT Gateway]
        end
        
        subgraph Private_Zone [Private Subnets]
            ASG[Auto Scaling Fleet]
        end
    end
    
    ALB --> ASG
    Bastion --> ASG
    ASG -->|Outbound Updates| NAT
    ASG -->|Access| S3[Private S3 Bucket]

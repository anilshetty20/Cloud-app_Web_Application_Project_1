CloudApp Project – Scalable Full Stack Deployment on AWS
📌 Overview

This project demonstrates a production-ready cloud architecture for deploying a full-stack application using AWS, Docker, and CI/CD.

Frontend: React app hosted on Amazon S3 and delivered via CloudFront
Backend: Dockerized application running on EC2 (Auto Scaling Group)
Database: PostgreSQL on Amazon RDS
CI/CD: GitHub Actions with Docker Hub
Networking: Secure VPC with public and private subnets
🧭 Architecture Flow
User → CloudFront → S3 (Frontend)
                  ↓
             /api/* requests
                  ↓
        CloudFront → ALB → EC2 (Docker Backend)
                                   ↓
                                 RDS
🌐 Networking Setup
VPC Design
1 VPC with 4 subnets:
2 Public Subnets → ALB, NAT Gateway
2 Private Subnets → EC2, RDS
Route Tables

Public Route Table

Route: 0.0.0.0/0 → Internet Gateway

Private Route Table

Route: 0.0.0.0/0 → NAT Gateway
Why this setup?
Public subnets allow internet-facing services
Private subnets secure backend and database
NAT Gateway enables outbound internet access for private instances
🔐 Security Configuration
Security Groups

1. ALB Security Group

Allows HTTP (80) and HTTPS (443) from the internet

2. EC2 Security Group

Allows port 5000 only from ALB

3. RDS Security Group

Allows PostgreSQL (5432) only from EC2
Security Strategy
Backend is not publicly accessible
Database is fully private
Access is restricted between layers
⚙️ Compute Layer
EC2 with Auto Scaling Group
Automatically scales based on traffic
Ensures high availability and fault tolerance
Launch Template
Defines EC2 configuration
Includes Docker setup and startup script
User Data Script
Installs Docker
Pulls latest backend image
Runs the container
⚖️ Load Balancing
Application Load Balancer (ALB)
Distributes incoming traffic across EC2 instances
Acts as a single entry point for backend
Target Group
Routes requests to healthy EC2 instances
Performs health checks
🗄 Database Layer
Amazon RDS (PostgreSQL)
Managed relational database
Automated backups
Secure and scalable
🎨 Frontend Deployment
Amazon S3
Hosts static frontend files
CloudFront (CDN)
Delivers content globally with low latency
Caches static content
🔗 Frontend–Backend Integration
CloudFront Configuration
Origin 1: S3 (Frontend)
Origin 2: ALB (Backend)
Behavior Rules
/api/* → Routed to ALB
/* → Routed to S3
Cache Policy
Disabled for /api/* to ensure real-time API responses
🐳 Docker Implementation
Purpose
Ensures consistency across environments
Simplifies deployment process
Workflow
Build Docker image
Push image to Docker Hub
EC2 instances pull the latest image during deployment
🔁 CI/CD Pipeline (GitHub Actions)
Trigger
Runs on push to the main branch
Backend Deployment Steps
Build Docker image
Push to Docker Hub
Update Launch Template
Refresh Auto Scaling Group
Frontend Deployment Steps
Install dependencies
Build production files
Upload to S3
Invalidate CloudFront cache
🚀 Key Features
Fully automated CI/CD pipeline
Scalable backend using Auto Scaling
Secure VPC architecture
Fast content delivery via CDN
Containerized backend with Docker
Zero manual deployment
🧠 DevOps Concepts Used
Continuous Integration and Deployment (CI/CD)
Docker Containerization
Immutable Infrastructure
Load Balancing
Auto Scaling
CDN Caching Strategy
Infrastructure Automation (AWS CLI)

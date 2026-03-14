(#) SAA Terminology Guide

This file collects the core terms and concepts you will encounter frequently while studying for the AWS Solutions Architect Associate (SAA-C03). For each term you'll find: a concise definition, when and how you'll use it, a short example, why it matters, and a metaphor to make the idea more memorable. Where useful, a reference link is included.

---

**1. Region / Availability Zone (AZ)**
- Definition: A Region is a geographically isolated area (e.g., us-east-1). An Availability Zone(AZ) is an isolated data center (or group) within a Region.
- When you use it: Choose Regions for latency, compliance, and cost; place resources in multiple AZs for high availability.
- Example: Deploy two EC2 instances in two AZs behind an Elastic Load Balancer.
- Why it matters: Regions/AZs determine fault isolation and data residency; spreading across AZs reduces single-point-of-failure risk.
- Metaphor: Think of a Region as a city and AZs as power-grid-separated neighborhoods — if one neighborhood loses power, the rest of the city still runs.
- Reference: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html

**2. IAM (Users, Groups, Roles, Policies)**
- Definition: Identity and Access Management for authentication/authorization. Users are human identities, Roles are assumed identities for services, Policies are permission documents.
- When you use it: Always create least-privilege roles for EC2/Lambda, avoid embedding long-term credentials in code.
- Example: Create an IAM role for Lambda with permission to PutItem in DynamoDB.
- Why it matters: Security and least privilege prevent accidental or malicious overreach.
- Metaphor: IAM is the building's access-control system — badges (users/roles) and door rules (policies).
- Reference: https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html

**3. VPC, Subnet, Route Table, Internet Gateway, NAT**
- Definition: VPC = virtual network. Subnets partition the VPC into logical segments (public/private). Route tables control network paths. Internet Gateway connects public subnets to the internet. NAT lets private instances reach the internet safely.
- When you use it: Design VPCs to isolate application tiers (web in public subnet, app/db in private subnets).
- Example: Web servers in public subnets with ELB; databases in private subnets with no direct internet access.
- Why it matters: Networking determines security perimeter and connectivity.
- Metaphor: VPC is your fenced campus; subnets are campus zones; route tables are campus maps; IGW is the main gate; NAT is a receptionist that forwards outgoing mail but hides internal addresses.
- Reference: https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html

**4. EC2, AMI, Instance Type, EBS, Instance Store**
- Definition: EC2 = virtual machine. AMI = image used to launch instances. Instance types define CPU/RAM. EBS = persistent block storage. Instance store = ephemeral storage tied to the instance lifetime.
- When you use it: EC2 for full-control compute; choose instance type based on workload; use EBS for durable volumes.
- Example: Launch t3.medium for small web server with a gp3 EBS volume for persistent data.
- Why it matters: Cost, performance, and durability trade-offs depend on instance type and storage choice.
- Metaphor: EC2 is a rented server; AMI is the preinstalled OS snapshot; EBS is a detachable hard drive; instance store is the server's temporary desk — cleared on reboot.
- Reference: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/what-is-ec2.html

**5. Auto Scaling Group (ASG) & Elastic Load Balancer (ELB)**
- Definition: ASG automatically adjusts the number of instances according to policies. ELB distributes incoming traffic across healthy targets.
- When you use it: To handle variable load and achieve high availability.
- Example: ASG scales from 2→10 instances during peak traffic; ALB routes HTTP requests to targets.
- Why it matters: Cost efficiency and fault tolerance.
- Metaphor: ASG is an automated staff rota that calls people in when busy; ELB is the receptionist directing callers to available agents.
- Reference: https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html

**6. S3 (Buckets, Objects, Storage Classes, Versioning, Lifecycle)**
- Definition: S3 is object storage. Buckets contain objects (files). Storage classes determine access/cost patterns. Versioning keeps object history. Lifecycle rules move/expire objects.
- When you use it: Store static assets, backups, and objects requiring high durability.
- Example: Host website assets in S3 + CloudFront; use lifecycle to move infrequently accessed objects to Glacier.
- Why it matters: Durability, cost, and access patterns shape storage design.
- Metaphor: S3 is a warehouse with shelves (buckets); storage classes are shelf types (fast-access vs archive); versioning is keeping older box copies.
- Reference: https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html

**7. RDS (Managed Databases) vs DynamoDB (NoSQL)**
- Definition: RDS provides managed relational databases (MySQL, Postgres). DynamoDB is serverless key-value and document NoSQL store.
- When you use it: Use RDS for relational schemas/complex queries; DynamoDB for massive scale with predictable access patterns.
- Example: Use RDS for transactional OLTP; use DynamoDB for session storage or high-scale lookup tables.
- Why it matters: Data consistency, query model, scaling approaches differ.
- Metaphor: RDS is a traditional library catalog searchable with complex queries; DynamoDB is a high-speed index list optimized for exact-key lookups.
- Reference RDS: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html
- Reference DynamoDB: https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html

**8. Lambda, API Gateway, Event-driven architecture**
- Definition: Lambda = serverless functions. API Gateway exposes HTTP APIs. Event-driven uses events (S3, SNS, SQS) to trigger processing.
- When you use it: Build lightweight, cost-efficient APIs and background workers without managing servers.
- Example: API Gateway → Lambda to handle HTTP request → write to DynamoDB.
- Why it matters: Fast iteration, pay-per-use, and scaling without server management.
- Metaphor: Lambda is a vending machine that dispenses a function when triggered; API Gateway is the storefront window.
- Reference Lambda: https://docs.aws.amazon.com/lambda/latest/dg/welcome.html

**9. CloudWatch (Metrics, Logs, Alarms)**
- Definition: Monitoring and observability service for metrics, logs, and alarms.
- When you use it: Track performance, set alarms for thresholds, and inspect logs for debugging.
- Example: Create CloudWatch alarm on CPU > 80% for 5 minutes to trigger an Auto Scaling scale-out.
- Why it matters: Operational visibility and automated responses to issues.
- Metaphor: CloudWatch is the building's sensor network — it monitors temperature, power, and alerts when thresholds are crossed.
- Reference: https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html

**10. CloudFormation / Infrastructure as Code (IaC)**
- Definition: CloudFormation templates describe and provision AWS resources as code.
- When you use it: Automate repeatable deployments and keep infrastructure versioned.
- Example: A template that creates VPC, subnets, ASG, ELB, and RDS resources.
- Why it matters: Repeatability, reduced configuration drift, safer changes.
- Metaphor: CloudFormation is a recipe — follow it to bake the same cake each time.
- Reference: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html

**11. ECR / ECS / EKS (Containers)**
- Definition: ECR = container registry. ECS = container orchestration service. EKS = managed Kubernetes.
- When you use it: Deploy containerized applications; choose ECS for simpler setups and EKS for Kubernetes-native workloads.
- Example: Build Docker image, push to ECR, deploy to ECS Fargate for serverless containers.
- Why it matters: Containers make deployments portable and consistent.
- Metaphor: ECR is the garage storing cars (images); ECS/EKS are the fleet managers deciding which car runs where and when.
- Reference ECR: https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html

**12. CI/CD (CodePipeline, CodeBuild, CodeDeploy)**
- Definition: Continuous Integration/Continuous Delivery services to build, test, and deploy code.
- When you use it: Automate build/test/deploy pipelines to reduce manual errors.
- Example: On git push, CodePipeline triggers CodeBuild to run tests, then CodeDeploy to update the application.
- Why it matters: Faster, safer deployments and repeatable release processes.
- Metaphor: CI/CD is an assembly line that builds and packages goods automatically after quality checks.
- Reference CodePipeline: https://docs.aws.amazon.com/codepipeline/latest/userguide/welcome.html

**13. SQS vs SNS**
- Definition: SQS = message queue (pull-based). SNS = publish/subscribe (push-based notifications).
- When you use it: Use SQS for decoupled, reliable message processing; SNS for fan-out notifications to multiple subscribers.
- Example: SNS topic sends notification to multiple SQS queues and an email endpoint.
- Why it matters: Choose push vs pull patterns depending on delivery and scaling needs.
- Metaphor: SNS is a public announcement speaker; SQS is a mailbox where consumers pick up messages when ready.
- Reference SNS: https://docs.aws.amazon.com/sns/latest/dg/welcome.html

**14. Encryption at Rest / In Transit (KMS)**
- Definition: Protecting data when stored (at rest) and when moving between systems (in transit). KMS manages cryptographic keys.
- When you use it: Enable encryption for S3, EBS, RDS; use TLS for network traffic.
- Example: Enable SSE-KMS on S3 bucket to use a KMS key for object encryption.
- Why it matters: Compliance, data protection, and risk reduction.
- Metaphor: Encryption at rest is a safe for your valuables; in transit is an armored van while moving them.
- Reference KMS: https://docs.aws.amazon.com/kms/latest/developerguide/overview.html

---

If you want, I can:
- Expand any single term into a one-page study note with diagrams and hands-on labs.
- Produce a printable cheat-sheet PDF of these terms.
- Add internal cross-links to your existing SAA notes and labs.

Which next step should I take? (expand term / create PDF / add links)


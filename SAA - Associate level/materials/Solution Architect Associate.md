---

# Certification 1 — AWS Certified Solutions Architect – Associate (Weeks 1–8)

The SAA-C03 exam validates ability to design distributed systems on AWS and design with the Well-Architected Framework in mind. AWS lists it as an associate exam, 130 minutes, 65 questions, and $150. ([Amazon Web Services, Inc.][1])

## What this certification is really about

This is not a “coding” exam first.
It is a **design and decision-making** exam.

You must learn:

* which service to choose
* why that choice is better
* how to make systems secure, resilient, and cost-aware

---

## SAA Week 1 — AWS basics, global infrastructure, IAM

### Topics

* AWS global infrastructure: Regions, Availability Zones, edge locations
* Shared responsibility model
* IAM users, groups, roles, policies
* least privilege
* temporary credentials vs long-term credentials

### Official docs

* IAM overview and getting started ([AWS Documentation][5])
* IAM policies and permissions ([AWS Documentation][6])
* IAM roles ([AWS Documentation][7])

### Beginner goal

By the end of the week, you should be able to explain:

* the difference between **authentication** and **authorization**
* why **roles** are usually preferred over hardcoded access keys
* how policy JSON works at a basic level

### Hands-on

* create a non-root administrative identity
* create an IAM role for EC2
* attach a managed policy
* read a simple policy JSON and explain it out loud

---

## SAA Week 2 — Compute: EC2, scaling, load balancing

### Topics

* EC2 basics
* instance types
* EBS vs instance store
* security groups
* AMIs
* Auto Scaling
* Elastic Load Balancing

### Official docs

* EC2 overview and getting started ([AWS Documentation][8])
* EC2 instances and instance types ([AWS Documentation][9])
* EC2 best practices ([AWS Documentation][10])

### Beginner goal

Understand when to choose:

* one EC2 instance
* Auto Scaling group
* load balancer in front
* Spot vs On-Demand at a conceptual level

### Hands-on

* launch a Linux EC2 instance
* connect to it
* install a small web server
* stop/start/terminate it
* compare two instance types and write notes on when each makes sense

---

## SAA Week 3 — Storage: S3, EBS, EFS basics

### Topics

* object vs block vs file storage
* S3 buckets, objects, versioning
* storage classes
* lifecycle rules
* bucket policies
* encryption basics

### Official docs

* S3 overview and getting started ([AWS Documentation][11])
* S3 storage classes ([AWS Documentation][12])
* S3 bucket configuration and policies ([AWS Documentation][13])

### Beginner goal

You should be able to answer:

* when S3 is better than EBS
* what versioning protects you from
* how lifecycle rules help with cost

### Hands-on

* create a bucket
* upload files
* enable versioning
* create a lifecycle rule
* create a bucket policy and explain what it allows

---

## SAA Week 4 — Networking: VPC, subnets, routing, gateways

### Topics

* what a VPC is
* public vs private subnet
* route tables
* internet gateway
* NAT gateway
* security groups vs NACLs
* VPC basics for RDS

### Official docs

* VPC overview, how it works, and getting started ([AWS Documentation][14])
* RDS in a VPC context ([AWS Documentation][15])

### Beginner goal

Draw this from memory:

* 1 VPC
* 2 public subnets
* 2 private subnets
* load balancer in public subnets
* app in private subnets
* database in private subnets

### Hands-on

* inspect the default VPC
* create a custom VPC
* create one public and one private subnet
* explain what makes one “public”

---

## SAA Week 5 — Databases: RDS, DynamoDB, basic architectural decisions

### Topics

* relational vs NoSQL
* RDS basics
* backups, Multi-AZ, read replicas
* DynamoDB basics
* partition key intuition
* latency vs scalability tradeoffs

### Official docs

* RDS overview and getting started ([AWS Documentation][16])
* DynamoDB overview and getting started ([AWS Documentation][17])

### Beginner goal

Be able to explain:

* when to choose RDS
* when to choose DynamoDB
* what Multi-AZ does
* why DynamoDB is good for high-scale key-value access

### Hands-on

* create an RDS instance
* connect from an EC2 instance
* create a DynamoDB table
* perform basic CRUD

---

## SAA Week 6 — Serverless and integration basics

### Topics

* Lambda
* event-driven architecture
* API Gateway
* basic decoupling
* when serverless is better than EC2

### Official docs

* Lambda overview and first function ([AWS Documentation][18])
* API Gateway overview and getting started ([AWS Documentation][19])
* REST API concepts in API Gateway ([AWS Documentation][20])

### Beginner goal

Understand the classic pattern:
**Client → API Gateway → Lambda → DynamoDB**

### Hands-on

* create a Lambda function
* connect it to API Gateway
* return JSON
* store a simple item in DynamoDB

---

## SAA Week 7 — Monitoring, architecture patterns, cost and security review

### Topics

* CloudWatch basics
* alarms and logs
* Well-Architected thinking
* high availability
* fault tolerance
* cost optimization basics

### Official docs

* CloudWatch overview, metrics, dashboards, logs ([AWS Documentation][21])

### Beginner goal

Look at any architecture and ask:

* where can it fail?
* how is it monitored?
* how can it scale?
* where can I reduce cost?

### Hands-on

* create a CloudWatch alarm
* inspect EC2 metrics
* view Lambda logs
* write 3 redesign ideas for a single-instance architecture

---

## SAA Week 8 — Exam prep week

### What to do

* domain-by-domain revision
* identify weak services
* do timed practice
* keep an “error notebook”
* retake only missed concepts, not everything

### Official exam resources

* SAA exam page and exam guide hub ([Amazon Web Services, Inc.][1])
* AWS certification prep plans and Skill Builder ([Amazon Web Services, Inc.][4])

### Pass criterion for yourself

Do not book the exam until:

* you can explain the main service choice in plain English
* your practice performance is consistently strong
* you can eliminate wrong answer choices by reasoning, not guessing

---

[1]: https://aws.amazon.com/certification/certified-solutions-architect-associate/?utm_source=chatgpt.com "AWS Certified Solutions Architect – Associate"
[2]: https://aws.amazon.com/certification/certified-developer-associate/?utm_source=chatgpt.com "AWS Certified Developer - Associate"
[3]: https://aws.amazon.com/certification/certified-devops-engineer-professional/?utm_source=chatgpt.com "AWS Certified DevOps Engineer – Professional"
[4]: https://aws.amazon.com/certification/certification-prep/?utm_source=chatgpt.com "Prepare for your AWS Certification Exam"
[5]: https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html?utm_source=chatgpt.com "What is IAM? - AWS Identity and Access Management"
[6]: https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html?utm_source=chatgpt.com "Policies and permissions in AWS Identity and Access ..."
[7]: https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html?utm_source=chatgpt.com "IAM roles - AWS Identity and Access Management"
[8]: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html?utm_source=chatgpt.com "What is Amazon EC2? - Amazon Elastic Compute Cloud"
[9]: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Instances.html?utm_source=chatgpt.com "Amazon EC2 instances - Amazon Elastic Compute Cloud"
[10]: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-best-practices.html?utm_source=chatgpt.com "Best practices for Amazon EC2"
[11]: https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html?utm_source=chatgpt.com "What is Amazon S3? - Amazon Simple Storage Service"
[12]: https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html?utm_source=chatgpt.com "Understanding and managing Amazon S3 storage classes"
[13]: https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-buckets-s3.html?utm_source=chatgpt.com "Creating, configuring, and working with Amazon S3 ..."
[14]: https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html?utm_source=chatgpt.com "What is Amazon VPC? - Amazon Virtual Private Cloud"
[15]: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.html?utm_source=chatgpt.com "Amazon VPC and Amazon RDS"
[16]: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html?utm_source=chatgpt.com "What is Amazon Relational Database Service (Amazon RDS)?"
[17]: https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html?utm_source=chatgpt.com "What is Amazon DynamoDB? - Amazon DynamoDB"
[18]: https://docs.aws.amazon.com/lambda/latest/dg/welcome.html?utm_source=chatgpt.com "What is AWS Lambda? - AWS Lambda"
[19]: https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html?utm_source=chatgpt.com "Amazon API Gateway - AWS Documentation"
[20]: https://docs.aws.amazon.com/apigateway/latest/developerguide/rest-api-develop.html?utm_source=chatgpt.com "Develop REST APIs in API Gateway"
[21]: https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html?utm_source=chatgpt.com "What is Amazon CloudWatch? - Amazon CloudWatch"
[22]: https://docs.aws.amazon.com/dynamodb/?utm_source=chatgpt.com "Amazon DynamoDB Documentation"
[23]: https://docs.aws.amazon.com/s3/?utm_source=chatgpt.com "Amazon Simple Storage Service Documentation"
[24]: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html?utm_source=chatgpt.com "What is CloudFormation?"
[25]: https://docs.aws.amazon.com/codepipeline/latest/userguide/welcome.html?utm_source=chatgpt.com "What is AWS CodePipeline? - AWS ..."
[26]: https://docs.aws.amazon.com/codebuild/latest/userguide/welcome.html?utm_source=chatgpt.com "What is AWS CodeBuild? - AWS CodeBuild"
[27]: https://docs.aws.amazon.com/codebuild/latest/userguide/concepts.html?utm_source=chatgpt.com "AWS CodeBuild concepts"
[28]: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-reference.html?utm_source=chatgpt.com "Introduction: CloudFormation Template Reference Guide"
[29]: https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html?utm_source=chatgpt.com "What is AWS Systems Manager? - ..."
[30]: https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html?utm_source=chatgpt.com "What is Amazon Elastic Container Registry? - Amazon ECR"
[31]: https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html?utm_source=chatgpt.com "What is Amazon Elastic Container Service?"
[32]: https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html?utm_source=chatgpt.com "What is Amazon EKS? - Amazon EKS"
[33]: https://docs.aws.amazon.com/codepipeline/latest/userguide/welcome-introducing.html?utm_source=chatgpt.com "A quick look at CodePipeline"
[34]: https://github.com/aws-samples?utm_source=chatgpt.com "AWS Samples"
[35]: https://github.com/awslabs/ec2-spot-workshops?utm_source=chatgpt.com "EC2 Spot Workshops"
[36]: https://github.com/aws-samples/serverless-patterns?utm_source=chatgpt.com "GitHub - aws-samples/serverless-patterns ..."
[37]: https://github.com/aws-samples/aws-serverless-workshops?utm_source=chatgpt.com "aws-samples/aws-serverless-workshops"
[38]: https://github.com/aws-samples/serverless-samples?utm_source=chatgpt.com "aws-samples/serverless-samples: This repository contains ..."
[39]: https://github.com/aws-samples/aws-serverless-webapp-workshop?utm_source=chatgpt.com "aws-samples/aws-serverless-webapp-workshop: Code ..."
[40]: https://github.com/aws-samples/eks-workshop-v2?utm_source=chatgpt.com "aws-samples/eks-workshop-v2: Hands-on labs for Amazon ..."
[41]: https://github.com/aws-samples/eks-workshop-developers?utm_source=chatgpt.com "aws-samples/eks-workshop-developers ..."
[42]: https://github.com/aws-samples/aws-serverless-saas-workshop?utm_source=chatgpt.com "aws-samples/aws-serverless-saas-workshop"
[43]: https://skillbuilder.aws/?utm_source=chatgpt.com "AWS Skill Builder"
[44]: https://docs.aws.amazon.com/ec2/?utm_source=chatgpt.com "Amazon Elastic Compute Cloud Documentation"
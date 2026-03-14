### The **beginner-friendly, fast-track, highly structured roadmap** for the three AWS certifications track:

1. **AWS Certified Solutions Architect – Associate (SAA-C03)(*Associate level*)**
2. **AWS Certified Developer – Associate (DVA-C02)(*Associate level*)**
3. **AWS Certified DevOps Engineer – Professional (DOP-C02)(*Professional level*)**

AWS lists SAA and DVA as associate-level certifications and DOP as a professional-level certification. AWS also notes that candidates with no IT work experience may benefit from first getting foundational AWS knowledge before attempting Developer Associate, which is why this roadmap starts from fundamentals and then builds upward. ([Amazon Web Services, Inc.][1])

## The best order

For a beginner who wants to move quickly, the smartest sequence is:

**Foundation → SAA → DVA → DOP**

Why this order:

* **SAA** builds broad AWS understanding: networking, compute, storage, databases, security, reliability. ([Amazon Web Services, Inc.][1])
* **DVA** then becomes much easier because you already understand the platform and can focus on building apps with Lambda, API Gateway, DynamoDB, IAM, and deployment. ([Amazon Web Services, Inc.][2])
* **DOP** is the hardest and expects comfort with CI/CD, infrastructure as code, monitoring, containers, and operations. ([Amazon Web Services, Inc.][3])

## My recommended pace

I’m going to assume you want a **serious fast-track plan** and can give this about **12–15 hours per week**. Under that assumption:

* **Weeks 1–8:** SAA
* **Weeks 9–14:** DVA
* **Weeks 15–22:** DOP

That is an **22-week roadmap**. It is aggressive, but realistic for a disciplined beginner.

---

# Phase 0 — Before starting any certification (2–3 days)

Your first goal is not “studying AWS.”
Your first goal is to make AWS feel normal.

## What to do

1. Create or clean up your AWS account.
2. Learn the console layout.
3. Install AWS CLI.
4. Install VS Code.
5. Learn basic terminal usage.
6. Set a strict note-taking structure:

   * service name
   * what problem it solves
   * when to use it
   * pricing intuition
   * security considerations
   * one hands-on lab

## Primary resources

Use AWS’s official certification prep hub and Skill Builder as your base. ([Amazon Web Services, Inc.][4])

## Your rule for the full journey

For every AWS service you study, answer these 5 questions:

1. What is it?
2. Why does it exist?
3. When should I use it?
4. What are the common mistakes?
5. What other AWS services does it connect with?

That single habit will make you learn much faster.

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

# Certification 2 — AWS Certified Developer – Associate (Weeks 9–14)

AWS positions Developer Associate as the certification for building, deploying, and debugging cloud-based applications on AWS. AWS also explicitly says people without IT work experience may benefit from first learning foundational AWS knowledge. ([Amazon Web Services, Inc.][2])

## What this certification is really about

This is the “build it correctly on AWS” cert.

You are shifting from:

* **architect thinking**
  to
* **developer + implementation thinking**

---

## DVA Week 9 — SDKs, CLI, IAM for applications, app auth basics

### Topics

* AWS CLI deeper usage
* SDK mental model
* IAM roles for compute
* app permissions
* secure credential handling

### Official docs

* IAM overview, roles, and policy behavior ([AWS Documentation][5])

### Beginner goal

Understand why application code should use roles instead of embedded credentials.

### Hands-on

* use AWS CLI to list resources
* run app code from EC2 or Lambda with a role
* verify access works without static credentials

---

## DVA Week 10 — Lambda deep dive

### Topics

* Lambda runtimes
* events
* environment variables
* logging
* permissions
* local development basics

### Official docs

* Lambda overview, runtimes, local development, first function ([AWS Documentation][18])

### Beginner goal

Know:

* how Lambda is invoked
* how permissions are granted
* where logs go
* how cold starts and execution environment matter conceptually

### Hands-on

* build two Lambda functions
* one HTTP-triggered
* one event-triggered
* inspect logs in CloudWatch
* test error handling

---

## DVA Week 11 — API Gateway + DynamoDB + basic serverless app building

### Topics

* HTTP API vs REST API idea
* route handling
* request/response flow
* DynamoDB CRUD, query vs scan
* local testing mindset

### Official docs

* API Gateway docs and serverless API getting started ([AWS Documentation][19])
* DynamoDB docs, API concepts, local development ([AWS Documentation][22])

### Beginner goal

Build a small CRUD application and understand each moving part.

### Hands-on

Build:

* create item
* list item
* update item
* delete item
  using:
* API Gateway
* Lambda
* DynamoDB

This single project will teach you more than hours of passive reading.

---

## DVA Week 12 — S3 integration, event-driven workflows, observability

### Topics

* S3 events
* Lambda triggers
* object metadata
* simple async pipelines
* CloudWatch logs and metrics for app debugging

### Official docs

* S3 docs and lifecycle/policy concepts ([AWS Documentation][23])
* CloudWatch docs ([AWS Documentation][21])

### Beginner goal

Understand how S3 can trigger downstream processing.

### Hands-on

* upload file to S3
* trigger Lambda
* write result to DynamoDB or another S3 location
* inspect logs

---

## DVA Week 13 — Deployment and infrastructure as code basics

### Topics

* CloudFormation basics
* stacks and templates
* simple deployment automation
* resource relationships

### Official docs

* CloudFormation overview, getting started, template guide, how stacks work ([AWS Documentation][24])

### Beginner goal

Understand that infrastructure is code, versioned, repeatable, and reviewable.

### Hands-on

* write or adapt a template that provisions:

  * S3 bucket
  * Lambda
  * IAM role
* deploy and update the stack

---

## DVA Week 14 — Exam prep week

### What to do

* re-run all key labs
* revise Lambda permissions, DynamoDB access patterns, API Gateway flow
* review deployment and observability
* do practice questions with strict timing

### Official exam resources

* DVA exam page and exam guide ([Amazon Web Services, Inc.][2])
* AWS prep hub / Skill Builder ([Amazon Web Services, Inc.][4])

---

# Certification 3 — AWS Certified DevOps Engineer – Professional (Weeks 15–22)

AWS positions DOP-C02 as a professional-level certification focused on implementing and managing continuous delivery systems and provisioning, operating, and managing distributed systems and services on AWS. ([Amazon Web Services, Inc.][3])

## What this certification is really about

This is not just “DevOps tools.”

It is about:

* repeatable infrastructure
* automated delivery
* observability
* operational safety
* recovery
* secure deployments
* container and platform operations

---

## DOP Week 15 — DevOps foundations, CI/CD mental model

### Topics

* source → build → test → deploy pipeline thinking
* deployment strategies
* artifacts
* rollback idea
* environment promotion

### Official docs

* CodePipeline overview, getting started, concepts, tutorials ([AWS Documentation][25])
* CodeBuild overview and getting started ([AWS Documentation][26])

### Beginner goal

Be able to describe what each stage in a delivery pipeline does.

### Hands-on

* create a very small CodePipeline
* add source stage
* add build stage
* inspect artifacts and logs

---

## DOP Week 16 — CodeBuild, buildspec, test automation

### Topics

* build environments
* buildspec.yml
* test execution
* artifacts
* logs and debugging failed builds

### Official docs

* CodeBuild concepts and buildspec reference ([AWS Documentation][27])

### Hands-on

* create a build project
* run tests
* intentionally break the build
* fix it and document the failure cause

---

## DOP Week 17 — Infrastructure as code at operational depth

### Topics

* CloudFormation stack lifecycle
* template structure
* safe updates
* best practices
* drift awareness mindset

### Official docs

* CloudFormation template reference and best practices ([AWS Documentation][28])

### Hands-on

* deploy a multi-resource stack
* update it safely
* practice rollback thinking
* split large infrastructure into logical pieces conceptually

---

## DOP Week 18 — Monitoring, alarms, logs, dashboards, operational visibility

### Topics

* metrics
* logs
* dashboards
* alerting
* root-cause workflow
* basic observability habits

### Official docs

* CloudWatch overview, metrics, dashboards, logs ([AWS Documentation][21])

### Hands-on

* create app and infra dashboards
* set alarms
* investigate a simulated failure
* create a simple runbook note

---

## DOP Week 19 — Systems Manager and operational automation

### Topics

* Systems Manager overview
* SSM Agent
* documents
* Parameter Store
* operational tasks at scale

### Official docs

* Systems Manager overview, agent, documents, Parameter Store ([AWS Documentation][29])

### Beginner goal

Understand how operations teams manage nodes and configuration without manually touching every machine.

### Hands-on

* store config in Parameter Store
* read it from an app or script
* review an SSM document
* understand how agent-based operations work

---

## DOP Week 20 — Containers: ECR, ECS, EKS basics

### Topics

* container image registry
* push/pull workflow
* ECS task definitions
* task roles
* EKS concepts at a high level
* when ECS is simpler than EKS

### Official docs

* ECR overview and image scanning ([AWS Documentation][30])
* ECS overview, getting started, task definitions, task IAM role ([AWS Documentation][31])
* EKS overview, getting started, cluster creation, IAM roles for service accounts ([AWS Documentation][32])

### Hands-on

* build a Docker image
* push it to ECR
* deploy to ECS
* read a task definition
* understand where app permissions come from

---

## DOP Week 21 — Reliability, deployment safety, rollback thinking

### Topics

* blue/green vs rolling thinking
* safe rollout mindset
* monitoring during deploy
* failure handling
* operational game-day mindset

### Official docs

* CodePipeline deployment integrations and release workflow concepts ([AWS Documentation][33])
* CloudWatch and CloudFormation best practices ([AWS Documentation][21])

### Hands-on

* update an application
* define what signals would tell you to rollback
* write a one-page deployment checklist

---

## DOP Week 22 — Exam prep week

### What to do

* full review of CI/CD, CloudFormation, CloudWatch, Systems Manager, ECS/EKS, ECR
* re-run hands-on labs
* do timed practice
* fix only your weakest operational topics

### Official exam resources

* DOP exam page and guide ([Amazon Web Services, Inc.][3])
* AWS prep plans on Skill Builder ([Amazon Web Services, Inc.][4])

---

# Best GitHub repos to use during the journey

These are especially useful because they are hands-on and practical.

### For Solutions Architect / general AWS practice

* **AWS Samples org** — broad collection of official example projects and patterns. ([GitHub][34])
* **EC2 Spot Workshops** — great for learning compute cost/performance patterns and EC2 operational ideas. ([GitHub][35])

### For Developer Associate

* **aws-samples/serverless-patterns** — tons of real integration examples across Lambda, event-driven design, and IaC. ([GitHub][36])
* **aws-samples/aws-serverless-workshops** — guided hands-on workshops for Lambda, API Gateway, DynamoDB, Step Functions, Kinesis, and more. ([GitHub][37])
* **aws-samples/serverless-samples** — end-to-end serverless examples including CI/CD and observability. ([GitHub][38])
* **aws-samples/aws-serverless-webapp-workshop** — excellent beginner project for S3 + Cognito + API Gateway + Lambda + DynamoDB. ([GitHub][39])

### For DevOps Engineer Professional

* **aws-samples/eks-workshop-v2** — hands-on labs for Amazon EKS. ([GitHub][40])
* **aws-samples/eks-workshop-developers** — developer-focused EKS and microservices learning. ([GitHub][41])
* **aws-samples/aws-serverless-saas-workshop** — useful for understanding more production-like multi-service deployment patterns. ([GitHub][42])

---

# Your weekly tracking schedule

Use this every week.

| Week |                       Main Focus | Hours | Must Finish                    | Output for Yourself  |
| ---- | -------------------------------: | ----: | ------------------------------ | -------------------- |
| 0    |                            Setup |     6 | AWS account, CLI, notes system | Working environment  |
| 1    |                 IAM + AWS basics |    12 | IAM, policies, roles           | 1-page IAM notes     |
| 2    |                    EC2 + scaling |    12 | launch EC2, instance types     | working EC2 demo     |
| 3    |                     S3 + storage |    12 | buckets, versioning, lifecycle | S3 lab notes         |
| 4    |                 VPC + networking |    15 | VPC, subnets, routing          | drawn architecture   |
| 5    |                   RDS + DynamoDB |    15 | DB labs                        | comparison notes     |
| 6    |             Lambda + API Gateway |    15 | serverless mini app            | API demo             |
| 7    | CloudWatch + architecture review |    12 | alarms, redesign practice      | review notebook      |
| 8    |                         SAA prep |    15 | practice + revision            | exam readiness check |
| 9    |             CLI/SDK/IAM for apps |    12 | secure app access              | app auth notes       |
| 10   |                 Lambda deep dive |    15 | logs, events, permissions      | Lambda mini labs     |
| 11   |       API Gateway + DynamoDB app |    15 | CRUD app                       | project complete     |
| 12   |        S3 events + observability |    12 | async pipeline                 | event-driven demo    |
| 13   |            CloudFormation basics |    12 | first stack                    | IaC notes            |
| 14   |                         DVA prep |    15 | practice + revision            | exam readiness check |
| 15   |                   CI/CD concepts |    12 | first pipeline                 | pipeline notes       |
| 16   |                        CodeBuild |    12 | buildspec, tests               | build demo           |
| 17   |         CloudFormation deepening |    12 | multi-resource stack           | IaC revision         |
| 18   |            CloudWatch operations |    12 | dashboard + alarms             | ops notes            |
| 19   |                  Systems Manager |    12 | Parameter Store + docs         | ops automation notes |
| 20   |                    ECR + ECS/EKS |    15 | image to container deploy      | container demo       |
| 21   |                deployment safety |    12 | rollback/runbook thinking      | deploy checklist     |
| 22   |                         DOP prep |    15 | practice + revision            | exam readiness check |

---

# Your daily study template

Use this every study day.

| Block   |   Time | What to do                                    |
| ------- | -----: | --------------------------------------------- |
| Block 1 | 45 min | Learn one concept from official docs          |
| Block 2 | 45 min | Watch/read explanation from AWS prep material |
| Break   | 10 min | Reset                                         |
| Block 3 | 60 min | Hands-on lab                                  |
| Block 4 | 20 min | Write notes in your own words                 |
| Block 5 | 20 min | 5–10 practice questions                       |
| Block 6 | 10 min | Log mistakes and tomorrow’s target            |

That is the fastest beginner-friendly format because it avoids passive learning.

---

# How to keep yourself on track

Use a simple scoring system every Sunday.

## Weekly self-check

Give yourself a score from 0–2 for each:

* I finished the official docs I planned
* I completed the hands-on lab
* I can explain the week’s main services without notes
* I updated my mistake notebook
* I practiced questions under time pressure

**8–10:** on track
**5–7:** acceptable but tighten up
**0–4:** do not move ahead; patch the weak area first

---

# The most important beginner rule

Do **not** try to memorize every AWS service.

Instead, master these service families first:

* **Identity/Security:** IAM
* **Compute:** EC2, Lambda
* **Storage:** S3, EBS
* **Networking:** VPC
* **Database:** RDS, DynamoDB
* **Observability:** CloudWatch
* **Dev workflows:** CodePipeline, CodeBuild, CloudFormation
* **Containers:** ECR, ECS, EKS
* **Operations:** Systems Manager

That set covers the majority of what matters across these three certifications. ([AWS Documentation][5])

---

# My recommendation for you specifically

Since you want to move fast, do this:

* **Book only the first certification mentally, not all three at once**
* Finish **SAA first**
* Build **one mini serverless project** during DVA
* Build **one CI/CD + container deployment project** during DOP

That gives you:

* certification progress
* actual skill
* resume material
* interview talking points

---

# Best “straightforward fast-track” resource stack

Keep your stack simple:

1. **AWS official exam page + exam guide** for scope. ([Amazon Web Services, Inc.][1])
2. **AWS Skill Builder** for structured prep. ([skillbuilder.aws][43])
3. **Official AWS docs** for service-by-service learning. ([AWS Documentation][44])
4. **GitHub workshops/repos** for hands-on work. ([GitHub][37])
5. **Your own mistake notebook** for exam prep.

That is cleaner and faster than juggling 20 random courses.


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

# Certification 1 — AWS Certified Solutions Architect – Associate (2‑Week Accelerated Tracker)

Use this tracker to complete the SAA-C03 roadmap in 14 days. Fill `Date`, update `Status`, add short `Feedback`, and `Notes` after each study session.

How to use:

- Set `Date` for each day when you study.
- Mark `Status` as `Not started` / `In progress` / `Done`.
- Keep `Feedback` short (what was hard, what to revisit).
- Use `Notes` for commands, AWS console paths, or links.

---

## Week 1 — Days 1–7 (Core fundamentals + Compute + Storage + Networking)

| Day | Date | Focus | Key Topics | Hands-on / Tasks | Status | Feedback | Notes |
|-----|------|-------|------------|------------------|--------|----------|-------|
| Day 1 |  | AWS basics & global infra / IAM | Regions, AZs, edge locations, Shared responsibility, IAM users/groups/roles, least privilege | Create non-root admin user; create IAM role for EC2; attach managed policy; read a sample policy JSON | Not started |  |  |
| Day 2 |  | IAM deep dive | IAM policies, policy simulator, temporary credentials, roles vs keys | Use Policy Simulator; create role with trust policy; test STS AssumeRole (or document steps) | Not started |  |  |
| Day 3 |  | EC2 fundamentals | Instance types, AMIs, EBS vs instance store, security groups | Launch Linux EC2; SSH in; install nginx; stop/start; compare 2 instance types | Not started |  |  |
| Day 4 |  | Auto Scaling & Load Balancing | Auto Scaling groups, ELB types, health checks | Create simple ASG (or document autoscaling steps); create ALB and target group; register instance | Not started |  |  |
| Day 5 |  | Storage basics: S3, EBS, EFS | Object vs block vs file; S3 classes, bucket policies, versioning | Create S3 bucket; upload files; enable versioning; add lifecycle rule; create EBS volume and attach (if possible) | Not started |  |  |
| Day 6 |  | Networking part 1: VPC basics | VPC, subnets, route tables, IGW, NAT, public vs private | Inspect default VPC; create custom VPC; make one public + one private subnet; launch instance in each and test connectivity | Not started |  |  |
| Day 7 |  | Networking part 2: Security | Security Groups vs NACLs, route tables, VPC for RDS | Diagram 1 VPC with 2 public + 2 private subnets; explain public/private differences; create SG and NACL examples | Not started |  |  |

---

## Week 2 — Days 8–14 (Databases, Serverless, Monitoring, Exam prep)

| Day | Date | Focus | Key Topics | Hands-on / Tasks | Status | Feedback | Notes |
|-----|------|-------|------------|------------------|--------|----------|-------|
| Day 8 |  | Databases intro | RDS basics, Multi-AZ, read replicas, backups, DynamoDB basics, partition key | Launch simple RDS (or review console steps); create DynamoDB table; perform CRUD via console or AWS CLI | Not started |  |  |
| Day 9 |  | Databases deep dive | When to choose RDS vs DynamoDB, latency vs scalability | Design a sample schema for RDS vs a DynamoDB access pattern; note partition key choices | Not started |  |  |
| Day 10 |  | Serverless fundamentals | Lambda, API Gateway, event-driven patterns, decoupling | Create Lambda function; connect to API Gateway; return JSON; write a simple item to DynamoDB | Not started |  |  |
| Day 11 |  | Integration & patterns | SQS, SNS, Step Functions, event-driven retries | Build a small flow (or diagram) using API-GW → Lambda → SQS → Lambda | Not started |  |  |
| Day 12 |  | Monitoring & ops | CloudWatch metrics, logs, alarms; Well‑Architected pillars; cost optimisation | Create CloudWatch alarm; view EC2/Lambda logs; note 3 ideas to reduce cost for a single-instance app | Not started |  |  |
| Day 13 |  | Revision: Weak spots | Revisit weak services identified earlier; timed practice | Do 1–2 timed practice sets focused on weak domains; update error notebook | Not started |  |  |
| Day 14 |  | Exam prep & mock test | Domain-by-domain revision, timed practice, exam strategy | Take final timed mock exam (65 Q / 130 min or shorter practice); review mistakes; update error notebook | Not started |  |  |

---

## Daily checklist (copy per day or use as reference)

- [ ] Read official doc summary (30–60m)
- [ ] Hands-on lab / console (30–90m)
- [ ] Write 3 concise notes: Why choose this service; Risks/failures; Cost considerations (15–30m)
- [ ] Add one exam-style reasoning note (how to eliminate wrong choices)

---

## Progress & Exam Readiness

| Metric | Target | Current |
|--------|--------:|--------:|
| Total study days completed | 14 | 0 |
| Hands-on labs completed | 10+ | 0 |
| Timed practice score (avg) | 75%+ | 0% |
| Weak topics logged | — | 0 |

---

## Notes / Links

- Official exam guide & resources: https://aws.amazon.com/certification/certified-solutions-architect-associate/
- Keep an `error notebook.md` in the course folder to list missed practice questions and root causes.

---

If you want, I can:

- populate the `Date` column for the next 14 calendar days, or
- convert this into a printable checklist per day, or
- create a simple CSV tracker you can open in a spreadsheet.


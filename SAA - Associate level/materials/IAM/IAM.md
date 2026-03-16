## What is IAM? — Complete Breakdown

---

### The one-line definition

IAM = the **security system** of your entire AWS account. It controls who can log in and what they can do once logged in.

---

### Two core jobs of IAM

```
Job 1: Authentication  →  controls who can SIGN IN
Job 2: Authorization   →  controls what they can DO
```

Every other feature of IAM exists to support these two jobs.

---

### Identities — who lives inside IAM

When you first create an AWS account, only ONE identity exists:

**Root user** — created automatically. Has complete, unrestricted access to everything. No policy can limit it. Think of it as the master key that unlocks every door.

Then you use IAM to create additional identities:

```
Root user
    ↓ creates
IAM Users     → individual humans (pratikrauniyar)
IAM Roles     → services and applications (Lambda, EC2)
IAM Groups    → collections of users (Developers, Admins)
```

Each of these gets exactly the permissions you give them — nothing more.

---

### Access Management — how permissions flow

The doc describes this flow:

```
1. User created in IAM
        ↓
2. User signs in with credentials
        ↓
3. IAM matches credentials to a principal
   (user / role / federated identity)
        ↓
4. Principal makes a request to do something
   e.g. "I want to read this S3 bucket"
        ↓
5. IAM checks: does this principal have permission?
        ↓
6. Yes → action executes
   No  → Access Denied
```

**Interesting detail from the doc:**

When you first log into the console and land on the home page — you're authenticated but not yet making any service requests. The moment you click on S3 or EC2, that's when an authorization request fires. IAM then checks three things:

```
1. Is your identity on the authorized list?
2. What policies control your access level?
3. Are any other policies in effect?
```

All three must clear before you get access.

---

### Eventually Consistent — an important gotcha

This is something most beginners don't know and it causes confusion.

IAM replicates your changes across **multiple servers worldwide** to ensure high availability. This replication takes time — it's not instant.

**What this means practically:**

```
You create a new IAM user
        ↓
IAM says "successfully created"
        ↓
You immediately try to use that user
        ↓
Sometimes → Access Denied or user not found
        ↓
Wait 10-30 seconds and try again
        ↓
Now it works
```

The same applies to:
- Creating or updating users
- Creating or updating groups
- Creating or updating roles
- Creating or updating policies

**The doc's advice:**
> Don't put IAM changes in critical high-availability code paths. Make IAM changes in a separate setup routine and verify they've propagated before depending on them.

In simple terms — don't create a user and immediately try to use them in the same script without a delay or verification check.

---

### Cost — what does IAM cost?

This surprises many beginners:

```
IAM itself          → FREE
IAM Identity Center → FREE
AWS STS             → FREE
```

You pay nothing for:
- Creating users, groups, roles
- Attaching policies
- Making authentication/authorization requests
- Using the CLI/console to manage IAM

**You only pay when** those IAM users/roles access other AWS services:
```
IAM user reads S3 bucket    → charged for S3 usage
IAM role starts EC2         → charged for EC2 usage
IAM user writes to DynamoDB → charged for DynamoDB usage
```

**One exception:**
IAM Access Analyzer has some paid features:
- External access analysis → free
- Unused access analysis → paid
- Customer policy checks → paid

---

### Integration — IAM works with everything

IAM is not standalone. Every single AWS service is wired into it:

```
S3        → IAM controls who can read/write buckets
EC2       → IAM controls who can start/stop instances
Lambda    → IAM roles control what functions can access
DynamoDB  → IAM controls who can read/write tables
RDS       → IAM controls database access
CloudWatch→ IAM controls who can view logs/metrics
```

Literally every AWS service checks IAM before doing anything. IAM is the one service that touches all others.

---

### The 3 extra things this doc covers

**1. Principal** — a fancy word for "whoever is making the request." Could be:
```
A human IAM user        → pratikrauniyar
An IAM role             → LambdaAccessRole
A federated identity    → company SSO user
An application          → your code using SDK
Another AWS account     → cross-account access
```

**2. Cross-account requests** — authorization requests can come from:
```
Your own account   → normal case
Another AWS account you trust → cross-account access
```
This is how large companies with multiple AWS accounts share resources between them.

**3. What authorized principals can actually do:**
The doc gives concrete examples:
```
Launch a new EC2 instance
Modify IAM group membership
Delete S3 buckets
```
Anything in AWS is an action. IAM controls all of them.

---

### Everything in one picture

```
┌─────────────────────────────────────────────┐
│              AWS ACCOUNT                     │
│                                             │
│  ┌─────────┐                                │
│  │  ROOT   │ ← one per account, god mode    │
│  │  USER   │                                │
│  └─────────┘                                │
│                                             │
│  ┌──────────────────────────────────────┐   │
│  │              IAM                     │   │
│  │  (free service, controls everything) │   │
│  │                                      │   │
│  │  Users   → humans                    │   │
│  │  Groups  → collections of users      │   │
│  │  Roles   → services/apps             │   │
│  │  Policies→ permission documents      │   │
│  └──────────────────────────────────────┘   │
│           ↓ controls access to ↓            │
│  ┌──────────────────────────────────────┐   │
│  │  S3 | EC2 | Lambda | DynamoDB | RDS  │   │
│  │  CloudWatch | SQS | SNS | and 200+   │   │
│  │  other AWS services                  │   │
│  └──────────────────────────────────────┘   │
│                                             │
└─────────────────────────────────────────────┘
```

---

### 5 key takeaways from this doc

**1.** IAM is free — use it as much as you want, zero cost for IAM itself.

**2.** Root user exists automatically — lock it away after initial setup, never use daily.

**3.** IAM changes are eventually consistent — allow a few seconds after making changes before using them.

**4.** Authorization requests fire on every action — clicking S3 in the console sends an auth request. Running any CLI command sends an auth request. Every single time.

**5.** IAM integrates with every AWS service — there is no AWS service that bypasses IAM. It is the foundation everything else is built on.
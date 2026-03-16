## How IAM Works — Deep Dive

This doc explains what happens **under the hood** every single time you or any service tries to do anything in AWS. Understanding this makes everything else click.

---

### The big flow — 3 steps every request goes through

```
Step 1: Authentication  →  Who are you?
Step 2: Authorization   →  What are you allowed to do?
Step 3: Action          →  OK, go do it
```

Every single AWS request — whether you click a button in the console, run a CLI command, or your Lambda function calls DynamoDB — goes through all 3 steps every time.

---

### Step 1 — Authentication (Who are you?)

Before AWS does anything, it needs to confirm your identity. Different types of principals authenticate differently:

**Root user:**
```
Email + Password
→ Full access to everything
→ Can't be restricted
```

**IAM user (you right now):**
```
Console  →  Account ID + Username + Password
CLI/SDK  →  Access Key + Secret Key
           OR aws login (browser session)
```

**Federated user (SSO/company login):**
```
Your identity provider (Google, Okta, AD)
authenticates you first
→ Passes your credentials to AWS
→ You never log into AWS directly
```

**IAM Role (for services like Lambda, EC2):**
```
Service requests temporary credentials
→ AWS STS issues short-lived tokens
→ Service uses those tokens automatically
→ Tokens expire and refresh automatically
```

**Anonymous users** — only a tiny handful of AWS services allow this (like public S3 buckets). Everything else requires authentication.

---

### Step 2 — Authorization (What can you do?)

Once AWS knows who you are, every request you make contains 5 pieces of information that IAM evaluates:

**1. Actions** — what you're trying to do
```
s3:GetObject         → read a file from S3
ec2:StartInstances   → start an EC2 server
iam:CreateUser       → create a new IAM user
dynamodb:PutItem     → write to DynamoDB
```

**2. Resources** — what specific thing you're acting on
```
arn:aws:s3:::my-bucket/*          → all files in my-bucket
arn:aws:ec2:us-east-1::instance/* → all EC2 instances
arn:aws:iam::xxxxxxxxxxxx:user/*  → all IAM users in account
```

**3. Principal** — who is making the request (you)
```
arn:aws:iam::xxxxxxxxxxxx:user/pratikrauniyar
```

**4. Environment data** — context about the request
```
IP address      → where is the request coming from?
Timestamp       → what time is it?
SSL enabled     → is the connection secure?
User agent      → CLI? Console? SDK?
```

**5. Resource data** — details about the target
```
DynamoDB table name
EC2 instance tags
S3 bucket region
```

AWS bundles all 5 into a **request context** and sends it to IAM to evaluate.

---

### The authorization decision rules — in exact order

This is the most important thing to understand. IAM follows these rules in this exact sequence:

```
Rule 1: Everything is DENIED by default
        (if no policy says yes → the answer is no)
            ↓
Rule 2: An explicit ALLOW in any policy overrides the default deny
        (someone gave you permission → you can do it)
            ↓
Rule 3: Boundaries/SCPs/session policies can OVERRIDE the allow
        (organization-level restrictions can block even allowed actions)
            ↓
Rule 4: An explicit DENY anywhere ALWAYS wins
        (if any policy says no → final answer is no, no matter what)
```

**The most critical rule: Explicit DENY always wins over everything.**

Example that trips people up:
```
Policy 1: Allow s3:DeleteObject  ← you added this
Policy 2: Deny  s3:DeleteObject  ← your org added this

Result: DENIED — the deny wins, always
```

This is why when you can't do something even though you think you have permission — always look for a hidden Deny somewhere.

---

### Visualizing the full request flow

```
You run: aws s3 ls --profile learning
              ↓
AWS receives request containing:
  - Action:    s3:ListBuckets
  - Principal: arn:aws:iam::xxxxxxxxxxxx:user/pratikrauniyar
  - Resource:  *
  - Env data:  your IP, timestamp, CLI user-agent
              ↓
IAM authenticates: "Is this really pratikrauniyar?"
  → Checks your session token
  → Yes, confirmed ✓
              ↓
IAM authorizes: "Can pratikrauniyar do s3:ListBuckets?"
  → Default deny applied first
  → Checks all policies attached to you
  → Checks groups you belong to
  → Checks any org-level SCPs
  → Checks for any explicit Denies
  → Finds Allow → no Denies blocking it
  → ALLOWED ✓
              ↓
S3 service executes: lists your buckets
              ↓
Returns result to your terminal
```

---

### Types of policies IAM evaluates

IAM doesn't just check one policy — it checks ALL of these that apply to you:

**Identity-based policies** — attached to YOU (user, group, role)
```json
{
  "Effect": "Allow",
  "Action": "s3:*",
  "Resource": "*"
}
```
Most common type. Controls what your identity can do.

**Resource-based policies** — attached to the RESOURCE itself
```json
{
  "Effect": "Allow",
  "Principal": {"AWS": "arn:aws:iam::xxxxxxxxxxxx:user/pratikrauniyar"},
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::my-bucket/*"
}
```
The S3 bucket itself says who can access it. Enables cross-account access.

**Permissions boundaries** — max limit on what a user/role can ever do
```
Even if a policy grants s3:DeleteBucket
If the boundary doesn't include s3:DeleteBucket
→ The user CANNOT delete buckets
```
Like a ceiling — policies can grant up to the boundary, never beyond it.

**Session policies** — temporary limits for assumed role sessions
```
You assume a role that has full S3 access
But your session policy limits it to read-only
→ You only get read-only for this session
```

**AWS Organizations SCPs** — org-wide restrictions applied to entire accounts
```
Your org says: "No one in this account can use eu-west-1"
Even if YOUR policy allows eu-west-1
→ You cannot use eu-west-1
```

**For a request to succeed ALL applicable policies must allow it:**
```
Identity policy  → Allow ✓
Resource policy  → Allow ✓
Boundary         → Allow ✓
SCP              → Allow ✓
No explicit Deny anywhere ✓
→ REQUEST SUCCEEDS
```

If even ONE says Deny or doesn't cover it → request fails.

---

### IAM supports over 40 actions on users alone

The doc mentions this to show how granular permissions can get. Just for IAM users:

```bash
# Just a sample of IAM user actions:
iam:CreateUser          → create a user
iam:DeleteUser          → delete a user
iam:GetUser             → view a user
iam:UpdateUser          → modify a user
iam:ListUsers           → list all users
iam:CreateLoginProfile  → give user console access
iam:DeleteLoginProfile  → remove console access
iam:AttachUserPolicy    → attach a policy to user
iam:DetachUserPolicy    → remove a policy from user
iam:AddUserToGroup      → add user to a group
iam:RemoveUserFromGroup → remove user from group
```

This means you can create a policy that allows someone to list users but not create them, or view a user but not modify them. Extremely granular.

---

### Conditions — making policies smarter

Policies can have conditions that make them context-aware:

**Only allow access from a specific IP:**
```json
{
  "Effect": "Allow",
  "Action": "s3:*",
  "Resource": "*",
  "Condition": {
    "IpAddress": {
      "aws:SourceIp": "203.0.113.0/24"
    }
  }
}
```

**Only allow access after a certain date:**
```json
{
  "Effect": "Allow",
  "Action": "s3:GetObject",
  "Resource": "*",
  "Condition": {
    "DateGreaterThan": {
      "aws:CurrentTime": "2025-01-01T00:00:00Z"
    }
  }
}
```

**Only allow when MFA is active:**
```json
{
  "Effect": "Allow",
  "Action": "*",
  "Resource": "*",
  "Condition": {
    "Bool": {
      "aws:MultiFactorAuthPresent": "true"
    }
  }
}
```

This last one is powerful — it forces MFA for everything. Without MFA verified, even valid credentials get denied.

---

### The complete picture in one diagram

```
Principal makes request
        ↓
┌─────────────────────────────┐
│     AUTHENTICATION          │
│  Is this really who         │
│  they claim to be?          │
│  Password / Token / Key     │
└─────────────┬───────────────┘
              ↓ YES
┌─────────────────────────────┐
│     AUTHORIZATION           │
│                             │
│  1. Default DENY            │
│  2. Check all policies      │
│     - Identity policies     │
│     - Resource policies     │
│     - Boundaries            │
│     - SCPs                  │
│  3. Any explicit DENY?      │
│     → DENIED (final)        │
│  4. Any ALLOW found?        │
│     → ALLOWED               │
└─────────────┬───────────────┘
              ↓ ALLOWED
┌─────────────────────────────┐
│     ACTION EXECUTES         │
│  Creates EC2 / Reads S3 /   │
│  Writes DynamoDB etc.       │
└─────────────────────────────┘
```

---

### The 3 things to always remember

**1. Default is always deny** — AWS never gives access unless explicitly told to. Zero trust by default.

**2. Explicit deny always wins** — if anything says no, the answer is no. Order doesn't matter, one deny kills the whole request.

**3. Every request is evaluated fresh** — IAM doesn't cache "you were allowed last time." Every single request goes through the full evaluation every time.
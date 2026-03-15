# 🚀 AWS Toolkit for VS Code — Beginner's Complete Guide

A **comprehensive, hands-on tutorial** that takes you from **complete beginner to confidently deploying serverless applications directly from VS Code** using the **AWS Toolkit extension**.

> **📝 Note**: This guide is written for people new to AWS. We'll go step-by-step with clear explanations, expected outputs, and helpful visuals.

---

## 🎯 What You'll Learn

By the end of this guide, you'll be able to:
- Set up AWS Toolkit in VS Code
- Connect your AWS account safely
- Deploy your first Lambda function (serverless code)
- Debug your applications locally
- Monitor your applications in production
- Deploy complete applications using infrastructure as code

---

# 📑 Table of Contents

* [1. Overview — What is AWS Toolkit?](#1-overview)
* [2. Prerequisites — What You Need](#2-prerequisites)
* [3. Step-by-Step Installation](#3-installation--setup)
* [4. How AWS Toolkit Works (Architecture)](#4-aws-toolkit-architecture)
* [5. Connecting to Your AWS Account](#5-authentication-methods)
* [6. Understanding the AWS Explorer Interface](#6-aws-explorer-interface-guide)
* [7. Foundation Activities — Start Here](#7-hands-on-activities--foundation)
* [8. Advanced Activities — Next Level](#8-hands-on-activities--proficiency)
* [9. Deployment Pipelines Explained](#9-deployment-pipelines)
* [10. Debugging & Monitoring Your Applications](#10-debugging--observability)
* [11. Quick Reference & Commands](#11-quick-reference)
* [12. Troubleshooting Common Problems](#12-troubleshooting-guide)
* [13. Best Practices & Optimization](#13-best-practices--optimization)
* [14. Knowledge Check](#14-knowledge-check)
* [15. Configuration Templates](#15-appendix-config-templates)

---

# 1. Overview — What is AWS Toolkit?

## What Does AWS Toolkit Do?

The **AWS Toolkit for VS Code** is an **extension that connects VS Code (your code editor) directly to Amazon AWS (the cloud platform)**. Instead of switching between different tools, you can do everything from VS Code:

- **Write code** → **deploy it to AWS** → **monitor it** → all without leaving your IDE!

### Real-World Analogy
Think of it like a **remote control for AWS**. Without it, you'd use the AWS website (console). With it, you get a **keyboard shortcut remote** that's faster and more integrated.

### What Can You Do?

| Feature           | What It Does | Real Example |
| ----------------- | ------------------------- | --- |
| **AWS Explorer** | See all your AWS services in a sidebar | Click to view all your Lambda functions without opening AWS website |
| **Lambda Deployment** | Deploy your code to AWS servers instantly | Write a function locally, hit Deploy, it's live in seconds |
| **SAM Integration** | Build serverless applications easily | Toolkit helps manage all the configuration for you |
| **CloudFormation** | Define infrastructure as code | Describe your servers/databases in YAML, deploy automatically |
| **CloudWatch Logs** | Watch your app's activity in real-time | See what your app did, errors, performance |
| **Step Functions** | Create workflow chains | Make Lambda1 run, then Lambda2, then Lambda3 automatically |
| **Local Debugging** | Test your code before deploying | Catch bugs on your computer, not in production |

---

# 2. Prerequisites — What You Need

## Hardware & Software

Before you start, make sure you have these installed on your computer:

| Requirement | Version | Why You Need It | Installation |
| ----------- | ------------- | --- | --- |
| **VS Code** | Latest stable (v1.80+) | Your code editor | [Download here](https://code.visualstudio.com) |
| **Node.js** | ≥ 18 LTS | Runs JavaScript applications | [Download here](https://nodejs.org) - Choose LTS |
| **Python** | ≥ 3.9 | For Python Lambda functions | [Download here](https://www.python.org) |
| **Docker** | Latest | Runs containers (needed for local testing) | [Download here](https://www.docker.com/products/docker-desktop) |
| **AWS CLI** | v2 | Command-line tool for AWS | [Installation guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) |
| **SAM CLI** | Latest | Builds & deploys serverless apps | Run: `pip install aws-sam-cli` |

### Verify Your Installation

Open a terminal and run these commands to check:

```bash
# Check Node.js
node --version
# Should print: v18.x.x or higher

# Check Python
python3 --version
# Should print: Python 3.9 or higher

# Check AWS CLI
aws --version
# Should print: aws-cli/2.x.x

# Check Docker
docker --version
# Should print: Docker version 20.x.x or higher
```

**Expected Output Example:**
```
$ node --version
v18.17.1
$ python3 --version
Python 3.11.4
$ aws --version
aws-cli/2.13.0 Python/3.11.4 Linux/5.15.0
$ docker --version
Docker version 24.0.0, build abcdef
```

---

## AWS Account & Credentials

You need an **AWS Account** with proper permissions set up:

### Step 1: Create an AWS Account (If You Don't Have One)
1. Go to [AWS Console](https://console.aws.amazon.com)
2. Click "Create an AWS Account"
3. Follow the sign-up process (will need credit card)

### Step 2: Create an IAM User (Don't Use Root Account!)
> ⚠️ **Important**: Never use your root AWS account for daily work. Create a separate user.

1. Log into AWS Console
2. Go to **IAM** (Identity and Access Management)
3. Click **Users** → **Create user**
4. Give it a name like `my-dev-user`
5. Attach policy: `AdministratorAccess` (for learning; restrict later)
6. Create **Access Keys** (not password)
7. **Save your Access Key ID and Secret Access Key** somewhere safe

### Step 3: Recommended IAM Policy
If you want fine-grained permissions, use this policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "lambda:*",
        "s3:*",
        "cloudformation:*",
        "logs:*",
        "dynamodb:*",
        "apigateway:*",
        "iam:GetRole",
        "iam:PassRole",
        "cloudwatch:*",
        "events:*"
      ],
      "Resource": "*"
    }
  ]
}
```

---

# 3. Step-by-Step Installation

## 3.1 Install AWS Toolkit Extension

### Step 1: Open VS Code
Launch VS Code on your computer.

### Step 2: Go to Extensions
Press these keys:
```
Cmd + Shift + X    (Mac)
Ctrl + Shift + X   (Windows/Linux)
```

**What you'll see:**
A sidebar will open on the left showing "Extensions" with a search box.

![Image placeholder: VS Code Extensions Panel](https://via.placeholder.com/400x300?text=VS+Code+Extensions+Panel)

### Step 3: Search for AWS Toolkit
In the search box, type:
```
AWS Toolkit
```

**What you'll see:**
Several results will appear. Look for **"AWS Toolkit"** published by **Amazon Web Services**.

### Step 4: Install the Extension
Click the blue **Install** button next to "AWS Toolkit".

**Expected Output:**
- The button will change to "Installing..." for 10-20 seconds
- Then it will change to "Uninstall"
- After a few seconds, you'll see an AWS logo (orange/yellow square) in the left sidebar

### Step 5: Verify Installation
Look at the left sidebar. You should now see an **AWS icon** (orange square). Click it.

**Expected Result:**
A panel will appear showing "AWS Explorer" with options to:
- Connect to AWS
- See documentation
- Create resources

---

## 3.2 Verify All Installations

Create a checklist in your head (or on paper):

| Component | Check | Status |
| ----------- | ----- | ------ |
| VS Code installed | Latest version open | ✅ |
| AWS icon visible in sidebar | Click orange square | ✅ |
| Extensions → AWS Toolkit | Shows "Uninstall" button | ✅ |
| Terminal working | Can open terminal with Ctrl+` | ✅ |

---

# 4. How AWS Toolkit Works (Architecture)

## The Big Picture

When you use AWS Toolkit, here's what happens behind the scenes:

```mermaid
flowchart TD
    A[Your Code in VS Code] -->|Click Deploy| B[AWS Toolkit Extension]
    B -->|Uses| C[AWS CLI & SAM CLI]
    C -->|Send to| D[AWS Cloud]
    D -->|Stores| E[Lambda Functions]
    D -->|Stores| F[S3 Buckets]
    D -->|Stores| G[Databases]
    
    H[Your Computer] -.->|Runs| C
    I[AWS Servers] -.->|Run| D
    
    style A fill:#4CAF50
    style D fill:#FF9800
    style B fill:#2196F3
```

### Step-by-Step Breakdown

**1. You Write Code**
- Create a Python or JavaScript file in VS Code
- This contains your "Lambda function" (a cloud function)

**2. You Click "Deploy"**
- Right-click your code in VS Code
- Select "Deploy to AWS"

**3. AWS Toolkit Packages Your Code**
- It prepares your code for deployment
- It gathers all dependencies (libraries you used)
- It creates a package ready for AWS

**4. AWS Toolkit Sends to AWS**
- It uses AWS CLI & SAM CLI to communicate with AWS
- These are command-line tools that know how to talk to AWS

**5. AWS Cloud Receives & Runs**
- AWS receives your code
- AWS stores it in a "Lambda Function" (a serverless computer)
- Your code is now **live and running 24/7**

**6. Results Come Back**
- When someone uses your code, results come back to VS Code
- You can see logs, errors, performance

---

## What Is "Serverless"?

> **Serverless** = "AWS manages the servers for you"
>
> - You write code
> - AWS provides the computer to run it
> - You only pay when someone uses it
> - You don't manage servers, updates, or security patches

---

# 5. Connecting to Your AWS Account

## What Does "Connecting" Mean?

Connecting = **Telling VS Code your AWS password/credentials so it can access your account**.

There are two ways:

### Method 1: SSO (Single Sign-On) — Recommended for Organizations
If your company uses AWS with SSO:
- Click AWS icon in sidebar
- Click "Get Started"
- Click "Use SSO"
- A browser window opens
- Log in with your company account
- Done! VS Code remembers you

### Method 2: Access Keys — Good for Personal Projects

#### Step 1: Get Access Keys from AWS
(You created these in Prerequisites section)

- Go to [AWS IAM Console](https://console.aws.amazon.com/iam/)
- Click your username (top right)
- Click "My security credentials"
- Click "Access keys"
- Click "Create access key"
- Copy: **Access Key ID** and **Secret Access Key**
- Store them safely!

#### Step 2: Configure AWS CLI Locally

Open Terminal and run:

```bash
aws configure
```

When prompted, enter:
- **Access Key ID**: [paste your access key]
- **Secret Access Key**: [paste your secret key]
- **Default region**: `us-east-1` (or your region)
- **Default output**: `json`

**Expected Output:**
```
AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE
AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPbgEjF7EXAMPLE
Default region name [None]: us-east-1
Default output format [None]: json
```

#### Step 3: Connect in VS Code

1. Click **AWS icon** in sidebar
2. Click **"Connect to AWS"**
3. Choose **"Use credentials"**
4. Choose your credentials profile (usually "default")

**Expected Result:**
- AWS Explorer shows your account name
- You can see your existing AWS resources (Lambda, S3, etc.)

---

# 6. Understanding the AWS Explorer Interface

## What You'll See

When connected, the AWS Explorer sidebar shows:

```
AWS Explorer
│
├─ 📦 Lambda              → Your Lambda functions
├─ 🪣 S3                  → Your storage buckets
├─ 📊 CloudWatch Logs     → Your application logs
├─ ⚙️ Step Functions       → Your workflows
├─ 🔌 API Gateway         → Your APIs
├─ 🗄️ DynamoDB            → Your databases
└─ 📋 Secrets Manager     → Your secrets
```

### Exploring Each Section

#### Lambda Section
**What it shows**: All your serverless functions

**How to use**:
- Click arrow to expand
- Right-click a function to:
  - Invoke it (run it)
  - View logs (see what it did)
  - Delete it

**Expected view:**
```
Lambda
├─ HelloWorld (function name)
├─ ImageResizer
└─ DataProcessor
```

#### S3 Section
**What it shows**: All your storage buckets (like Google Drive, but for AWS)

**How to use**:
- Click to browse files inside
- Right-click to upload files
- Download files from here

#### CloudWatch Logs
**What it shows**: Records of what your functions did

**Use it to**:
- Find errors
- See performance data
- Debug problems
- Track who used your functions

---

# 7. Foundation Activities — Start Here

## Activity 1: Install AWS Toolkit
*Time: 3-5 minutes*

### What You'll Learn
How to add AWS Toolkit to VS Code.

### Step-by-Step

**Step 1**: Open VS Code

**Step 2**: Open Extensions panel
```
Mac: Cmd + Shift + X
Windows/Linux: Ctrl + Shift + X
```

**Step 3**: Type in search box
```
AWS Toolkit
```

**Step 4**: Find the official AWS Toolkit extension
Look for the one published by "Amazon Web Services" with the most downloads/stars.

**Step 5**: Click the blue "Install" button

**Step 6**: Wait 20 seconds for installation

**What to look for next**:
- The AWS icon appears in the left sidebar
- The icon looks like an orange square with a smile

**Troubleshooting**:
- If you don't see the icon, try reloading VS Code (Cmd + R or Ctrl + R)
- If still stuck, restart VS Code completely

### ✅ How to Know You Succeeded
- Orange AWS icon visible in sidebar
- Clicking it shows "AWS Explorer" panel

---

## Activity 2: Connect to Your AWS Account
*Time: 5-10 minutes*

### What You'll Learn
How to give VS Code access to your AWS account.

### Prerequisites
- AWS account created
- IAM user created
- Access keys saved

### Step-by-Step

**Step 1**: Click the AWS icon in sidebar

**Step 2**: Click "Get Started" or "Connect to AWS"

**Step 3**: A dialog box appears asking how you want to connect
- Choose **"Use credentials from AWS credentials file"** (easiest for beginners)

**Step 4**: It will ask which profile to use
- Choose **"default"** (this is standard)

**Step 5**: Wait 10-30 seconds

**What you'll see**:
- A message: "Successfully connected to AWS"
- AWS Explorer shows your account name
- You see numbers/letters like: `[aws-profile: default]`

**Expected Output in VS Code**:
```
AWS Explorer
Connected: aws-profile: default
Region: us-east-1

Lambda
  (empty or shows existing functions)

S3
  (empty or shows existing buckets)
```

### ✅ How to Know You Succeeded
- No red error messages
- AWS Explorer shows "Connected: ..."
- You can see sections like Lambda, S3, etc.

### Troubleshooting
**Problem**: "AccessDenied" error
- **Solution**: Check your IAM permissions. Go back to AWS Console → IAM → Users → your-user → Permissions
- Make sure user has `AdministratorAccess` (for learning)

**Problem**: "Credentials not found" error
- **Solution**: Run `aws configure` in terminal again and re-enter your access keys

---

## Activity 3: Explore AWS Explorer & Your Services
*Time: 5 minutes*

### What You'll Learn
How to navigate AWS Explorer and see what services are available.

### Step-by-Step

**Step 1**: Click AWS icon in sidebar (orange square)

**Step 2**: Look at the different sections:

| Section | Click to Expand | What You See |
| --- | --- | --- |
| **Lambda** | Arrow icon | Your cloud functions (if any) |
| **S3** | Arrow icon | Your storage buckets (if any) |
| **CloudWatch Logs** | Arrow icon | Your application logs |
| **DynamoDB** | Arrow icon | Your databases (if any) |

**Step 3**: Click the arrow next to **Lambda**

**Expected Output**:
```
Lambda
├─ (empty) - if you haven't created any yet
└─ (or shows: existing-function-name)
```

**Step 4**: Click the arrow next to **S3**

**Expected Output**:
```
S3
├─ (empty) - if you haven't created any buckets
└─ (or shows: my-example-bucket)
```

**Step 5**: Right-click on a section to see options

**Example: Right-click on "Lambda"**
```
Create Lambda Function...
Deploy SAM Application...
```

### ✅ How to Know You Succeeded
- All sections expanded without errors
- You can see available AWS services

---

## Activity 4: View CloudWatch Logs (If You Have Functions)
*Time: 5 minutes*

### What You'll Learn
How to see what your applications are doing.

### Prerequisites
- Must have at least one deployed Lambda function (we'll create one next)
- Connected to AWS

### Step-by-Step

**Step 1**: Click AWS icon in sidebar

**Step 2**: Expand "CloudWatch Logs" section

**Step 3**: You'll see log groups (organized records of what happened)

**Expected Output** (example):
```
CloudWatch Logs
├─ /aws/lambda/my-function-1
├─ /aws/lambda/my-function-2
└─ /aws/lambda/my-function-3
```

**Step 4**: Click the arrow next to a log group to expand it

**Expected Output** (example):
```
/aws/lambda/my-function-1
└─ 2024-01-15T10:30:00Z - first execution log
```

**Step 5**: Click on a log to view details

**What you'll see** (example):
```
[INFO] Function executed
Duration: 50 ms
Billed Duration: 100 ms
```

### ✅ How to Know You Succeeded
- You can see log groups without errors
- Clicking a log shows details

### Note
**Don't have functions yet?** That's ok! We'll create one in the next activity.

---

## Activity 5: Create Your First Lambda Function Locally
*Time: 15 minutes*

### What You'll Learn
How to create a simple serverless function on your computer (before uploading to AWS).

### Prerequisites
- VS Code open
- AWS Toolkit installed & connected

### Step-by-Step

**Step 1**: Create a new folder for your project

In terminal, run:
```bash
mkdir my-first-lambda
cd my-first-lambda
```

**Step 2**: Create a new Python file

In VS Code:
- File → New File
- Type the following code:

```python
def lambda_handler(event, context):
    """
    This is a Lambda function - it runs in the AWS cloud!
    
    event = data sent to it
    context = information about the function
    """
    
    name = event.get("name", "World")  # Get 'name' from input, default to "World"
    
    return {
        "statusCode": 200,  # 200 = success
        "body": f"Hello, {name}! Welcome to AWS Lambda!"
    }
```

**Step 3**: Save the file
```
File → Save
Name it: lambda_function.py
Choose folder: my-first-lambda
```

**Step 4**: Understand what this code does

| Part | What It Does | Example |
| --- | --- | --- |
| `def lambda_handler(event, context):` | Defines your function | AWS calls this automatically |
| `event.get("name", "World")` | Gets input data | If you send `{"name": "Alice"}`, it gets "Alice" |
| `"statusCode": 200` | Returns success code | 200 = OK, 400 = error |
| `"body": f"Hello..."` | The actual response | What gets sent back |

### ✅ How to Know You Succeeded
- File saved as `lambda_function.py`
- No red squiggly lines under code (syntax errors)

---

## Activity 6: Deploy Lambda Function to AWS
*Time: 10-15 minutes*

### What You'll Learn
How to upload your function to AWS so it runs in the cloud 24/7.

### Prerequisites
- Completed Activity 5 (have lambda_function.py)
- AWS Toolkit connected
- Have Python 3.9+ installed

### Step-by-Step

**Step 1**: Open AWS Explorer (orange icon in sidebar)

**Step 2**: Find "Lambda" section

**Step 3**: Right-click on "Lambda" → Select "Create Lambda Function"

**Expected Dialog**:
```
Lambda Function Name:
[ input field ]

Runtime: (dropdown showing)
○ Python 3.9
○ Python 3.10
○ Python 3.11
```

**Step 4**: Fill in the details

- **Name**: `my-first-lambda` (or any name with no spaces)
- **Runtime**: Choose `Python 3.11` (or latest)
- **Handler**: `lambda_function.lambda_handler`

**Step 5**: Click "Create"

**What happens** (you'll see in VS Code):
- VS Code might say "Creating..." (takes 30-60 seconds)
- A notification appears: "✅ Successfully created Lambda function"
- In AWS Explorer, under Lambda, you'll see `my-first-lambda`

**Expected Output** (in AWS Explorer):
```
Lambda
├─ my-first-lambda      ← Your new function!
```

**Step 6**: Refresh AWS Explorer to confirm
- Click the refresh icon (looks like circular arrow)
- Or press F5

### ✅ How to Know You Succeeded
- No error messages
- Your function name appears in AWS Explorer
- Green checkmark notification

### Troubleshooting

**Problem**: "Lambda is not defined" or similar error
- **Solution**: Make sure your file is named `lambda_function.py` exactly

**Problem**: "AccessDenied" error
- **Solution**: Check IAM permissions. Make sure your user has `lambda:CreateFunction` permission

**Problem**: Takes longer than 60 seconds
- **Solution**: This is normal first time. AWS is provisioning servers. Wait a bit longer.

---

## Activity 7: Invoke (Run) Your Lambda Function
*Time: 5 minutes*

### What You'll Learn
How to execute your function and see results.

### Prerequisites
- Completed Activity 6 (function deployed)

### Step-by-Step

**Step 1**: Click AWS icon → Lambda section

**Step 2**: Right-click your function name (`my-first-lambda`)

**Step 3**: Select "Invoke on AWS"

**Step 4**: A dialog might ask for input. Enter:
```json
{
  "name": "Alice"
}
```

**Step 5**: Click "Invoke"

**What you'll see** (Expected Output):
```
Invocation successful!

Response:
{
  "statusCode": 200,
  "body": "Hello, Alice! Welcome to AWS Lambda!"
}

Duration: 234 ms
Billed Duration: 235 ms
```

### What Those Numbers Mean
- **Duration**: Time your code actually ran
- **Billed Duration**: Time you're charged for (AWS rounds up)

### Try Again with Different Input

**Step 6**: Right-click function again → "Invoke on AWS"

**Step 7**: Try different input:
```json
{
  "name": "Bob"
}
```

**Expected Output**:
```json
{
  "statusCode": 200,
  "body": "Hello, Bob! Welcome to AWS Lambda!"
}
```

### ✅ How to Know You Succeeded
- Response shows your custom message
- No errors
- Works with different inputs

---

## Activity 8: View Your Function's Logs
*Time: 5 minutes*

### What You'll Learn
How to see what your function is doing behind the scenes.

### Prerequisites
- Completed Activity 7 (invoked function at least once)

### Step-by-Step

**Step 1**: Click AWS icon → CloudWatch Logs section

**Step 2**: Expand CloudWatch Logs

**Expected Output** (you should see):
```
CloudWatch Logs
├─ /aws/lambda/my-first-lambda
```

**Step 3**: Click the arrow to expand the log group

**Step 4**: Right-click on it → "View Logs"

**What you'll see** (Example):
```
2024-03-15 10:45:23.456 START RequestId: abc123...
2024-03-15 10:45:23.789 Duration: 234 ms
2024-03-15 10:45:23.890 Billed Duration: 235 ms
2024-03-15 10:45:23.891 Status: 200
2024-03-15 10:45:24.000 END RequestId: abc123...
```

### What This Means

| Line | What It Means |
| --- | --- |
| `START RequestId: abc123` | AWS started running your function |
| `Duration: 234 ms` | Your code took 234 milliseconds to finish |
| `Status: 200` | Success! (200 = OK) |
| `END RequestId` | Function execution finished |

### ✅ How to Know You Succeeded
- You can see log entries
- Timestamps match when you invoked the function
- No error messages in logs

---

## Activity 9: Explore S3 (Cloud Storage)
*Time: 10 minutes*

### What You'll Learn
What S3 is, and how to store files in the cloud.

### What Is S3?
> **S3** = "Simple Storage Service" = Cloud storage like Google Drive, but for AWS
>
> - Store files in "buckets" (folders in the cloud)
> - Access files from anywhere
> - Pay based on what you use

### Step-by-Step

**Step 1**: Go to AWS Explorer → S3 section

**Step 2**: Click arrow to expand S3

**Expected Output** (if empty):
```
S3
(no items yet)
```

**Step 3**: Create a bucket. Right-click "S3" → "Create S3 Bucket"

**Step 4**: Enter bucket name:
```
my-first-bucket-[your-unique-number]
```

> **Important**: Bucket names must be globally unique (no other AWS user can have this name)
> Add a random number to make it unique: `my-first-bucket-92837`

**Step 5**: Click "Create"

**Expected Notification**:
```
✅ Successfully created S3 bucket
```

**Step 6**: Expand S3 section again

**Expected Output**:
```
S3
├─ my-first-bucket-92837
```

### ✅ How to Know You Succeeded
- Bucket appears in S3 section
- No error messages

---

## Activity 10: Upload a File to S3
*Time: 5 minutes*

### What You'll Learn
How to store files in your cloud storage.

### Prerequisites
- Completed Activity 9 (have S3 bucket)
- Have a test file (create one if needed)

### Step-by-Step

**Step 1**: Create a test file in VS Code

- File → New File
- Type some content:
```
Hello from the cloud!
This is my first file in S3.
```
- Save as `test-file.txt`

**Step 2**: Go to AWS Explorer → S3

**Step 3**: Expand your bucket

**Expected Output**:
```
S3
├─ my-first-bucket-92837
   (empty - no files yet)
```

**Step 4**: Right-click on your bucket → "Upload Files"

**Step 5**: A file picker opens. Select `test-file.txt`

**Step 6**: Click "Open"

**What happens**:
- AWS uploads your file (takes 1-5 seconds)
- Notification shows: ✅ Upload successful

**Expected Output** (in S3 Explorer):
```
S3
├─ my-first-bucket-92837
   └─ test-file.txt  ← Your uploaded file!
```

### ✅ How to Know You Succeeded
- File appears in S3 bucket
- No error messages

---

## Activity 11: Create an API (Web Endpoint)
*Time: 15-20 minutes*

### What You'll Learn
How to create a URL that anyone can call to run your Lambda function.

### What Is an API?
> **API** = A web address that triggers your code
>
> - Similar to `instagram.com/` or `google.com/search`
> - When someone visits, your Lambda runs
> - Results are sent back

### How It Works

```mermaid
sequenceDiagram
    User->>Browser: Visit myapi.example.com/hello
    Browser->>API Gateway: Send request
    API Gateway->>Lambda: Run my function!
    Lambda->>Database: Get data if needed
    Lambda->>API Gateway: Return response
    API Gateway->>Browser: Show result
    Browser->>User: User sees "Hello Alice!"
```

### Step-by-Step

**Step 1**: Create a new folder
```bash
mkdir my-first-api
cd my-first-api
```

**Step 2**: Create template file. Create `template.yaml`:

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31

Resources:
  MyFirstAPI:
    Type: AWS::Serverless::Function
    Properties:
      FunctionName: my-first-api
      Runtime: python3.11
      Handler: app.lambda_handler
      Events:
        ApiEvent:
          Type: Api
          Properties:
            Path: /hello
            Method: get
            RestApiId: !Ref MyRestApi

  MyRestApi:
    Type: AWS::Serverless::Api
    Properties:
      StageName: Prod
```

**Step 3**: Create Python file `app.py`:

```python
def lambda_handler(event, context):
    """
    This function is called when someone visits the API endpoint
    """
    
    # Get 'name' from the URL query string
    # Example: /hello?name=Alice
    query_params = event.get("queryStringParameters", {}) or {}
    name = query_params.get("name", "Guest")
    
    return {
        "statusCode": 200,
        "body": f"Hello, {name}! This is your first API!"
    }
```

**Step 4**: Save both files

**Step 5**: Deploy. Right-click folder in VS Code → "Deploy SAM Application"

**Step 6**: Follow the prompts:
- Choose S3 bucket to store code
- Choose region (e.g., us-east-1)
- Confirm deployment

**Expected Notification**:
```
✅ Deployment successful
API Endpoint: https://abc123.execute-api.us-east-1.amazonaws.com/Prod/hello
```

**Step 7**: Test the endpoint

Copy the URL and add a query parameter:
```
https://abc123.execute-api.us-east-1.amazonaws.com/Prod/hello?name=Alice
```

Visit in browser → You'll see:
```
Hello, Alice! This is your first API!
```

### ✅ How to Know You Succeeded
- Deployment completes without errors
- URL provided in notification
- Visiting URL shows your custom message

---



---

# 8. Advanced Activities — Next Level

## Activity 12: Debug Lambda Locally (Run Code on Your Computer)
*Time: 20 minutes*

### What You'll Learn
How to test your Lambda code on your computer before uploading to AWS (catch bugs faster!).

### What's "Local Debugging"?
> **Local Debugging** = Running and testing your code on your machine before AWS.
>
> - **Benefits**: Faster feedback, catch errors quickly, doesn't cost money
> - **How**: SAM CLI simulates AWS on your computer using Docker

### Prerequisites
- Docker installed and running
- Lambda function from Activity 6
- SAM CLI installed

### Step-by-Step

**Step 1**: Start Docker

Make sure Docker is running:
```bash
docker --version
# Should print: Docker version 24.0.x
```

**Step 2**: Create a `template.yaml` file

In your `my-first-lambda` folder, create `template.yaml`:

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31

Resources:
  MyFirstLambda:
    Type: AWS::Serverless::Function
    Properties:
      FunctionName: my-first-lambda
      Runtime: python3.11
      Handler: lambda_function.lambda_handler
      CodeUri: .
```

**Step 3**: Open terminal in VS Code
```
Ctrl + ` (backtick)
```

**Step 4**: Build your function locally
```bash
sam build
```

**Expected Output**:
```
Running SAMCli install Python PEP 517 packaging...
Building application...

Build Succeeded

Built Artifacts  : .aws-sam/build
Built Template   : .aws-sam/build/template.yaml
```

**Step 5**: Start local debugging
```bash
sam local invoke -e events/event.json
```

(If `events/event.json` doesn't exist, create it with):
```json
{
  "name": "DebugTest"
}
```

**Expected Output**:
```
Invoking lambda_function.lambda_handler (python3.11)
Local image was not found...
Building image...
Running HelloWorldFunction from /path/to/.aws-sam/build

START RequestId: mock-aws-request-id
Duration: 45 ms
END RequestId: mock-aws-request-id

Response:
{
  "statusCode": 200,
  "body": "Hello, DebugTest! Welcome to AWS Lambda!"
}
```

### ✅ How to Know You Succeeded
- `sam build` completes without errors
- `sam local invoke` runs your function locally
- Output shows your function's response

### Debug Flow Diagram
```mermaid
sequenceDiagram
    participant You as You (VS Code)
    participant Docker as Docker (Your Computer)
    participant Lambda as Lambda Function
    
    You->>Docker: sam local invoke
    Docker->>Docker: Start container
    Docker->>Lambda: Run function
    Lambda->>Lambda: Execute code
    Lambda->>Docker: Send response
    Docker->>You: Display result in terminal
```

---

## Activity 13: Create a Step Function Workflow
*Time: 20-30 minutes*

### What You'll Learn
How to chain multiple Lambda functions together into a workflow.

### What's a Step Function?
> **Step Function** = Orchestration service that runs multiple steps in sequence
>
> Think of it like a recipe:
> 1. Get user data (Lambda 1)
> 2. Validate data (Lambda 2)
> 3. Save to database (Lambda 3)

### Workflow Diagram
```mermaid
flowchart LR
    Start([Start]) -->|Input| Step1["Step 1: Get Data"]
    Step1 -->|Output| Step2["Step 2: Validate"]
    Step2 -->|Output| Step3["Step 3: Save"]
    Step3 --> End([End])
    
    style Start fill:#4CAF50
    style End fill:#FF6B6B
    style Step1 fill:#2196F3
    style Step2 fill:#2196F3
    style Step3 fill:#2196F3
```

### Step-by-Step

**Step 1**: Create 3 simple Lambda functions

Function 1 - `step1_get_data.py`:
```python
def lambda_handler(event, context):
    user_id = event.get("user_id", "unknown")
    return {
        "user_id": user_id,
        "data": f"Data for user {user_id}"
    }
```

Function 2 - `step2_validate.py`:
```python
def lambda_handler(event, context):
    user_id = event.get("user_id")
    data = event.get("data")
    
    is_valid = len(data) > 0
    
    return {
        "user_id": user_id,
        "data": data,
        "is_valid": is_valid
    }
```

Function 3 - `step3_save.py`:
```python
def lambda_handler(event, context):
    user_id = event.get("user_id")
    data = event.get("data")
    is_valid = event.get("is_valid")
    
    if is_valid:
        return {"status": "saved", "user_id": user_id}
    else:
        return {"status": "validation failed"}
```

**Step 2**: Deploy all 3 functions to AWS (right-click each, deploy)

**Step 3**: Create `step_function.json` state machine definition:

```json
{
  "Comment": "A simple step function workflow",
  "StartAt": "GetUserData",
  "States": {
    "GetUserData": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123456789:function:step1_get_data",
      "Next": "ValidateData"
    },
    "ValidateData": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123456789:function:step2_validate",
      "Next": "SaveData"
    },
    "SaveData": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123456789:function:step3_save",
      "End": true
    }
  }
}
```

**Step 4**: Create step function in AWS

In AWS Explorer:
- Right-click "Step Functions"
- Select "New Step Function"
- Paste your state machine JSON
- Name it: `my-workflow`
- Click Create

**Step 5**: Test the workflow

- Right-click `my-workflow`
- Select "Execute"
- Enter input:
```json
{
  "user_id": "user123"
}
```

**Expected Output** (After execution completes):
```
Execution Status: Succeeded

Step 1 Output: {"user_id": "user123", "data": "Data for user user123"}
Step 2 Output: {"user_id": "user123", "data": "...", "is_valid": true}
Step 3 Output: {"status": "saved", "user_id": "user123"}
```

### ✅ How to Know You Succeeded
- Step Function created without errors
- Execution completes with "Succeeded" status
- Output shows all 3 functions ran in order

---

## Activity 14: Connect Lambda to DynamoDB Database
*Time: 25-35 minutes*

### What You'll Learn
How to store and retrieve data from a database in your Lambda functions.

### What's DynamoDB?
> **DynamoDB** = AWS's serverless database (automatically scales, pay-per-use)
>
> Think of it like a spreadsheet in the cloud that stores structured data

### Architecture Diagram
```mermaid
flowchart LR
    A[User Request] --> B[API Gateway]
    B --> C[Lambda Function]
    C -->|Read/Write| D[(DynamoDB Database)]
    D -->|Return Data| C
    C --> B
    B --> A
    
    style A fill:#4CAF50
    style D fill:#FF9800
```

### Step-by-Step

**Step 1**: Create a DynamoDB table in AWS

In AWS Console:
1. Go to DynamoDB service
2. Click "Create table"
3. Fill in:
   - **Table name**: `Users`
   - **Partition key**: `user_id` (String)
   - **Billing mode**: Pay-per-request

**Expected Notification**:
```
✅ Table 'Users' created successfully
```

**Step 2**: Create Lambda function `dynamodb_lambda.py`:

```python
import boto3
import json
from datetime import datetime

# Create DynamoDB client
dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('Users')

def lambda_handler(event, context):
    """
    Save or retrieve user data from DynamoDB
    """
    
    action = event.get('action', 'put')  # 'put' = save, 'get' = retrieve
    user_id = event.get('user_id')
    
    try:
        if action == 'put':
            # Save new user
            user_data = {
                'user_id': user_id,
                'name': event.get('name'),
                'email': event.get('email'),
                'created_at': datetime.now().isoformat()
            }
            table.put_item(Item=user_data)
            return {
                'statusCode': 200,
                'body': json.dumps('User saved successfully')
            }
        
        elif action == 'get':
            # Retrieve user
            response = table.get_item(Key={'user_id': user_id})
            
            if 'Item' in response:
                return {
                    'statusCode': 200,
                    'body': json.dumps(response['Item'])
                }
            else:
                return {
                    'statusCode': 404,
                    'body': json.dumps('User not found')
                }
    
    except Exception as e:
        return {
            'statusCode': 500,
            'body': json.dumps(f'Error: {str(e)}')
        }
```

**Step 3**: Update IAM permissions

Your Lambda needs permission to read/write DynamoDB:

1. Go to AWS IAM Console
2. Find your Lambda's role
3. Add inline policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "dynamodb:GetItem",
        "dynamodb:PutItem",
        "dynamodb:Query",
        "dynamodb:Scan"
      ],
      "Resource": "arn:aws:dynamodb:*:*:table/Users"
    }
  ]
}
```

**Step 4**: Deploy the function

**Step 5**: Test saving data

Invoke with:
```json
{
  "action": "put",
  "user_id": "user123",
  "name": "Alice Johnson",
  "email": "alice@example.com"
}
```

**Expected Output**:
```json
{
  "statusCode": 200,
  "body": "User saved successfully"
}
```

**Step 6**: Test retrieving data

Invoke with:
```json
{
  "action": "get",
  "user_id": "user123"
}
```

**Expected Output**:
```json
{
  "statusCode": 200,
  "body": {
    "user_id": "user123",
    "name": "Alice Johnson",
    "email": "alice@example.com",
    "created_at": "2024-03-15T10:45:23.123456"
  }
}
```

### ✅ How to Know You Succeeded
- Function saves data without errors
- Retrieving returns the same data
- DynamoDB table shows data in console

---

## Activity 15: Set Up Automatic Triggers with EventBridge
*Time: 20 minutes*

### What You'll Learn
How to run Lambda functions automatically based on events (without manual invocation).

### What's EventBridge?
> **EventBridge** = A service that monitors events and triggers actions automatically
>
> **Examples**:
> - Every hour, run cleanup function
> - When file uploaded to S3, resize image
> - When email received, process it

### Event Flow
```mermaid
flowchart LR
    A[Event Source] -->|"Event Happens"| B[EventBridge]
    B -->|"Condition Met?"| C{Check}
    C -->|"Yes"| D["Trigger Lambda"]
    C -->|"No"| E["Ignore"]
    D --> F[Function Runs]
    
    style B fill:#4CAF50
    style D fill:#2196F3
```

### Step-by-Step

**Step 1**: Create a trigger function `scheduled_lambda.py`:

```python
import json
from datetime import datetime

def lambda_handler(event, context):
    """
    This function runs on a schedule automatically
    """
    
    current_time = datetime.now().isoformat()
    
    return {
        'statusCode': 200,
        'message': 'Scheduled function executed!',
        'timestamp': current_time
    }
```

**Step 2**: Deploy this function to AWS

**Step 3**: Set up automatic trigger

In AWS Console:
1. Go to Lambda
2. Find your `scheduled_lambda` function
3. Click "Add trigger"
4. Choose "EventBridge (CloudWatch Events)"
5. Create new rule:
   - **Rule name**: `my-schedule`
   - **Schedule**: `rate(5 minutes)` (runs every 5 minutes)

**Step 4**: Save trigger

**Expected Notification**:
```
✅ Trigger created successfully
Your function will run every 5 minutes
```

**Step 5**: Monitor execution

Check CloudWatch Logs:
- AWS Explorer → CloudWatch Logs
- Look for `/aws/lambda/scheduled_lambda`
- You should see executions every 5 minutes

### ✅ How to Know You Succeeded
- Trigger created without errors
- Function shows execution history
- Logs show invocations at regular intervals

---

## Activity 16: Deploy to Multiple Environments (Dev, Staging, Production)
*Time: 30 minutes*

### What You'll Learn
How to deploy the same code to different environments with different configurations.

### Why Multiple Environments?
```mermaid
graph TD
    A["Your Code"] --> B["DEV Environment"]
    A --> C["STAGING Environment"]
    A --> D["PRODUCTION Environment"]
    
    B -->|"Safe Testing"| B1["Limited users"]
    C -->|"Pre-production"| C1["Full testing"]
    D -->|"Live"| D1["Real users"]
    
    style B fill:#FFEB3B
    style C fill:#FF9800
    style D fill:#F44336
```

### Step-by-Step

**Step 1**: Create `template.yaml` with parameters:

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31

Parameters:
  EnvironmentName:
    Type: String
    Default: dev
    AllowedValues:
      - dev
      - staging
      - prod
    Description: "Which environment to deploy to?"
  
  MemorySize:
    Type: Number
    Default: 128
    Description: "Lambda memory (dev=128, staging=256, prod=512)"

Resources:
  MyFunction:
    Type: AWS::Serverless::Function
    Properties:
      FunctionName: !Sub "my-function-${EnvironmentName}"
      Runtime: python3.11
      Handler: app.lambda_handler
      MemorySize: !Ref MemorySize
      Environment:
        Variables:
          ENVIRONMENT: !Ref EnvironmentName
```

**Step 2**: Create `samconfig.toml` for configuration:

```toml
[dev.deploy.parameters]
parameter_overrides = "EnvironmentName=dev MemorySize=128"
s3_prefix = "dev"

[staging.deploy.parameters]
parameter_overrides = "EnvironmentName=staging MemorySize=256"
s3_prefix = "staging"

[prod.deploy.parameters]
parameter_overrides = "EnvironmentName=prod MemorySize=512"
s3_prefix = "prod"
```

**Step 3**: Deploy to dev environment:

```bash
sam deploy --config-env dev
```

**Step 4**: Deploy to staging environment:

```bash
sam deploy --config-env staging
```

**Step 5**: Deploy to prod environment:

```bash
sam deploy --config-env prod
```

**Expected Output**:
```
Deploying to environment: prod
Function Name: my-function-prod
Memory: 512 MB
Region: us-east-1

✅ Deployment successful!
```

**Step 6**: Verify in AWS

Check Lambda functions:
- `my-function-dev` (128 MB)
- `my-function-staging` (256 MB)
- `my-function-prod` (512 MB)

### ✅ How to Know You Succeeded
- All 3 function versions deployed
- Different memory configurations apply
- Each environment is isolated

---

## Activity 17: Infrastructure as Code with SAM Templates
*Time: 25 minutes*

### What You'll Learn
How to define your entire cloud infrastructure in a configuration file.

### What's "Infrastructure as Code"?
> **IaC** = Describing cloud resources in a file (not clicking buttons in AWS Console)
>
> **Benefits**:
> - Reproducible
> - Version controlled (track history)
> - Shareable with team
> - Automated deployments

### Complete SAM Template Example

`template.yaml`:
```yaml
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
Description: Complete serverless application

Parameters:
  Environment:
    Type: String
    Default: dev
    AllowedValues: [dev, prod]

Globals:
  Function:
    Timeout: 30
    Runtime: python3.11
    Environment:
      Variables:
        TABLE_NAME: !Ref UsersTable

Resources:
  # 1. API Gateway (Web Endpoint)
  MyAPI:
    Type: AWS::Serverless::Api
    Properties:
      StageName: !Ref Environment
      Auth:
        DefaultAuthorizer: MyCognitoAuth
        Authorizers:
          MyCognitoAuth:
            FunctionArn: !GetAtt AuthFunction.Arn

  # 2. Lambda Function 1: Get Users
  GetUsersFunction:
    Type: AWS::Serverless::Function
    Properties:
      FunctionName: !Sub "get-users-${Environment}"
      Handler: handlers/get_users.lambda_handler
      CodeUri: src/
      Policies:
        - DynamoDBCrudPolicy:
            TableName: !Ref UsersTable
      Events:
        GetUsersAPI:
          Type: Api
          Properties:
            RestApiId: !Ref MyAPI
            Path: /users
            Method: GET

  # 3. Lambda Function 2: Create User
  CreateUserFunction:
    Type: AWS::Serverless::Function
    Properties:
      FunctionName: !Sub "create-user-${Environment}"
      Handler: handlers/create_user.lambda_handler
      CodeUri: src/
      Policies:
        - DynamoDBCrudPolicy:
            TableName: !Ref UsersTable
      Events:
        CreateUserAPI:
          Type: Api
          Properties:
            RestApiId: !Ref MyAPI
            Path: /users
            Method: POST

  # 4. DynamoDB Table
  UsersTable:
    Type: AWS::DynamoDB::Table
    Properties:
      TableName: !Sub "users-${Environment}"
      AttributeDefinitions:
        - AttributeName: user_id
          AttributeType: S
      KeySchema:
        - AttributeName: user_id
          KeyType: HASH
      BillingMode: PAY_PER_REQUEST

  # 5. CloudWatch Alarms (Monitoring)
  HighErrorRateAlarm:
    Type: AWS::CloudWatch::Alarm
    Properties:
      AlarmName: !Sub "high-errors-${Environment}"
      MetricName: Errors
      Namespace: AWS/Lambda
      Statistic: Sum
      ComparisonOperator: GreaterThanThreshold
      Threshold: 10
      AlertActions:
        - !Ref AlertTopic

  # 6. SNS Topic (Notifications)
  AlertTopic:
    Type: AWS::SNS::Topic
    Properties:
      TopicName: !Sub "alerts-${Environment}"

Outputs:
  APIEndpoint:
    Description: "API Gateway endpoint URL"
    Value: !Sub "https://${MyAPI}.execute-api.${AWS::Region}.amazonaws.com/${Environment}"
    Export:
      Name: !Sub "APIEndpoint-${Environment}"

  UsersTableName:
    Description: "DynamoDB Table Name"
    Value: !Ref UsersTable

  UsersTableArn:
    Description: "DynamoDB Table ARN"
    Value: !GetAtt UsersTable.Arn
```

**Step-by-Step**:

**Step 1**: Create this `template.yaml` in your project

**Step 2**: Create folder structure:
```bash
mkdir -p src/handlers
```

**Step 3**: Create handler files

`src/handlers/get_users.py`:
```python
import boto3
import json
import os

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table(os.environ['TABLE_NAME'])

def lambda_handler(event, context):
    response = table.scan()
    return {
        'statusCode': 200,
        'body': json.dumps(response['Items'])
    }
```

**Step 4**: Build and deploy
```bash
sam build
sam deploy --guided
```

**Expected Output**:
```
✅ Successfully created/updated stack my-app in region us-east-1

Outputs provided:
- APIEndpoint: https://abc123.execute-api.us-east-1.amazonaws.com/dev
- UsersTableName: users-dev
- UsersTableArn: arn:aws:dynamodb:us-east-1:123456789:table/users-dev
```

### What Got Created Automatically
- API Gateway endpoint
- 2 Lambda functions
- DynamoDB table
- CloudWatch alarms
- SNS topic
- All permissions and roles

### ✅ How to Know You Succeeded
- Deployment completes
- All resources appear in AWS Explorer
- API endpoint works when called

---

## Activity 18: Set Up CI/CD Pipeline (Automatic Deployments)
*Time: 30-45 minutes*

### What You'll Learn
How to automatically test and deploy code when you push to GitHub.

### What's CI/CD?
> **CI/CD** = Continuous Integration / Continuous Deployment
>
> - **CI** = Automatically test code when you push
> - **CD** = Automatically deploy if tests pass

### Pipeline Visualization
```mermaid
flowchart LR
    A["Developer<br/>Push Code"] --> B["GitHub"]
    B --> C["GitHub Actions"]
    C --> D["Run Tests"]
    D --> E{Tests<br/>Passed?}
    E -->|Yes| F["Deploy to AWS"]
    E -->|No| G["Notify Developer"]
    F --> H["Live in Production"]
    
    style C fill:#4CAF50
    style F fill:#2196F3
    style H fill:#FF9800
```

### Step-by-Step

**Step 1**: Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to AWS

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v2
      
      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.11'
      
      - name: Install SAM CLI
        run: pip install aws-sam-cli
      
      - name: Build application
        run: sam build
      
      - name: Run tests
        run: python -m pytest
      
      - name: Deploy to AWS
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        run: sam deploy --no-confirm-changeset --use-container
      
      - name: Notify Success
        run: echo "✅ Deployment successful!"
```

**Step 2**: Create GitHub repository

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/yourname/my-app
git push -u origin main
```

**Step 3**: Add AWS credentials to GitHub Secrets

1. Go to GitHub repository
2. Settings → Secrets and variables → Actions
3. Click "New repository secret"
4. Add `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`

**Step 4**: Make a change to your code

```bash
git add .
git commit -m "Update function"
git push
```

**Step 5**: Watch it deploy

Go to GitHub → Actions tab. You'll see the pipeline running:

```
✅ Checkout code
✅ Setup Python 3.11
✅ Install SAM CLI
✅ Build application
✅ Run tests
✅ Deploy to AWS
✅ Deployment successful!
```

### ✅ How to Know You Succeeded
- GitHub Actions workflow runs
- All steps pass
- Function updated in AWS
- No manual deployment needed

---

## Activity 19: Monitor Your Application with CloudWatch
*Time: 20 minutes*

### What You'll Learn
How to watch your application's performance and detect problems.

### What Can You Monitor?

| Metric | What It Means | Alert When |
| --- | --- | --- |
| **Invocations** | How many times function ran | High = maybe attack? |
| **Errors** | How many failed | Any = problem |
| **Duration** | How long functions take | Slow = performance issue |
| **Throttles** | Request limit exceeded | Any = need more capacity |
| **Concurrency** | How many running at once | High = capacity issue |

### Monitoring Dashboard
```mermaid
graph TD
    A["Your Application"] --> B["CloudWatch Metrics"]
    B --> C["Logs"]
    B --> D["Alarms"]
    D --> E["Notifications"]
    
    C --> F["Errors & Debugging"]
    C --> G["Performance Analysis"]
    
    style B fill:#4CAF50
    style E fill:#F44336
```

### Step-by-Step

**Step 1**: Create CloudWatch Dashboard

In AWS Console:
1. Go to CloudWatch
2. Dashboards → Create dashboard
3. Name: `my-app-dashboard`
4. Add widgets:
   - Lambda Invocations
   - Lambda Errors
   - Lambda Duration
   - Lambda Throttles

**Step 2**: View logs

AWS Explorer → CloudWatch Logs:
```
CloudWatch Logs
├─ /aws/lambda/my-function
   ├─ 2024-03-15T10:00:00Z - SUCCESS
   ├─ 2024-03-15T10:01:00Z - SUCCESS
   └─ 2024-03-15T10:02:00Z - ERROR
```

**Step 3**: Set up alarms

Create alarm for high errors:
1. CloudWatch → Alarms → Create alarm
2. Metric: Lambda Errors
3. Threshold: > 5 errors in 5 minutes
4. Action: Send email/SMS notification

**Expected Setup**:
```
Alarm Name: high-error-rate
Condition: Errors > 5 in 5 minutes
Action: Send email to ops-team@company.com
Status: ENABLED
```

**Step 4**: Create custom metrics

`log_metrics.py`:
```python
import boto3

cloudwatch = boto3.client('cloudwatch')

def lambda_handler(event, context):
    # Your business logic here
    processed_records = 150
    
    # Send custom metric
    cloudwatch.put_metric_data(
        Namespace='MyApp',
        MetricData=[
            {
                'MetricName': 'ProcessedRecords',
                'Value': processed_records,
                'Unit': 'Count'
            }
        ]
    )
    
    return {'statusCode': 200}
```

### ✅ How to Know You Succeeded
- Dashboard displays metrics
- Alarms configured
- Notifications working
- Can see logs in real-time

---

## Activity 20: Cost Optimization Tips
*Time: 15 minutes*

### Why Optimize Costs?

AWS can be expensive if you're not careful. Here are proven tips to reduce costs:

```mermaid
graph TD
    A["AWS Bill"] --> B["Lambda Duration"]
    A --> C["Memory Allocation"]
    A --> D["Data Transfer"]
    A --> E["Storage"]
    
    B -->|"Longer = More $"| B1["Optimize code"]
    C -->|"More = More $"| C1["Find right size"]
    D -->|"More = More $"| D1["Cache responses"]
    E -->|"More = More $"| E1["Delete old data"]
    
    style B1 fill:#4CAF50
    style C1 fill:#4CAF50
```

### Optimization Strategies

#### 1. **Right-Size Lambda Memory**

```python
# ❌ BAD: Using 3008 MB for simple task = expensive!
# Lambda: 3008 MB memory, 5 second execution time
# Price: ~$0.80 per 1 million invocations

# ✅ GOOD: Using 128 MB for simple task = cheap!
# Lambda: 128 MB memory, 1 second execution time
# Price: ~$0.021 per 1 million invocations

# Cost saved: 95%!
```

**How to find right size**:
1. Deploy function with 1024 MB
2. Invoke it and check CloudWatch Logs
3. Note max memory used
4. Set Lambda memory to slightly higher (e.g., max 300 MB → set 512 MB)

#### 2. **Cache Queries**

```python
import json
from datetime import datetime, timedelta

cache = {}

def lambda_handler(event, context):
    user_id = event.get('user_id')
    
    # Check if we already fetched this recently
    if user_id in cache:
        cached_data, cached_time = cache[user_id]
        if datetime.now() - cached_time < timedelta(minutes=5):
            return {'statusCode': 200, 'body': json.dumps(cached_data)}
    
    # Not cached, fetch from database
    user_data = fetch_from_database(user_id)
    cache[user_id] = (user_data, datetime.now())
    
    return {'statusCode': 200, 'body': json.dumps(user_data)}
```

#### 3. **Use On-Demand Pricing Wisely**

| Service | Pricing Model | Best For |
| --- | --- | --- |
| **DynamoDB On-Demand** | Pay per read/write | Unpredictable traffic |
| **DynamoDB Provisioned** | Fixed capacity | Predictable traffic |
| **Lambda** | Pay per 100ms  | Already cheap! |
| **S3** | Pay per GB | Storage optimization |

#### 4. **Delete Unused Resources**

```bash
# Find and delete old Lambda functions
aws lambda list-functions | grep -i "old\|test\|temp"

# Find and delete old DynamoDB tables
aws dynamodb list-tables | grep -i "backup\|old"

# Find and delete old S3 buckets
aws s3 ls | grep -i "temp"
```

#### 5. **Set Cost Alerts**

In AWS Billing Console:
1. Budgets → Create budget
2. Set alert when spending exceeds $50/month
3. Get email notifications

### Cost Estimation Examples

```
Small Application (10,000 invocations/month):
- Lambda: $0.20/month
- DynamoDB: $1-5/month
- Data Transfer: $0.09/month
- Total: ~$2/month

Medium Application (1,000,000 invocations/month):
- Lambda: $20/month
- DynamoDB: $50-100/month
- Data Transfer: $2-5/month
- Total: ~$70-130/month
```

### ✅ How to Know You Succeeded
- Understand your Lambda memory needs
- Caching implemented
- Cost alerts set
- Monthly bill < $10 for low-traffic app

---

# 9. Deployment Pipelines Explained

## What's a Deployment Pipeline?

A **pipeline** is a series of steps your code goes through before reaching users.

```mermaid
flowchart TD
    A["Your Local Code"] --> B["Step 1: Build"]
    B --> C["Step 2: Test"]
    C --> D["Step 3: Package"]
    D --> E["Step 4: Deploy to Dev"]
    E --> F["Step 5: Deploy to Staging"]
    F --> G["Step 6: Deploy to Production"]
    G --> H["🎉 Live for Users!"]
    
    style A fill:#4CAF50
    style H fill:#FF9800
    style B fill:#2196F3
    style C fill:#2196F3
    style G fill:#F44336
```

### Each Step Explained

**Step 1: Build**
- Collect all your files
- Install dependencies
- Prepare everything for AWS

**Step 2: Test**
- Run automated tests
- Catch bugs early
- Ensure quality

**Step 3: Package**
- Create ZIP file of code
- Compress dependencies
- Ready for AWS

**Step 4-6: Deploy**
- Send code to dev (testing)
- Send code to staging (pre-production)
- Send code to production (live)

---

# 10. Debugging & Monitoring Your Applications

## Debugging = Finding & Fixing Problems

### Local Debugging (On Your Computer)

```mermaid
sequenceDiagram
    participant DevI as Developer
    participant VSCode as VS Code
    participant Breakpoint as Breakpad
    participant Docker as Docker
    
    DevI->>VSCode: Set breakpoint on line 15
    DevI->>VSCode: Click Debug
    VSCode->>Docker: Start local container
    Docker->>Breakpoint: Run function
    Breakpoint->>Breakpoint: Execute to line 15
    Breakpoint->>VSCode: Halt at breakpoint
    DevI->>VSCode: Inspect variables
    VSCode->>DevI: Show variable values
```

**How to Debug Locally**:

1. Set breakpoint (click left margin of code)
2. Press F5 to debug
3. Code stops at breakpoint
4. Hover variables to see values
5. Step through code line-by-line
6. Find the bug!

### Cloud Debugging (In AWS)

**View Logs Real-Time**:
```bash
# Terminal
aws logs tail /aws/lambda/my-function --follow
```

**CloudWatch Logs Show**:
```
[INFO] Starting execution
[INFO] Received event: {"user_id": "123"}
[ERROR] KeyError: 'name' ← Bug is here!
[INFO] Execution failed
```

### Common Issues & Solutions

| Error | Cause | Fix |
| --- | --- | --- |
| `KeyError: 'name'` | Missing key in input | Add default: `event.get('name', 'default')` |
| `Timeout` | Code takes too long | Optimize loops, use caching |
| `AccessDenied` | IAM permission issue | Add policy to Lambda role |
| `OutOfMemory` | Lambda memory exhausted | Increase memory or optimize code |

---

# 11. Quick Reference & Commands

## Essential Commands

### SAM CLI
```bash
# Build your application
sam build

# Test locally
sam local invoke

# Deploy to AWS
sam deploy --guided
sam deploy  # (uses previous settings)

# Delete everything
sam delete
```

### AWS CLI
```bash
# View Lambda functions
aws lambda list-functions

# View S3 buckets
aws s3 ls

# View DynamoDB tables
aws dynamodb list-tables

# View logs
aws logs tail /aws/lambda/my-function --follow
```

### Docker
```bash
# Check if running
docker ps

# Start Docker Desktop (on Mac)
open /Applications/Docker.app
```

## VS Code Keyboard Shortcuts

| Action | Windows/Linux | Mac |
| --- | --- | --- |
| Command Palette | Ctrl+Shift+P | Cmd+Shift+P |
| Extensions | Ctrl+Shift+X | Cmd+Shift+X |
| Terminal | Ctrl+` | Ctrl+` |
| Debug | F5 | F5 |
| Set Breakpoint | Ctrl+F8 | Cmd+F8 |

---

# 12. Troubleshooting Common Problems

## Decision Tree

```mermaid
flowchart TD
    Start["Something not working?"] --> Q1{"Is it a<br/>connection<br/>issue?"}
    
    Q1 -->|Yes| A["Check credentials<br/>aws configure<br/>Reconnect in Toolkit"]
    Q1 -->|No| Q2{"Is it an<br/>IAM<br/>permission?"}
    
    Q2 -->|Yes| B["Go to IAM Console<br/>Check user policies<br/>Add AdministratorAccess"]
    Q2 -->|No| Q3{"Is Docker<br/>running?"}
    
    Q3 -->|Yes| C["Check logs<br/>AWS Explorer → CloudWatch"]
    Q3 -->|No| D["Start Docker Desktop<br/>Try again"]
    
    A --> E["Try again"]
    B --> E
    C --> F["Debug code"]
    D --> E
```

## Common Errors & Fixes

### Error: "Extension not found"

**Solution**:
1. Open Extensions (Cmd+Shift+X)
2. Search "AWS Toolkit"
3. Click Install
4. Reload VS Code (Cmd+R)

### Error: "AWS CLI not found"

**Solution**:
```bash
# Install AWS CLI
pip install awscli

# Verify
aws --version  # Should print: aws-cli/2.x.x
```

### Error: "Could not connect to AWS"

**Solution**:
```bash
# Test credentials
aws sts get-caller-identity

# Should print your AWS account info
```

### Error: "Docker is not running"

**Solution**:
- Mac: Open `/Applications/Docker.app`
- Windows: Open Docker Desktop
- Wait 30 seconds for startup
- Try again

### Error: "Permission Denied" on Lambda

**Solution**:

Go to IAM Console:
1. Users → your-user
2. Add inline policy:

```json
{
  "Effect": "Allow",
  "Action": "lambda:*",
  "Resource": "*"
}
```

### Error: "Function timeout"

**Solution**:
- Increase timeout in SAM template:
```yaml
Resources:
  MyFunction:
    Properties:
      Timeout: 60  # Increase from 30 to 60 seconds
```

### Error: "Out of memory"

**Solution**:
- Increase Lambda memory:
```yaml
Resources:
  MyFunction:
    Properties:
      MemorySize: 512  # Increase from 128 to 512 MB
```

---

# 13. Best Practices & Optimization

## Security Best Practices

### ✅ DO:
- Use IAM roles with least privilege
- Never hardcode credentials
- Use Secrets Manager for sensitive data
- Enable logging for audit trails
- Use VPC for network isolation

### ❌ DON'T:
- Use root AWS account
- Share access keys
- Store secrets in code
- Deploy without testing
- Use overly permissive IAM policies

### Example: Secure Secret Storage

```python
import boto3
import json

secrets_client = boto3.client('secretsmanager')

def get_database_password():
    """
    Safely retrieve database password from Secrets Manager
    Never store in code!
    """
    response = secrets_client.get_secret_value(
        SecretId='prod/database/password'
    )
    return json.loads(response['SecretString'])['password']

def lambda_handler(event, context):
    db_password = get_database_password()
    # Use password to connect to database
    return {'statusCode': 200}
```

## Performance Best Practices

### Optimize Lambda Memory

```python
# Measure actual memory usage
import tracemalloc

def lambda_handler(event, context):
    tracemalloc.start()
    
    # Your code here
    result = expensive_operation()
    
    current, peak = tracemalloc.get_traced_memory()
    print(f"Peak Memory Used: {peak / 1024 / 1024:.2f} MB")
    
    tracemalloc.stop()
    return result
```

### Use ENV Variables, Not Hardcoding

```python
# ❌ BAD
def lambda_handler(event, context):
    database_url = "prod-db.example.com:5432"  # Hardcoded!
    
# ✅ GOOD
import os

def lambda_handler(event, context):
    database_url = os.environ.get('DATABASE_URL')  # From environment
```

### Implement Retry Logic

```python
import time
from functools import wraps

def retry(max_attempts=3, wait_seconds=2):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(max_attempts):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt == max_attempts - 1:
                        raise
                    time.sleep(wait_seconds ** attempt)
        return wrapper
    return decorator

@retry(max_attempts=3, wait_seconds=1)
def call_external_api():
    # This function will retry up to 3 times if it fails
    pass
```

---

# 14. Knowledge Check

## Can You Do These?

After completing this guide, you should be able to:

**Foundation Level:**
- ✅ Install AWS Toolkit in VS Code
- ✅ Connect your AWS account
- ✅ Create and deploy a Lambda function
- ✅ Invoke Lambda remotely
- ✅ View CloudWatch logs
- ✅ Create S3 buckets and upload files

**Proficiency Level:**
- ✅ Debug Lambda locally using SAM
- ✅ Create API endpoints with API Gateway
- ✅ Store data in DynamoDB
- ✅ Chain functions with Step Functions
- ✅ Set up automatic triggers with EventBridge
- ✅ Deploy to multiple environments
- ✅ Write Infrastructure as Code (SAM templates)

**Advanced Level:**
- ✅ Set up CI/CD pipelines with GitHub Actions
- ✅ Monitor applications with CloudWatch
- ✅ Optimize costs
- ✅ Implement security best practices
- ✅ Debug production issues

---

# 15. Configuration Templates

## Useful Templates You Can Copy & Modify

### Template 1: Simple Lambda Template

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31

Resources:
  HelloFunction:
    Type: AWS::Serverless::Function
    Properties:
      FunctionName: hello-world
      Runtime: python3.11
      Handler: app.lambda_handler
```

### Template 2: Lambda with S3 Trigger

```yaml
Resources:
  ImageProcessorFunction:
    Type: AWS::Serverless::Function
    Properties:
      Runtime: python3.11
      Handler: image_processor.lambda_handler
      Events:
        S3UploadEvent:
          Type: S3
          Properties:
            Bucket: !Ref MyBucket
            Events: s3:ObjectCreated:*
  
  MyBucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: my-bucket-12345
```

### Template 3: API Gateway + Lambda + DynamoDB

```yaml
Resources:
  MyAPI:
    Type: AWS::Serverless::Api
    Properties:
      StageName: Prod

  GetFunction:
    Type: AWS::Serverless::Function
    Properties:
      Handler: get.lambda_handler
      Policies:
        - DynamoDBCrudPolicy:
            TableName: !Ref UsersTable
      Events:
        GetAPI:
          Type: Api
          Properties:
            RestApiId: !Ref MyAPI
            Path: /users/{id}
            Method: GET

  UsersTable:
    Type: AWS::DynamoDB::Table
    Properties:
      TableName: users
      AttributeDefinitions:
        - AttributeName: id
          AttributeType: S
      KeySchema:
        - AttributeName: id
          KeyType: HASH
      BillingMode: PAY_PER_REQUEST
```

### Template 4: launch.json for Local Debugging

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "aws-sam",
      "request": "direct-invoke",
      "name": "Debug Lambda with SAM",
      "invokeTarget": {
        "target": "template",
        "logicalId": "HelloFunction"
      },
      "runtime": "python3.11",
      "payload": {
        "json": {
          "name": "Test User"
        }
      }
    }
  ]
}
```

---

## Helpful Resources

- [AWS Toolkit Documentation](https://docs.aws.amazon.com/toolkit-for-vscode/)
- [AWS SAM Documentation](https://docs.aws.amazon.com/serverless-application-model/)
- [AWS Lambda Best Practices](https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html)
- [CloudWatch Logs Documentation](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/)
- [AWS Cost Management](https://aws.amazon.com/cost-management/)

---

## Next Steps

1. **Complete all 20 activities** in order (foundation first!)
2. **Build a real project** combining multiple services
3. **Join AWS communities** for help and networking
4. **Keep learning** about new AWS services
5. **Practice, practice, practice!**

---

**Congratulations! You're now ready to build serverless applications with AWS! 🎉**



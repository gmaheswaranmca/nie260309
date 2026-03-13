### Logging

### AWS CloudTrail

Explain:

* Tracks **who performed actions**
* Used for auditing and security.

Example:

```
User deletes EC2
CloudTrail records it
```

## AWS CloudTrail – Logging and Auditing

### What is AWS CloudTrail?

**AWS CloudTrail** is a service that records **all API activities happening inside an AWS account**.

It helps you answer questions like:

* **Who did an action?**
* **When was it done?**
* **From where was it done?**
* **What resource was affected?**

CloudTrail is mainly used for **security monitoring, auditing, and compliance**.

---

### What CloudTrail Tracks

CloudTrail records **API calls made in AWS**, such as:

| Action           | Example                          |
| ---------------- | -------------------------------- |
| EC2 operations   | Launch, stop, terminate instance |
| IAM changes      | Create user, attach policy       |
| S3 access        | Create bucket, delete object     |
| Security changes | Modify security groups           |

Each action becomes an **event record**.

---

### Example Scenario

Suppose someone deletes an EC2 instance.

```
User deletes EC2 instance
        ↓
AWS API call happens
        ↓
CloudTrail records the event
        ↓
Event stored in logs
```

CloudTrail log will contain details like:

* **User name** – who performed the action
* **Time** – when the action occurred
* **Source IP** – where the request came from
* **Resource** – which EC2 instance was affected
* **Action** – what operation was performed

Example event:

```
Event Name: TerminateInstances
User: traineruser
Service: EC2
Time: 2026-03-12T15:20:00Z
Source IP: 103.x.x.x
```

---

### Where CloudTrail Logs Are Stored

CloudTrail logs can be stored in:

* **Amazon S3** → Long-term log storage
* **Amazon CloudWatch** → Real-time monitoring and alerts

Example flow:

```
User Action
    ↓
AWS API Call
    ↓
CloudTrail records event
    ↓
Logs stored in S3 / CloudWatch
```

---

### Key Uses of CloudTrail

**1️⃣ Security Investigation**

If someone changes a security rule:

```
Security group modified
        ↓
CloudTrail shows who changed it
```

---

**2️⃣ Compliance & Auditing**

Companies use CloudTrail logs to prove:

* Who accessed resources
* What changes were made
* When the change happened

---

**3️⃣ Troubleshooting**

Example:

```
EC2 instance terminated unexpectedly
        ↓
Check CloudTrail
        ↓
Find user or service that deleted it
```

---

### Simple One-Line Summary

**CloudTrail records every action performed in AWS so you know who did what and when.**



## AWS CloudTrail – 5 Minute Practical Lab (Demo)

This lab helps students **see how AWS records user actions** for **security and auditing**.

We will:

1. Enable CloudTrail
2. Perform an action (create/delete resource)
3. View the recorded event

Service used: **AWS CloudTrail**

---

# Step 1 — Open CloudTrail

1. Login to **AWS Console**
2. Search **CloudTrail**
3. Open **CloudTrail Dashboard**

You will see **Event history**.

Important:
CloudTrail **already records events automatically** in Event History.

---

# Step 2 — Perform an Action

Now perform a simple action.

Example: Create an EC2 instance.

Go to:

**Amazon EC2**

Steps:

1. Open **EC2**
2. Click **Launch Instance**
3. Name: `cloudtrail-demo`
4. Select **Amazon Linux**
5. Click **Launch Instance**

Even if the instance is stopped or terminated later, the action is **logged**.

---

# Step 3 — Go Back to CloudTrail

1. Open **CloudTrail**
2. Click **Event History**

Now filter:

```
Event source = ec2.amazonaws.com
```

You will see events like:

| Event              | Meaning     |
| ------------------ | ----------- |
| RunInstances       | EC2 created |
| StartInstances     | EC2 started |
| StopInstances      | EC2 stopped |
| TerminateInstances | EC2 deleted |

---

# Step 4 — Open an Event

Click **RunInstances**.

You will see details:

Example information recorded:

| Field      | Meaning                     |
| ---------- | --------------------------- |
| Event Name | RunInstances                |
| Username   | traineruser                 |
| Event Time | When it happened            |
| Source IP  | Where the request came from |
| Region     | AWS region                  |
| Resource   | Instance ID                 |

Example:

```
Event: RunInstances
User: traineruser
Source IP: 49.xx.xx.xx
Region: ap-south-1
```

---

# Step 5 — Show the JSON Log

Scroll down → **Event record**

You will see **full JSON log** like:

```json
{
  "eventName": "RunInstances",
  "eventSource": "ec2.amazonaws.com",
  "userIdentity": {
     "type": "IAMUser",
     "userName": "traineruser"
  },
  "awsRegion": "ap-south-1"
}
```

Explain:

> CloudTrail records **every API call as JSON logs**.

---

# Demo Architecture

```
User Action
     ↓
AWS API Call
     ↓
CloudTrail records event
     ↓
Visible in Event History
```

---

# What Students Learn

Students understand:

✔ AWS tracks all actions
✔ Security auditing
✔ Troubleshooting resource changes
✔ API-based cloud operations

---

# Best Demo Trick (Students Love This)

Ask a student to:

1. Delete EC2 instance

Then show CloudTrail event:

```
TerminateInstances
User: student-user
```

Explain:

> Even if a resource is deleted, **CloudTrail remembers who deleted it**.

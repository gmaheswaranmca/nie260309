**Final Recap + Architecture Demo (30 min)** to understand the difference between **Serverless vs Server-based architecture**.

---

# Final Recap + Architecture Demo

## 1️⃣ Serverless Architecture

Architecture:

```
User
 ↓
CloudFront (CDN)
 ↓
S3 (React Static Website)
 ↓
API Gateway
 ↓
Lambda (Backend Logic)
 ↓
DynamoDB (Database)
```

### Explanation Flow

**User**

* User opens the website in browser.

↓

**CloudFront**

* Global CDN
* Delivers content faster from nearest location.

Example:

```
User in India → CloudFront Edge Location → Website loads faster
```

↓

**S3**

* Stores **React build files**
* Works as **static website hosting**

Files stored:

```
index.html
main.js
style.css
images
```

↓

**API Gateway**

* Works like **front door for backend APIs**
* Receives requests from frontend

Example:

```
GET /trainers
POST /students
```

↓

**Lambda**

* Backend code runs here
* No server management required

Example:

```
Node.js
Python
Java
```

↓

**DynamoDB**

* Fully managed **NoSQL database**

Example table:

```
Trainer
-------------
id
name
skills
```

---

### Key Idea

You **do not manage servers**.

AWS automatically handles:

* Scaling
* Infrastructure
* Availability

You **pay only when API runs**.

---

# 2️⃣ Server-Based Architecture

Architecture:

```
User
 ↓
Application Load Balancer
 ↓
EC2 Instances (Auto Scaling)
 ↓
Backend Application
 ↓
MongoDB Atlas / RDS
```

### Explanation Flow

**User**

User opens the website.

↓

**ALB (Application Load Balancer)**

* Distributes traffic to multiple EC2 instances

Example:

```
User 1 → EC2 Instance 1
User 2 → EC2 Instance 2
User 3 → EC2 Instance 3
```

↓

**EC2 Instances**

These are **virtual servers** running your application.

Example:

```
Node.js app
Python Flask app
Java Spring Boot
```

↓

**Auto Scaling Group**

Automatically creates more EC2 instances when load increases.

Example:

```
CPU > 70%
 → Launch new EC2 instance
```

↓

**Database**

Options:

* MongoDB Atlas
* Amazon RDS (MySQL, PostgreSQL)

---

# Key Difference

| Feature           | Serverless Architecture | Server-Based Architecture |
| ----------------- | ----------------------- | ------------------------- |
| Server management | ❌ No                    | ✅ Yes                     |
| Scaling           | Automatic               | Auto Scaling required     |
| Cost              | Pay per request         | Pay for running servers   |
| Best for          | APIs, event systems     | Full applications         |
| Infrastructure    | Managed by AWS          | Managed by DevOps         |

---

# Simple Analogy (Students love this)

### Serverless = Taxi

You **pay only when you travel**.

```
Ride → Pay
No ride → No payment
```

Example:

```
Lambda execution
```

---

### Server-based = Own Car

You pay even if not using.

```
Car EMI
Fuel
Maintenance
Parking
```

Example:

```
Running EC2 instances
```

---

# Final Closing Statement for Students

In real-world systems companies often use **both architectures together**.

Example:

```
Frontend → S3 + CloudFront

Heavy backend → EC2

Small APIs → Lambda

Database → RDS / DynamoDB
```

This is called **Hybrid Cloud Architecture**.

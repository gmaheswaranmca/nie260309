To place **two EC2 instances behind an Application Load Balancer (ALB)** in AWS, follow these **simple step-by-step instructions**.

---

## 1️⃣ Ensure EC2 Instances are Ready

Before creating the load balancer:

1. Launch **2 EC2 instances**.
2. Both instances must:

   * Be in the **same VPC**
   * Have **HTTP server running** (Node, Nginx, Apache, React build server etc.)
3. Security Group of EC2 must allow:

| Type | Port | Source               |
| ---- | ---- | -------------------- |
| HTTP | 80   | Anywhere (0.0.0.0/0) |

Test first:

```
http://EC2_PUBLIC_IP
```

Both instances should show the application.

---

## 2️⃣ Create Target Group

ALB sends traffic to a **Target Group**.

Go to:

**EC2 → Target Groups → Create Target Group**

Settings:

| Option      | Value           |
| ----------- | --------------- |
| Target type | Instances       |
| Protocol    | HTTP            |
| Port        | 80              |
| VPC         | Select your VPC |

Health Check:

| Option   | Value |
| -------- | ----- |
| Protocol | HTTP  |
| Path     | /     |

Click **Next**

Now **Register Targets**

Select:

* EC2 Instance 1
* EC2 Instance 2

Click **Include as pending below**

Then:

**Create Target Group**

---

## 3️⃣ Create Application Load Balancer

Go to:

**EC2 → Load Balancers → Create Load Balancer**

Choose:

**Application Load Balancer**

---

### Basic configuration

| Setting | Value           |
| ------- | --------------- |
| Name    | my-alb          |
| Scheme  | Internet-facing |
| IP type | IPv4            |

---

### Network Mapping

Select **at least 2 subnets**

Example:

* us-east-1a
* us-east-1b

(ALB requires 2 availability zones)

---

### Security Group

Create or select a security group allowing:

| Type | Port | Source    |
| ---- | ---- | --------- |
| HTTP | 80   | 0.0.0.0/0 |

---

### Listener

Default:

```
HTTP : 80
```

---

### Forward To Target Group

Select the **Target Group** created earlier.

---

Click **Create Load Balancer**

---

## 4️⃣ Wait for Health Check

Go to:

**EC2 → Target Groups → Targets**

You should see:

```
Instance1 → healthy
Instance2 → healthy
```

If you see ❌ **unhealthy**, usually:

* Port mismatch
* Health check path wrong
* Security group issue

---

## 5️⃣ Test the Load Balancer

Go to:

**EC2 → Load Balancers**

Copy the **DNS name**

Example:

```
http://my-alb-123456789.us-east-1.elb.amazonaws.com
```

Open in browser.

Refresh multiple times.

Traffic will go to **both EC2 instances**.

---

## 6️⃣ Simple Demo Trick (Recommended for Teaching)

In each EC2 instance:

### Instance 1

```
Instance 1 Server
```

### Instance 2

```
Instance 2 Server
```

Now refresh ALB URL.

You will see:

```
Instance 1
Instance 2
Instance 1
Instance 2
```

This shows **load balancing**.

---

✅ **Architecture**

```
Users
   │
   ▼
Application Load Balancer
   │
   ├── EC2 Instance 1
   └── EC2 Instance 2
```

---

## 7️⃣ Important Security Group Rule (Very Important)

**EC2 security group**

Allow traffic **from ALB security group**, not from internet.

Example:

```
Type: HTTP
Port: 80
Source: ALB-SecurityGroup
```

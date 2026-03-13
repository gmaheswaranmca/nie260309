## ☁️ Amazon CloudWatch – Monitoring EC2

**Amazon CloudWatch** is a monitoring and observability service in **Amazon Web Services** used to track metrics, logs, and alarms for AWS resources such as **Amazon EC2**, **Amazon RDS**, **Amazon S3**, etc.

It helps detect problems and automatically trigger alerts.

---

# 📊 What CloudWatch Monitors

For **EC2 instances**, CloudWatch provides default metrics:

| Metric            | Meaning                  |
| ----------------- | ------------------------ |
| CPUUtilization    | CPU usage percentage     |
| NetworkIn         | Incoming network traffic |
| NetworkOut        | Outgoing network traffic |
| DiskReadOps       | Disk read operations     |
| DiskWriteOps      | Disk write operations    |
| StatusCheckFailed | Instance health          |

Example:

```
CPU Utilization = 75%
→ Server is under heavy load
→ CloudWatch Alarm can trigger notification
```

---

# 🔔 Practical Lab – Create CPU Utilization Alarm

Goal:

```
EC2 CPU > 70%
      ↓
CloudWatch Alarm Triggered
```

---

# Step 1 — Open CloudWatch

1. Login to **AWS Console**
2. Search **CloudWatch**
3. Open **CloudWatch Dashboard**

---

# Step 2 — Go to Alarms

Left menu:

```
CloudWatch
   ↓
Alarms
   ↓
Create Alarm
```

Click **Create Alarm**

---

# Step 3 — Select Metric

Choose:

```
Select metric
   ↓
EC2
   ↓
Per-Instance Metrics
```

Select:

```
CPUUtilization
```

Choose your **EC2 instance**

Click **Select Metric**

---

# Step 4 — Configure Condition

Set:

```
Threshold type : Static
Whenever CPUUtilization is

Greater than : 70
```

Period:

```
5 minutes
```

Evaluation:

```
1 datapoint within 5 minutes
```

Meaning:

```
If CPU > 70% for 5 minutes
→ Alarm triggers
```

---

# Step 5 — Configure Notification

Choose **SNS Topic**

Create new topic:

```
Topic name: ec2-cpu-alert
Email: your-email@gmail.com
```

You will receive **email confirmation**.

---

# Step 6 — Name the Alarm

Example:

```
Alarm Name:
EC2-High-CPU-Alarm
```

Click:

```
Create Alarm
```

---

# 📈 Final Architecture

```
EC2 Instance
     │
     │ CPU Utilization Metric
     ▼
CloudWatch Monitoring
     │
     │ CPU > 70%
     ▼
CloudWatch Alarm
     │
     ▼
SNS Notification
     │
     ▼
Email Alert
```

---

# 🧪 Test the Alarm (Demo for Students)

Login to EC2 and run CPU load.

Example:

```bash
sudo yum install stress -y
stress --cpu 2 --timeout 300
```

This will increase CPU usage.

CloudWatch will detect:

```
CPU > 70%
```

Alarm will change state:

```
OK → ALARM
```

You will receive **email alert**.

---

# 🧠 Trainer Tip (For Your AWS Training)

This practical demonstrates **3 AWS services integration**:

```
EC2 → CloudWatch → SNS
```

# Trainer Demonstration
```
-> CloudWatch
-> Alarms
-> Create Alarm
-> Metric
    -> Select Metric
    -> EC2
    -> Per-Instance Metrics
        -> CPUUtilization
   -> Conditions
      -> Greater than : Define the threshold value:70
   -> Next
-> Configure Actions
   -> In alarm 
      -> topic -> Create
      -> name: "cpu-alert"
   -> Email endpoints that will receive the notification…
      -> gmaheswaranmca@gmail.com
      -> Create Topic
   -> Next
-> Add alarm details
   -> name: cpu-alarm
   -> Next
-> Create Alarm

-> Go to mail -> Confirm
```
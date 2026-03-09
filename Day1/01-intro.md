## I) Cloud Computing Models

### A. Service Models (What you consume)

#### 1. Infrastructure as a Service (IaaS)
**Definition:**
You rent virtualized computing resources — servers, storage, networking — and manage the OS and applications yourself.

**You manage:**
OS, middleware, runtime, applications, data
**Cloud provider manages:**
Hardware, virtualization, networking

**AWS Examples:**

* Amazon Web Services
* Amazon EC2
* Amazon EBS
* Amazon VPC

**Use Cases:**

* Hosting custom web apps
* Dev/Test environments
* Lift-and-shift migration

---

#### 2. Platform as a Service (PaaS)
**Definition:**
You deploy applications; cloud manages infrastructure and runtime.

**You manage:**
Application code, configuration
**Cloud provider manages:**
OS, runtime, scaling, patching

**AWS Examples:**

* AWS Elastic Beanstalk
* AWS Lambda
* Amazon RDS

**Use Cases:**

* Web & mobile backend APIs
* Microservices
* Serverless applications

---

#### 3. Software as a Service (SaaS)
**Definition:**
Complete software delivered via internet.

**You manage:**
Only usage & configurations
**Provider manages:**
Everything else

**Examples:**

* Amazon WorkSpaces
* Amazon QuickSight


## 🌩️ Cloud Computing – Service Models (Summary Table)

| Service Model | Full Form                   | What You Get                          | Who Manages What?                                                         | Best For                                   | Examples                                                            |
| ------------- | --------------------------- | ------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------ | ------------------------------------------------------------------- |
| **IaaS**      | Infrastructure as a Service | Virtual machines, storage, networking | 🔹 Cloud: Hardware, virtualization  <br> 🔹 User: OS, runtime, apps, data | System admins, DevOps, full control needed | Amazon EC2, Microsoft Azure Virtual Machines, Google Compute Engine |
| **PaaS**      | Platform as a Service       | Runtime environment, middleware, OS   | 🔹 Cloud: Infra + OS + runtime  <br> 🔹 User: Application & data          | Developers focusing only on coding         | AWS Elastic Beanstalk, Azure App Service, Google App Engine         |
| **SaaS**      | Software as a Service       | Ready-to-use software                 | 🔹 Cloud: Everything  <br> 🔹 User: Just uses the software                | End users, businesses                      | Gmail, Microsoft 365, Salesforce                                    |

---

## 🔎 Quick Understanding (Very Short)

* **IaaS** → You rent **infrastructure**
* **PaaS** → You rent a **development platform**
* **SaaS** → You use a **complete software**

---

## 🏗️ Responsibility Comparison

| Layer          | IaaS  | PaaS  | SaaS  |
| -------------- | ----- | ----- | ----- |
| Applications   | You   | You   | Cloud |
| Data           | You   | You   | Cloud |
| Runtime        | You   | Cloud | Cloud |
| OS             | You   | Cloud | Cloud |
| Virtualization | Cloud | Cloud | Cloud |
| Servers        | Cloud | Cloud | Cloud |
| Networking     | Cloud | Cloud | Cloud |

---

### B. Deployment Models (Where it runs)

| Model         | Description                       | Example           |
| ------------- | --------------------------------- | ----------------- |
| Public Cloud  | Resources shared across customers | AWS               |
| Private Cloud | Dedicated to single organization  | On-prem OpenStack |
| Hybrid Cloud  | Mix of public + private           | AWS + Data center |
| Multi-Cloud   | Multiple cloud providers          | AWS + Azure       |

---

## II) AWS Global Infrastructure

### Key Components

### 1. Regions

* Physical geographic areas (e.g., Mumbai, Frankfurt)
* Each region has multiple AZs
* Example: Asia Pacific (Mumbai)
* 
#### ✅ What is a Region?

A **Region** is a **separate geographic area**.

Each region contains multiple **Availability Zones (AZs)**.

📌 Example Regions:

* Asia Pacific (Mumbai)
* US East (N. Virginia)
* Europe (Frankfurt)

#### 🔹 Key Points

* Fully isolated from other regions
* Data does NOT automatically replicate between regions
* Choose region based on:

  * Customer location
  * Compliance requirements
  * Cost
  * Service availability
  * 
### 2. Availability Zones (AZs)

* One or more data centers inside a region
* Isolated but connected with low latency
* Example: ap-south-1a, ap-south-1b

#### ✅ What is an AZ?

An **Availability Zone** is:

* One or more data centers
* Inside a region
* Connected with low-latency private fiber

Example:

* Mumbai Region → ap-south-1a, ap-south-1b, ap-south-1c

#### 🔹 Why AZs?

* Protect against data center failure
* Used for High Availability architecture
* Deploy EC2 in multiple AZs

Example:

* EC2 in AZ-A
* EC2 in AZ-B
* Load Balancer distributes traffic


### 3. Edge Locations

* Used for content delivery & caching
* Used by Amazon CloudFront


#### ✅ What are Edge Locations?

Edge Locations are used for:

* Content delivery
* Caching
* Reducing latency

Mainly used by:

* Amazon CloudFront

#### 🔹 Purpose

If your server is in Mumbai and user is in London:

Instead of fetching data from Mumbai every time:

* Data is cached in London Edge Location
* Faster delivery

### 4. Regional Edge Cache

* Larger caching locations
* Between Region and Edge Location
* Improves performance for dynamic content

### 5. Local Zones & Wavelength Zones

* Bring AWS services closer to end users
* Low latency for gaming, 5G apps

#### 🌍 Local Zones

* Bring AWS services closer to large metro cities
* Reduce latency for gaming, media, real-time apps

Example:

* Los Angeles Local Zone

---

#### 🌐 Wavelength Zones

* Designed for 5G applications
* Ultra-low latency
* Used for IoT, AR/VR
---

### Why Global Infrastructure Matters?

* High Availability (HA)
* Disaster Recovery (DR)
* Fault Tolerance
* Low Latency
* Compliance (data residency)

---

#### 🏗️ Example Production Architecture (Exam 10–15 Marks)

Suppose:

Users in India

Architecture:

* Users → Route 53
* Route 53 → Load Balancer
* Load Balancer → EC2 in Multiple AZs
* Database → RDS Multi-AZ
* Static files → S3
* Global users → CloudFront Edge Locations

This ensures:

* High Availability
* Fault Tolerance
* Low Latency
* Scalability

---

#### 🧠 Quick Exam Summary

| Component         | Meaning             | Purpose                |
| ----------------- | ------------------- | ---------------------- |
| Region            | Geographic area     | Compliance & isolation |
| Availability Zone | Data center cluster | High availability      |
| Edge Location     | CDN location        | Low latency            |
| Local Zone        | City-level infra    | Ultra-low latency      |
| Wavelength        | 5G zone             | Real-time apps         |


## III) AWS Services Overview (Category Wise)

---

### i. Compute Services

* Amazon EC2 – Virtual machines
* AWS Lambda – Serverless functions
* Amazon ECS – Containers
* Amazon EKS – Kubernetes

#### More...

Used to run applications and workloads.

| Service               | Purpose               |                       |
| --------------------- | --------------------- | --------------------- |
| Amazon EC2            | Virtual servers (VMs) | Elastic Compute Cloud |
| AWS Lambda            | Serverless computing  |  |
| Amazon ECS            | Run Docker containers | Elastic Container Service |
| Amazon EKS            | Managed Kubernetes    | Elastic Kubernetes Service |
| AWS Elastic Beanstalk | PaaS deployment       |                       |
| AWS Fargate           | Serverless containers |                       |

---

#### 1. Amazon EC2 (Elastic Compute Cloud)

✅ What is EC2?

EC2 provides **virtual servers (instances)** in the cloud.

You choose:

* OS (Linux / Windows)
* CPU & RAM
* Storage
* Networking

---

#### 📌 Key Components

* AMI (Amazon Machine Image)
* Instance Type (t2.micro, m5.large, etc.)
* Security Group (Firewall)
* EBS Volume
* Key Pair (SSH login)

---

#### 🎯 Use Cases

* Web servers
* Application servers
* Dev/Test environments
* Custom enterprise applications

---

#### 💰 Pricing Models

* On-Demand
* Reserved
* Spot
* Savings Plans

---

#### 2. AWS Lambda (Serverless)

✅ What is Lambda?

Run code **without managing servers**.

* Upload code
* Define trigger
* AWS runs automatically

---

#### 📌 Triggers

* S3 upload
* API Gateway request
* DynamoDB change
* CloudWatch event

---

#### 🎯 Use Cases

* REST APIs
* File processing
* Event-driven systems
* Backend for mobile apps

---

#### 👍 Advantages

* No server management
* Auto scaling
* Pay per execution

#### ⚠️ Limitations

* Execution time limit
* Cold start latency

---

#### 3. Amazon ECS (Elastic Container Service)

✅ What is ECS?

Run and manage **Docker containers**.

Two modes:

* EC2 launch type
* Fargate launch type

---

#### 🎯 Use Cases

* Microservices
* Scalable backend systems
* Containerized applications

---

#### 4. Amazon EKS (Elastic Kubernetes Service)

✅ What is EKS?

Managed Kubernetes service.

If you know Kubernetes, EKS runs it on AWS without managing control plane.

---

#### 🎯 Use Cases

* Enterprise Kubernetes workloads
* Cloud-native applications
* Multi-container microservices

---

#### 5. AWS Fargate

✅ What is Fargate?

Serverless compute for containers.

You do NOT manage:

* EC2 instances
* Scaling
* Infrastructure

Used with:

* ECS
* EKS

---

#### 🎯 Best For

* Small teams
* Event-based container workloads
* Simplified container management

---

#### 6. AWS Elastic Beanstalk

✅ What is Elastic Beanstalk?

PaaS service to deploy:

* Java
* .NET
* Node.js
* Python
* PHP

You upload code → AWS handles:

* EC2
* Load Balancer
* Auto Scaling

---

#### 7. AWS Auto Scaling

✅ What is Auto Scaling?

Automatically increases or decreases EC2 instances based on:

* CPU usage
* Network traffic
* Custom metrics

---

#### 🔥 Production-Level Architecture (Compute Example)

Example Web App Architecture:

Users
↓
Route 53
↓
Load Balancer
↓
EC2 (Auto Scaling across AZs)
↓
RDS Database
↓
S3 for static files
↓
CloudFront for global delivery

This ensures:

* High availability
* Fault tolerance
* Scalability
* Cost optimization

---

#### 📊 Compute Services Comparison

| Service   | Server Management     | Scaling     | Best For              |
| --------- | --------------------- | ----------- | --------------------- |
| EC2       | You manage            | Manual/Auto | Full control          |
| Lambda    | No servers            | Automatic   | Event-driven          |
| ECS       | Container-based       | Manual/Auto | Docker apps           |
| EKS       | Kubernetes            | Advanced    | Enterprise K8s        |
| Fargate   | Serverless containers | Automatic   | Simplified containers |
| Beanstalk | Managed PaaS          | Automatic   | Quick deployment      |

---

#### 🧠 Quick Exam Summary

AWS Compute Services allow you to run applications in different ways:

* EC2 → Virtual machines
* Lambda → Serverless
* ECS/EKS → Containers
* Fargate → Serverless containers
* Beanstalk → PaaS deployment
* Auto Scaling → Automatic scaling

---

### ii. Storage Services
Storage services in Amazon Web Services
allow you to store data in different formats based on use case:
* Object Storage
* Block Storage
* File Storage
* Archival Storage
* Hybrid Storage

Examples:
* Amazon S3 – Object storage
* Amazon EBS – Block storage
* Amazon EFS – Shared file system
* Amazon S3 Glacier – Archive

---

#### 1. Amazon S3 (Simple Storage Service)
✅ What is S3?

S3 is **object storage** used to store:

* Images
* Videos
* Documents
* Backups
* Static website files

Data is stored as:

> Bucket → Object (File) → Metadata


---

#### 📌 Important Concepts

* Bucket (global unique name)
* Object (file)
* Versioning
* Lifecycle rules
* Storage classes
* IAM policies
* S3 is regional service

---

#### 📦 S3 Storage Classes

| Class                | Use Case                    |
| -------------------- | --------------------------- |
| Standard             | Frequently accessed data    |
| Intelligent-Tiering  | Auto cost optimization      |
| Standard-IA          | Infrequent access           |
| One Zone-IA          | Single AZ storage           |
| Glacier Instant      | Archive but quick retrieval |
| Glacier Flexible     | Archive                     |
| Glacier Deep Archive | Long-term archive           |

---

#### 🎯 Use Cases

* Static website hosting
* Backup & restore
* Data lake
* Media storage

---

#### 2. Amazon EBS (Elastic Block Store)
✅ What is EBS?

EBS is **block storage** used with EC2 instances.

It acts like a **hard disk** attached to a VM.

---
#### 📌 Key Features

* Attached to one EC2 (by default)
* Persistent storage
* Snapshots stored in S3
* Different volume types:
  * gp3 (General Purpose SSD)
  * io1/io2 (High performance)
  * st1 (Throughput optimized HDD)
  * sc1 (Cold HDD)

---

#### 🎯 Use Cases

* Database storage
* Boot volume for EC2
* High-performance applications

---

#### 3. Amazon EFS (Elastic File System)

✅ What is EFS?

EFS is **file storage** for multiple EC2 instances.

It supports:

* NFS protocol
* Shared access

---

#### 📌 Key Features

* Multi-AZ support
* Automatically scales
* Shared storage
* Good for Linux workloads

---

#### 🎯 Use Cases

* Content management systems
* Shared file systems
* Web servers sharing files

---

#### 4. Amazon S3 Glacier (Archival Storage)

✅ What is Glacier?

Low-cost long-term archival storage.

Used for:

* Compliance storage
* Backup archives
* Rarely accessed data

---
#### 📌 Retrieval Times

| Tier         | Retrieval Time   |
| ------------ | ---------------- |
| Instant      | Milliseconds     |
| Flexible     | Minutes to hours |
| Deep Archive | 12 hours         |

---
#### 5. AWS Storage Gateway (Hybrid Storage)

 ✅ What is Storage Gateway?

Connects on-premise data center to AWS cloud storage.

Used for:

* Hybrid cloud environments
* Gradual migration

---

#### 🔥 Storage Types Comparison

| Feature     | S3            | EBS               | EFS            | Glacier          |
| ----------- | ------------- | ----------------- | -------------- | ---------------- |
| Type        | Object        | Block             | File           | Archive          |
| Used With   | Internet apps | EC2               | Multiple EC2   | S3 lifecycle     |
| Shared?     | Yes (via URL) | No (single EC2)   | Yes            | No               |
| Scalability | Unlimited     | Limited by volume | Auto scaling   | Unlimited        |
| Best For    | Static data   | Databases         | Shared storage | Long-term backup |

---

#### 🏗️ Production Architecture Example

Web Application:

* Static files → S3
* EC2 boot volume → EBS
* Shared uploads → EFS
* Old backups → Glacier

This ensures:

* Cost optimization
* Performance
* High availability
* Durability (S3 = 11 9’s durability)

---

#### 🧠 Exam-Oriented Summary

AWS Storage Services include:

* S3 → Object storage
* EBS → Block storage
* EFS → File storage
* Glacier → Archival storage
* Storage Gateway → Hybrid storage

Each is selected based on:

* Access frequency
* Performance requirement
* Sharing requirement
* Cost optimization

---

#### ✅ When to Use What?

| Storage | Suitable for Database? | Why                                |
| ------- | ---------------------- | ---------------------------------- |
| EBS     | ✅ Yes                 | Block storage, low latency         |
| RDS     | ✅ Best option         | Managed DB, replication, backup    |
| EFS     | ❌ No                  | Shared file system, higher latency |
| S3      | ❌ No                  | Object storage only                |

---

### iii. Database Services
* Amazon RDS – MySQL, PostgreSQL
* Amazon DynamoDB – NoSQL
* Amazon Aurora – High performance DB
* Amazon Redshift – Analytics

---

#### Overview of AWS Database Services

AWS provides:

| Category              | Service     | Type                             |
| --------------------- | ----------- | -------------------------------- |
| Relational            | RDS         | SQL                              |
| Relational (Advanced) | Aurora      | High-performance SQL             |
| NoSQL                 | DynamoDB    | Key-Value / Document             |
| In-Memory             | ElastiCache | Redis / Memcached                |
| Data Warehouse        | Redshift    | Analytics                        |
| Graph                 | Neptune     | Graph DB                         |
| Time Series           | Timestream  | IoT / Metrics                    |
| Ledger                | QLDB        | Blockchain-like immutable ledger |
| Document              | DocumentDB  | MongoDB compatible               |

---

#### 1. What is RDS?

Managed relational database service.

Supported Engines:

* MySQL
* PostgreSQL
* MariaDB
* Oracle
* SQL Server

---

#### Key Features

##### ✅ Automated Backups

* Daily snapshot
* Point-in-time recovery

##### ✅ Multi-AZ Deployment

* Primary + Standby
* Automatic failover

##### ✅ Read Replicas

* Improve read performance
* Used for reporting

---

#### Architecture Example (Production)

```
Users
   ↓
Load Balancer
   ↓
Auto Scaling EC2
   ↓
RDS (Multi-AZ)
   ↓
Standby DB (Auto Failover)
```

---

#### When to Use RDS?

* Banking systems
* ERP
* E-commerce transactions
* Structured data

---

#### 2. Amazon Aurora

What is Aurora?

Cloud-optimized relational database built by AWS.

Compatible with: !Note: Compatible meaning "it is NOT" but "ported to"

* MySQL (OR)
* PostgreSQL

---

#### Why Aurora is Special?

| Feature                | Benefit         |
| ---------------------- | --------------- |
| 6 Copies across 3 AZs  | High durability |
| Auto-scaling storage   | Up to 128 TB    |
| Faster than MySQL      | 5x performance  |
| Faster than PostgreSQL | 3x performance  |

---

#### Architecture

Aurora separates:

* Compute Layer
* Storage Layer

Storage auto-replicates across AZs.

---

#### Aurora Serverless

* Auto-start
* Auto-pause
* Pay per usage
* Good for dev/test

---

#### When to Use?

* High traffic applications
* SaaS platforms
* Enterprise apps

---

#### 3. Amazon DynamoDB (NoSQL)
What is DynamoDB?

Fully managed NoSQL database.

Data Model:

* Key-Value
* Document

---

#### Key Concepts

##### 🔹 Partition Key

Primary identifier.

##### 🔹 Sort Key

Optional secondary key.

##### 🔹 Global Secondary Index (GSI)

Alternate query method.

---

#### Features

| Feature             | Benefit                  |
| ------------------- | ------------------------ |
| Serverless          | No infrastructure        |
| Millisecond latency | Fast                     |
| Global Tables       | Multi-region replication |
| Auto Scaling        | Handles traffic spikes   |

---

#### Use Cases

* Gaming leaderboards
* IoT
* Real-time analytics
* Serverless apps (Lambda)

---

#### 4. Amazon ElastiCache
What is ElastiCache?

In-memory caching service.

Supports:

* Redis
* Memcached

---

#### Why Use Cache?

Without Cache:

```
User → EC2 → RDS → Response (Slow)
```

With Cache:

```
User → EC2 → ElastiCache → Response (Fast)
```

---

#### Use Cases

* Session storage
* Leaderboards
* Frequently accessed data
* API response caching

---

#### 5. Amazon Redshift (Data Warehouse)

What is Redshift?

Petabyte-scale data warehouse.

Used for:

* Analytics
* Business Intelligence
* Reporting

---

#### Architecture

* Leader Node
* Compute Nodes
* Columnar storage

---

#### Use Case Example

```
S3 → Redshift → Power BI / Tableau
```

---

#### 6. Amazon Neptune (Graph DB)

What is Neptune?

Graph database.

Stores:

* Nodes
* Edges
* Relationships

#### 🧠 Summary — Who Uses Graph Databases

📍 **Enterprises / Corporates**
Airbus, Siemens, Samsung, UBS, eBay, NASA, Cisco

📍 **Financial Services**
JPMorgan Chase, Intuit, fraud detection teams in banks

📍 **Tech & Social Platforms**
LinkedIn-style recommendations & relationship analysis

📍 **Knowledge & Analytics**
Museums, scientific research knowledge graphs

📍 **Cloud Services**
AWS Neptune customers & Neo4j Atlas users

---

#### Use Cases

* Social networks
* Fraud detection
* Recommendation engines

---

#### 7. Amazon Timestream

Time-series database.

Used for:

* IoT sensor data
* Monitoring metrics
* DevOps monitoring

---

#### 8. Amazon QLDB

Ledger database.

Immutable transaction log.

Used for:

* Banking
* Financial audits
* Supply chain tracking

---

#### 9. Amazon DocumentDB

MongoDB-compatible document database.

Used for:

* JSON-based apps
* Content management
* Catalog systems

---

#### Simple Analogy

Think like this:

MySQL → AWS has Aurora MySQL (compatible)

PostgreSQL → AWS has Aurora PostgreSQL (compatible)

MongoDB → AWS has DocumentDB (compatible)

#### Comparison Table (Important for Exam)

| Feature    | RDS                     | Aurora                | DynamoDB       | Redshift       |
| ---------- | ----------------------- | --------------------- | -------------- | -------------- |
| Type       | Relational              | Relational            | NoSQL          | Data Warehouse |
| Serverless | ❌                       | ✅ (Serverless)        | ✅              | ❌              |
| Scaling    | Vertical + Read Replica | Auto storage          | Auto           | Cluster        |
| Best For   | Traditional Apps        | High-performance apps | Real-time apps | Analytics      |

---

#### Production-Level Architecture (Full Stack)

```
Users
   ↓
Route 53
   ↓
CloudFront
   ↓
ALB
   ↓
Auto Scaling EC2
   ↓
ElastiCache
   ↓
Aurora (Multi-AZ)
   ↓
S3 Backups
```

---

#### Important Viva Questions

1. Difference between RDS and Aurora?
2. What is Multi-AZ?
3. What is Read Replica?
4. DynamoDB vs RDS?
5. Why use ElastiCache?
6. What is Global Table?
7. When to use Redshift instead of RDS?

---

#### Basic Definition RDS and Aurora

| Feature  | Amazon RDS                                     | Amazon Aurora                            |
| -------- | ---------------------------------------------- | ---------------------------------------- |
| Type     | Managed relational DB service                  | Cloud-native relational DB               |
| Engines  | MySQL, PostgreSQL, Oracle, SQL Server, MariaDB | MySQL-compatible & PostgreSQL-compatible |
| Built By | AWS (manages standard DB engines)              | AWS (custom-built engine)                |

👉 **Simple Meaning**

* RDS = Managed traditional database
* Aurora = High-performance AWS-optimized database

---

#### Amazon RDS Architecture

How it Works

* DB runs on EC2 internally
* Storage attached (EBS)
* Multi-AZ = Standby copy in another AZ
* Failover takes 60–120 seconds

Storage is tied to the instance.

---

#### Amazon Aurora Architecture

How it Works

* Compute layer separated from storage
* Storage automatically replicates 6 copies across 3 AZs
* Faster failover (usually <30 seconds)
* Shared distributed storage

Storage is independent from compute.

---

#### Performance Difference

| Feature                | RDS      | Aurora          |
| ---------------------- | -------- | --------------- |
| MySQL Performance      | Standard | Up to 5x faster |
| PostgreSQL Performance | Standard | Up to 3x faster |
| Read Replicas          | Up to 5  | Up to 15        |
| Failover Speed         | Slower   | Faster          |

Aurora is designed for high traffic systems.

---

#### Availability & Durability

| Feature              | RDS                          | Aurora                |
| -------------------- | ---------------------------- | --------------------- |
| Multi-AZ             | Yes                          | Yes (default design)  |
| Copies of Data       | 2 copies (primary + standby) | 6 copies across 3 AZs |
| Auto-healing storage | No                           | Yes                   |

Aurora is more fault tolerant.

---

#### Scaling

| Feature           | RDS           | Aurora                   |
| ----------------- | ------------- | ------------------------ |
| Storage Scaling   | Manual        | Automatic (up to 128 TB) |
| Compute Scaling   | Manual resize | Faster scaling           |
| Serverless Option | No            | Yes (Aurora Serverless)  |

Aurora supports auto-start, auto-pause (good for dev/test).

---

#### Cost Difference

| RDS                 | Aurora              |
| ------------------- | ------------------- |
| Cheaper             | Slightly expensive  |
| Good for small apps | Best for enterprise |

If traffic is low → RDS
If traffic is high → Aurora

---

#### When To Use What?

✅ Use RDS When:

* Small to medium application
* Budget sensitive
* Using Oracle / SQL Server
* Traditional ERP systems

✅ Use Aurora When:

* High traffic e-commerce
* SaaS platform
* Banking systems
* Need high performance
* Need fast failover

---

#### Real Production Example

Small College Website

→ RDS MySQL (enough)

Amazon-like E-commerce

→ Aurora MySQL (high traffic)

---

#### Quick Interview Answer (1 Minute)

> Amazon RDS is a managed relational database service that supports multiple database engines like MySQL, PostgreSQL, Oracle, and SQL Server.
> Amazon Aurora is a cloud-native database built by AWS that is MySQL and PostgreSQL compatible, provides better performance, automatic storage scaling, 6-way replication across 3 Availability Zones, and faster failover.

---

### iv. Networking & Content Delivery
* Amazon VPC – Network isolation
* Amazon Route 53 – DNS
* Amazon CloudFront – CDN
* Elastic Load Balancing – Traffic distribution

---

### v. Security & Identity
* AWS Identity and Access Management – User & role management
* AWS Key Management Service – Encryption keys
* AWS Shield – DDoS protection
* AWS WAF – Web firewall

---

## IV) Cloud Advantages (Important for Exams & Interviews)

* Pay-as-you-go pricing
* Scalability
* Elasticity
* High availability
* Disaster recovery
* Global reach
* Security compliance
* Automation & DevOps ready

---

## 5) Shared Responsibility Model (Important Concept)

| AWS Responsible For | Customer Responsible For |
| ------------------- | ------------------------ |
| Physical security   | Data                     |
| Hardware            | IAM configuration        |
| Networking          | Application security     |
| Hypervisor          | OS patches (IaaS)        |

---

# Quick Summary

Cloud computing provides:

* Service Models → IaaS, PaaS, SaaS
* Deployment Models → Public, Private, Hybrid
* Global Infrastructure → Regions, AZs, Edge
* AWS Services → Compute, Storage, DB, Network, Security

```
```

AWS has **hundreds of services**, and many are commonly referred to by **abbreviations**. As a developer (especially since you are learning architecture and cloud systems), it is useful to know the **most common AWS abbreviations grouped by category**.

---

# AWS Cloud – Important Services, Concepts & Abbreviations

## 1. Compute Services

| Abbreviation | Full Form                  | Purpose                    |
| ------------ | -------------------------- | -------------------------- |
| **EC2**      | Elastic Compute Cloud      | Virtual machines in AWS    |
| **ECS**      | Elastic Container Service  | Container orchestration    |
| **EKS**      | Elastic Kubernetes Service | Managed Kubernetes         |
| **Fargate**  | (No abbreviation)          | Serverless containers      |
| **Lambda**   | AWS Lambda                 | Serverless compute         |
| **ASG**      | Auto Scaling Group         | Automatic scaling of EC2   |
| **AMI**      | Amazon Machine Image       | Template for EC2 instances |

---

## 2. Storage Services

| Abbreviation | Full Form              | Purpose               |
| ------------ | ---------------------- | --------------------- |
| **S3**       | Simple Storage Service | Object storage        |
| **EBS**      | Elastic Block Store    | Block storage for EC2 |
| **EFS**      | Elastic File System    | Shared file system    |
| **FSx**      | File System X          | Managed file systems  |
| **Glacier**  | Amazon S3 Glacier      | Archive storage       |
| **S3 IA**    | S3 Infrequent Access   | Low-cost storage tier |

---

## 3. Database Services

| Abbreviation    | Full Form                   | Purpose                         |
| --------------- | --------------------------- | ------------------------------- |
| **RDS**         | Relational Database Service | Managed SQL databases           |
| **Aurora**      | Amazon Aurora               | High-performance MySQL/Postgres |
| **DynamoDB**    | (No abbreviation)           | NoSQL key-value DB              |
| **DAX**         | DynamoDB Accelerator        | In-memory cache                 |
| **Neptune**     | Amazon Neptune              | Graph database                  |
| **QLDB**        | Quantum Ledger Database     | Ledger / immutable database     |
| **Timestream**  | Amazon Timestream           | Time-series database            |
| **ElastiCache** | (Redis/Memcached)           | In-memory cache                 |

---

## 4. Networking & CDN

| Abbreviation | Full Form                           | Purpose                        |
| ------------ | ----------------------------------- | ------------------------------ |
| **VPC**      | Virtual Private Cloud               | Private AWS network            |
| **IGW**      | Internet Gateway                    | Internet access                |
| **NAT**      | Network Address Translation Gateway | Private subnet internet access |
| **ELB**      | Elastic Load Balancer               | Traffic distribution           |
| **ALB**      | Application Load Balancer           | Layer 7 load balancing         |
| **NLB**      | Network Load Balancer               | High performance L4            |
| **Route53**  | Amazon Route 53                     | DNS service                    |
| **CF**       | CloudFront                          | CDN                            |
| **TGW**      | Transit Gateway                     | VPC interconnect               |

---

## 5. Messaging & Event Services

| Abbreviation    | Full Form                   | Purpose                 |
| --------------- | --------------------------- | ----------------------- |
| **SQS**         | Simple Queue Service        | Message queue           |
| **SNS**         | Simple Notification Service | Pub/Sub messaging       |
| **SES**         | Simple Email Service        | Email sending           |
| **EventBridge** | Amazon EventBridge          | Event bus               |
| **MQ**          | Amazon MQ                   | Managed message brokers |
| **Kinesis**     | Amazon Kinesis              | Real-time streaming     |

---

## 6. Security & Identity

| Abbreviation | Full Form                      | Purpose               |
| ------------ | ------------------------------ | --------------------- |
| **IAM**      | Identity and Access Management | Permissions           |
| **KMS**      | Key Management Service         | Encryption keys       |
| **STS**      | Security Token Service         | Temporary credentials |
| **WAF**      | Web Application Firewall       | Web protection        |
| **Shield**   | AWS Shield                     | DDoS protection       |
| **Cognito**  | Amazon Cognito                 | Authentication        |
| **ACM**      | AWS Certificate Manager        | SSL certificates      |

---

## 7. DevOps & Monitoring

| Abbreviation     | Full Form                                      | Purpose                |
| ---------------- | ---------------------------------------------- | ---------------------- |
| **CI/CD**        | Continuous Integration / Continuous Deployment | DevOps pipeline        |
| **CloudWatch**   | Amazon CloudWatch                              | Monitoring             |
| **CloudTrail**   | AWS CloudTrail                                 | API logging            |
| **CDK**          | Cloud Development Kit                          | Infrastructure as code |
| **SAM**          | Serverless Application Model                   | Serverless deployment  |
| **CodeBuild**    | AWS CodeBuild                                  | Build service          |
| **CodeDeploy**   | AWS CodeDeploy                                 | Deployment service     |
| **CodePipeline** | AWS CodePipeline                               | CI/CD pipeline         |

---

## 8. Analytics & Big Data

| Abbreviation   | Full Form         | Purpose             |
| -------------- | ----------------- | ------------------- |
| **EMR**        | Elastic MapReduce | Big data processing |
| **Athena**     | Amazon Athena     | Query S3 using SQL  |
| **Redshift**   | Amazon Redshift   | Data warehouse      |
| **Glue**       | AWS Glue          | ETL service         |
| **OpenSearch** | Amazon OpenSearch | Search analytics    |

---

## 9. Architecture Concepts

| Abbreviation | Full Form              | Meaning                   |
| ------------ | ---------------------- | ------------------------- |
| **AZ**       | Availability Zone      | Isolated data center      |
| **Region**   | AWS Region             | Geographic cluster of AZs |
| **IaC**      | Infrastructure as Code | Code-based infra          |
| **HA**       | High Availability      | Resilient systems         |
| **DR**       | Disaster Recovery      | Backup strategy           |
| **TTL**      | Time To Live           | Cache duration            |

---

## 10. Containers & Microservices

| Abbreviation | Full Form                  | Purpose                 |
| ------------ | -------------------------- | ----------------------- |
| **ECR**      | Elastic Container Registry | Docker registry         |
| **ECS**      | Elastic Container Service  | Container orchestration |
| **EKS**      | Elastic Kubernetes Service | Managed Kubernetes      |
| **FaaS**     | Function as a Service      | Lambda-like compute     |

---

💡 **Example Architecture Abbreviation Chain**

Typical AWS microservice architecture:

```
Client
   ↓
Route53
   ↓
CloudFront
   ↓
ALB
   ↓
ECS / Lambda
   ↓
SQS
   ↓
RDS / DynamoDB
   ↓
S3
```

---

✅ The **10 most important abbreviations for backend developers** are:

* **EC2**
* **S3**
* **Lambda**
* **RDS**
* **DynamoDB**
* **VPC**
* **SQS**
* **SNS**
* **IAM**
* **CloudWatch**

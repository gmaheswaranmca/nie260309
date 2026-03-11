If we move the **React frontend to Amazon S3**, the architecture becomes cleaner and closer to production. The **frontend is static**, so it can be hosted from S3, while **Express runs on EC2** and **MongoDB Atlas remains the database**.

Below is the **complete process from EC2 launch → GitHub → deployment → S3 frontend hosting**.

---

# 1. Final Architecture

```
User Browser
      |
      |
Amazon S3 (React static site)
      |
      | API calls
      |
EC2 Instance (Express API :5000)
      |
      |
MongoDB Atlas
```

Services involved:

* Amazon Web Services
* MongoDB
* Amazon EC2
* Amazon S3

---

# 2. Launch EC2 (Backend Only)

Go to **AWS Console → EC2 → Launch Instance**

Configuration:

| Setting       | Value        |
| ------------- | ------------ |
| AMI           | Ubuntu 22.04 |
| Instance type | t2.micro     |
| Storage       | 8GB          |

Security group:

| Type       | Port |
| ---------- | ---- |
| SSH        | 22   |
| Custom TCP | 5000 |

Launch instance.

---

# 3. Connect to EC2

```bash
ssh -i trainer.pem ubuntu@EC2_PUBLIC_IP
```

Example:

```bash
ssh -i trainer.pem ubuntu@54.xx.xx.xx
```

---

# 4. Update Server

```bash
sudo apt update
sudo apt upgrade -y
```

---

# 5. Install Node.js

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs
```

Check:

```bash
node -v
npm -v
```

---

# 6. Install Git

```bash
sudo apt install git -y
```

---

# 7. Clone GitHub Project

```bash
git clone https://github.com/yourusername/mern-trainer-app.git
```

Enter project:

```bash
cd mern-trainer-app
```

---

# 8. Setup Backend

```bash
cd backend
npm install
```

Create env file:

```bash
nano .env
```

Example:

```
PORT=5000
MONGO_URL=mongodb+srv://username:password@cluster.mongodb.net/trainerdb
```

Save.

---

# 9. Allow EC2 Access in MongoDB Atlas

Open **MongoDB Atlas**

Go to **Network Access**

Add:

```
0.0.0.0/0
```

This allows EC2 connection.

---

# 10. Run Backend

```bash
node server.js
```

Test API:

```
http://EC2_PUBLIC_IP:5000/trainers
```

Expected output:

```json
[
 { "name": "Mahesh", "skills": "React" },
 { "name": "Arun", "skills": "Node" },
 { "name": "Divya", "skills": "MongoDB" }
]
```

---

# 11. Keep Backend Running (PM2)

Install PM2:

```bash
sudo npm install pm2 -g
```

Start backend:

```bash
pm2 start server.js
```

Check:

```bash
pm2 list
```

Enable auto restart:

```bash
pm2 startup
pm2 save
```

---

# 12. Build React App Locally

On your **local machine**, go to frontend:

```bash
cd frontend
npm install
```

Update API URL.

Replace:

```
http://localhost:5000
```

with

```
http://EC2_PUBLIC_IP:5000
```

Then build:

```bash
npm run build
```

This creates:

```
dist/
```

---

# 13. Create S3 Bucket

Go to **Amazon S3**

Click **Create Bucket**

Example:

```
trainer-react-app
```

Settings:

* Region → same as EC2
* **Disable Block Public Access**
* Enable static hosting later

Create bucket.

---

# 14. Enable Static Website Hosting

Inside S3 bucket:

Go to **Properties**

Enable:

```
Static website hosting
```

Set:

```
Index document: index.html
Error document: index.html
```

---

# 15. Upload React Build

Open folder:

```
frontend/dist
```

Upload **all files inside dist** to S3 bucket.

Upload:

```
index.html
assets/
```

---

# 16. Allow Public Access

Go to **Permissions → Bucket Policy**

Add:

```json
{
"Version":"2012-10-17",
"Statement":[
{
"Sid":"PublicRead",
"Effect":"Allow",
"Principal":"*",
"Action":["s3:GetObject"],
"Resource":["arn:aws:s3:::trainer-react-app/*"]
}
]
}
```

---

# 17. Access Frontend

Go to:

```
S3 → Properties → Static Website Hosting
```

Example URL:

```
http://trainer-react-app.s3-website-us-east-1.amazonaws.com
```

Open in browser.

You will see:

```
TrainerApp
List Trainers
Add Trainer
```

---

# 18. Application Flow

```
User Browser
      |
      |
S3 Static Website
(React App)
      |
      | REST API
      |
EC2 Express Server
:5000
      |
      |
MongoDB Atlas
```

---

# 19. Why This Architecture Is Better

Advantages:

✔ React served by CDN (fast)
✔ EC2 only handles API
✔ scalable architecture
✔ lower server load
✔ cheaper hosting

---

# 20. Real Production Improvement

Companies usually add:

```
CloudFront
```

Architecture becomes:

```
User
  |
CloudFront CDN
  |
S3 (React)
  |
EC2 API
  |
MongoDB Atlas
```

* faster globally
* secure
* HTTPS

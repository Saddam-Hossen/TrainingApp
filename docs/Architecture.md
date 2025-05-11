
# 🏗️ System Architecture & Flow – TrainingApp

This document outlines the overall architecture and data flow for the TrainingApp platform.

---

## 📐 Architecture Overview

```
+-------------+       HTTPS       +----------------+       REST        +------------+       TCP/IP       +-----------+
|  Frontend   |  <--------------> |  Spring Boot   | <---------------> |  MongoDB   | <---------------> |   Files   |
|  (React.js) |                   |    Backend     |                   |  (NoSQL)   |                   |  (AWS S3) |
+-------------+                   +----------------+                   +------------+                   +-----------+
       |                                |                                      |                               |
       |                                |--> Auth & Authorization (JWT)        |                               |
       |                                |--> Business Logic                    |                               |
       |                                |--> REST APIs                         |                               |
       |                                |                                      |                               |
       |-----> Axios HTTP Calls ------->|                                      |                               |
```

---

## 🔁 Request-Response Flow

1. **User Login**
   - React login form sends `POST /api/auth/login` to Spring Boot
   - Server validates credentials, generates JWT, and returns it
   - Token is stored in frontend (e.g., localStorage)

2. **Fetching Data**
   - Frontend sends requests with JWT in `Authorization` header
   - Backend validates JWT and processes request
   - Data is retrieved from MongoDB and returned to the frontend

3. **Creating/Updating Resources**
   - Admin/Trainer can create training sessions, upload files
   - Files are stored on AWS S3 or similar cloud storage
   - MongoDB stores metadata (e.g., file links, training info)

4. **Tracking Progress**
   - Learners' progress and attendance are updated via `PUT /api/attendance`
   - Backend updates user-training relation in MongoDB

5. **Feedback Submission**
   - Learner sends POST feedback to Spring Boot
   - Feedback is saved in MongoDB under relevant training ID

---

## 🧩 Component Breakdown

### Frontend (React)
- Role-based dashboards
- Training calendar
- File upload components
- RESTful communication using Axios

### Backend (Spring Boot)
- RESTful API with layered architecture (Controller, Service, Repository)
- Security: JWT + Role-based access
- File management and validation
- Centralized error handling

### Database (MongoDB)
- Collections: `users`, `trainings`, `attendance`, `feedback`, `files`
- Schema-less structure suitable for flexible data models

---

## ☁️ Deployment & Infra

- Containerized using **Docker**
- Deployed on **AWS** using ECS or EC2 instances
- CI/CD via **GitHub Actions**
- Optional orchestration with **Kubernetes**

---

## ✅ Security Practices

- Passwords hashed using BCrypt
- JWT-based authentication & authorization
- HTTPS enforced
- Role-based API access control
- Secure file uploads

---


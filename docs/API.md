
# 📘 API Documentation – TrainingApp

> This document provides an overview of the key API endpoints for the TrainingApp backend (Spring Boot REST APIs).

---

## 🔐 Authentication

### `POST /api/auth/login`
Authenticate a user and retrieve a JWT token.

**Request Body**
```json
{
  "username": "admin_user",
  "password": "securePassword"
}
```

**Response**
```json
{
  "token": "jwt-token-string",
  "role": "ADMIN"
}
```

---

## 👥 Users

### `GET /api/users`
Get a list of all users. (Admin only)

**Headers**
```
Authorization: Bearer <jwt-token>
```

**Response**
```json
[
  {
    "id": "user123",
    "name": "John Doe",
    "role": "TRAINER",
    "email": "john@example.com"
  }
]
```

---

## 📆 Trainings

### `POST /api/trainings`
Create a new training session.

**Request Body**
```json
{
  "title": "Java Fundamentals",
  "trainerId": "trainer123",
  "startDate": "2024-01-10",
  "endDate": "2024-01-20",
  "description": "Introductory Java training for developers"
}
```

**Response**
```json
{
  "status": "success",
  "trainingId": "training456"
}
```

---

## 📥 Uploads

### `POST /api/uploads`
Upload resources like PDFs or videos for a session.

**Multipart Form Data**
- `file`: PDF or video
- `trainingId`: ID of the related session

**Response**
```json
{
  "status": "uploaded",
  "url": "https://your-bucket-url/training456/resource.pdf"
}
```

---

## ✅ Attendance & Progress

### `PUT /api/attendance`
Mark attendance or update progress.

**Request Body**
```json
{
  "userId": "learner123",
  "trainingId": "training456",
  "progress": 80
}
```

**Response**
```json
{
  "status": "updated"
}
```

---

## 📝 Feedback

### `POST /api/feedback`
Submit feedback for a training session.

**Request Body**
```json
{
  "userId": "learner123",
  "trainingId": "training456",
  "rating": 4,
  "comment": "Great content and delivery!"
}
```

**Response**
```json
{
  "status": "received"
}
```

---

## ℹ️ Notes

- All protected routes require a valid JWT token in the `Authorization` header.
- Roles: `ADMIN`, `TRAINER`, `LEARNER`
- Date format: `YYYY-MM-DD`


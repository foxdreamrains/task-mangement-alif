# Task Management System

> Technical Test - Backend (Go + Gin), Frontend (React Native), MySQL, Redis

## Overview

Task Management System adalah aplikasi sederhana untuk mengelola daftar tugas (Task Management) yang dibangun menggunakan:

- **Backend:** Golang (Gin Framework)
- **Database:** MySQL
- **Cache:** Redis
- **Frontend:** React Native + TypeScript

Aplikasi ini dibuat untuk memenuhi kebutuhan technical test dengan tetap memperhatikan clean code, struktur project yang baik, dan kemudahan maintenance.

---

# Technology Stack

## Backend

- Go 1.24+
- Gin
- GORM
- MySQL
- Redis
- Testify

## Frontend

- React Native
- TypeScript
- Axios
- React Navigation

---

# Features

## Backend

- Create Task
- Get All Tasks
- Get Task Detail
- Update Task
- Soft Delete Task
- Search Task
- Status Filter
- Assignee Filter
- Pagination
- Sorting
- Consistent Error Response
- Duplicate Title Validation (HTTP 409)
- Redis Cache
- Cache Invalidation

---

## Frontend

- Task List
- Search Task
- Filter by Status
- Pagination
- Edit Task Modal
- Loading Indicator
- Auto Refresh after Update
- Error Handling

---

# Project Structure

## Backend

```
backend
│
├── cmd
├── config
├── controllers
├── middleware
├── models
├── repository
├── routes
├── services
├── utils
├── tests
├── go.mod
└── main.go
```

---

## Frontend

```
frontend

src
│
├── api
├── components
├── hooks
├── navigation
├── screens
└── types
```

---

# Installation

## Clone Repository

```bash
git clone <repository-url>

cd task-management
```

---

# Backend Setup

## Install Dependencies

```bash
go mod tidy
```

---

## Create .env

```env
APP_PORT=8080

DB_HOST=localhost
DB_PORT=3306
DB_USER=root
DB_PASSWORD=password
DB_NAME=task_management

REDIS_HOST=localhost
REDIS_PORT=6379
```

---

## Run MySQL

Pastikan MySQL telah berjalan.

Buat database

```sql
CREATE DATABASE task_management;
```

---

## Run Redis

Windows

```
redis-server
```

Linux

```
sudo service redis-server start
```

---

## Run Backend

```bash
go run main.go
```

Backend akan berjalan pada

```
http://localhost:8080
```

---

# Frontend Setup

Masuk ke folder frontend

```bash
cd frontend
```

Install dependency

```bash
npm install
```

atau

```bash
yarn
```

---

Edit Base URL

```
src/api/index.ts
```

```typescript
export default axios.create({
    baseURL: "http://YOUR-IP:8080/api"
});
```

Jika menggunakan Android Emulator

```
10.0.2.2
```

Jika menggunakan perangkat fisik

```
IP Laptop
```

Contoh

```
192.168.1.10:8080
```

---

Run aplikasi

```bash
npx react-native run-android
```

atau

```bash
npx react-native run-ios
```

---

# API Endpoints

## Task

| Method | Endpoint | Description |
|---------|----------|-------------|
| GET | /api/tasks | Get All Tasks |
| GET | /api/tasks/:id | Get Task Detail |
| POST | /api/tasks | Create Task |
| PUT | /api/tasks/:id | Update Task |
| DELETE | /api/tasks/:id | Soft Delete |

---

## Filtering

```
GET /api/tasks
```

Query Parameter

| Parameter | Example |
|------------|---------|
| keyword | meeting |
| status | Done |
| assignee | Alif |
| page | 1 |
| limit | 10 |
| sort | created_at desc |

Example

```
GET /api/tasks?keyword=test&page=1&limit=10&status=Done
```

---

# Redis Cache

GET `/api/tasks`

Cache Duration

```
60 Seconds
```

Cache Key

```
tasks:{query-parameters}
```

Example

```
tasks?page=1&limit=10

tasks?status=Done&page=2

tasks?keyword=test
```

Cache akan dihapus otomatis setelah

- Create Task
- Update Task
- Delete Task

---

# Error Response

Semua endpoint menggunakan format response yang konsisten.

```json
{
    "success": false,
    "message": "Task not found"
}
```

---

# Success Response

```json
{
    "success": true,
    "message": "Task updated successfully",
    "data": {}
}
```

---

# Testing

## Backend

Menjalankan seluruh test

```bash
go test ./...
```

Coverage

- Update Task
- Search Task
- Cache Invalidation

---

## Frontend

```bash
npm test
```

Coverage

- Search Component
- Task List Component

---

# Assumptions

- Soft Delete menggunakan GORM.
- Redis hanya melakukan caching pada endpoint GET Task.
- Cache dihapus setiap terjadi perubahan data.
- Sorting default berdasarkan ID DESC.

---

# Future Improvements

- JWT Authentication
- Refresh Token
- Docker Support
- Swagger Documentation
- Unit Test Coverage >90%
- CI/CD Pipeline
- Logging
- Request Validation
- Role Based Access Control (RBAC)
- File Attachment
- Notification Service

---

# Screenshots

Tambahkan screenshot aplikasi pada bagian ini.

```
docs/

home.png
edit.png
search.png
```

---

# Author

**Alifi V**

Backend Developer

Technical Test Submission

---

# Notes

Terima kasih atas kesempatan yang diberikan untuk mengikuti proses technical test.

Aplikasi ini dikembangkan dengan fokus pada:

- Clean Architecture
- Readable Code
- Maintainability
- Scalability
- Best Practice Golang
- RESTful API Standard
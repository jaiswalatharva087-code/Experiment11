# Student REST API with JWT Authentication

A Node.js RESTful API built with Express and SQLite3 that features JSON Web Token (JWT) authorization for protected routes. This project allows managing student records securely by requiring valid JWT tokens for all CRUD operations.

---

## 📌 Features

- **JWT Authentication:** Secure `/auth/login` endpoint issuing 1-hour access tokens.
- **Protected Endpoints:** Middleware (`authenticateJWT`) enforcing token verification on all `/students` routes.
- **Database Integration:** SQLite3 database with automatic initialization and schema creation.
- **Full CRUD Support:** Create, Read, Update, and Delete student records.

---

## 🛠️ Tech Stack

- **Runtime:** Node.js
- **Framework:** Express.js
- **Database:** SQLite3
- **Authentication:** JSON Web Token (`jsonwebtoken`)

---

## 📁 Repository Structure

```text
.
├── app.js             # Main application entry point & API routes
├── db.js              # Database connection & schema initialization
├── mydatabase.db      # SQLite database file (generated at runtime)
├── package.json       # Node.js dependencies and scripts
└── README.md          # Project documentation

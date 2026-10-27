# Student REST API with JWT Authentication

A lightweight and secure RESTful API built with **Node.js, Express.js, and SQLite3**, featuring JSON Web Token (JWT) authentication. This project provides complete CRUD (Create, Read, Update, Delete) operations for managing student records, with protected endpoints requiring valid JWT authentication.

## 🚀 Features

- **JWT Authentication:** Login endpoint that generates signed JWT access tokens valid for 1 hour.
- **Protected Routes:** Middleware verifies JWT tokens before allowing access to student endpoints.
- **SQLite Database:** Lightweight database with automatic table initialization.
- **CRUD Operations:** Create, read, update, and delete student records.
- **Token Handling:** Supports Bearer tokens in the `Authorization` header and raw token strings, if implemented by the application.

## 🛠️ Tech Stack

- **Runtime:** Node.js
- **Web Framework:** Express.js
- **Database:** SQLite3
- **Authentication:** JSON Web Token (`jsonwebtoken`)

## 📁 Project Structure

```text
Student-REST-API/
├── app.js          # Server setup, API routes, and JWT middleware
├── db.js           # SQLite database connection and schema setup
├── package.json    # Dependencies and npm scripts
├── mydatabase.db   # SQLite database (created automatically)
└── README.md       # Project documentation
```

## 🚦 Getting Started

### Prerequisites

Make sure you have the following installed:

- [Node.js](https://nodejs.org/) (v14 or higher)
- npm (Node Package Manager)

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/your-username/your-repository-name.git
   ```

2. Navigate to the project directory:

   ```bash
   cd your-repository-name
   ```

3. Install dependencies:

   ```bash
   npm install
   ```

### Run the Server

```bash
npm start
```

The server initializes the SQLite database if it does not already exist and runs at:

`http://localhost:3000`

## 🔐 Environment Variables

You can configure a custom secret key for signing JWT tokens using the `JWT_SECRET` environment variable.

**Linux/macOS:**

```bash
export JWT_SECRET="your_custom_secure_secret"
```

**Windows PowerShell:**

```powershell
$env:JWT_SECRET="your_custom_secure_secret"
```

If the variable is not configured, the application uses the fallback secret `your_secret_key` for demonstration purposes.

## 📡 API Documentation

### Public Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | Returns a welcome message |
| POST | `/auth/login` | Authenticates the user and returns a JWT |

### 1. Root Endpoint

**Request:**

```http
GET /
```

**Response (200 OK):**

```text
Welcome to the Student
```

### 2. User Login

**Request:**

```http
POST /auth/login
Content-Type: application/json
```

**Default Credentials:**

```json
{
  "username": "admin",
  "password": "admin123"
}
```

**Successful Response (200 OK):**

```json
{
  "token": "YOUR_JWT_TOKEN"
}
```

Copy the returned token and use it to access protected endpoints.

### Protected Endpoints

All `/students` endpoints require a valid JWT access token.

**Authorization Header:**

```http
Authorization: Bearer YOUR_JWT_TOKEN
```

| Method | Endpoint | Description |
|---|---|---|
| GET | `/students` | Retrieve all students |
| GET | `/students/:id` | Retrieve a student by ID |
| POST | `/students` | Create a new student |
| PUT | `/students/:id` | Update an existing student |
| DELETE | `/students/:id` | Delete a student |

### Request Body Examples

**Create a Student — `POST /students`**

```json
{
  "name": "Alice",
  "age": 20,
  "grade": "A"
}
```

**Update a Student — `PUT /students/:id`**

```json
{
  "name": "Alice Smith",
  "age": 21,
  "grade": "A+"
}
```

Replace `:id` with the actual student ID when making requests.

## 🧪 Testing the API

### Option 1: Using Postman

1. Start the server.
2. Send a `POST` request to `http://localhost:3000/auth/login`.
3. Select **Body → raw → JSON** and enter the login credentials.
4. Copy the JWT token from the response.
5. Create a request to an endpoint such as `GET http://localhost:3000/students`.
6. Open the **Authorization** tab, select **Bearer Token**, and paste your token.
7. Send the request to test the protected endpoint.

### Option 2: Using cURL

**1. Login and obtain a token**

```bash
curl -X POST http://localhost:3000/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username":"admin","password":"admin123"}'
```

**2. Retrieve all students**

Replace `YOUR_JWT_TOKEN_HERE` with the token returned by the login endpoint.

```bash
curl -X GET http://localhost:3000/students \
  -H "Authorization: Bearer YOUR_JWT_TOKEN_HERE"
```

**3. Create a student**

```bash
curl -X POST http://localhost:3000/students \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN_HERE" \
  -d '{"name":"John Doe","age":22,"grade":"B"}'
```

## 🔒 Security Notes

This project uses hardcoded demonstration credentials (`admin` / `admin123`) and may use a fallback JWT secret. These settings are suitable only for learning and testing.

For production use:

- Hash passwords using a library such as `bcrypt`.
- Store user credentials securely in a database.
- Keep JWT secrets in environment variables.
- Use a strong, randomly generated JWT secret.
- Never commit `.env` files or sensitive credentials to GitHub.
- Validate and sanitize incoming request data.

## 📜 License

This project is available under the **MIT License**, provided the repository includes the corresponding MIT license terms.

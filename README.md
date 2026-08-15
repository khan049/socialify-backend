# Socialify Backend

Backend API for **Socialify**, a social platform focused on connecting users for communication and video calls.

The backend provides authentication, user onboarding, friend management, protected APIs, MongoDB persistence, and Stream Chat integration for real-time communication.

## 🚀 Features

* 🔐 JWT-based authentication using HTTP-only cookies
* 👤 User registration, login, logout, and onboarding
* 🔒 Protected routes with authentication middleware
* 🔑 Password hashing with bcrypt
* 👥 User recommendations and friend management
* 🤝 Send, accept, and manage friend requests
* 💬 Stream Chat integration for real-time communication
* 🎫 Secure Stream Chat token generation
* 🗄️ MongoDB database with Mongoose
* 🌐 CORS and cookie-based authentication
* 🧩 Modular controller, route, model, and middleware architecture

## 🛠️ Tech Stack

| Technology    | Purpose                   |
| ------------- | ------------------------- |
| Node.js       | Runtime                   |
| Express.js    | REST API                  |
| MongoDB       | Database                  |
| Mongoose      | ODM                       |
| JWT           | Authentication            |
| bcryptjs      | Password hashing          |
| Stream Chat   | Real-time communication   |
| Cookie Parser | Authentication cookies    |
| CORS          | Cross-origin requests     |
| dotenv        | Environment configuration |

## 🏗️ Architecture

```text
Client
  │
  ▼
Express API
  │
  ├── Authentication
  │     ├── Signup
  │     ├── Login
  │     ├── Logout
  │     └── Onboarding
  │
  ├── User Management
  │     ├── Recommendations
  │     ├── Friends
  │     └── Friend Requests
  │
  ├── Chat
  │     └── Stream Token Generation
  │
  └── Authentication Middleware
          │
          ▼
      MongoDB
          │
          ▼
     Stream Chat
```

## 📁 Project Structure

```text
socialify-backend/
│
├── src/
│   ├── controllers/
│   │   ├── auth.controller.js
│   │   ├── chat.controller.js
│   │   └── user.controller.js
│   │
│   ├── lib/
│   │   ├── db.js
│   │   └── stream.js
│   │
│   ├── middleware/
│   │   └── auth.middleware.js
│   │
│   ├── models/
│   │   ├── FriendRequest.js
│   │   └── User.js
│   │
│   ├── routes/
│   │   ├── auth.route.js
│   │   ├── chat.route.js
│   │   └── user.route.js
│   │
│   └── server.js
│
├── .gitignore
├── package.json
└── package-lock.json
```

## 🔐 Authentication Flow

Socialify uses JWT authentication stored in an HTTP-only cookie.

```text
Signup / Login
      │
      ▼
Validate credentials
      │
      ▼
Hash / verify password
      │
      ▼
Generate JWT
      │
      ▼
HTTP-only cookie
      │
      ▼
Protected API request
      │
      ▼
Authentication middleware
      │
      ▼
Authenticated user
```

Passwords are hashed using bcrypt before being stored, while protected routes verify the JWT and load the associated user without exposing the stored password.

## 👥 Friend System

Authenticated users can:

* Discover recommended users
* View their friends
* Send friend requests
* Accept incoming requests
* View incoming requests
* View outgoing pending requests

Friend relationships are stored using MongoDB references between users, while friend requests maintain a `pending` or `accepted` state.

## 💬 Real-Time Communication

Socialify integrates **Stream Chat** for real-time communication.

The backend:

1. Creates/updates Stream users when users sign up or complete onboarding.
2. Generates authenticated Stream Chat tokens.
3. Returns tokens only through protected chat routes.

```text
Authenticated User
       │
       ▼
GET /api/chat/token
       │
       ▼
JWT Authentication
       │
       ▼
Generate Stream Token
       │
       ▼
Stream Chat Client
```

## 🔌 API Overview

### Authentication

```http
POST /api/auth/signup
POST /api/auth/login
POST /api/auth/logout
POST /api/auth/onboarded
GET  /api/auth/me
```

### Users & Friends

```http
GET  /api/user/
GET  /api/user/friends
POST /api/user/friend-request/:id
PUT  /api/user/friend-request/:id/accept
GET  /api/user/friend-requests
GET  /api/user/outgoing-friend-requests
```

### Chat

```http
GET /api/chat/token
```

Most user and chat endpoints require authentication.

## ⚙️ Environment Variables

Create a `.env` file:

```env
PORT=5000

MONGO_URI=your_mongodb_connection_string

JWT_SECRET_KEY=your_jwt_secret

STREAM_API_KEY=your_stream_api_key
STREAM_API_SECRET=your_stream_api_secret
```

> Never commit your `.env` file or expose your Stream API secret.

## ▶️ Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/khan049/socialify-backend.git
cd socialify-backend
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

Create `.env` using the variables shown above.

### 4. Start development server

```bash
npm run dev
```

### 5. Start production server

```bash
npm start
```

## 🧪 Development

The project uses:

```bash
npm run dev
```

for development with Nodemon and:

```bash
npm start
```

for running the production server.

## 🔒 Security

The backend includes several security-focused practices:

* Password hashing with bcrypt
* JWT authentication
* HTTP-only authentication cookies
* Protected API routes
* Password exclusion when retrieving authenticated users
* Environment-based secret management
* CORS configuration

## 📌 Project Status

Backend implementation for the Socialify application.

The API is structured to support authentication, social connections, and real-time communication while keeping business logic separated into controllers, routes, models, and middleware.

## 👨‍💻 Author

**Junayed Ali Khan**

GitHub: https://github.com/khan049

# CogniDispatch Auth Service

The **Auth Service** is the authentication and identity control microservice within the **CogniDispatch** platform. It handles user registration, secure credential storage, and login authentication for both client roles (Homeowners) and emergency responders (Technicians/Vendors).

## 🚀 Technology Stack
*   **Runtime**: Node.js (v18+)
*   **Web Framework**: Express.js
*   **Security & Networking**: CORS, Helmet
*   **Cryptography**: Custom password hashing (via shared database adapter utility)

---

## 📁 Repository Structure
```
├── controllers/          # Express route controllers (Authentication logic)
│   └── authController.js # Signup and login workflows
├── shared/               # Database adapter and schema configs
├── Dockerfile            # Container build specification
├── package.json          # Node dependencies
└── server.js             # Entry point
```

---

## ⚙️ Environment Variables & Config

This service requires database connectivity. It reads the following parameters:

| Variable | Description | Default |
| :--- | :--- | :--- |
| `PORT` | Listening TCP Port for the service | `5001` |
| `MONGODB_URI_FILE` | Path to file containing Cosmos DB connection string (Key Vault secrets mounter) | *None* |
| `JWT_SECRET_FILE` | Path to file containing JWT token secret | *None* |

---

## 🛣️ API Endpoints

All routes are prefixed with `/api/auth`.

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| **GET** | `/api/auth/health` | Service health status check |
| **POST** | `/api/auth/register` | Registers a new user session. Roles: `HOMEOWNER` (client) or `TECHNICIAN` (vendor support) |
| **POST** | `/api/auth/login` | Authenticates email/password credentials and issues session details |

---

## 🛠️ Local Development

### 1. Prerequisites
*   Node.js (v18+)
*   A running local MongoDB instance (or Cosmos DB emulator)

### 2. Startup Commands
From the service root:
```bash
# Install dependencies
npm install

# Run the development server
npm start
```
The server will start listening at `http://localhost:5001/`.

---

## 🐳 Docker Container Build

```bash
docker build -t cogniregistry.azurecr.io/cogni-auth-service:latest .
```

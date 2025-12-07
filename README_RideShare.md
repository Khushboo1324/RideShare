# 🚖 RideShare – Ride Sharing Backend (Spring Boot + JWT + MongoDB)

A secure ride‑sharing backend built using **Spring Boot**, **JWT Authentication**, and **MongoDB**.  
Supports **User** and **Driver** roles with different permissions and ride lifecycle operations.

---

## 🛠 Tech Stack
| Component | Technology |
|---------|------------|
| Backend | Spring Boot 4 |
| Security | Spring Security + JWT |
| Database | MongoDB |
| Build Tool | Maven |
| Language | Java 21 |

---

## ▶️ How to Run Locally

### 1️⃣ Clone the repo
```bash
git clone https://github.com/khushboo1324/RideShare.git
cd RideShare
```

### 2️⃣ Configure `application.properties`
```properties
server.port=8080
spring.application.name=RideShare
spring.data.mongodb.uri=mongodb://localhost:27017/RideShareDB
jwt.secret= key-haha-haha-no-one-can-guess-this-haha-haha-1234567890
jwt.expiration-ms=3600000
```

### 3️⃣ Start MongoDB
Make sure MongoDB is running on your system (default port 27017).

### 4️⃣ Run the project
```bash
mvn spring-boot:run
```
Server will start at:
```text
http://localhost:8080
```

---

## 🔐 Authentication Flow

| Action | Endpoint | Method | Auth |
|-------|----------|--------|------|
| Register | `/api/auth/register` | POST | ❌ |
| Login | `/api/auth/login` | POST | ❌ |
| Other APIs | any `/api/v1/**` | — | ✔️ Requires JWT |

After login, you will receive a JWT token:
```json
{
  "token": "xxxxx.yyyyy.zzzzz"
}
```

Use this token in **Authorization Header** for all protected endpoints:
```text
Authorization: Bearer <TOKEN>
```

---

## 🧪 Request Samples (Postman)

### 🔹 Register (User / Driver)
```http
POST /api/auth/register
Content-Type: application/json

{
  "username": "ramesh",
  "password": "pass12345",
  "role": "USER"
}
```

```http
POST /api/auth/register
Content-Type: application/json

{
  "username": "driverA",
  "password": "pass12345",
  "role": "DRIVER"
}
```

### 🔹 Login
```http
POST /api/auth/login
Content-Type: application/json

{
  "username": "ramesh",
  "password": "pass12345"
}
```

---

## 🚕 Role-Based APIs

### 👤 USER APIs
| Action | Endpoint | Method |
|--------|----------|--------|
| Create ride request | `/api/v1/rides` | POST |
| View my rides | `/api/v1/user/rides` | GET |

📌 Example Create Ride Body:
```json
{
  "pickupLocation": "Mumbai",
  "dropLocation": "Delhi"
}
```

### 🚗 DRIVER APIs
| Action | Endpoint | Method |
|--------|----------|--------|
| View pending ride requests | `/api/v1/driver/rides/requests` | GET |
| Accept ride | `/api/v1/driver/rides/{rideId}/accept` | PUT |
| Complete ride | `/api/v1/rides/{rideId}/complete` | PUT |

---

## 📌 Status Flow of a Ride
```text
REQUESTED → ACCEPTED → COMPLETED
```

---

## 🗄 MongoDB Collections

| Collection | Stores |
|-----------|--------|
| `users` | User credentials and roles |
| `rides` | Ride records and driver assignment |

---

## 🎯 Future Scope (Optional)

- Payment integration
- Rating and feedback
- Live driver tracking
- Email/OTP notifications

---

## ⭐ Author

Developed by **Choudhary Khushboo**

---


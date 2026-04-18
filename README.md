# 🚍 Neo Booking System Backend

![Node.js](https://img.shields.io/badge/Node.js-Backend-green)
![Express](https://img.shields.io/badge/Express.js-Framework-black)
![MongoDB](https://img.shields.io/badge/MongoDB-Database-green)
![JWT](https://img.shields.io/badge/Auth-JWT-blue)
![License](https://img.shields.io/badge/License-MIT-yellow)

A robust backend API built using **Node.js, Express, and MongoDB** for the **Neo Booking System**, a bus reservation platform that supports secure authentication, real-time seat tracking, and booking management.

---

## 📌 Overview

The Neo Booking System backend is designed to handle all core operations of a bus booking application, including user management, bus search, seat availability tracking, and ticket booking.

---

## 🚀 Features

- 🔐 JWT-based user authentication
- 🔍 Bus search with filters (source, destination, price, company)
- 💺 Seat availability tracking by journey date
- 🧾 Booking creation and management
- 📡 RESTful API design for frontend integration
- 🗄️ MongoDB database integration

---

## 🛠️ Tech Stack

- **Backend:** Node.js, Express.js  
- **Database:** MongoDB  
- **Authentication:** JSON Web Tokens (JWT)  
- **Tools:** Postman / Thunder Client  

---

## 📋 Prerequisites

Make sure you have the following installed:

- Node.js (v14 or above)
- MongoDB (Local or MongoDB Atlas)
- npm or yarn

---

## ⚙️ Installation & Setup

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/your-username/neoyatra-backend.git
cd neoyatra-backend
2️⃣ Install Dependencies
npm install
3️⃣ Configure Environment Variables

Create a .env file in the root directory:

MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_secret_key
PORT=5000
🔗 MongoDB Setup
Using MongoDB Atlas
Create an account on MongoDB Atlas
Create a free cluster
Copy your connection string

Example:

MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/neoyatra?retryWrites=true&w=majority
Using Local MongoDB
MONGO_URI=mongodb://localhost:27017/neoyatra
4️⃣ Seed Sample Data (Optional)
node seed.js
5️⃣ Run the Server
npm run dev

Server will run at:

👉 http://localhost:5000

📡 API Endpoints
🔐 Authentication
Register User
POST /api/auth/register
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "password123"
}
Login User
POST /api/auth/login
{
  "email": "john@example.com",
  "password": "password123"
}

Response:

{
  "token": "jwt_token_here",
  "user": {
    "id": "user_id",
    "name": "John Doe",
    "email": "john@example.com"
  }
}
🚌 Bus Routes
Search Buses
GET /api/buses

Query Params:

from
to
maxPrice
company

Example:

/api/buses?from=Delhi&to=Lucknow&maxPrice=1500
Get Bus Details
GET /api/buses/:id
Check Seat Availability
GET /api/buses/:id/availability?journeyDate=YYYY-MM-DD

Response:

["1A", "2B", "5C"]
🎟️ Booking Routes
Create Booking (Protected)
POST /api/bookings

Headers:

x-auth-token: <your_token>
{
  "bus": "bus_id",
  "seats": ["1A", "2B"],
  "passengers": [
    {
      "name": "John Doe",
      "age": "25",
      "gender": "Male"
    }
  ],
  "total": 2400,
  "journeyDate": "2025-08-30"
}
Get My Bookings (Protected)
GET /api/bookings/my-bookings
🔒 Authentication

Protected routes require a valid JWT token in headers:

axios.get('/api/bookings/my-bookings', {
  headers: {
    'x-auth-token': 'your_jwt_token_here'
  }
})
📁 Project Structure
neoyatra-backend/
│
├── models/
│   ├── User.js
│   ├── Bus.js
│   └── Booking.js
│
├── routes/
│   ├── auth.js
│   ├── buses.js
│   └── bookings.js
│
├── middleware/
│   └── auth.js
│
├── db.js
├── server.js
├── seed.js
├── package.json
└── .env
🧪 Testing the API

Use tools like:

Postman
Thunder Client (VS Code extension)
Example cURL
# Register
curl -X POST http://localhost:5000/api/auth/register \
-H "Content-Type: application/json" \
-d '{"name":"Test User","email":"test@example.com","password":"password123"}'

# Login
curl -X POST http://localhost:5000/api/auth/login \
-H "Content-Type: application/json" \
-d '{"email":"test@example.com","password":"password123"}'
🐛 Troubleshooting
❌ MongoDB Connection Error
Verify MONGO_URI
Ensure MongoDB service is running
Check Atlas network access
❌ Port Already in Use
Change PORT in .env
Kill process using port 5000
❌ JWT Issues
Ensure JWT_SECRET is set
Use a valid random string
📈 Future Improvements
Online payment integration
Admin dashboard
Email/SMS booking confirmation
Real-time seat locking
Ticket cancellation & refund system

📜 License

This project is licensed under the MIT License.
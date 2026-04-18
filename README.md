Neo Booking System Backend

A backend service built with Node.js, Express, and MongoDB for the Neo Booking System bus reservation platform. This API handles user accounts, bus discovery, seat checking, and ticket booking operations.

Main Features
Secure user login and signup using JWT authentication
Search buses with multiple filter options
Check available and already-booked seats
Create and manage passenger bookings
Clean REST API structure for frontend integration
Requirements

Before running the project, make sure you have:

Node.js version 14 or above
MongoDB installed locally or a cloud database such as MongoDB Atlas
npm or yarn
Setup Instructions
1. Open the backend folder
cd neoyatra-backend
2. Install all required packages
npm install
3. Configure environment variables

Create a .env file inside the backend folder and add the following:

MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_secret_key
MongoDB Connection Options
Using MongoDB Atlas
Create an account on MongoDB Atlas
Build a free cluster
Copy the connection URI
Replace the password section with your actual database password

Example:

MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/neoyatra?retryWrites=true&w=majority
Using Local MongoDB
MONGO_URI=mongodb://localhost:27017/neoyatra
JWT Secret

Set any strong random string as your JWT secret.

Example:

JWT_SECRET=my_secure_secret_key
Optional: Add Sample Data

To insert demo bus records into the database, run:

node seed.js

This helps during testing by adding preloaded bus details.

Run the Server

Start the backend using:

npm run dev

Once started, the server will run at:

http://localhost:5000
API Routes
Authentication Routes
Register a User

POST /api/auth/register

Request body:

{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "password123"
}
Login

POST /api/auth/login

Request body:

{
  "email": "john@example.com",
  "password": "password123"
}

Response example:

{
  "token": "jwt_token_here",
  "user": {
    "id": "user_id",
    "name": "John Doe",
    "email": "john@example.com"
  }
}
Bus Routes
Search Buses

GET /api/buses

Supported query parameters:

from
to
maxPrice
company

Example:

/api/buses?from=Delhi&to=Lucknow&maxPrice=1500
Get Bus Details

GET /api/buses/:id

Returns details of a specific bus using its ID.

Check Seat Availability

GET /api/buses/:id/availability

Required query parameter:

journeyDate

Example:

/api/buses/123/availability?journeyDate=2025-08-30

Sample response:

["1A", "2B", "5C"]

This response contains the seat numbers that are already booked for the selected journey date.

Booking Routes
Create a Booking

POST /api/bookings

This is a protected route and requires a valid token in the x-auth-token header.

Request body:

{
  "bus": "bus_id_here",
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
View My Bookings

GET /api/bookings/my-bookings

This is also a protected route and requires the x-auth-token header.

It returns all bookings for the logged-in user, including bus information.

Authentication Note

Any protected API route must include the JWT token in the request header.

Example using Axios:

axios.get('/api/bookings/my-bookings', {
  headers: {
    'x-auth-token': 'your_jwt_token_here'
  }
})
Folder Structure
neoyatra-backend/
├── models/
│   ├── User.js
│   ├── Bus.js
│   └── Booking.js
├── routes/
│   ├── auth.js
│   ├── buses.js
│   └── bookings.js
├── middleware/
│   └── auth.js
├── db.js
├── server.js
├── seed.js
├── package.json
└── .env
Description
models/ → Contains database schemas
routes/ → Contains API route handlers
middleware/ → Includes authentication middleware
db.js → MongoDB connection configuration
server.js → Main server entry point
seed.js → Script for inserting demo bus data
API Testing

You can test the endpoints using tools such as:

Postman
Thunder Client
cURL

Example commands:

# Register a new user
curl -X POST http://localhost:5000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{"name":"Test User","email":"test@example.com","password":"password123"}'

# Login with existing account
curl -X POST http://localhost:5000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","password":"password123"}'
Common Issues and Fixes
Database Connection Problem
Make sure the MONGO_URI value in .env is correct
Confirm MongoDB is running if you are using a local database
If using Atlas, check whether your IP is allowed in network settings
Port Conflict
Change the PORT value in .env
Or stop the process already using port 5000
JWT Error
Verify that JWT_SECRET is present in the .env file
Use a proper random string instead of leaving it blank
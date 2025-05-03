### food-delivery-system

# Order Service
Overview
The Order Service is a core component of the Food-Delivery platform, responsible for managing the creation and tracking of customer orders. It provides a seamless experience for users to place orders with delivery details, integrating with other services (e.g., cart and restaurant services) to ensure a smooth order flow. This service focuses on order creation and management, ensuring scalability and reliability.

# Features

Order Creation: Allows users to create orders with delivery details such as address and phone number.
Order Tracking: Stores order details, including items, restaurant information, and status, for tracking purposes.
Cart Integration: Integrates with the cart service to fetch order items and clear the cart after order placement.
Error Handling: Implements robust error handling for order-related operations, ensuring a user-friendly experience.

# Prerequisites

Node.js: Version 14.x or higher.
MongoDB: A running MongoDB instance for storing order data.
Environment Variables: Configure the following in a .env file:PORT=5001
MONGODB_URI=mongodb://localhost:27017/order-service
JWT_SECRET=your-secret-key

# Installation

Clone the repository:
git clone https://github.com/your-username/your-repo.git
cd order-service

Install dependencies:
npm install


Set up environment variables:

Create a .env file in the root directory and add the required variables as listed above.

Start the application:
npm start

The service will run on http://localhost:5001 by default.

API Endpoints
Order Management

Create Order
POST /api/orders
Body: {
  "deliveryAddress": "123 Main St, City",
  "phoneNumber": "1234567890",
  "restaurantAddress": "456 Restaurant Ave, Food City"
}


Description: Creates a new order for the authenticated user, using items from their cart.
Response: 201 with { message: "Order created successfully", orderId, order, totalAmount } or 400/500 with error details.



# Frontend Integration
The Order Service integrates with a React frontend (e.g., CreateOrder component). Key integration points:

Order Creation Flow:
The CreateOrder component allows users to input delivery details (e.g., address, phone number) and fetches restaurant details based on the cart.
Upon submission, it sends a request to the /api/orders endpoint to create the order.


API Calls: Use axios or a similar library to call the above endpoints, passing JWT tokens in the Authorization header.
Error Handling: The frontend handles 400 and 500 responses with user-friendly messages (e.g., via react-toastify).

Models
Order Model

Schema:
customerId (String, required): The ID of the user placing the order.
restaurantId (String, required): The ID of the restaurant associated with the order.
items (Array of Objects, required): List of items in the order, each with:
itemId (String, required): Item ID.
name (String, required): Item name.
price (Number, required): Item price.
quantity (Number, required): Item quantity.


totalAmount (Number, required): The total cost of the order.
deliveryAddress (String, required): The delivery address for the order.
phoneNumber (String, required): The customer’s phone number.
restaurantAddress (String, optional): The address of the restaurant.
status (String, default: 'placed'): The status of the order (e.g., 'placed', 'accepted', 'preparing', 'delivered', 'canceled').
createdAt (Date, default: current timestamp): The timestamp when the order was created.


Dependencies

Express: For building the API server.
Mongoose: For MongoDB object modeling and schema validation.
jsonwebtoken: For JWT-based authentication.
dotenv: For managing environment variables.


# Testing

Unit Tests: Write tests for the order creation logic using jest and supertest.
Integration Tests: Test the API endpoints with a mock MongoDB instance (e.g., using mongodb-memory-server).
Manual Testing:
Use Postman to send a POST request to /api/orders with the required fields.
Verify the order is saved in MongoDB with the correct status and details.

Contributing

Fork the repository.
Create a new branch (git checkout -b feature/your-feature).
Make your changes and commit (git commit -m "Add your feature").
Push to the branch (git push origin feature/your-feature).
Create a Pull Request.

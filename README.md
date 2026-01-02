# 👕 T-Shirt Store Backend API

A production-ready RESTful API for an e-commerce t-shirt store built with Node.js, Express, and MongoDB.

[![Live API](https://img.shields.io/badge/API-Live-brightgreen)](https://tshirt-store.onrender.com/api-docs/)
[![Node.js](https://img.shields.io/badge/Node.js-18+-green)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Express-4.x-blue)](https://expressjs.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB-8.x-green)](https://www.mongodb.com/)
[![License](https://img.shields.io/badge/License-ISC-yellow)](./LICENSE)

<p align="center">
 <img src="https://user-images.githubusercontent.com/81709725/171385115-0a72bda1-fbc2-40c5-aa03-8acbb0912f6d.png" alt="T-Shirt Store API" />
</p>

## 📚 API Documentation

Explore the complete API documentation with interactive testing:

🔗 **[Live Swagger Documentation](https://tshirt-store.onrender.com/api-docs/)**

---

## ✨ Features

### 🔐 Authentication & Authorization

- **JWT-based authentication** with httpOnly cookies
- **Role-based access control** (User, Manager, Admin)
- Secure password hashing with bcrypt
- Password reset via email tokens

### 👤 User Management

- User registration with profile photo upload
- Login/Logout with secure token handling
- Forgot password & reset password flow
- User dashboard with profile updates
- Admin can manage all users

### 🛍️ Product Management

- Full CRUD operations for products
- Multiple product images via Cloudinary
- Product categories (shortsleeves, longsleeves, sweatshirt, hoodies)
- Product search, filtering & pagination
- Product reviews and ratings system

### 📦 Order Management

- Create and track orders
- Order history for users
- Admin order management with status updates
- Detailed order information with shipping details

### 💳 Payment Integration

- **Stripe** payment processing
- **Razorpay** payment processing
- Secure payment intent creation

---

## 🛠️ Tech Stack

| Category           | Technology                |
| ------------------ | ------------------------- |
| **Runtime**        | Node.js                   |
| **Framework**      | Express.js                |
| **Database**       | MongoDB with Mongoose ODM |
| **Authentication** | JWT (JSON Web Tokens)     |
| **File Upload**    | Cloudinary                |
| **Payments**       | Stripe, Razorpay          |
| **Email**          | Nodemailer                |
| **Documentation**  | Swagger/OpenAPI 3.0       |
| **Validation**     | Validator.js              |

---

## 🚀 Getting Started

### Prerequisites

- Node.js 18+ installed
- MongoDB database (local or Atlas)
- Cloudinary account
- Stripe account (for payments)
- Razorpay account (for payments)

### Installation

1. **Clone the repository**

```bash
git clone https://github.com/SaketKothari/tshirt-store-backend-api.git
cd tshirt-store-backend-api
```

2. **Install dependencies**

```bash
npm install
```

3. **Configure environment variables**

Create a `.env` file in the root directory:

```env
# Server
PORT=4000

# Database
MONGODB_URL=mongodb://localhost:27017/tshirt-store

# JWT
JWT_SECRET=your-super-secret-jwt-key
JWT_EXPIRY=3d
COOKIE_TIME=3

# Cloudinary
CLOUDINARY_NAME=your-cloud-name
CLOUDINARY_API_KEY=your-api-key
CLOUDINARY_API_SECRET=your-api-secret

# Stripe
STRIPE_API_KEY=sk_test_...
STRIPE_SECRET_KEY=sk_test_...

# Razorpay
RAZORPAY_API_KEY=rzp_test_...
RAZORPAY_SECRET=your-razorpay-secret

# Email (SMTP)
SMTP_HOST=smtp.mailtrap.io
SMTP_PORT=587
SMTP_USER=your-smtp-user
SMTP_PASS=your-smtp-password
```

4. **Start the server**

```bash
# Development mode (with hot reload)
npm run dev

# Production mode
npm start
```

5. **Access the API**

- API Base URL: `http://localhost:4000/api/v1`
- Swagger Docs: `http://localhost:4000/api-docs`

---

## 📁 Project Structure

```
tshirt-store-backend-api/
├── config/
│   └── db.js                 # MongoDB connection
├── controllers/
│   ├── homeController.js     # Health check endpoints
│   ├── userController.js     # User authentication & profile
│   ├── productController.js  # Product CRUD & reviews
│   ├── orderController.js    # Order management
│   └── paymentController.js  # Payment processing
├── middlewares/
│   ├── bigPromise.js         # Async error wrapper
│   └── user.js               # Auth & role middlewares
├── models/
│   ├── user.js               # User schema
│   ├── product.js            # Product schema
│   └── order.js              # Order schema
├── routes/
│   ├── home.js               # Home routes
│   ├── user.js               # User routes
│   ├── product.js            # Product routes
│   ├── order.js              # Order routes
│   └── payment.js            # Payment routes
├── utils/
│   ├── cookieToken.js        # JWT token helper
│   ├── customError.js        # Custom error class
│   ├── emailHelper.js        # Email sending utility
│   └── whereClause.js        # Query builder for filtering
├── views/
│   └── signuptest.ejs        # Test view template
├── app.js                    # Express app setup
├── index.js                  # Server entry point
├── swagger.yaml              # API documentation
└── package.json
```

---

## 🔌 API Endpoints

### Authentication

| Method | Endpoint                        | Description            |
| ------ | ------------------------------- | ---------------------- |
| POST   | `/api/v1/signup`                | Register new user      |
| POST   | `/api/v1/login`                 | User login             |
| GET    | `/api/v1/logout`                | User logout            |
| POST   | `/api/v1/forgotPassword`        | Request password reset |
| POST   | `/api/v1/password/reset/:token` | Reset password         |

### User Profile

| Method | Endpoint                       | Description      |
| ------ | ------------------------------ | ---------------- |
| GET    | `/api/v1/userdashboard`        | Get current user |
| POST   | `/api/v1/userdashboard/update` | Update profile   |
| POST   | `/api/v1/password/update`      | Change password  |

### Products

| Method | Endpoint                    | Description                     |
| ------ | --------------------------- | ------------------------------- |
| GET    | `/api/v1/products`          | Get all products (with filters) |
| GET    | `/api/v1/product/:id`       | Get single product              |
| GET    | `/api/v1/reviews?id=`       | Get product reviews             |
| PUT    | `/api/v1/review`            | Add/Update review               |
| DELETE | `/api/v1/review?productId=` | Delete review                   |

### Orders

| Method | Endpoint               | Description       |
| ------ | ---------------------- | ----------------- |
| POST   | `/api/v1/order/create` | Create new order  |
| GET    | `/api/v1/order/:id`    | Get order details |
| GET    | `/api/v1/myorder`      | Get user's orders |

### Payments

| Method | Endpoint                  | Description             |
| ------ | ------------------------- | ----------------------- |
| GET    | `/api/v1/stripekey`       | Get Stripe public key   |
| GET    | `/api/v1/razorpaykey`     | Get Razorpay public key |
| POST   | `/api/v1/capturestripe`   | Create Stripe payment   |
| POST   | `/api/v1/capturerazorpay` | Create Razorpay order   |

### Admin Routes

| Method | Endpoint                    | Description         |
| ------ | --------------------------- | ------------------- |
| GET    | `/api/v1/admin/users`       | Get all users       |
| GET    | `/api/v1/admin/user/:id`    | Get user by ID      |
| PUT    | `/api/v1/admin/user/:id`    | Update user         |
| DELETE | `/api/v1/admin/user/:id`    | Delete user         |
| GET    | `/api/v1/admin/products`    | Get all products    |
| POST   | `/api/v1/admin/product/add` | Add product         |
| PUT    | `/api/v1/admin/product/:id` | Update product      |
| DELETE | `/api/v1/admin/product/:id` | Delete product      |
| GET    | `/api/v1/admin/orders`      | Get all orders      |
| PUT    | `/api/v1/admin/order/:id`   | Update order status |
| DELETE | `/api/v1/admin/order/:id`   | Delete order        |

### Manager Routes

| Method | Endpoint                | Description                |
| ------ | ----------------------- | -------------------------- |
| GET    | `/api/v1/manager/users` | Get users with 'user' role |

---

## 🔒 Authentication

The API supports two authentication methods:

### 1. Cookie Authentication

After login, a JWT token is automatically set as an httpOnly cookie named `token`.

### 2. Bearer Token

Pass the JWT token in the Authorization header:

```
Authorization: Bearer <your-jwt-token>
```

---

## 🧪 Testing the API

### Using Swagger UI

Visit the [Swagger Documentation](https://tshirt-store.onrender.com/api-docs/) to test endpoints directly in your browser.

### Using cURL

```bash
# Register a new user
curl -X POST https://tshirt-store.onrender.com/api/v1/signup \
 -F "name=John Doe" \
 -F "email=john@example.com" \
 -F "password=password123" \
 -F "photo=@/path/to/photo.jpg"

# Login
curl -X POST https://tshirt-store.onrender.com/api/v1/login \
 -H "Content-Type: application/json" \
 -d '{"email":"john@example.com","password":"password123"}'

# Get all products
curl https://tshirt-store.onrender.com/api/v1/products
```

### Using Postman

Import the Swagger specification from `swagger.yaml` into Postman for a complete collection.

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the ISC License.

---

## 👨‍💻 Author

**Saket Kothari**

- Website: [saketkothari.vercel.app](https://saketkothari.vercel.app)\
- GitHub: [@SaketKothari](https://github.com/SaketKothari)

---

## ⭐ Show Your Support

Give a ⭐️ if this project helped you!

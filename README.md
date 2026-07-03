# Natours API

A powerful RESTful API backend for a tour booking application built with Node.js, Express, and MongoDB.

## 📝 Description

Natours is a comprehensive backend API that provides tour management functionality with advanced features including filtering, sorting, pagination, and field limiting. The project demonstrates best practices in Node.js development using MVC architecture, proper error handling, and environment configuration.

## ✨ Features

- **RESTful API Design**: Follows REST conventions for clean and predictable endpoints
- **CRUD Operations**: Complete Create, Read, Update, Delete functionality for tours
- **Advanced Querying**: 
  - Filtering with advanced operators (gte, gt, lte, lt)
  - Sorting by multiple fields
  - Pagination for large datasets
  - Field limiting for optimized responses
- **Error Handling**: Custom error handling with AppError class and catchAsync utility
- **Environment Configuration**: Secure management of environment variables with dotenv
- **MVC Architecture**: Clean separation of concerns with Models, Views, and Controllers
- **Data Validation**: Built-in validation with Mongoose schemas and validator library
- **Development Tools**: ESLint with Airbnb config, Prettier for code formatting
- **Logging**: HTTP request logging with Morgan in development mode

## 🛠 Technologies Used

### Backend
- **Node.js** (>=18.0.0) - JavaScript runtime
- **Express.js** - Web framework for Node.js
- **MongoDB** - NoSQL database
- **Mongoose** - MongoDB object modeling for Node.js

### Development Tools
- **dotenv** - Environment variable management
- **morgan** - HTTP request logger
- **slugify** - URL slug generation
- **validator** - String validation and sanitization
- **ESLint** - Code linting with Airbnb style guide
- **Prettier** - Code formatting

## 📁 Project Structure

```
starter/
├── controllers/           # Route controllers
│   ├── errorController.js # Error handling controller
│   ├── tourController.js  # Tour-related controllers
│   └── userController.js # User-related controllers
├── models/               # Data models
│   └── tourmodel.js     # Tour model schema
├── routes/              # API routes
│   ├── tourRoutes.js    # Tour routes
│   └── userRoutes.js    # User routes
├── utils/               # Utility functions
│   ├── AppError.js      # Custom error class
│   ├── apiFeatures.js   # Query building utility
│   └── catchAsync.js    # Async error wrapper
├── public/              # Static files
├── dev-data/            # Development data
├── app.js               # Express app configuration
├── server.js            # Server startup file
├── package.json         # Project dependencies
└── .env.example         # Environment variables template
```

## 🚀 Installation Guide

### Prerequisites
- Node.js (>=18.0.0)
- MongoDB installed and running
- Git

### Step 1: Clone the Repository
```bash
git clone <repository-url>
cd starter
```

### Step 2: Install Dependencies
```bash
npm install
```

### Step 3: Set Up Environment Variables
```bash
cp .env.example .env
```

Edit the `.env` file with your configuration:
```env
NODE_ENV=development
PORT=3000

# Database
DATABASE=mongodb://localhost:27017/natours
DATABASE_PASSWORD=your_database_password

# Mapbox Token (if using maps)
MAPBOX_TOKEN=your_mapbox_access_token_here
```

### Step 4: Start MongoDB
Make sure MongoDB is running on your system:
```bash
# For MongoDB Community Edition
sudo systemctl start mongod

# Or using Docker
docker run -d -p 27017:27017 --name mongodb mongo
```

## 🏃 Running the Project

### Development Mode
```bash
npm start
```
This will start the server with nodemon for automatic restarts on file changes.

### Production Mode
```bash
npm run start:prod
```

### Debug Mode
```bash
npm run debug
```

The server will start on `http://localhost:3000` by default.

## 📚 API Endpoints

### Tour Routes

| Method | Endpoint | Description | Example |
|--------|----------|-------------|---------|
| GET | `/api/v1/tours` | Get all tours with filtering, sorting, pagination | `GET /api/v1/tours?price[gte]=500&sort=price` |
| GET | `/api/v1/tours/:id` | Get a specific tour | `GET /api/v1/tours/5c88fa8cf4afda39709c2955` |
| POST | `/api/v1/tours` | Create a new tour | `POST /api/v1/tours` |
| PATCH | `/api/v1/tours/:id` | Update a tour | `PATCH /api/v1/tours/5c88fa8cf4afda39709c2955` |
| DELETE | `/api/v1/tours/:id` | Delete a tour | `DELETE /api/v1/tours/5c88fa8cf4afda39709c2955` |
| GET | `/api/v1/tours/top-5-cheap` | Get top 5 cheap tours (alias) | `GET /api/v1/tours/top-5-cheap` |

### User Routes

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/v1/users` | Get all users |
| GET | `/api/v1/users/:id` | Get a specific user |
| POST | `/api/v1/users` | Create a new user |
| PATCH | `/api/v1/users/:id` | Update a user |
| DELETE | `/api/v1/users/:id` | Delete a user |

### Query Parameters

#### Filtering
```bash
# Basic filtering
GET /api/v1/tours?duration=5&difficulty=easy

# Advanced filtering with operators
GET /api/v1/tours?price[gte]=500&price[lte]=1000
```

#### Sorting
```bash
# Sort by price (ascending)
GET /api/v1/tours?sort=price

# Sort by price (descending) and ratings
GET /api/v1/tours?sort=-price,ratingsAverage
```

#### Field Limiting
```bash
# Select specific fields
GET /api/v1/tours?fields=name,price,description

# Exclude fields
GET /api/v1/tours?fields=-duration,-guides
```

#### Pagination
```bash
# Page 2, 10 results per page
GET /api/v1/tours?page=2&limit=10
```

## 🚨 Error Handling

The API implements a comprehensive error handling system:

### Custom Error Class (AppError)
- Extends the native Error class
- Includes status code and operational error flag
- Provides consistent error responses

### catchAsync Utility
- Wraps async route handlers to eliminate try-catch blocks
- Automatically passes errors to the error handling middleware

### Error Response Format
```json
{
  "status": "error",
  "error": {
    "statusCode": 404,
    "status": "fail",
    "message": "No tour found with that ID"
  }
}
```

### Development vs Production Errors
- **Development**: Detailed error stack traces and messages
- **Production**: Generic error messages for security

## 🔧 Configuration

### Environment Variables
- `NODE_ENV`: Environment mode (development/production)
- `PORT`: Server port (default: 3000)
- `DATABASE`: MongoDB connection string
- `DATABASE_PASSWORD`: MongoDB password
- `MAPBOX_TOKEN`: Mapbox access token for map features

### Code Quality
- **ESLint**: Enforces code style and catches potential errors
- **Prettier**: Ensures consistent code formatting
- **Airbnb Style Guide**: Industry-standard JavaScript style guide

## 🚀 Future Improvements

- [ ] **Authentication & Authorization**: JWT-based user authentication
- [ ] **Rate Limiting**: Prevent API abuse with rate limiting middleware
- [ ] **Caching**: Implement Redis caching for improved performance
- [ ] **API Documentation**: Auto-generate API docs with Swagger/OpenAPI
- [ ] **Testing**: Unit and integration tests with Jest
- [ ] **File Uploads**: Image upload functionality for tours
- [ ] **Email Integration**: Notification system for bookings
- [ ] **Payment Integration**: Stripe or PayPal integration
- [ ] **Docker Support**: Containerize the application
- [ ] **CI/CD Pipeline**: Automated testing and deployment

## 👨‍💻 Author

**Usuman**
- GitHub: [@Abdulai059](https://github.com/Abdulai059)
- Project: [Natours API](https://github.com/Abdulai059/node-express-first-api)

## 📄 License

This project is licensed under the ISC License.

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](https://github.com/Abdulai059/node-express-first-api/issues).

---

**Note**: This is a learning project built to demonstrate Node.js, Express, and MongoDB best practices. Feel free to use it as a reference for your own projects!

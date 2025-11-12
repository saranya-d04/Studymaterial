# 🎯 Talent Gauge - Employee Assessment & Project Management System

![Node.js](https://img.shields.io/badge/-Node.js-339933?logo=node.js&logoColor=white)
![Express.js](https://img.shields.io/badge/-Express.js-000000?logo=express&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/-PostgreSQL-336791?logo=postgresql&logoColor=white)
![JWT](https://img.shields.io/badge/-JWT-000000?logo=jsonwebtokens&logoColor=white)
![Sequelize](https://img.shields.io/badge/-Sequelize-52B0E7?logo=sequelize&logoColor=white)

A comprehensive **role-based web application** built for enterprise-level employee assessment and project management, featuring robust authentication, role-based access control, and complete CRUD operations.

## 🚀 Features

### 🔐 Authentication & Security
- **JWT-based authentication** with access & refresh tokens
- **Role-based access control** (Admin/Evaluator)
- **Password hashing** with bcryptjs (12 salt rounds)
- **Secure middleware** for route protection
- **Input validation** and comprehensive error handling

### 👥 User Management
- **Admin users** - Full system access and user management
- **Evaluator users** - Assessment and evaluation capabilities
- **Profile management** with secure password updates
- **User creation and management** (Admin only)

### 📊 Core Modules
- **Employee Management** - Complete employee data handling
- **OJT Programs** - On-the-job training program management
- **OJT Topics** - Training topic categorization
- **Project Management** - Project assignment and tracking
- **Assessment System** - Performance evaluation and scoring

### 🛡️ Security Features
- **CORS configuration** for secure cross-origin requests
- **Helmet.js** for security headers
- **Morgan logging** for request tracking
- **Environment-based configuration**
- **SQL injection protection** via Sequelize ORM

## 🏗️ Technology Stack

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web application framework
- **PostgreSQL** - Primary database
- **Sequelize ORM** - Database object-relational mapping
- **JWT** - Authentication tokens
- **bcryptjs** - Password hashing
- **express-validator** - Input validation

### Development Tools
- **Postman** - API testing with comprehensive collections
- **PowerShell** - Test automation scripts
- **Git** - Version control

## 📁 Project Structure

```
backend/
├── src/
│   ├── config/
│   │   └── db.js                 # Database configuration
│   ├── controllers/
│   │   ├── BaseController.js     # Base CRUD controller
│   │   ├── authController.js     # Authentication logic
│   │   ├── userController.js     # User management
│   │   ├── employeeController.js # Employee operations
│   │   ├── ojtController.js      # OJT program management
│   │   ├── ojtTopicController.js # OJT topic handling
│   │   ├── projectController.js  # Project management
│   │   └── assessmentResultController.js # Assessment logic
│   ├── middleware/
│   │   ├── auth.js              # JWT authentication middleware
│   │   └── roleAuth.js          # Role-based authorization
│   ├── models/
│   │   ├── index.js             # Model associations
│   │   ├── User.js              # User model with password hashing
│   │   ├── Employee.js          # Employee data model
│   │   ├── OJT.js               # OJT program model
│   │   ├── OJTTopic.js          # OJT topic model
│   │   ├── Project.js           # Project management model
│   │   └── AssessmentResult.js  # Assessment scoring model
│   ├── routes/
│   │   ├── authRoutes.js        # Authentication endpoints
│   │   ├── users.js             # User management routes
│   │   ├── employees.js         # Employee CRUD routes
│   │   ├── ojts.js              # OJT program routes
│   │   ├── ojt-topics.js        # OJT topic routes
│   │   ├── projects.js          # Project management routes
│   │   └── assessments.js       # Assessment routes
│   └── utils/
│       ├── tokenManager.js      # JWT token utilities
│       └── validators.js        # Input validation helpers
├── *.postman_collection.json    # Comprehensive API testing
├── *.postman_environment.json   # Testing environment setup
├── test-auth.ps1               # PowerShell test automation
├── create-test-users.js        # Database initialization
└── server.js                   # Application entry point
```

## 🔧 Installation & Setup

### Prerequisites
- **Node.js** (v18 or higher)
- **PostgreSQL** (v13 or higher)
- **npm** or **yarn**

### 1. Clone Repository
```bash
git clone https://github.com/saranya-d04/Talent_gauge24.git
cd Talent_gauge24
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Environment Configuration
Create a `.env` file in the root directory:
```env
# Database Configuration
DB_HOST=localhost
DB_PORT=5432
DB_NAME=employee_assessment_new
DB_USER=your_db_user
DB_PASSWORD=your_db_password

# JWT Configuration
JWT_SECRET=your_super_secret_jwt_key_here_make_it_long_and_complex
JWT_REFRESH_SECRET=your_refresh_token_secret_key_here
JWT_EXPIRES_IN=24h
JWT_REFRESH_EXPIRES_IN=7d

# Server Configuration
PORT=5000
NODE_ENV=development

# CORS Configuration
FRONTEND_URL=http://localhost:3000
```

### 4. Database Setup
```bash
# Create database in PostgreSQL
createdb employee_assessment_new

# Initialize database and create test users
node create-test-users.js
```

### 5. Start Server
```bash
npm start
# or for development with auto-reload
npm run dev
```

Server will be running at: `http://localhost:5000`

## 🔑 API Endpoints

### Authentication
| Method | Endpoint | Description | Access |
|--------|----------|-------------|---------|
| POST | `/api/auth/login` | User login | Public |
| GET | `/api/auth/me` | Get current user profile | Authenticated |
| PUT | `/api/auth/profile` | Update user profile | Authenticated |
| PUT | `/api/auth/change-password` | Change password | Authenticated |
| POST | `/api/auth/refresh` | Refresh JWT token | Authenticated |
| POST | `/api/auth/logout` | User logout | Authenticated |

### Users (Admin Only)
| Method | Endpoint | Description | Access |
|--------|----------|-------------|---------|
| GET | `/api/users` | Get all users | Admin/Evaluator |
| GET | `/api/users/:id` | Get user by ID | Admin/Evaluator |
| POST | `/api/users` | Create new user | Admin |
| PUT | `/api/users/:id` | Update user | Admin/Evaluator |
| DELETE | `/api/users/:id` | Delete user | Admin |

### Employees
| Method | Endpoint | Description | Access |
|--------|----------|-------------|---------|
| GET | `/api/employees` | Get all employees | Admin/Evaluator |
| GET | `/api/employees/:id` | Get employee by ID | Admin/Evaluator |
| POST | `/api/employees` | Create employee | Admin/Evaluator |
| PUT | `/api/employees/:id` | Update employee | Admin/Evaluator |
| DELETE | `/api/employees/:id` | Delete employee | Admin |

### OJT Programs
| Method | Endpoint | Description | Access |
|--------|----------|-------------|---------|
| GET | `/api/ojts` | Get all OJT programs | Admin/Evaluator |
| GET | `/api/ojts/:id` | Get OJT by ID | Admin/Evaluator |
| POST | `/api/ojts` | Create OJT program | Admin/Evaluator |
| PUT | `/api/ojts/:id` | Update OJT program | Admin/Evaluator |
| DELETE | `/api/ojts/:id` | Delete OJT program | Admin |

### Projects
| Method | Endpoint | Description | Access |
|--------|----------|-------------|---------|
| GET | `/api/projects` | Get all projects | Admin/Evaluator |
| GET | `/api/projects/:id` | Get project by ID | Admin/Evaluator |
| POST | `/api/projects` | Create project | Admin/Evaluator |
| PUT | `/api/projects/:id` | Update project | Admin/Evaluator |
| DELETE | `/api/projects/:id` | Delete project | Admin |

### Assessments
| Method | Endpoint | Description | Access |
|--------|----------|-------------|---------|
| GET | `/api/assessments` | Get all assessments | Admin/Evaluator |
| GET | `/api/assessments/:id` | Get assessment by ID | Admin/Evaluator |
| POST | `/api/assessments` | Create assessment | Admin/Evaluator |
| PUT | `/api/assessments/:id` | Update assessment | Admin/Evaluator |
| DELETE | `/api/assessments/:id` | Delete assessment | Admin |

## 🧪 Testing

### Postman Collections
The repository includes comprehensive Postman collections:

1. **Import Collections:**
   - `Talent_Gauge_AUTH_Testing_Fixed.postman_collection.json`
   - `Talent_Gauge_Development.postman_environment.json`

2. **Test Sequence:**
   - Login as Admin → Get Profile → Test Role-based Access
   - Login as Evaluator → Test Limited Access
   - Error Scenarios → Invalid Credentials, Tokens, etc.

### PowerShell Testing
```powershell
# Run automated authentication tests
.\test-auth.ps1
```

### Default Test Users
| Role | Email | Password |
|------|-------|----------|
| Admin | admin@talentgauge.com | admin123 |
| Evaluator | evaluator1@talentgauge.com | eval123 |

## 🔒 Security Best Practices

- **Environment Variables** - All sensitive data in `.env`
- **Password Hashing** - bcryptjs with 12 salt rounds
- **JWT Security** - Separate access/refresh tokens with expiration
- **Input Validation** - express-validator for all inputs
- **SQL Injection Protection** - Sequelize ORM parameterized queries
- **CORS Configuration** - Controlled cross-origin access
- **Security Headers** - Helmet.js implementation

## 🚀 Deployment

### Production Environment
1. Set `NODE_ENV=production` in environment
2. Use strong JWT secrets (32+ characters)
3. Configure production database
4. Set up SSL/HTTPS
5. Configure proper CORS origins
6. Set up monitoring and logging

### Docker Support (Coming Soon)
```dockerfile
# Dockerfile will be added for containerized deployments
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👩‍💻 Author

**Saranya D** - [GitHub Profile](https://github.com/saranya-d04)

## 🙏 Acknowledgments

- Express.js community for excellent middleware ecosystem
- Sequelize team for robust ORM functionality
- PostgreSQL for reliable database performance
- JWT.io for authentication standards

---

⭐ **Star this repository if you found it helpful!**

🐛 **Found a bug?** [Create an issue](https://github.com/saranya-d04/Talent_gauge24/issues)

💡 **Have a feature request?** [Start a discussion](https://github.com/saranya-d04/Talent_gauge24/discussions)
# WeIntern - Internship & Job Portal

![WeIntern Banner](https://media.licdn.com/dms/image/v2/D4D0BAQHWluK5kMV56g/company-logo_200_200/company-logo_200_200/0/1736077351822/weinternx_logo?e=1761177600&v=beta&t=dDP2VZ6eLVcFjSvKOi0Ngn8HbtyLCqcGRewHDf_1SDY)


A platform that connects students with internships, projects, and real-world learning. Features include internship listings, dashboards, application tracking, and task management.

---

## 🚀 Features

### Student Module
- ✅ Registration/Login with JWT authentication
- 👤 Complete profile creation with resume upload
- 🔍 Advanced internship search and filtering
- 📝 One-click application system
- 📊 Personal dashboard with application tracking

### Recruiter Module
- 🏢 Post and manage internship listings
- 👥 Review and manage applicants
- ⭐ Shortlist and track candidates
- 📈 Analytics dashboard for recruitment insights

### Admin Module
- ✅ Company verification system
- 📊 Monitor platform data and analytics
- 🛠️ Manage internships and applications
- 📧 Handle service requests

### Core Features
- 📧 Email notifications via SendGrid/Nodemailer
- 🔐 Secure JWT-based authentication
- 📱 Responsive design with Tailwind CSS
- 🔄 Real-time status updates

### Future Enhancements
- 🤖 AI-based internship recommendations
- 💬 In-app chat system
- 📅 Interview scheduling
- 🎮 Gamification with badges
- 🔗 LinkedIn integration
- 👥 Multi-tenant support

---

## 🛠️ Tech Stack

### Backend
```
// Core Technologies
Node.js + Express.js     // Server framework
MongoDB + Mongoose       // Database and ODM
JWT                     // Token-based authentication
bcrypt                  // Password hashing
Nodemailer/SendGrid     // Email notifications
Express Validator       // Input validation
Multer                  // File upload handling
```

### Frontend
```javascript
// Frontend Stack
Next.js (React 18)      // UI framework with App Router
TypeScript              // Type-safe development
Tailwind CSS            // Utility-first CSS framework
shadcn/ui               // Modern component library
React Query             // Data fetching and caching
React Hook Form         // Form management
Zustand                 // State management
Lucide React            // Icon library
```

### DevOps & Tools
- **Git** - Version control
- **GitHub** - Code repository
- **Postman** - API testing
- **MongoDB Atlas** - Cloud database
- **Vercel/Netlify** - Frontend deployment
- **Heroku/Railway** - Backend deployment

---

## 📁 Project Structure

```
weintern/
├── backend/
│   ├── controllers/          # Business logic for API endpoints
│   │   ├── authController.js
│   │   ├── internshipController.js
│   │   ├── applicationController.js
│   │   └── serviceController.js
│   ├── models/              # MongoDB schemas
│   │   ├── User.js
│   │   ├── Internship.js
│   │   ├── Application.js
│   │   └── ServiceRequest.js
│   ├── routes/              # API routes
│   │   ├── auth.js
│   │   ├── internships.js
│   │   ├── applications.js
│   │   └── services.js
│   ├── middleware/          # Auth, validation, error handling
│   │   ├── auth.js
│   │   ├── validation.js
│   │   └── errorHandler.js
│   ├── utils/               # Email notifications, helpers
│   │   ├── sendEmail.js
│   │   └── helpers.js
│   ├── config/              # DB config, env variables
│   │   └── database.js
│   ├── app.js               # Express server setup
│   └── package.json
│
├── frontend/
│   ├── public/              # Static assets
│   ├── src/
│   │   ├── components/      # Reusable UI components
│   │   │   ├── ui/         # shadcn/ui components
│   │   │   ├── forms/      # Form components
│   │   │   ├── layout/     # Layout components
│   │   │   └── common/     # Common components
│   │   ├── app/            # Next.js App Router pages
│   │   │   ├── page.tsx    # Home page
│   │   │   ├── about/
│   │   │   ├── internships/
│   │   │   ├── dashboard/
│   │   │   └── auth/
│   │   ├── lib/            # Utilities and configurations
│   │   │   ├── api.ts      # API client
│   │   │   ├── utils.ts    # Helper functions
│   │   │   └── constants.ts
│   │   └── styles/         # Global styles
│   │       └── globals.css
│   ├── next.config.js
│   ├── tailwind.config.js
│   └── package.json
│
├── README.md
├── .gitignore
└── docker-compose.yml       # Optional containerization
```

---

## 🗄️ Database Schema

### Users Collection
```javascript
// User Model Schema
{
  _id: ObjectId,
  name: {
    type: String,
    required: true,
    trim: true
  },
  email: {
    type: String,
    required: true,
    unique: true,
    lowercase: true
  },
  passwordHash: {
    type: String,
    required: true
  },
  role: {
    type: String,
    enum: ['student', 'recruiter', 'admin'],
    default: 'student'
  },
  profile: {
    bio: String,
    skills: [String],
    location: String,
    resume: String,          // File path for resume
    company: String,         // For recruiter users
    website: String,         // For recruiter users
    phone: String,
    linkedin: String
  },
  isVerified: {
    type: Boolean,
    default: false
  },
  createdAt: {
    type: Date,
    default: Date.now
  },
  updatedAt: {
    type: Date,
    default: Date.now
  }
}
```

### Internships Collection
```javascript
// Internship Model Schema
{
  _id: ObjectId,
  title: {
    type: String,
    required: true
  },
  description: {
    type: String,
    required: true
  },
  requirements: [String],
  duration: {
    type: String,
    required: true
  },
  stipend: {
    amount: Number,
    currency: {
      type: String,
      default: 'INR'
    }
  },
  location: {
    type: String,
    required: true
  },
  type: {
    type: String,
    enum: ['remote', 'onsite', 'hybrid'],
    default: 'onsite'
  },
  skills: [String],
  companyId: {
    type: ObjectId,
    ref: 'User',
    required: true
  },
  applicationDeadline: Date,
  status: {
    type: String,
    enum: ['active', 'closed', 'draft'],
    default: 'active'
  },
  applicationsCount: {
    type: Number,
    default: 0
  },
  createdAt: {
    type: Date,
    default: Date.now
  },
  updatedAt: {
    type: Date,
    default: Date.now
  }
}
```

### Applications Collection
```javascript
// Application Model Schema
{
  _id: ObjectId,
  studentId: {
    type: ObjectId,
    ref: 'User',
    required: true
  },
  internshipId: {
    type: ObjectId,
    ref: 'Internship',
    required: true
  },
  status: {
    type: String,
    enum: ['applied', 'shortlisted', 'rejected', 'selected'],
    default: 'applied'
  },
  coverLetter: String,
  resumeUrl: String,
  appliedAt: {
    type: Date,
    default: Date.now
  },
  updatedAt: {
    type: Date,
    default: Date.now
  }
}
```

### ServiceRequests Collection
```javascript
// Service Request Model Schema
{
  _id: ObjectId,
  businessName: {
    type: String,
    required: true
  },
  email: {
    type: String,
    required: true
  },
  serviceType: {
    type: String,
    required: true
  },
  description: {
    type: String,
    required: true
  },
  status: {
    type: String,
    enum: ['pending', 'in-progress', 'completed'],
    default: 'pending'
  },
  createdAt: {
    type: Date,
    default: Date.now
  },
  updatedAt: {
    type: Date,
    default: Date.now
  }
}
```

---

## 🔌 API Endpoints

### Authentication Routes
```javascript
// Authentication endpoints
POST   /api/auth/signup          // Register new user
POST   /api/auth/login           // Login user
GET    /api/auth/me              // Get current user profile
POST   /api/auth/logout          // Logout user
POST   /api/auth/forgot-password // Send reset password email
POST   /api/auth/reset-password  // Reset password with token
```

### Internship Routes
```javascript
// Internship management endpoints
POST   /api/internships          // Create new internship (recruiter)
GET    /api/internships          // List all internships (with filters)
GET    /api/internships/:id      // Get specific internship details
PATCH  /api/internships/:id      // Update internship (recruiter)
DELETE /api/internships/:id      // Delete internship (recruiter)
GET    /api/internships/company/:id // Get company's internships
```

### Application Routes
```javascript
// Application management endpoints
POST   /api/applications         // Apply for internship (student)
GET    /api/applications         // List applications (admin/recruiter)
GET    /api/applications/student // Get current student's applications
GET    /api/applications/internship/:id // Get internship applications
PATCH  /api/applications/:id     // Update application status (recruiter)
DELETE /api/applications/:id     // Withdraw application (student)
```

### Service Request Routes
```javascript
// Service request endpoints
POST   /api/services            // Submit service request
GET    /api/services            // List service requests (admin)
PATCH  /api/services/:id        // Update request status (admin)
DELETE /api/services/:id        // Delete service request (admin)
```

### User Profile Routes
```javascript
// User profile management
GET    /api/users/profile       // Get user profile
PATCH  /api/users/profile       // Update user profile
POST   /api/users/upload-resume // Upload resume file
DELETE /api/users/profile       // Delete user account
```

---

## ⚙️ Installation & Setup

### Prerequisites
```bash
# Required software versions
Node.js >= 18.0.0
MongoDB >= 5.0
npm >= 8.0.0
```

### Environment Variables

**Backend `.env`:**
```env
# Server Configuration
NODE_ENV=development
PORT=5000

# Database
MONGODB_URI=mongodb://localhost:27017/weintern
# For MongoDB Atlas:
# MONGODB_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/weintern

# Authentication
JWT_SECRET=your_super_secure_jwt_secret_key_here_minimum_32_characters
JWT_EXPIRES_IN=7d

# Email Configuration (Choose one)
# SendGrid
SENDGRID_API_KEY=your_sendgrid_api_key_here

# Nodemailer (Gmail)
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=your-email@gmail.com
EMAIL_PASS=your-app-password

# File Upload
UPLOAD_PATH=./uploads
MAX_FILE_SIZE=5242880  # 5MB in bytes

# Frontend URL (for CORS)
FRONTEND_URL=http://localhost:3000

# Admin Configuration
ADMIN_EMAIL=admin@weintern.com
```

**Frontend `.env.local`:**
```env
# API Configuration
NEXT_PUBLIC_API_URL=http://localhost:5000
NEXT_PUBLIC_APP_URL=http://localhost:3000

# File Upload Configuration
NEXT_PUBLIC_MAX_FILE_SIZE=5242880

# Analytics (Optional)
NEXT_PUBLIC_GA_ID=your_google_analytics_id
```

### Installation Steps

1. **Clone the repository:**
```bash
git clone https://github.com/your-username/weintern.git
cd weintern
```

2. **Backend Setup:**
```bash
cd backend

# Install dependencies
npm install

# Install development dependencies
npm install -D nodemon concurrently

# Create uploads directory
mkdir uploads
```

3. **Frontend Setup:**
```bash
cd ../frontend

# Install dependencies
npm install

# Install additional UI dependencies
npm install @radix-ui/react-dialog @radix-ui/react-dropdown-menu
npm install lucide-react class-variance-authority clsx tailwind-merge
```

4. **Database Setup:**
```bash
# Option 1: Local MongoDB
# Start MongoDB service
sudo systemctl start mongod  # Linux
brew services start mongodb-community  # macOS

# Option 2: MongoDB Atlas
# Create account at https://cloud.mongodb.com
# Create cluster and get connection string
```

5. **Start Development Servers:**

**Backend (Terminal 1):**
```bash
cd backend
npm run dev
# Server running on http://localhost:5000
```

**Frontend (Terminal 2):**
```bash
cd frontend
npm run dev
# Application running on http://localhost:3000
```

---

## 🚀 Development Workflow

### Backend Development Commands
```bash
# Development with auto-restart
npm run dev

# Production mode
npm start

# Run tests
npm test

# Lint code
npm run lint

# Database seeding (if implemented)
npm run seed
```

### Frontend Development Commands
```bash
# Development server
npm run dev

# Build for production
npm run build

# Start production server
npm run start

# Run tests
npm run test

# Lint code
npm run lint

# Type checking
npm run type-check
```

### Code Examples

**Backend: Express Server Setup (app.js)**
```javascript
const express = require('express');
const cors = require('cors');
const helmet = require('helmet');
const rateLimit = require('express-rate-limit');
const connectDB = require('./config/database');
require('dotenv').config();

const app = express();

// Connect to database
connectDB();

// Middleware
app.use(helmet());
app.use(cors({
  origin: process.env.FRONTEND_URL,
  credentials: true
}));

// Rate limiting
const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100 // limit each IP to 100 requests per windowMs
});
app.use(limiter);

app.use(express.json({ limit: '10mb' }));
app.use(express.urlencoded({ extended: true }));

// Routes
app.use('/api/auth', require('./routes/auth'));
app.use('/api/internships', require('./routes/internships'));
app.use('/api/applications', require('./routes/applications'));
app.use('/api/services', require('./routes/services'));
app.use('/api/users', require('./routes/users'));

// Global error handler
app.use(require('./middleware/errorHandler'));

const PORT = process.env.PORT || 5000;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

**Frontend: API Client Setup (lib/api.ts)**
```typescript
// API Client Configuration
const API_BASE_URL = process.env.NEXT_PUBLIC_API_URL || 'http://localhost:5000';

class ApiClient {
  private baseURL: string;
  private token: string | null = null;

  constructor(baseURL: string) {
    this.baseURL = baseURL;
    this.token = typeof window !== 'undefined' 
      ? localStorage.getItem('token') 
      : null;
  }

  setToken(token: string) {
    this.token = token;
    if (typeof window !== 'undefined') {
      localStorage.setItem('token', token);
    }
  }

  private async request<T>(
    endpoint: string, 
    options: RequestInit = {}
  ): Promise<T> {
    const url = `${this.baseURL}${endpoint}`;
    const headers = {
      'Content-Type': 'application/json',
      ...(this.token && { Authorization: `Bearer ${this.token}` }),
      ...options.headers,
    };

    const response = await fetch(url, { ...options, headers });
    
    if (!response.ok) {
      const error = await response.json();
      throw new Error(error.message || 'API request failed');
    }

    return response.json();
  }

  // Authentication methods
  async login(email: string, password: string) {
    return this.request<{ token: string; user: any }>('/api/auth/login', {
      method: 'POST',
      body: JSON.stringify({ email, password }),
    });
  }

  async register(userData: any) {
    return this.request<{ token: string; user: any }>('/api/auth/signup', {
      method: 'POST',
      body: JSON.stringify(userData),
    });
  }

  // Internship methods
  async getInternships(filters?: any) {
    const params = filters ? `?${new URLSearchParams(filters)}` : '';
    return this.request<any>(`/api/internships${params}`);
  }

  async createInternship(internshipData: any) {
    return this.request<any>('/api/internships', {
      method: 'POST',
      body: JSON.stringify(internshipData),
    });
  }

  // Application methods
  async applyForInternship(applicationData: any) {
    return this.request<any>('/api/applications', {
      method: 'POST',
      body: JSON.stringify(applicationData),
    });
  }
}

export const apiClient = new ApiClient(API_BASE_URL);
```

---

## 🧪 API Testing

### Using cURL
```bash
# Health check
curl http://localhost:5000/health

# Register new user
curl -X POST http://localhost:5000/api/auth/signup \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "email": "john@example.com",
    "password": "password123",
    "role": "student"
  }'

# Login user
curl -X POST http://localhost:5000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "john@example.com",
    "password": "password123"
  }'

# Get internships (with authentication)
curl -H "Authorization: Bearer YOUR_JWT_TOKEN" \
     http://localhost:5000/api/internships

# Apply for internship
curl -X POST \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "internshipId": "64a1b2c3d4e5f6789012345",
    "coverLetter": "I am interested in this internship..."
  }' \
  http://localhost:5000/api/applications
```

### Postman Collection
```json
{
  "info": {
    "name": "WeIntern API",
    "description": "Complete API collection for WeIntern platform"
  },
  "variable": [
    {
      "key": "baseUrl",
      "value": "http://localhost:5000"
    },
    {
      "key": "token",
      "value": ""
    }
  ],
  "item": [
    {
      "name": "Authentication",
      "item": [
        {
          "name": "Register",
          "request": {
            "method": "POST",
            "header": [],
            "body": {
              "mode": "raw",
              "raw": "{\n  \"name\": \"Test User\",\n  \"email\": \"test@example.com\",\n  \"password\": \"password123\",\n  \"role\": \"student\"\n}",
              "options": {
                "raw": {
                  "language": "json"
                }
              }
            },
            "url": {
              "raw": "{{baseUrl}}/api/auth/signup",
              "host": ["{{baseUrl}}"],
              "path": ["api", "auth", "signup"]
            }
          }
        }
      ]
    }
  ]
}
```

---

## 🛠️ Troubleshooting

### Common Issues & Solutions

#### 1. MongoDB Connection Error
```bash
# Error: MongoServerError: Authentication failed
# Solutions:
✅ Check MongoDB connection string in .env
✅ Ensure MongoDB service is running
✅ For Atlas: verify network access and credentials

# Test connection:
node -e "
const mongoose = require('mongoose');
mongoose.connect(process.env.MONGODB_URI)
  .then(() => console.log('✅ Database connected'))
  .catch(err => console.log('❌ Connection failed:', err.message));
"
```

#### 2. JWT Authentication Issues
```bash
# Error: JsonWebTokenError: invalid token
# Solutions:
✅ Check JWT_SECRET in backend .env
✅ Verify token format in requests
✅ Check token expiration

# Debug JWT token:
node -e "
const jwt = require('jsonwebtoken');
const token = 'YOUR_TOKEN_HERE';
try {
  const decoded = jwt.verify(token, process.env.JWT_SECRET);
  console.log('✅ Token valid:', decoded);
} catch(err) {
  console.log('❌ Token invalid:', err.message);
}
"
```

#### 3. CORS Issues
```javascript
// Error: CORS policy blocking requests
// Backend solution (app.js):
app.use(cors({
  origin: [
    'http://localhost:3000',
    'http://localhost:3001',
    process.env.FRONTEND_URL
  ],
  credentials: true,
  methods: ['GET', 'POST', 'PUT', 'PATCH', 'DELETE'],
  allowedHeaders: ['Content-Type', 'Authorization']
}));
```

#### 4. File Upload Issues
```bash
# Error: File too large or upload failed
# Solutions:
✅ Check MAX_FILE_SIZE in .env
✅ Ensure uploads directory exists
✅ Verify file permissions

# Create uploads directory:
mkdir -p backend/uploads/resumes
chmod 755 backend/uploads
```

#### 5. Email Service Issues
```javascript
// SendGrid configuration (utils/sendEmail.js):
const sgMail = require('@sendgrid/mail');
sgMail.setApiKey(process.env.SENDGRID_API_KEY);

const sendEmail = async (to, subject, html) => {
  try {
    await sgMail.send({
      to,
      from: process.env.FROM_EMAIL,
      subject,
      html
    });
    console.log('✅ Email sent successfully');
  } catch (error) {
    console.error('❌ Email failed:', error.message);
    throw error;
  }
};
```

### Performance Optimization

#### Database Indexing
```javascript
// Add indexes for better query performance
// In your models:

// User.js
userSchema.index({ email: 1 });
userSchema.index({ role: 1 });

// Internship.js
internshipSchema.index({ companyId: 1 });
internshipSchema.index({ status: 1 });
internshipSchema.index({ skills: 1 });
internshipSchema.index({ location: 1 });

// Application.js
applicationSchema.index({ studentId: 1 });
applicationSchema.index({ internshipId: 1 });
applicationSchema.index({ status: 1 });
```

#### API Response Caching
```javascript
// Install redis for caching
npm install redis

// Cache middleware (middleware/cache.js):
const redis = require('redis');
const client = redis.createClient();

const cache = (duration = 300) => {
  return async (req, res, next) => {
    const key = req.originalUrl;
    try {
      const cached = await client.get(key);
      if (cached) {
        return res.json(JSON.parse(cached));
      }
      
      const originalSend = res.json;
      res.json = function(data) {
        client.setex(key, duration, JSON.stringify(data));
        return originalSend.call(this, data);
      };
      
      next();
    } catch (error) {
      next();
    }
  };
};
```

---

## 🚀 Deployment

### Production Environment Variables
```env
# Production Backend .env
NODE_ENV=production
PORT=8080
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/weintern-prod
JWT_SECRET=super-secure-production-jwt-secret-key
SENDGRID_API_KEY=production-sendgrid-key
FRONTEND_URL=https://your-domain.com
```

### Docker Deployment
```dockerfile
# Dockerfile for backend
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
EXPOSE 5000
CMD ["npm", "start"]
```

```yaml
# docker-compose.yml
version: '3.8'
services:
  backend:
    build: ./backend
    ports:
      - "5000:5000"
    environment:
      - NODE_ENV=production
      - MONGODB_URI=mongodb://mongo:27017/weintern
    depends_on:
      - mongo
    
  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    depends_on:
      - backend
      
  mongo:
    image: mongo:5.0
    ports:
      - "27017:27017"
    volumes:
      - mongo_data:/data/db

volumes:
  mongo_data:
```

---

## 📈 Future Enhancements

### Phase 1: AI Integration
- 🤖 Machine learning-based internship recommendations
- 📊 Sentiment analysis of applications
- 🔍 Smart resume parsing and matching

### Phase 2: Communication Features
- 💬 Real-time chat system with Socket.io
- 📹 Video interview integration
- 📧 Advanced email templating

### Phase 3: Advanced Features
- 🎮 Gamification with points and badges
- 📅 Integrated calendar for interviews
- 🔗 LinkedIn and GitHub integration
- 📱 Mobile app development

---

## 📝 License

```
MIT License

Copyright (c) 2024 WeIntern

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. **Fork the repository**
2. **Create a feature branch:** `git checkout -b feature/amazing-feature`
3. **Commit your changes:** `git commit -m 'Add amazing feature'`
4. **Push to the branch:** `git push origin feature/amazing-feature`
5. **Open a Pull Request**

### Code Style Guidelines
- Use consistent indentation (2 spaces)
- Follow ESLint configuration
- Write meaningful commit messages
- Add comments for complex logic
- Update documentation for new features

---

## 📞 Support

### Getting Help
- 📖 **Documentation**: Check this README first
- 🐛 **Bug Reports**: Create an issue on GitHub
- 💡 **Feature Requests**: Open a discussion
- 📧 **Email Support**: support@weintern.com

### Development Support
- 🔍 **Debug Mode**: Set `NODE_ENV=development` for detailed logs
- 📊 **Monitoring**: Check browser console and server logs
- 🧪 **Testing**: Use Postman collection for API testing

---

**WeIntern** - *Connecting talent with opportunity, one internship at a time.* 🚀

[![Made with ❤️ by WeIntern Team](https://img.shields.io/badge/Made%20with%20❤️%20by-WeIntern%20Team-red?style=for-the-badge)](https://github.com/your-username/weintern)

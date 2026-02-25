# 📚 DARSHAN EASE - Complete Setup & Development Guide

> Complete step-by-step guide for project setup, development, execution, and deployment

**Last Updated**: February 25, 2026  
**Version**: 1.0.0  
**Repository**: https://github.com/sachinsoni27/DarshanEase

---

## 📋 Table of Contents

1. [Project Setup and Configuration](#project-setup-and-configuration)
2. [Creating Project Folder](#creating-project-folder)
3. [Client Setup](#client-setup)
4. [Server Setup & Backend Development](#server-setup--backend-development)
5. [Backend Structure](#backend-structure)
6. [Database Development](#database-development)
7. [Frontend Structure](#frontend-structure)
8. [Frontend Development](#frontend-development)
9. [Project Execution](#project-execution)
10. [Output Screenshots](#output-screenshots)
11. [Resources & Drive Links](#resources--drive-links)

---

## 🏗️ Project Setup and Configuration

### Prerequisites

Before starting, ensure you have the following installed on your system:

#### Required Software
- **Node.js** (v14 or higher) - [Download](https://nodejs.org/)
- **npm** (comes with Node.js) or **yarn**
- **MongoDB** (v4.4 or higher) - [Download](https://www.mongodb.com/try/download/community)
- **Git** - [Download](https://git-scm.com/)
- **Visual Studio Code** - [Download](https://code.visualstudio.com/)

#### Optional but Recommended
- **MongoDB Compass** - GUI for MongoDB
- **Postman** - API testing tool
- **Thunder Client** - VS Code extension for API testing

### System Requirements

```
OS: Windows 10/11, macOS 10.14+, or Ubuntu 18.04+
RAM: Minimum 4GB (8GB recommended)
Storage: 2GB free space
Internet: Required for npm packages and Firebase
```

### Verify Installations

```bash
# Check Node.js version
node --version
# Expected: v14.0.0 or higher

# Check npm version
npm --version
# Expected: v6.0.0 or higher

# Check Git version
git --version
# Expected: git version 2.x or higher

# Check MongoDB version (if installed locally)
mongod --version
# Expected: MongoDB version 4.4 or higher
```

---

## 📁 Creating Project Folder

### Step 1: Clone Repository

```bash
# Navigate to your desired location
cd Documents

# Clone the repository
git clone https://github.com/sachinsoni27/DarshanEase.git

# Navigate into the project
cd DarshanEase

# List contents
ls -la
```

### Step 2: Project Structure

```
DarshanEase/
├── backend/                 # Node.js + Express server
│   ├── models/             # MongoDB schemas
│   ├── routes/             # API endpoints
│   ├── seed/               # Database seeding
│   ├── .env                # Environment variables
│   ├── server.js           # Main server file
│   ├── package.json        # Dependencies
│   └── config.js           # Configuration
│
├── frontend/               # React + Vite application
│   ├── src/
│   │   ├── pages/          # React pages
│   │   ├── components/     # React components
│   │   ├── context/        # State management
│   │   ├── services/       # API services
│   │   ├── firebase/       # Firebase config
│   │   ├── App.tsx         # Main app
│   │   └── main.tsx        # Entry point
│   ├── .env.local          # Environment variables
│   ├── package.json        # Dependencies
│   ├── vite.config.ts      # Vite configuration
│   └── tsconfig.json       # TypeScript config
│
├── package.json            # Root package.json
├── README.md               # Project overview
├── ARCHITECTURE.md         # Architecture documentation
└── .gitignore             # Git ignore rules
```

### Step 3: Create Environment Files

```bash
# Create backend .env file
cat > backend/.env << EOF
PORT=5000
MONGO_URI=mongodb://localhost:27017/darshanease
NODE_ENV=development
JWT_SECRET=your-secret-key-here
EOF

# Create frontend .env.local file
cat > frontend/.env.local << EOF
VITE_API_BASE_URL=http://localhost:5000/api
VITE_FIREBASE_API_KEY=your-firebase-key
VITE_FIREBASE_AUTH_DOMAIN=your-firebase-auth-domain
VITE_FIREBASE_PROJECT_ID=your-firebase-project-id
VITE_FIREBASE_STORAGE_BUCKET=your-firebase-storage
VITE_FIREBASE_MESSAGING_SENDER_ID=your-messaging-id
VITE_FIREBASE_APP_ID=your-app-id
EOF
```

---

## 🖥️ Client Setup

### Step 1: Navigate to Frontend Directory

```bash
# From project root
cd frontend

# Or if in different directory
cd path/to/DarshanEase/frontend
```

### Step 2: Install Dependencies

```bash
# Using npm
npm install

# Or using yarn
yarn install

# Expected output: Added XXX packages
```

### Step 3: Configure Environment Variables

Create `.env.local` file with Firebase credentials:

```env
# Firebase Configuration (Get from Firebase Console)
VITE_FIREBASE_API_KEY=your-api-key
VITE_FIREBASE_AUTH_DOMAIN=your-project.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your-project-id
VITE_FIREBASE_STORAGE_BUCKET=your-bucket.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=your-sender-id
VITE_FIREBASE_APP_ID=your-app-id

# API Configuration
VITE_API_BASE_URL=http://localhost:5000/api

# Google Maps API Key
VITE_GOOGLE_MAPS_API_KEY=your-google-maps-key
```

### Step 4: Verify Installation

```bash
# Check if all dependencies are installed
npm list

# Check for any vulnerabilities
npm audit

# Build check (verifies configuration)
npm run build --dry-run
```

### Step 5: Key Dependencies

```json
{
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-router-dom": "^6.x.x",
    "firebase": "^9.x.x",
    "axios": "^1.x.x",
    "tailwindcss": "^3.x.x",
    "framer-motion": "^10.x.x"
  },
  "devDependencies": {
    "vite": "^4.x.x",
    "typescript": "^5.x.x",
    "@vitejs/plugin-react": "^4.x.x"
  }
}
```

---

## ⚙️ Server Setup & Backend Development

### Step 1: Navigate to Backend Directory

```bash
# From project root
cd backend

# Verify you're in correct directory
pwd
# Expected: /path/to/DarshanEase/backend
```

### Step 2: Install Backend Dependencies

```bash
# Install npm packages
npm install

# Expected dependencies:
# - express
# - mongoose
# - cors
# - dotenv
# - nodemon (for development)
```

### Step 3: Configure Environment Variables

Create `.env` file:

```env
# Server Configuration
PORT=5000
NODE_ENV=development

# MongoDB Configuration
MONGO_URI=mongodb://localhost:27017/darshanease
# Alternative for MongoDB Atlas:
# MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/darshanease

# Authentication
JWT_SECRET=your-super-secret-jwt-key

# CORS Configuration
CORS_ORIGIN=http://localhost:3000

# Firebase Configuration (optional for backend)
FIREBASE_API_KEY=your-firebase-key
FIREBASE_PROJECT_ID=your-project-id
```

### Step 4: Start MongoDB

#### Option 1: Local MongoDB

```bash
# Windows
mongod --dbpath "C:\data\db"

# macOS/Linux
mongod --dbpath /usr/local/var/mongodb

# Check if MongoDB is running
mongo --version
# or
mongosh --version
```

#### Option 2: MongoDB Atlas (Cloud)

```bash
# Update MONGO_URI in .env:
MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/darshanease?retryWrites=true&w=majority
```

### Step 5: Start Backend Server

```bash
# Development mode with auto-reload
npm run dev

# Or start production server
npm start

# Expected output:
# Server running on port 5000
# Connected to MongoDB
```

### Step 6: Test Backend

```bash
# Test API endpoint (in new terminal)
curl http://localhost:5000/api/temples

# Expected response:
# {"success": true, "data": [...]}
```

---

## 🔧 Backend Structure

### Directory Layout

```
backend/
├── models/
│   ├── Temple.js           # Temple schema & model
│   ├── FoodPlace.js        # Food place schema
│   ├── Hotel.js            # Hotel schema
│   └── User.js             # User schema (optional)
│
├── routes/
│   ├── templeRoutes.js     # GET, POST /api/temples
│   ├── foodRoutes.js       # GET, POST /api/food
│   ├── hotelRoutes.js      # GET, POST /api/hotels
│   ├── seedRoutes.js       # POST /api/seed
│   └── authRoutes.js       # POST /api/auth (optional)
│
├── middleware/
│   ├── errorHandler.js     # Error handling
│   ├── cors.js             # CORS configuration
│   └── auth.js             # Authentication
│
├── seed/
│   └── seedData.js         # Sample data for seeding
│
├── config/
│   └── database.js         # Database connection
│
├── .env                    # Environment variables
├── server.js               # Main server file
├── package.json            # Dependencies
└── README.md               # Backend documentation
```

### Key Files Explained

#### server.js (Main Server)

```javascript
// server.js
const express = require('express');
const cors = require('cors');
const mongoose = require('mongoose');
require('dotenv').config();

const app = express();

// Middleware
app.use(cors());
app.use(express.json());

// Database Connection
mongoose.connect(process.env.MONGO_URI, {
  useNewUrlParser: true,
  useUnifiedTopology: true,
})
.then(() => console.log('MongoDB connected'))
.catch(err => console.log('MongoDB error:', err));

// Routes
app.use('/api/temples', require('./routes/templeRoutes'));
app.use('/api/food', require('./routes/foodRoutes'));
app.use('/api/hotels', require('./routes/hotelRoutes'));
app.use('/api/seed', require('./routes/seedRoutes'));

// Error handling middleware
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: 'Something went wrong!' });
});

// Start server
const PORT = process.env.PORT || 5000;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

#### Models Example: Temple.js

```javascript
// models/Temple.js
const mongoose = require('mongoose');

const templeSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true,
    unique: true
  },
  location: {
    type: String,
    required: true
  },
  description: String,
  deity: String,
  coordinates: {
    latitude: Number,
    longitude: Number
  },
  timings: {
    opening: String,
    closing: String
  },
  festivals: [String],
  imageUrl: String,
  createdAt: {
    type: Date,
    default: Date.now
  }
});

module.exports = mongoose.model('Temple', templeSchema);
```

#### Routes Example: templeRoutes.js

```javascript
// routes/templeRoutes.js
const express = require('express');
const Temple = require('../models/Temple');
const router = express.Router();

// GET all temples
router.get('/', async (req, res) => {
  try {
    const temples = await Temple.find();
    res.json({ success: true, data: temples });
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

// GET single temple
router.get('/:id', async (req, res) => {
  try {
    const temple = await Temple.findById(req.params.id);
    if (!temple) return res.status(404).json({ error: 'Temple not found' });
    res.json({ success: true, data: temple });
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

// POST new temple
router.post('/', async (req, res) => {
  try {
    const temple = new Temple(req.body);
    await temple.save();
    res.status(201).json({ success: true, data: temple });
  } catch (error) {
    res.status(400).json({ error: error.message });
  }
});

module.exports = router;
```

---

## 🗄️ Database Development

### MongoDB Setup

#### Step 1: Install MongoDB Community Edition

**Windows:**
```bash
# Download installer from mongodb.com
# Run installer and follow setup wizard
# Default installation path: C:\Program Files\MongoDB\Server\6.0

# Verify installation
mongod --version
```

**macOS (with Homebrew):**
```bash
# Install MongoDB
brew tap mongodb/brew
brew install mongodb-community

# Start MongoDB service
brew services start mongodb-community
```

**Linux (Ubuntu):**
```bash
# Add MongoDB repository
curl https://www.mongodb.org/static/pgp/server-6.0.asc | apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-6.0.list

# Install MongoDB
sudo apt-get update
sudo apt-get install -y mongodb-org

# Start MongoDB
sudo systemctl start mongod
```

#### Step 2: MongoDB Atlas (Cloud Alternative)

```bash
# 1. Go to https://www.mongodb.com/cloud/atlas
# 2. Sign up for free account
# 3. Create new cluster
# 4. Configure connection settings
# 5. Get connection string:
#    mongodb+srv://username:password@cluster.mongodb.net/dbname

# Add to .env:
MONGO_URI=mongodb+srv://username:password@cluster0.xxxxx.mongodb.net/darshanease
```

### Create Database Connection

#### config/database.js

```javascript
// config/database.js
const mongoose = require('mongoose');

const connectDB = async () => {
  try {
    const conn = await mongoose.connect(process.env.MONGO_URI, {
      useNewUrlParser: true,
      useUnifiedTopology: true,
    });
    
    console.log('✅ MongoDB Connected:', conn.connection.host);
    console.log('📦 Database:', conn.connection.name);
    return conn;
  } catch (error) {
    console.error('❌ MongoDB Connection Error:', error.message);
    process.exit(1);
  }
};

module.exports = connectDB;
```

### Create Schema and Models

#### models/Temple.js

```javascript
const mongoose = require('mongoose');

const templeSchema = new mongoose.Schema(
  {
    name: {
      type: String,
      required: [true, 'Temple name is required'],
      unique: true,
      trim: true,
      maxlength: [100, 'Name cannot exceed 100 characters']
    },
    location: {
      type: String,
      required: [true, 'Location is required'],
      trim: true
    },
    description: {
      type: String,
      trim: true
    },
    deity: {
      type: String,
      trim: true
    },
    coordinates: {
      latitude: {
        type: Number,
        min: [-90, 'Invalid latitude'],
        max: [90, 'Invalid latitude']
      },
      longitude: {
        type: Number,
        min: [-180, 'Invalid longitude'],
        max: [180, 'Invalid longitude']
      }
    },
    timings: {
      opening: String,
      closing: String
    },
    festivals: [String],
    imageUrl: {
      type: String,
      match: [/^https?:\/\/.+/, 'Please provide valid image URL']
    },
    rating: {
      type: Number,
      min: [0, 'Rating cannot be less than 0'],
      max: [5, 'Rating cannot be more than 5'],
      default: 0
    },
    reviews: {
      type: Number,
      default: 0
    }
  },
  { timestamps: true }
);

// Indexes for performance
templeSchema.index({ location: 1 });
templeSchema.index({ name: 'text', description: 'text' });

module.exports = mongoose.model('Temple', templeSchema);
```

#### models/FoodPlace.js

```javascript
const mongoose = require('mongoose');

const foodPlaceSchema = new mongoose.Schema(
  {
    name: {
      type: String,
      required: [true, 'Food place name is required'],
      trim: true
    },
    type: {
      type: String,
      enum: ['Restaurant', 'Cafe', 'Sweet Shop', 'Dhaba', 'Other'],
      required: true
    },
    cuisine: [String],
    location: {
      type: String,
      required: true
    },
    coordinates: {
      latitude: Number,
      longitude: Number
    },
    priceRange: {
      type: String,
      enum: ['Budget', 'Moderate', 'Premium'],
      default: 'Moderate'
    },
    contact: String,
    specialities: [String],
    imageUrl: String,
    rating: {
      type: Number,
      min: 0,
      max: 5,
      default: 0
    }
  },
  { timestamps: true }
);

module.exports = mongoose.model('FoodPlace', foodPlaceSchema);
```

#### models/Hotel.js

```javascript
const mongoose = require('mongoose');

const hotelSchema = new mongoose.Schema(
  {
    name: {
      type: String,
      required: [true, 'Hotel name is required'],
      trim: true
    },
    category: {
      type: String,
      enum: ['Budget', 'Standard', 'Premium', 'Luxury'],
      required: true
    },
    address: {
      type: String,
      required: true
    },
    coordinates: {
      latitude: Number,
      longitude: Number
    },
    contact: String,
    amenities: [String],
    pricePerNight: {
      type: Number,
      required: true
    },
    imageUrl: String,
    rating: {
      type: Number,
      min: 0,
      max: 5,
      default: 0
    },
    availableRooms: {
      type: Number,
      default: 0
    }
  },
  { timestamps: true }
);

module.exports = mongoose.model('Hotel', hotelSchema);
```

### Database Seeding

```javascript
// seed/seedData.js
const mongoose = require('mongoose');
require('dotenv').config();

const Temple = require('../models/Temple');
const FoodPlace = require('../models/FoodPlace');
const Hotel = require('../models/Hotel');

const seedData = async () => {
  try {
    // Connect to MongoDB
    await mongoose.connect(process.env.MONGO_URI, {
      useNewUrlParser: true,
      useUnifiedTopology: true,
    });

    // Clear existing data
    await Temple.deleteMany({});
    await FoodPlace.deleteMany({});
    await Hotel.deleteMany({});

    // Seed temples
    const temples = await Temple.insertMany([
      {
        name: 'Varanasi Kashi Vishwanath Temple',
        location: 'Varanasi, Uttar Pradesh',
        deity: 'Lord Shiva',
        description: 'One of the holiest temples dedicated to Lord Shiva',
        timings: { opening: '04:00 AM', closing: '11:00 PM' },
        coordinates: { latitude: 25.3209, longitude: 82.9958 },
        festivals: ['Maha Shivaratri', 'Baisakhi'],
        imageUrl: 'https://example.com/temple1.jpg'
      },
      // Add more temples...
    ]);

    // Seed food places
    const foodPlaces = await FoodPlace.insertMany([
      {
        name: 'Local Dhaba',
        type: 'Dhaba',
        cuisine: ['Indian', 'North Indian'],
        location: 'Varanasi',
        coordinates: { latitude: 25.32, longitude: 82.99 },
        priceRange: 'Budget',
        specialities: ['Daal Puri', 'Chole Bhature']
      },
      // Add more food places...
    ]);

    // Seed hotels
    const hotels = await Hotel.insertMany([
      {
        name: 'Riverside Hotel',
        category: 'Standard',
        address: 'Near Dashashwamedh Ghat, Varanasi',
        coordinates: { latitude: 25.32, longitude: 82.99 },
        amenities: ['WiFi', 'AC', 'Restaurant', 'Parking'],
        pricePerNight: 2500
      },
      // Add more hotels...
    ]);

    console.log('✅ Database seeded successfully!');
    console.log(`📍 ${temples.length} temples added`);
    console.log(`🍕 ${foodPlaces.length} food places added`);
    console.log(`🏨 ${hotels.length} hotels added`);

    process.exit(0);
  } catch (error) {
    console.error('❌ Seeding error:', error);
    process.exit(1);
  }
};

seedData();
```

Run seeding:
```bash
cd backend
node seed/seedData.js
```

---

## 🎨 Frontend Structure

### Directory Organization

```
frontend/src/
├── pages/
│   ├── Home.tsx                # Landing page
│   ├── Temples.tsx             # Temple listings
│   ├── TempleDetails.tsx       # Temple details
│   ├── Food.tsx                # Food destinations
│   ├── Hotels.tsx              # Hotel listings
│   ├── PlanTrip.tsx            # Trip planner
│   ├── Map.tsx                 # Interactive map
│   ├── Login.tsx               # User login
│   ├── Signup.tsx              # User registration
│   └── AllFeedbacks.tsx        # Community feedback
│
├── components/
│   ├── Navbar.tsx              # Navigation bar
│   ├── Footer.tsx              # Footer component
│   ├── TempleCard.tsx          # Temple card
│   ├── FoodCard.tsx            # Food card
│   ├── HotelCard.tsx           # Hotel card
│   ├── AddTripModal.tsx        # Trip modal
│   ├── FeedbackForm.tsx        # Feedback form
│   ├── ErrorBoundary.tsx       # Error handling
│   └── LoadingSkeletons.tsx    # Loading states
│
├── context/
│   ├── AuthContext.tsx         # Auth state
│   └── PlannerContext.tsx      # Trip planning state
│
├── services/
│   └── apiService.ts           # API calls
│
├── firebase/
│   └── config.ts               # Firebase config
│
├── data/
│   └── templesData.ts          # Static temple data
│
├── App.tsx                     # Main app component
├── App.css                     # Global styles
├── main.tsx                    # Entry point
└── index.css                   # Global CSS
```

### Frontend Key Components

#### Context: AuthContext.tsx

```typescript
// src/context/AuthContext.tsx
import React, { createContext, useContext, useState, useEffect } from 'react';
import { auth } from '../firebase/config';
import { onAuthStateChanged, User } from 'firebase/auth';

interface AuthContextType {
  user: User | null;
  loading: boolean;
  isAuthenticated: boolean;
}

const AuthContext = createContext<AuthContextType | undefined>(undefined);

export const AuthProvider: React.FC<{ children: React.ReactNode }> = ({ children }) => {
  const [user, setUser] = useState<User | null>(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    const unsubscribe = onAuthStateChanged(auth, (currentUser) => {
      setUser(currentUser);
      setLoading(false);
    });

    return unsubscribe;
  }, []);

  const value = {
    user,
    loading,
    isAuthenticated: !!user
  };

  return (
    <AuthContext.Provider value={value}>
      {children}
    </AuthContext.Provider>
  );
};

export const useAuth = () => {
  const context = useContext(AuthContext);
  if (!context) {
    throw new Error('useAuth must be used within AuthProvider');
  }
  return context;
};
```

#### Service: apiService.ts

```typescript
// src/services/apiService.ts
import axios from 'axios';

const API_BASE_URL = import.meta.env.VITE_API_BASE_URL || 'http://localhost:5000/api';

const apiClient = axios.create({
  baseURL: API_BASE_URL,
  headers: {
    'Content-Type': 'application/json',
  },
});

// Temples
export const templeAPI = {
  getAll: () => apiClient.get('/temples'),
  getById: (id: string) => apiClient.get(`/temples/${id}`),
  create: (data: any) => apiClient.post('/temples', data),
};

// Food Places
export const foodAPI = {
  getAll: () => apiClient.get('/food'),
  getByLocation: (location: string) => apiClient.get(`/food/location/${location}`),
  create: (data: any) => apiClient.post('/food', data),
};

// Hotels
export const hotelAPI = {
  getAll: () => apiClient.get('/hotels'),
  getByLocation: (location: string) => apiClient.get(`/hotels/location/${location}`),
  create: (data: any) => apiClient.post('/hotels', data),
};

// Seed
export const seedAPI = {
  status: () => apiClient.get('/seed/status'),
  seedTemples: () => apiClient.post('/seed/temples'),
  seedFood: () => apiClient.post('/seed/food'),
  seedHotels: () => apiClient.post('/seed/hotels'),
};

export default apiClient;
```

---

## 💻 Frontend Development

### Step 1: Start Development Server

```bash
# Navigate to frontend directory
cd frontend

# Start dev server
npm run dev

# Expected output:
# VITE v4.x.x  ready in xxx ms
# ➜  Local:   http://localhost:5173/
```

### Step 2: Hot Module Reloading

Changes to files automatically refresh the browser - no manual restart needed.

### Step 3: Build for Production

```bash
# Build optimized production bundle
npm run build

# Output files in dist/ folder for deployment
```

### Step 4: Development Workflow

```bash
# Terminal 1: Start backend
cd backend
npm run dev

# Terminal 2: Start frontend
cd frontend
npm run dev

# Open browser to http://localhost:5173/
```

---

## 🚀 Project Execution

### Complete Execution Steps

#### Step 1: Start MongoDB

```bash
# Terminal 1
mongod

# Or if using MongoDB Atlas, skip this step
```

#### Step 2: Start Backend Server

```bash
# Terminal 2
cd backend
npm install
npm run dev

# Expected output:
# ✅ Server running on port 5000
# ✅ MongoDB connected
```

#### Step 3: Seed Database (First Time Only)

```bash
# Terminal 3
cd backend
node seed/seedData.js

# Expected output:
# ✅ Database seeded successfully!
# 📍 XX temples added
# 🍕 XX food places added
# 🏨 XX hotels added
```

#### Step 4: Start Frontend

```bash
# Terminal 4
cd frontend
npm install
npm run dev

# Open http://localhost:5173/
```

#### Step 5: Test Application

```
1. Landing Page: http://localhost:5173/
2. Browse Temples: http://localhost:5173/temples
3. Login/Signup: http://localhost:5173/login
4. Plan Trip: http://localhost:5173/plan-trip
5. View Map: http://localhost:5173/map
```

### Troubleshooting Common Issues

```
ERROR: "Port 5000 already in use"
→ Kill process: lsof -ti:5000 | xargs kill -9

ERROR: "Cannot find module"
→ Delete node_modules and package-lock.json, then npm install

ERROR: "MongoDB connection refused"
→ Start MongoDB: mongod
→ Or check MongoDB Atlas connection string

ERROR: "Firebase not initialized"
→ Check .env.local has all Firebase keys
→ Verify firebase/config.ts is correct

ERROR: "API 404 Not Found"
→ Verify backend is running on port 5000
→ Check API_BASE_URL in .env.local
→ Test: curl http://localhost:5000/api/temples
```

---

## 📸 Output Screenshots

### 1. Landing Page
```
┌─────────────────────────────────────────────────┐
│  DARSHAN EASE - Divine Journey Begins          │ 
├─────────────────────────────────────────────────┤
│                                                  │
│         🙏 Welcome to Spiritual Tourism 🙏      │
│                                                  │
│  ┌─────────────────────────────────────────┐   │
│  │  [ Explore Temples ]  [ Plan Your Trip ]│   │
│  └─────────────────────────────────────────┘   │
│                                                  │
│  Featured Temples:                              │
│  ┌──────────────┐ ┌──────────────┐             │
│  │ Varanasi     │ │ Taj Mahal    │ ...         │
│  │ ★★★★★       │ │ ★★★★★       │             │
│  └──────────────┘ └──────────────┘             │
│                                                  │
└─────────────────────────────────────────────────┘
```

### 2. Temple Listing Page
```
┌─────────────────────────────────────────────────┐
│  🏛️ Explore Sacred Temples                      │
├─────────────────────────────────────────────────┤
│                                                  │
│  Filter: [Location ▼] [Deity ▼] [Rating ▼]    │
│  Search: [_____________________]                │
│                                                  │
│  ┌──────────────┐ ┌──────────────┐             │
│  │ Temple Name  │ │ Temple Name  │             │
│  │ Location     │ │ Location     │             │
│  │ ★★★★★ (234) │ │ ★★★★☆ (120) │             │
│  │ [+ Add Trip] │ │ [+ Add Trip] │             │
│  └──────────────┘ └──────────────┘             │
│                                                  │
│  [Previous] ⚫⚪⚪ [Next]                         │
│                                                  │
└─────────────────────────────────────────────────┘
```

### 3. Trip Planning Page
```
┌─────────────────────────────────────────────────┐
│  📍 Plan Your Sacred Journey                    │
├─────────────────────────────────────────────────┤
│                                                  │
│  Trip Name: [My Spiritual Journey]              │
│  Duration: [Start Date] - [End Date]            │
│  Budget: Amount [$]                             │
│                                                  │
│  Selected Temples:                              │
│  1. Varanasi Kashi Vishwanath                   │
│  2. Bodh Gaya Mahabodhi Temple                  │
│  3. Jaipur City Palace                          │
│                                                  │
│  Distance Calculation:                          │
│  • Varanasi → Bodh Gaya: 150 km                │
│  • Bodh Gaya → Jaipur: 450 km                  │
│  Total: 600 km                                  │
│                                                  │
│  Suggestions:                                   │
│  🍕 Nearby Food: [Show 5]                      │
│  🏨 Hotels: [Show 5]                           │
│                                                  │
│  [Save Trip] [Export] [Share]                   │
│                                                  │
└─────────────────────────────────────────────────┘
```

### 4. Console Output - Backend

```
$ npm run dev

> backend@1.0.0 dev
> nodemon server.js

[nodemon] 3.0.1
[nodemon] to restart at any time, type `rs`
[nodemon] watching path(s): *.*
[nodemon] watching extensions: js,json
[nodemon] starting `node server.js`

✅ Server running on port 5000
📦 Database: darshanease
✅ MongoDB connected to mongodb://localhost:27017/darshanease

GET /api/temples 200 - 15.234 ms
GET /api/temples/507f1f77bcf86cd799439011 200 - 8.123 ms
POST /api/temples 201 - 42.567 ms
```

### 5. Console Output - Frontend

```
$ npm run dev

VITE v4.4.9 ready in 845 ms

➜  Local:   http://localhost:5173/
➜  press h to show help

✅ React configured
✅ TypeScript initialized
✅ Tailwind CSS loaded
✅ Firebase initialized
✅ API service connected to http://localhost:5000/api

GET /api/temples 304 (Not Modified) 120ms
GET /api/food 200 130ms
GET /api/hotels 200 145ms
```

---

## 🔗 Resources & Drive Links

### Important Links

#### Project Repository
- **GitHub Repository**: https://github.com/sachinsoni27/DarshanEase
- **Live Demo**: https://darshan-ease-9xqrek4ey-sachin-sonis-projects.vercel.app/

#### Documentation
- **Architecture Documentation**: [./ARCHITECTURE.md](./ARCHITECTURE.md)
- **API Documentation**: [./API_DOCUMENTATION.md](./API_DOCUMENTATION.md)
- **Deployment Guide**: [./DEPLOYMENT.md](./DEPLOYMENT.md)
- **Getting Started**: [./GETTING_STARTED.md](./GETTING_STARTED.md)

#### Official Documentation
- **React**: https://react.dev
- **TypeScript**: https://www.typescriptlang.org
- **Vite**: https://vitejs.dev
- **Express.js**: https://expressjs.com
- **MongoDB**: https://docs.mongodb.com
- **Firebase**: https://firebase.google.com/docs
- **Tailwind CSS**: https://tailwindcss.com/docs

### Development Tools

#### Required Tools
- **Node.js**: https://nodejs.org/
- **Git**: https://git-scm.com/
- **VS Code**: https://code.visualstudio.com/
- **MongoDB**: https://www.mongodb.com/try/download/community
- **MongoDB Compass**: https://www.mongodb.com/products/compass

#### Recommended Extensions (VS Code)
```
- ES7+ React/Redux/React-Native snippets
- Prettier - Code formatter
- Thunder Client (API testing)
- MongoDB for VS Code
- Tailwind CSS IntelliSense
- TypeScript Vue Plugin
```

### Installation Guide Links

#### Windows
- Node.js: https://nodejs.org/dist/v18.x/
- MongoDB: https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/
- Git: https://git-scm.com/download/win

#### macOS
- Node.js: via Homebrew `brew install node`
- MongoDB: via Homebrew `brew install mongodb-community`
- Git: via Homebrew `brew install git`

#### Linux (Ubuntu)
- Node.js: https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions
- MongoDB: https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/
- Git: `sudo apt-get install git`

### Database Resources

#### MongoDB
- **Documentation**: https://docs.mongodb.com/
- **MongoDB Atlas**: https://www.mongodb.com/cloud/atlas
- **Mongoose Docs**: https://mongoosejs.com/

#### Firebase
- **Console**: https://console.firebase.google.com/
- **Documentation**: https://firebase.google.com/docs
- **Authentication**: https://firebase.google.com/docs/auth

### API Testing Tools
- **Postman**: https://www.postman.com/downloads/
- **Thunder Client**: VS Code Extension
- **cURL**: Built-in command-line tool
- **REST Client**: VS Code Extension

### Deployment Platforms
- **Vercel**: https://vercel.com (Frontend)
- **Heroku**: https://www.heroku.com (Backend)
- **Railway**: https://railway.app (Backend)
- **MongoDB Atlas**: https://www.mongodb.com/cloud/atlas (Database)

### Learning Resources
- **React Documentation**: https://react.dev/learn
- **Node.js Best Practices**: https://nodejs.org/en/docs/guides/
- **MongoDB University**: https://university.mongodb.com/
- **Firebase Tutorials**: https://firebase.google.com/learn
- **Tailwind Tutorial**: https://tailwindcss.com/learn

### Support & Community
- **GitHub Issues**: Report bugs on https://github.com/sachinsoni27/DarshanEase/issues
- **Stack Overflow**: Tag questions with `[darshan-ease]`
- **Discord Community**: Join our Discord server (link in README)
- **Email Support**: sachinsoniofficial2003@gmail.com
- **Phone**: 9936503035

---

## 📞 Team Contact Information

### Development Team
- **Lead Developer**: Sachin Soni
  - Email: sachinsoniofficial2003@gmail.com
  - Phone: 9936503035
  - GitHub: https://github.com/sachinsoni27

- **Frontend Developer**: Sakshi Singh
- **Backend Developer**: Satish Kumar

### Report Issues
- Create GitHub Issue: https://github.com/sachinsoni27/DarshanEase/issues/new
- Email: sachinsoniofficial2003@gmail.com

---

## ✅ Verification Checklist

Before considering setup complete, verify:

```
Backend Setup:
□ Node.js installed (node --version)
□ MongoDB running (mongod status)
□ Backend dependencies installed (npm list)
□ .env file configured
□ Server running on port 5000
□ API endpoints responding (curl http://localhost:5000/api/temples)

Frontend Setup:
□ Node.js and npm working
□ Frontend dependencies installed
□ .env.local configured with Firebase keys
□ Dev server running (npm run dev)
□ Browser showing http://localhost:5173/
□ Firebase authentication working

Database:
□ MongoDB connected
□ Collections created (temples, food, hotels)
□ Sample data seeded
□ Can query from API

Integration:
□ Frontend can connect to backend
□ API calls working (network tab in DevTools)
□ Firebase auth operational
□ Pages loading correctly
□ No console errors
```

---

**Created**: February 25, 2026  
**Last Updated**: February 25, 2026  
**Version**: 1.0.0  
**Status**: ✅ Complete and Ready for Development

© 2026 DARSHAN EASE. All rights reserved.  
Developed by Sachin Soni, Sakshi Singh, and Satish Kumar

# 🚀 DARSHAN EASE - Getting Started Guide

> Step-by-step instructions to set up and run DARSHAN EASE locally

---

## ✅ Prerequisites

Before starting, ensure you have:

- **Node.js**: v14.0.0 or higher
  - Download from [nodejs.org](https://nodejs.org/)
  - Verify: `node --version` and `npm --version`

- **MongoDB**: Local or Cloud instance
  - Local: Download from [mongodb.com](https://www.mongodb.com/try/download/community)
  - Cloud: Use [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) (free tier available)

- **Git**: For version control
  - Download from [git-scm.com](https://git-scm.com/)

- **Text Editor/IDE**: VS Code recommended
  - Download from [code.visualstudio.com](https://code.visualstudio.com/)

- **Firebase Account**: For authentication
  - Sign up at [console.firebase.google.com](https://console.firebase.google.com/)

---

## 📋 Step 1: Clone the Repository

```bash
# Clone the DARSHAN EASE repository
git clone https://github.com/sachinsoni27/DarshanEase.git

# Navigate to the project directory
cd DarshanEase

# Verify the project structure
ls
```

---

## 📦 Step 2: Install Dependencies

### Install All at Once (Recommended)
```bash
npm run install-all
```

This command installs dependencies for:
- Root project
- Backend (`backend/`)
- Frontend (`frontend/`)

### Or Manually Install Each
```bash
# Root dependencies
npm install

# Backend dependencies
cd backend
npm install

# Frontend dependencies
cd ../frontend
npm install
```

---

## 🔧 Step 3: Configure Environment Variables

### Backend Configuration (`backend/.env`)

Create a `.env` file in the `backend/` directory:

```bash
# Database Configuration
MONGO_URI=mongodb://127.0.0.1:27017/darshanease
# Or for MongoDB Atlas:
# MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/darshanease

# Server Configuration
PORT=5000
NODE_ENV=development

# CORS Configuration
FRONTEND_URL=http://localhost:5173

# Optional: Firebase Admin SDK (for future authentication)
# FIREBASE_PROJECT_ID=your_project_id
# FIREBASE_PRIVATE_KEY=your_private_key
# FIREBASE_CLIENT_EMAIL=your_client_email
```

**Note**: Replace MongoDB URI with your actual connection string

### Frontend Configuration (`frontend/.env.local`)

Create a `.env.local` file in the `frontend/` directory:

```bash
# API Configuration
VITE_API_BASE_URL=http://localhost:5000/api

# Firebase Configuration
VITE_FIREBASE_API_KEY=your_firebase_api_key
VITE_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your_project_id
VITE_FIREBASE_STORAGE_BUCKET=your_project.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
VITE_FIREBASE_APP_ID=your_app_id
```

**Getting Firebase Credentials**:
1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Create a new project or select existing
3. Go to Project Settings
4. Copy web app configuration
5. Paste into `.env.local`

---

## 🗄️ Step 4: Setup MongoDB

### Option A: Local MongoDB

```bash
# Start MongoDB service (Windows)
net start MongoDB

# Start MongoDB service (macOS with Homebrew)
brew services start mongodb-community

# Start MongoDB service (Linux)
sudo systemctl start mongod

# Verify MongoDB is running
mongo --version
```

### Option B: MongoDB Atlas (Cloud)

1. Sign up at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a free cluster
3. Get connection string
4. Update `MONGO_URI` in `backend/.env`

---

## ▶️ Step 5: Start the Application

### Option A: Start Both Servers (Recommended)
```bash
npm start
```

This runs in concurrent mode using concurrently package.

### Option B: Start Servers Separately

**Terminal 1 - Backend:**
```bash
npm run backend
```

**Terminal 2 - Frontend:**
```bash
npm run frontend
```

### What to Look For
- Backend console: `Server running on http://localhost:5000`
- Frontend console: `VITE v... ready in ... ms`
- No CORS errors

---

## 🌐 Step 6: Access the Application

After servers start successfully, access:

| Service | URL | Purpose |
|---------|-----|---------|
| Frontend | http://localhost:5173 | Main website |
| Backend API | http://localhost:5000/api | API endpoints |
| Seed Page | http://localhost:5173/seed | Database initialization |
| Health Check | http://localhost:5000/api/status | API health |

---

## 📊 Step 7: Seed Database (Optional)

Data needs to be seeded for full functionality.

### Method 1: Via Frontend (Easiest)
1. Open http://localhost:5173/seed
2. Click "Seed Temples", "Seed Food", "Seed Hotels"
3. Wait for success messages
4. Check status

### Method 2: Via API (Using curl)
```bash
# Seed temples
curl -X POST http://localhost:5000/api/seed/temples

# Seed food places
curl -X POST http://localhost:5000/api/seed/food

# Seed hotels
curl -X POST http://localhost:5000/api/seed/hotels

# Check status
curl http://localhost:5000/api/seed/status
```

### Method 3: Via Postman
1. Open Postman
2. Create POST request to `http://localhost:5000/api/seed/temples`
3. Send request
4. Repeat for food and hotels

---

## 🧪 Step 8: Verify Setup

### Test Backend API
```bash
# Get all temples (should return array)
curl http://localhost:5000/api/temples

# Get single temple
curl http://localhost:5000/api/temples/[temple_id]

# Get all food places
curl http://localhost:5000/api/food

# Get all hotels
curl http://localhost:5000/api/hotels
```

### Test Frontend
1. Visit http://localhost:5173
2. Navigate through pages
3. Check browser console for errors (`F12`)
4. Verify API calls in Network tab

---

## 🔄 First Time Setup Checklist

- [ ] Node.js and npm installed
- [ ] MongoDB installed or Atlas configured
- [ ] Repository cloned
- [ ] Dependencies installed (`npm run install-all`)
- [ ] Backend `.env` configured
- [ ] Frontend `.env.local` configured
- [ ] MongoDB running
- [ ] Backend started (`npm run backend`)
- [ ] Frontend started (`npm run frontend`)
- [ ] Frontend accessible at http://localhost:5173
- [ ] Backend endpoints responding
- [ ] Database seeded with data
- [ ] No console errors

---

## 🛑 Troubleshooting

### Issue: "Cannot find module"
```bash
# Solution: Delete node_modules and reinstall
rm -rf node_modules backend/node_modules frontend/node_modules
npm run install-all
```

### Issue: MongoDB connection error
```bash
# Check MongoDB is running
mongo --version

# Update MONGO_URI in backend/.env
# Verify connection string is correct
```

### Issue: CORS errors
```bash
# Ensure FRONTEND_URL in backend/.env matches your frontend URL
# Check VITE_API_BASE_URL in frontend/.env.local is correct
```

### Issue: Port already in use
```bash
# Kill process on port 5000
# Windows: netstat -ano | findstr :5000 && taskkill /PID [PID] /F
# Mac/Linux: lsof -ti:5000 | xargs kill -9

# Or use different port in backend/.env
PORT=5001
```

### Issue: Firebase auth not working
```bash
# Verify Firebase credentials in frontend/.env.local
# Check Firebase project settings
# Enable Email/Password authentication in Firebase Console
```

For more issues, see [TROUBLESHOOTING.md](TROUBLESHOOTING.md)

---

## 📚 Next Steps

After successful setup:

1. **Explore the Application**
   - Visit http://localhost:5173
   - Click through different pages
   - Interact with features

2. **Read Documentation**
   - [FEATURES.md](FEATURES.md) - Feature overview
   - [API_DOCUMENTATION.md](API_DOCUMENTATION.md) - API reference
   - [ARCHITECTURE.md](ARCHITECTURE.md) - System design

3. **Make Changes**
   - Edit `/frontend/src` for UI changes
   - Edit `/backend` for API changes
   - Changes auto-reload in development

4. **Test Thoroughly**
   - Use [TROUBLESHOOTING.md](TROUBLESHOOTING.md) if issues
   - Check console for errors
   - Test all major features

5. **Contribute**
   - See [CONTRIBUTING.md](CONTRIBUTING.md)
   - Create feature branches
   - Submit pull requests

---

## 🚀 Development Commands

| Command | Purpose |
|---------|---------|
| `npm start` | Start both servers |
| `npm run backend` | Start backend only |
| `npm run frontend` | Start frontend only |
| `npm run build:frontend` | Build frontend for production |
| `npm run dev` | Same as `npm start` |
| `npm run install-all` | Install all dependencies |

---

## 🆘 Need Help?

1. **Check Documentation**: Browse [DOCUMENTATION.md](DOCUMENTATION.md)
2. **Check Troubleshooting**: See [TROUBLESHOOTING.md](TROUBLESHOOTING.md)
3. **Create GitHub Issue**: With detailed error messages
4. **Contact Team**: sachinsoniofficial2003@gmail.com

---

## ✅ Setup Complete!

You're all set to start developing with DARSHAN EASE! 🎉

- **Frontend**: http://localhost:5173
- **Backend**: http://localhost:5000/api
- **Documentation**: See [DOCUMENTATION.md](DOCUMENTATION.md)

Happy coding! 🕉️

---

**Version**: 1.0.0  
**Last Updated**: February 25, 2026

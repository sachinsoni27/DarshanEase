# 🔧 DARSHAN EASE - Troubleshooting Guide

> Common issues, solutions, and FAQ

---

## 🚨 Quick Troubleshooting

### Application Won't Start

**Problem**: `npm start` fails or hangs

**Solutions**:

```bash
# Clear npm cache
npm cache clean --force

# Remove node_modules and reinstall
rm -rf node_modules backend/node_modules frontend/node_modules
npm run install-all

# Try starting components individually
npm run backend
npm run frontend
```

### Port Already in Use

**Problem**: `Error: listen EADDRINUSE: address already in use :::5000`

**Solutions**:

```bash
# Windows: Find and kill process on port 5000
netstat -ano | findstr :5000
taskkill /PID [PID_NUMBER] /F

# Mac/Linux: Kill process on port 5000
lsof -ti:5000 | xargs kill -9

# Use different port
# Edit backend/.env
PORT=5001
```

### MongoDB Connection Error

**Problem**: `MongooseError: Cannot connect to MongoDB`

**Solutions**:

```bash
# Check MongoDB URI in backend/.env
# Correct format: mongodb://localhost:27017/darshanease

# Verify MongoDB is running
mongod --version

# For Windows, start MongoDB service
net start MongoDB

# For Mac with Homebrew
brew services start mongodb-community

# Test connection
mongo "mongodb://localhost:27017/darshanease"
```

### CORS Errors

**Problem**: `Access to XMLHttpRequest blocked by CORS policy`

**Solutions**:

1. **Verify URLs**
   - Frontend: http://localhost:5173
   - Backend: http://localhost:5000

2. **Check Environment Variables**
   ```bash
   # backend/.env
   FRONTEND_URL=http://localhost:5173
   
   # frontend/.env.local
   VITE_API_BASE_URL=http://localhost:5000/api
   ```

3. **Clear Browser Cache**
   - Press F12
   - Right-click refresh button
   - Click "Clear cache and hard refresh"

---

## 🎨 Frontend Issues

### Page Doesn't Load or Shows Blank

**Problem**: Frontend URL loads but shows blank page

**Steps to Diagnose**:

1. **Check Browser Console** (F12)
   - Look for error messages
   - Check Network tab for failed requests

2. **Check if Vite started**
   ```bash
   # Terminal should show:
   # > vite v... ready in ... ms
   ```

3. **Clear cache**
   ```bash
   # Delete .vite cache
   rm -rf frontend/.vite
   ```

4. **Restart frontend**
   ```bash
   npm run frontend
   ```

### Images Not Loading

**Problem**: Images appear as broken links

**Solutions**:

```bash
# Check public folder
ls frontend/public/

# Verify image paths in code start with /
# Correct: src="/images/temple.jpg"
# Wrong: src="images/temple.jpg"

# For external URLs, verify they're accessible
# Check CORS settings if loading external images
```

### Styling Issues

**Problem**: Tailwind CSS not applied or styles missing

**Solutions**:

```bash
# Rebuild Tailwind
npm run build:frontend

# Check tailwind.config.js exists
ls frontend/tailwind.config.js

# Verify content paths in config:
# content: ["./src/**/*.{js,jsx,ts,tsx}"]

# Clear browser cache (Ctrl+Shift+Delete)
```

### API Calls Failing

**Problem**: API requests return 404 or connection errors

**Diagnostics**:

```javascript
// Open browser console and check Network tab
// Look for requests to http://localhost:5000/api

// Manually test endpoint
const testAPI = async () => {
  try {
    const response = await fetch('http://localhost:5000/api/temples');
    console.log(await response.json());
  } catch (error) {
    console.error('API Error:', error);
  }
};
testAPI();
```

### Firebase Authentication Not Working

**Problem**: Login/signup fails or shows Firebase errors

**Solutions**:

1. **Check Firebase Configuration**
   ```bash
   # Verify frontend/.env.local has all Firebase keys
   VITE_FIREBASE_API_KEY=...
   VITE_FIREBASE_AUTH_DOMAIN=...
   VITE_FIREBASE_PROJECT_ID=...
   ```

2. **Enable Authentication in Firebase**
   - Go to Firebase Console
   - Select Project
   - Go to Authentication
   - Click "Get Started"
   - Enable "Email/Password"

3. **Check Firebase Rules**
   ```javascript
   // In Firestore Rules, allow read/write:
   match /{document=**} {
     allow read, write: if request.auth != null;
   }
   ```

4. **Test Authentication**
   ```typescript
   import { auth } from '@/firebase/config';
   import { signInWithEmailAndPassword } from 'firebase/auth';
   
   const testAuth = async () => {
     try {
       const user = await signInWithEmailAndPassword(auth, email, password);
       console.log('Auth works:', user);
     } catch (error) {
       console.error('Auth error:', error);
     }
   };
   ```

---

## ⚙️ Backend Issues

### Backend Server Not Starting

**Problem**: `npm run backend` fails immediately

**Solutions**:

```bash
# Check Node version
node --version  # Should be >=14.0.0

# Check if port is free
netstat -ano | findstr :5000

# Verify backend/.env exists and is valid
cat backend/.env

# Try starting with verbose output
cd backend && npm start -- --inspect
```

### API Endpoints Return 404

**Problem**: Calling API endpoints returns `Cannot POST /api/temples`

**Solutions**:

1. **Verify Routes are Configured**
   ```javascript
   // backend/server.js should have:
   app.use('/api/temples', templeRoutes);
   app.use('/api/food', foodRoutes);
   app.use('/api/hotels', hotelRoutes);
   app.use('/api/seed', seedRoutes);
   ```

2. **Check Routes File**
   ```bash
   ls backend/routes/
   # Should show: foodRoutes.js, hotelRoutes.js, templeRoutes.js, seedRoutes.js
   ```

3. **Test URLs**
   ```bash
   # Base URL should work
   curl http://localhost:5000/
   
   # API endpoints
   curl http://localhost:5000/api/status
   curl http://localhost:5000/api/temples
   ```

### Database Seeding Fails

**Problem**: Seed endpoints return errors or don't populate data

**Solutions**:

```bash
# Check seed file exists
ls backend/seed/seedData.js

# Manually run seed
cd backend && node seed/seedData.js

# Check database directly
mongo darshanease
db.temples.count()

# Clear database and reseed
db.temples.deleteMany({})
db.temples.insertMany([...])
```

### Unexpected Errors

**Problem**: Backend returns 500 errors with vague messages

**Solutions**:

1. **Enable Detailed Logging**
   ```bash
   # backend/.env
   NODE_ENV=development
   LOG_LEVEL=debug
   ```

2. **Check Backend Logs**
   ```bash
   npm run backend 2>&1 | tee backend.log
   cat backend.log | grep -i error
   ```

3. **Check Server Console**
   - Look for stack traces
   - Identify exact error source
   - Fix issue

---

## 💾 Database Issues

### Cannot Connect to MongoDB

```bash
# Check MongoDB service status
mongod --version

# Verify connection string
# Should be: mongodb://localhost:27017/darshanease
# Or: mongodb+srv://user:pass@cluster.mongodb.net/darshanease

# Test connection with mongo shell
mongo "mongodb://localhost:27017/darshanease"

# Or with newer MongoDB CLI
mongosh "mongodb://localhost:27017/darshanease"
```

### Slow Database Queries

```bash
# Check indexes
mongo darshanease
db.temples.getIndexes()

# Create indexes for frequently searched fields
db.temples.createIndex({ location: 1 })
db.temples.createIndex({ name: "text" })

# Check query performance
db.temples.explain("executionStats").find({ location: "Mathura" })
```

### Data Not Persisting

```bash
# Verify database name is correct
# Check MongoDB connection in backend/.env

# Verify data is actually being inserted
mongo darshanease
db.temples.find().pretty()

# Check for data in correct collection
show collections
```

---

## 🔐 Authentication Issues

### Login Always Fails

**Problem**: Login endpoint returns 401 Unauthorized

**Solutions**:

1. **Check Credentials**
   - Verify user exists in database
   - Check password hash algorithm

2. **Check Firebase Setup**
   ```bash
   # In Firebase Console:
   # Authentication > Email/Password > Enabled
   ```

3. **Check Token Generation**
   ```bash
   # Verify JWT secret in backend/.env
   JWT_SECRET=your_secret_key_here
   ```

### Session Expires Too Quickly

**Problem**: User logged out unexpectedly

**Solutions**:

1. **Increase Session Timeout**
   ```bash
   # backend/.env
   SESSION_TIMEOUT=86400  # 24 hours in seconds
   ```

2. **Check Token Expiration**
   ```bash
   # Verify TOKEN_EXPIRY in backend
   TOKEN_EXPIRY=24h
   ```

---

## 🌐 Network Issues

### Frontend Can't Reach Backend

**Problem**: Network requests fail with connection refused

**Diagnostic Steps**:

```bash
# 1. Check if backend is running
curl http://localhost:5000/api/status

# 2. Check CORS settings
# Response headers should include:
# Access-Control-Allow-Origin: http://localhost:5173

# 3. Check firewall
# Windows Firewall should allow Node.js

# 4. Check Network tab in DevTools
# See actual error message
```

### Slow API Responses

**Solutions**:

```bash
# Implement response caching
// In apiService.ts
const cache = new Map();

// Optimize database queries
db.temples.find().limit(50)

// Use pagination
GET /api/temples?page=1&limit=50
```

---

## 📱 Deployment Issues

### Vercel Deploy Fails

```bash
# Check build command
npm run build:frontend

# Verify Vercel configuration
cat vercel.json

# Check .env variables in Vercel dashboard
# Settings > Environment Variables

# Redeploy
git push origin main
```

### Backend Deployment Issues

```bash
# Check Heroku logs
heroku logs -a app-name --tail

# Verify environment variables
heroku config -a app-name

# Check Procfile
cat Procfile
# Should contain: web: cd backend && npm start
```

---

## ❓ FAQ

### Q: My changes aren't showing up
**A**: 
- Hard refresh browser (Ctrl+Shift+R)
- Check if frontend recompiled (check terminal output)
- Try `npm run frontend` again

### Q: Port 3000 already in use
**A**: Change port in config or kill process on that port

### Q: MongoDB says "authentication failed"
**A**: Check username/password in MONGO_URI, check whitelist in Atlas

### Q: CORS error on production
**A**: Update FRONTEND_URL in production .env to match deployed URL

### Q: Error about missing dependencies
**A**: Run `npm run install-all` to install all deps

### Q: My data disappeared
**A**: Check if seeding ran since last session, verify DB connection

### Q: App works locally but not deployed
**A**: Check that all .env variables are set in deployment platform

### Q: Vite build is huge
**A**: Run `npm run build:frontend` and check bundle size

---

## 🆘 Still Stuck?

1. **Check Documentation**
   - [GETTING_STARTED.md](GETTING_STARTED.md)
   - [API_DOCUMENTATION.md](API_DOCUMENTATION.md)
   - [ARCHITECTURE.md](ARCHITECTURE.md)

2. **Check GitHub Issues**
   - Search for similar problems
   - Create new issue with:
     - Error message
     - Steps to reproduce
     - Environment details

3. **Contact Team**
   - Email: sachinsoniofficial2003@gmail.com
   - Phone: 9936503035
   - GitHub: [github.com/sachinsoni27/DarshanEase](https://github.com/sachinsoni27/DarshanEase)

---

## 🐛 Reporting Issues

When creating GitHub issue, include:

```
### Environment
- OS: Windows/Mac/Linux
- Node Version: v14.0.0
- npm Version: 6.0.0
- Browser: Chrome 120

### Error Message
[Full error message and stack trace]

### Steps to Reproduce
1. First step
2. Second step
3. Expected vs actual

### Screenshots
[Attach relevant screenshots]
```

---

## ✅ Verification Checklist

### Backend
- [ ] Port 5000 is available
- [ ] MongoDB is running
- [ ] `.env` file exists with correct MONGO_URI
- [ ] All route files are in `backend/routes/`
- [ ] Models are in `backend/models/`
- [ ] `npm start` works without errors

### Frontend
- [ ] Port 5173 is available
- [ ] `.env.local` file exists
- [ ] `VITE_API_BASE_URL=http://localhost:5000/api`
- [ ] Firebase keys are configured
- [ ] `npm run dev` starts successfully

### Connection
- [ ] Backend responds to `http://localhost:5000`
- [ ] Frontend can access `http://localhost:5173`
- [ ] Frontend API calls reach backend (check Network tab)
- [ ] No CORS errors in console

---

## 🐛 Common Issues & Solutions

### Issue 1: Backend Port 5000 Already in Use

**On Windows:**
```bash
# Find process using port 5000
netstat -ano | findstr :5000

# Kill the process (replace PID)
taskkill /PID {PID} /F
```

**On macOS/Linux:**
```bash
# Find process
lsof -i :5000

# Kill process
kill -9 {PID}
```

**Or change port in `backend/.env`:**
```
PORT=5001
```

---

### Issue 2: MongoDB Connection Fails

**Check if MongoDB is running:**
```bash
# Windows (if installed)
tasklist | findstr mongod

# macOS
brew services list | grep mongodb

# Linux
systemctl status mongod
```

**Start MongoDB:**
```bash
# Windows
mongod

# macOS
brew services start mongodb-community

# Linux
sudo systemctl start mongod
```

**Or use MongoDB Atlas:**
1. Create account at https://www.mongodb.com/cloud/atlas
2. Create a cluster
3. Update `MONGO_URI` in `backend/.env`
```
MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/darshanease
```

---

### Issue 3: CORS Errors

**Error Message:**
```
Access to XMLHttpRequest at 'http://localhost:5000/api/...' 
from origin 'http://localhost:5173' has been blocked by CORS policy
```

**Solution:**
1. Check `backend/config.js` has correct CORS settings
2. Ensure `backend/server.js` includes CORS middleware
3. Check `frontend/.env.local` has correct API URL

**backend/config.js:**
```javascript
const corsConfig = {
    origin: 'http://localhost:5173',
    credentials: true,
    methods: ['GET', 'POST', 'PUT', 'DELETE'],
};
```

---

### Issue 4: Frontend Can't Connect to API

**Check Network Tab in Browser DevTools:**
1. Open DevTools (F12)
2. Go to Network tab
3. Make an API call
4. Check if request is sent to `http://localhost:5000/api/...`
5. Check response status and any error messages

**Verify API Base URL:**
```bash
# In Browser Console
console.log(import.meta.env.VITE_API_BASE_URL)
# Should output: http://localhost:5000/api
```

**Check Backend is Running:**
```bash
# In Terminal
curl http://localhost:5000

# Should show API info
```

---

### Issue 5: Database Seeding Not Working

**Check MongoDB Connection First:**
```bash
# In Terminal, run
npm run backend

# Should see: ✅ MongoDB Connected: DARSHAN EASE DB
```

**Manually Seed Data:**
```bash
# In another terminal
curl -X POST http://localhost:5000/api/seed/temples
curl -X POST http://localhost:5000/api/seed/food
curl -X POST http://localhost:5000/api/seed/hotels
```

**Or via Browser:**
1. Visit `http://localhost:5173/seed`
2. Wait for data to populate
3. Check browser console for errors

---

### Issue 6: React Component Errors

**Clear node_modules and reinstall:**
```bash
# Frontend
cd frontend
rm -rf node_modules package-lock.json
npm install

# Or Backend
cd backend
rm -rf node_modules package-lock.json
npm install
```

**Clear Browser Cache:**
- Hard Refresh: Ctrl+Shift+R (Windows) or Cmd+Shift+R (macOS)

---

### Issue 7: TypeScript/Build Errors

**Frontend Build Error:**
```bash
cd frontend
npm run build

# Check for type errors
```

**Solution:**
```bash
# Ensure typescript is installed
npm install -D typescript

# Run type check
npx tsc --noEmit
```

---

## 🔍 Debugging Tips

### 1. Check Backend Logs
```bash
# Look for errors in terminal where backend is running
# Should see:
# ✅ MongoDB Connected
# 🕉️  DARSHAN EASE Server Running
# ✅ Port: 5000
```

### 2. Check Frontend Console
```javascript
// Open DevTools (F12) → Console
// Look for:
// - API errors
// - Component errors
// - Network failures

// Test API manually
fetch('http://localhost:5000/api/temples')
  .then(r => r.json())
  .then(d => console.log(d))
```

### 3. Check Network Requests
1. Open DevTools → Network tab
2. Make an API call (click a button, navigate page)
3. Look for request to `http://localhost:5000/api/...`
4. Check status code (should be 200, 201 for success)
5. Check response in Response tab

### 4. MongoDB Compass
- Download: https://www.mongodb.com/products/tools/compass
- Connect to your MongoDB instance
- Browse collections to verify data was seeded

---

## 📋 File Structure Verification

### Backend Must Have
```
backend/
├── .env                    ✅ Environment config
├── config.js              ✅ Configuration
├── server.js              ✅ Main server
├── package.json           ✅ Dependencies
├── models/
│   ├── Temple.js          ✅ Model
│   ├── FoodPlace.js       ✅ Model
│   └── Hotel.js           ✅ Model
└── routes/
    ├── templeRoutes.js    ✅ API routes
    ├── foodRoutes.js      ✅ API routes (NEW)
    ├── hotelRoutes.js     ✅ API routes (NEW)
    └── seedRoutes.js      ✅ API routes (NEW)
```

### Frontend Must Have
```
frontend/
├── .env.local             ✅ Environment config
├── vite.config.ts         ✅ Vite config
├── tsconfig.json          ✅ TypeScript config
├── package.json           ✅ Dependencies
└── src/
    ├── config.ts          ✅ Frontend config (NEW)
    ├── App.tsx            ✅ Main app
    ├── main.tsx           ✅ Entry point
    ├── services/
    │   └── apiService.ts  ✅ API client (NEW)
    ├── components/
    │   ├── ErrorBoundary.tsx     ✅ Error handling (NEW)
    │   └── LoadingSkeletons.tsx  ✅ Loading states (NEW)
    ├── hooks/
    │   └── useApi.ts      ✅ Custom hooks (NEW)
    ├── utils/
    │   └── apiHelpers.ts  ✅ Helper functions (NEW)
    ├── pages/
    ├── context/
    └── data/
```

---

## 🧪 Testing Connections

### Test Backend Endpoints
```bash
# Get all temples
curl http://localhost:5000/api/temples

# Get all food places
curl http://localhost:5000/api/food

# Get all hotels
curl http://localhost:5000/api/hotels

# Check seed status
curl http://localhost:5000/api/seed/status
```

### Test Frontend Loading
1. Open `http://localhost:5173` in browser
2. Check console for any errors
3. Try navigating to different pages
4. Try seeding data from `/seed` page

---

## 📞 Still Having Issues?

### Check These Files:
1. **PROJECT_SETUP.md** - Complete setup guide
2. **ARCHITECTURE.md** - System architecture
3. **FILES_CONNECTIONS.md** - File relationships
4. **QUICK_START.md** - Quick reference

### Logs to Check:
- Backend terminal output
- Browser DevTools Console
- Browser DevTools Network tab
- MongoDB logs

### Common Error Messages:

| Error | Cause | Solution |
|-------|-------|----------|
| `connect ECONNREFUSED 127.0.0.1:5000` | Backend not running | Start backend: `npm run backend` |
| `CORS error` | Frontend-backend mismatch | Check API URL in `.env.local` |
| `MongoDB connection failed` | MongoDB not running | Start MongoDB or use Atlas |
| `Module not found` | Missing dependencies | Run `npm install` |
| `PORT 5000 already in use` | Another process on port | Change PORT in `.env` |

---

## ✨ Success Indicators

✅ Backend is working when:
- Terminal shows: `✅ MongoDB Connected`
- Terminal shows: `✅ DARSHAN EASE Server Running`
- `curl http://localhost:5000` returns JSON response

✅ Frontend is working when:
- Browser loads without JavaScript errors
- Console shows: `🕉️ DARSHAN EASE V2.0 - Mobile Optimization Live 🚀`
- Can navigate between pages

✅ Connection is working when:
- Can make API calls from frontend
- Network tab shows requests to `http://localhost:5000/api/...`
- Responses have status 200
- Can seed data from `/seed` page

---

## 🎉 You're Good to Go!

If all checks pass, your DARSHAN EASE application is fully connected and ready to use!

```
npm start
# Open http://localhost:5173
# Navigate to /seed to populate data
# Enjoy exploring!
```

🙏 Hari Om!

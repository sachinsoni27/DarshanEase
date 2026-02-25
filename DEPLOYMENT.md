# 🚀 DARSHAN EASE - Deployment Guide

> Instructions for deploying DARSHAN EASE to production

---

## 🌐 Deployment Overview

DARSHAN EASE uses a split deployment strategy:

| Component | Hosting | Status |
|-----------|---------|--------|
| Frontend | Vercel | ✅ Automated CI/CD |
| Backend | Heroku/Railway/Local | Manual/Custom |
| Database | MongoDB Atlas | Cloud |
| Assets | Vercel CDN | Automated |

---

## 🚀 Frontend Deployment (Vercel)

### Prerequisites
- GitHub account with repository
- Vercel account (free)
- Repository at https://github.com/sachinsoni27/DarshanEase

### Step 1: Connect GitHub to Vercel

1. Visit [Vercel](https://vercel.com)
2. Click "New Project"
3. Select GitHub
4. Authorize Vercel
5. Select `DarshanEase` repository

### Step 2: Configure Build Settings

Set these values in Vercel:

**Build Command**:
```bash
cd frontend && npm run build
```

**Output Directory**:
```
frontend/dist
```

**Environment Variables**:
```
VITE_API_BASE_URL=https://api.yourdomain.com
VITE_FIREBASE_API_KEY=your_key
VITE_FIREBASE_AUTH_DOMAIN=your_domain
VITE_FIREBASE_PROJECT_ID=your_project_id
VITE_FIREBASE_STORAGE_BUCKET=your_bucket
VITE_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
VITE_FIREBASE_APP_ID=your_app_id
```

### Step 3: Add Redirects (for SPA routing)

Create `frontend/public/vercel.json`:
```json
{
  "rewrites": [
    { "source": "/(.*)", "destination": "/index.html" }
  ]
}
```

### Step 4: Deploy

1. Commit changes to main branch
2. Vercel automatically deploys
3. Get live URL: [darshan-ease.vercel.app](https://darshan-ease-9xqrek4ey-sachin-sonis-projects.vercel.app/)
4. View deployment logs if needed

### Continuous Deployment

After setup, every push to main branch automatically:
- Triggers build
- Runs tests
- Deploys to production
- Updates live site

---

## 🔧 Backend Deployment

### Option 1: Heroku Deployment

#### Prerequisites
- Heroku account (free tier available)
- Heroku CLI installed
- Git repository

#### Step 1: Create Heroku App

```bash
heroku login
heroku create darshanease-api
```

#### Step 2: Add Environment Variables

```bash
heroku config:set -a darshanease-api \
  MONGO_URI=mongodb+srv://user:pass@cluster.mongodb.net/darshanease \
  NODE_ENV=production \
  PORT=5000 \
  FRONTEND_URL=https://darshan-ease-9xqrek4ey-sachin-sonis-projects.vercel.app
```

#### Step 3: Deploy Backend

```bash
# Deploy only backend
git subtree push --prefix backend heroku main

# Or deploy full repository and use Procfile
echo "web: cd backend && npm start" > Procfile
git add Procfile
git commit -m "Add Procfile"
git push heroku main
```

#### Step 4: View Logs

```bash
heroku logs -a darshanease-api --tail
```

### Option 2: Railway.app Deployment

1. Visit [Railway.app](https://railway.app)
2. Create new project
3. Connect GitHub repository
4. Select `backend` directory
5. Add environment variables
6. Deploy

### Option 3: Render Deployment

1. Visit [Render](https://render.com)
2. Create new Web Service
3. Connect GitHub repository
4. Configure build and start commands
5. Add environment variables
6. Deploy

### Option 4: DigitalOcean App Platform

1. Visit [DigitalOcean App Platform](https://cloud.digitalocean.com/apps)
2. Create new app
3. Connect GitHub
4. Configure services
5. Add environment variables
6. Deploy

---

## 🗄️ Database Deployment (MongoDB Atlas)

### Step 1: Create MongoDB Atlas Account

1. Visit [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create free account
3. Create new organization

### Step 2: Create Cluster

1. Click "Create a Cluster"
2. Choose free tier (M0)
3. Select cloud provider and region
4. Click "Create Cluster"
5. Wait for cluster creation (5-10 minutes)

### Step 3: Create Database User

1. In MongoDB Atlas, go to Database Access
2. Click "Add New Database User"
3. Create username and password
4. Set role to "Read and write to any database"
5. Save credentials securely

### Step 4: Get Connection String

1. Click "Connect"
2. Select "Connect your application"
3. Copy connection string
4. Replace `<username>` and `<password>`
5. Copy to `MONGO_URI` in backend .env

### Step 5: Whitelist IP

1. Go to Network Access
2. Click "Add IP Address"
3. Add `0.0.0.0/0` for development
4. Or add specific IPs for production

### Connection String Example
```
mongodb+srv://username:password@cluster0.mongodb.net/darshanease?retryWrites=true&w=majority
```

---

## 🔐 Environment Variables Setup

### Production Frontend (.env.local or Vercel)

```bash
# API Configuration
VITE_API_BASE_URL=https://your-backend-url.com/api

# Firebase Production
VITE_FIREBASE_API_KEY=your_prod_api_key
VITE_FIREBASE_AUTH_DOMAIN=yourproject.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=yourproject
VITE_FIREBASE_STORAGE_BUCKET=yourproject.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=123456789
VITE_FIREBASE_APP_ID=1:123456789:web:abc123def456
```

### Production Backend (.env)

```bash
# Database
MONGO_URI=mongodb+srv://user:pass@cluster.mongodb.net/darshanease

# Server
PORT=5000
NODE_ENV=production

# CORS
FRONTEND_URL=https://darshan-ease-9xqrek4ey-sachin-sonis-projects.vercel.app/

# Firebase (optional)
FIREBASE_PROJECT_ID=yourproject
FIREBASE_PRIVATE_KEY=your_private_key
FIREBASE_CLIENT_EMAIL=firebase@yourproject.iam.gserviceaccount.com
```

---

## ✅ Pre-Deployment Checklist

- [ ] All tests pass locally
- [ ] No console errors or warnings
- [ ] Environment variables configured
- [ ] Database seeded with data
- [ ] Firebase project created and configured
- [ ] MongoDB Atlas cluster created
- [ ] API endpoints tested
- [ ] Frontend builds without errors
- [ ] CORS configured for production URL
- [ ] Security headers set
- [ ] SSL/HTTPS enabled
- [ ] Backups configured

---

## 🧪 Post-Deployment Testing

### Frontend Testing
```bash
# Check if site loads
curl https://darshan-ease-9xqrek4ey-sachin-sonis-projects.vercel.app

# Check Network tab in DevTools
# Verify API calls go to correct endpoint
# Test all major features
```

### Backend Testing
```bash
# Check API health
curl https://your-backend-url.com/api/status

# Test API endpoints
curl https://your-backend-url.com/api/temples
curl https://your-backend-url.com/api/food
curl https://your-backend-url.com/api/hotels
```

---

## 📊 Monitoring & Analytics

### Frontend Monitoring
- **Vercel Analytics**: Built-in analytics dashboard
- **Sentry**: Error tracking and monitoring
- **Google Analytics**: User behavior tracking

### Backend Monitoring
```bash
# Monitor logs
heroku logs -a darshanease-api --tail

# View error rates
# Monitor API response times
# Track database performance
```

### Database Monitoring
- MongoDB Atlas has built-in monitoring
- View connection stats
- Monitor query performance
- Set up alerts

---

## 🔄 Continuous Integration/Deployment (CI/CD)

### GitHub Actions Example

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  deploy-frontend:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm run install-all
      - run: npm run build:frontend
      - name: Deploy to Vercel
        uses: amondnet/vercel-action@master
        with:
          args: deploy --prod --dir=frontend/dist

  deploy-backend:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: akhileshns/heroku-deploy@v3.12.12
        with:
          heroku_api_key: ${{ secrets.HEROKU_API_KEY }}
          heroku_app_name: darshanease-api
          heroku_email: ${{ secrets.HEROKU_EMAIL }}
          usedocker: false
```

---

## 🐛 Troubleshooting Deployment

### Build Fails on Vercel

```bash
# Check build logs in Vercel dashboard
# Verify environment variables are set
# Clear cache and redeploy
```

### API Connection Failed

```bash
# Check CORS settings in backend
# Verify VITE_API_BASE_URL is correct
# Test API endpoint directly with curl
```

### Database Connection Error
```bash
# Verify MongoDB URI in .env
# Check IP whitelist in MongoDB Atlas
# Verify database user credentials
```

### Performance Issues
```bash
# Enable caching
# Optimize database queries
# Use CDN for static assets
# Enable gzip compression
```

---

## 🚀 Scaling Strategy
Vercel
### Frontend Scaling
- Netlify handles auto-scaling
- No additional configuration needed
- Monitor analytics for traffic

### Backend Scaling
- Use Heroku Dynos or equivalent
- Implement caching layer (Redis)
- Use database read replicas
- Implement rate limiting

### Database Scaling
- MongoDB Atlas auto-scaling
- Use indexes for queries
- Implement archiving strategy
- Monitor storage usage

---

## 💰 Cost Optimization
Vercel
### Free/Cheap Options
- **Frontend**: Netlify (free tier)
- **Backend**: Heroku (free tier deprecated, try Railway/Render)
- **Database**: MongoDB Atlas (free tier: 512MB)
- **Monitoring**: Sentry (limited free tier)

### Paid Options
- Heroku: $7-50/month per dyno
- Railway: $5-30/month
- Render: $7-100/month
- MongoDB Atlas: $10-50/month (production)

---

## 🔐 Security Checklist

- [ ] Use HTTPS everywhere
- [ ] Secure API keys in environment variables
- [ ] Enable CORS only for trusted domains
- [ ] Implement rate limiting
- [ ] Use strong MongoDB passwords
- [ ] Enable database authentication
- [ ] Regular security audits
- [ ] Keep dependencies updated
- [ ] Monitor for vulnerabilities
- [ ] Enable error logging and monitoring

---

## 📞 Support

Having deployment issues?

1. Check Netlify/Hosting provider logs
2. Review [TROUBLESHOOTING.md](TROUBLESHOOTING.md)
3. Check API responses with curl
4. Monitor network requests in DevTools
5. Create GitHub issue with details

---

**Version**: 1.0.0  
**Last Updated**: February 25, 2026  
**Status**: ✅ Complete Deployment Guide

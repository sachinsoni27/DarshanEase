# 🕉️ DARSHAN EASE - Temple Discovery Platform

> Connect with the Divine | Discover Temples | Plan Your Pilgrimage

[![Live Demo](https://img.shields.io/badge/Demo-Live-success)](https://darshan-ease-9xqrek4ey-sachin-sonis-projects.vercel.app/)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-61dafb?style=flat&logo=react&logoColor=black)](https://react.dev/)
[![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=node.js&logoColor=white)](https://nodejs.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-13aa52?style=flat&logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![Vercel](https://img.shields.io/badge/Deployed%20on-Vercel-000000?style=flat&logo=vercel&logoColor=white)](https://vercel.com/)

---

## 📖 About DARSHAN EASE

DARSHAN EASE is a comprehensive web application designed to help devotees discover temples, explore sacred destinations, and plan their spiritual journeys seamlessly. Whether you're looking for ancient temples, specific deities, local cuisine, accommodations, or pilgrimage guidance, DARSHAN EASE makes it all easy and accessible.

**Darshan** (दर्शन) means "the sight or vision of the divine," and DARSHAN EASE simplifies this sacred experience for modern pilgrims.

---

## ✨ Key Features

### 🏛️ Temple Discovery
- Search temples by name, location, or deity
- View detailed temple information (history, timings, festivals)
- Explore coordinates and navigation
- Browse special events and festivities

### 🗺️ Smart Trip Planning
- Plan multi-temple pilgrimage routes
- Organize temple visits with custom itineraries
- Save favorite temples and trips
- Share trip plans with other devotees

### 🍽️ Food Discovery
- Find local and traditional cuisine near temples
- Filter by cuisine type and location
- View restaurant details and ratings
- Discover prasad (sacred offerings)

### 🏨 Accommodation Search
- Find hotels and lodges near temples
- Filter by category and price range
- View amenities and contact information
- Book accommodations directly

### 📍 Map View
- Interactive map with temple locations
- Hotel and food place markers
- Real-time location tracking
- Navigate to destinations

### ✍️ Community Feedback
- Share travel experiences
- Rate temples and services
- Read others' feedback
- Community-driven insights

### 📱 User Accounts & Authentication
- Create and manage accounts
- Save trips and preferences
- Track travel history
- Personalized recommendations

### 📋 Yatra Guidelines
- Sacred pilgrimage guidelines
- Temple etiquette and rules
- Best practices for visits
- Safety and precautions

### 👥 Team & Community
- Meet the DARSHAN EASE team
- Community contributors
- Share feedback
- Connect with devotees

---

## 🛠️ Tech Stack

### Frontend
- **Framework**: React 18+ with TypeScript
- **Build Tool**: Vite
- **Styling**: Tailwind CSS + PostCSS
- **State Management**: Context API + Custom Hooks
- **Animations**: Framer Motion
- **Routing**: React Router
- **Authentication**: Firebase
- **HTTP Client**: Axios

### Backend
- **Runtime**: Node.js
- **Framework**: Express.js
- **Database**: MongoDB
- **ODM**: Mongoose
- **Environment**: dotenv
- **CORS**: Cross-Origin Resource Sharing enabled
- **Error Handling**: Custom middleware

### DevOps & Deployment
- **Frontend Hosting**: Vercel (with CI/CD)
- **Backend**: Node.js server (Local/Cloud)
- **Version Control**: Git & GitHub
- **Package Manager**: npm

---

## 🚀 Quick Start

### For Users
Visit the live application: **[darshan-ease.vercel.app](https://darshan-ease-9xqrek4ey-sachin-sonis-projects.vercel.app/)**

### For Developers

#### Prerequisites
- Node.js v14.0.0 or higher
- npm v6.0.0 or higher
- MongoDB (local or Atlas cloud)
- Git

#### Installation (5 minutes)
```bash
# 1. Clone the repository
git clone https://github.com/Dhananjay0376/DarshanEase.git
cd DarshanEase

# 2. Install all dependencies
npm run install-all

# 3. Configure environment variables
# Create backend/.env and frontend/.env.local (see GETTING_STARTED.md)

# 4. Start the application
npm start
```

#### Access the Application
- **Frontend**: http://localhost:5173
- **Backend API**: http://localhost:5000/api
- **Seed Page**: http://localhost:5173/seed

See [GETTING_STARTED.md](GETTING_STARTED.md) for detailed setup instructions.

---

## 📚 Documentation

Access our comprehensive documentation:

| Document | Purpose |
|----------|---------|
| [DOCUMENTATION.md](DOCUMENTATION.md) | 📚 Complete documentation index |
| [GETTING_STARTED.md](GETTING_STARTED.md) | 🚀 Installation and setup guide |
| [FEATURES.md](FEATURES.md) | ✨ Detailed feature overview |
| [API_DOCUMENTATION.md](API_DOCUMENTATION.md) | 📡 Backend API reference |
| [ARCHITECTURE.md](ARCHITECTURE.md) | 🏗️ System architecture and design |
| [DEPLOYMENT.md](DEPLOYMENT.md) | 🚢 Deployment and hosting guide |
| [CONTRIBUTING.md](CONTRIBUTING.md) | 🤝 Contribution guidelines |
| [TROUBLESHOOTING.md](TROUBLESHOOTING.md) | 🔧 Common issues and solutions |

---

## 🏗️ Project Structure

```
DarshanEase/
├── frontend/                 # React + TypeScript frontend
│   ├── src/
│   │   ├── pages/           # Route pages (Home, Temples, Food, Hotels, etc.)
│   │   ├── components/      # Reusable UI components
│   │   ├── context/         # State management (Auth, Planner)
│   │   ├── services/        # API service layer
│   │   ├── firebase/        # Firebase configuration
│   │   ├── utils/           # Utility functions
│   │   └── data/            # Static data
│   ├── public/              # Static assets
│   ├── package.json
│   ├── vite.config.ts
│   ├── tsconfig.json
│   └── tailwind.config.js
│
├── backend/                  # Node.js + Express backend
│   ├── models/              # MongoDB schemas (Temple, Food, Hotel)
│   ├── routes/              # API routes
│   ├── seed/                # Database seed data
│   ├── server.js            # Main server entry point
│   ├── config.js            # Configuration
│   ├── package.json
│   └── .env                 # Environment variables
│
├── documentation/           # Documentation files
│   ├── README.md
│   ├── GETTING_STARTED.md
│   ├── FEATURES.md
│   ├── API_DOCUMENTATION.md
│   ├── ARCHITECTURE.md
│   ├── DEPLOYMENT.md
│   ├── CONTRIBUTING.md
│   └── TROUBLESHOOTING.md
│
└── package.json            # Root package.json
```

---

## 🔄 Data Models

### Temple
```javascript
{
  _id: ObjectId,
  name: String,
  location: String,
  description: String,
  deity: String,
  coordinates: { latitude, longitude },
  timings: { opening, closing },
  festivals: [String],
  imageUrl: String
}
```

### FoodPlace
```javascript
{
  _id: ObjectId,
  name: String,
  type: String,
  cuisine: String,
  location: String,
  coordinates: { latitude, longitude },
  priceRange: String,
  contact: String
}
```

### Hotel
```javascript
{
  _id: ObjectId,
  name: String,
  category: String,
  amenities: [String],
  address: String,
  coordinates: { latitude, longitude },
  contact: String,
  pricePerNight: Number
}
```

---

## 🧪 Testing

### API Endpoints
Test the API using curl or Postman:

```bash
# Get all temples
curl http://localhost:5000/api/temples

# Get specific temple details
curl http://localhost:5000/api/temples/:id

# Get all food places
curl http://localhost:5000/api/food

# Get all hotels
curl http://localhost:5000/api/hotels

# Seed database
curl -X POST http://localhost:5000/api/seed/temples
```

See [API_DOCUMENTATION.md](API_DOCUMENTATION.md) for complete API reference.

---

## 📊 Development Workflow

### Making Changes
1. Create a new branch: `git checkout -b feature/your-feature`
2. Make your changes
3. Test locally: `npm start`
4. Commit: `git commit -m "feat: describe your changes"`
5. Push: `git push origin feature/your-feature`
6. Create a Pull Request

### Building for Production
```bash
npm run build
```

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed contribution guidelines.

---

## 🚢 Deployment

### Frontend (Netlify)
- Automatically deployed on push to main branch
- Live at: [darshan-ease.vercel.app](https://darshan-ease-9xqrek4ey-sachin-sonis-projects.vercel.app/)

### Backend
- Deploy to your preferred cloud platform
- See [DEPLOYMENT.md](DEPLOYMENT.md) for detailed instructions

---

## 📈 Performance & Optimization

- ⚡ Vite for fast development and optimized builds
- 🎯 Tailwind CSS for minimal CSS bundle
- 🔄 React Context for lightweight state management
- 📦 Code splitting with React Router
- 🖼️ Image optimization

---

## 🔒 Security

- 🔐 Firebase Authentication
- 🛡️ CORS protection
- ✅ Environment variables for sensitive data
- 🔒 MongoDB connection security
- 🚫 HTTPS on production

---

## 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on:
- Development setup
- Coding standards
- Commit conventions
- Pull request process

---

## 📞 Support

### Getting Help
1. Check [TROUBLESHOOTING.md](TROUBLESHOOTING.md) for common issues
2. Review [GETTING_STARTED.md](GETTING_STARTED.md) for setup help
3. Check GitHub Issues for similar problems
4. Create a new GitHub Issue with detailed information

### Contact Information
- **Email**: sachinsoniofficial2003@gmail.com
- **Phone**: 9936503035
- **GitHub**: [sachinsoni27/DarshanEase](https://github.com/sachinsoni27/DarshanEase)

---

## 📄 License

This project is licensed under the ISC License - see the LICENSE file for details.

---

## ✨ Credits

**DARSHAN EASE** is created and maintained by **Sachin Soni**, **Sakshi Singh**, and **Satish Kumar** with support from the open-source community.

---

## 🙏 Gratitude

> "दर्शन" - The sight or vision of the divine
> 
> DARSHAN EASE aims to make this sacred experience accessible to all devotees.

---

**Last Updated**: February 25, 2026  
**Version**: 1.0.0  
**Status**: ✅ Active & Maintained

© 2026 DARSHAN EASE. All rights reserved.

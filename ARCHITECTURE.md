# 🏗️ DARSHAN EASE - Complete Architecture Documentation

> Comprehensive architecture overview including MVC pattern, ER-Diagrams, user flows, and technical design

---

## 📊 Table of Contents

1. [Project Architecture Overview](#project-architecture-overview)
2. [Technical Architecture](#technical-architecture)
3. [ER-Diagram](#er-diagram)
4. [Features Architecture](#features-architecture)
5. [Roles and Responsibilities](#roles-and-responsibilities)
6. [User Flow Diagrams](#user-flow-diagrams)
7. [MVC Pattern Implementation](#mvc-pattern-implementation)

---

## 🏗️ Project Architecture Overview

### High-Level System Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                    DARSHAN EASE APPLICATION                         │
├─────────────────────────────────────────────────────────────────────┤
│                                                                       │
│  ┌──────────────────────────┐        ┌──────────────────────────┐   │
│  │   CLIENT LAYER           │        │   SERVER LAYER           │   │
│  │   (React + TypeScript)   │        │   (Node.js + Express)    │   │
│  ├──────────────────────────┤        ├──────────────────────────┤   │
│  │                          │        │                          │   │
│  │  • Presentation Layer    │◄─────►│  • API Layer             │   │
│  │  • Business Logic        │  HTTP │  • Authentication        │   │
│  │  • State Management      │        │  • Business Logic        │   │
│  │  • Firebase Auth         │        │  • Database Operations   │   │
│  │  • Local Storage         │        │  • Error Handling        │   │
│  │                          │        │                          │   │
│  └──────────────────────────┘        └──────────────────────────┘   │
│           ↓                                      ↓                   │
│  ┌──────────────────────────┐        ┌──────────────────────────┐   │
│  │  External Services       │        │  Database Layer          │   │
│  ├──────────────────────────┤        ├──────────────────────────┤   │
│  │                          │        │                          │   │
│  │  • Firebase (Auth)       │        │  • MongoDB (Temples,     │   │
│  │  • Google Maps API       │        │    Food, Hotels)         │   │
│  │  • Vercel CDN            │        │  • Firestore (Users,     │   │
│  │                          │        │    Trips, Feedback)      │   │
│  │                          │        │                          │   │
│  └──────────────────────────┘        └──────────────────────────┘   │
│                                                                       │
└─────────────────────────────────────────────────────────────────────┘
```

### Deployment Architecture

```
Developer → GitHub (sachinsoni27/DarshanEase)
              ↓
        ┌─────────────────────────────────┐
        │  CI/CD Pipeline (GitHub Actions)│
        └─────────────────────────────────┘
              ↓
    ┌─────────────────┬──────────────────┐
    ↓                 ↓
┌─────────┐      ┌──────────┐
│ Vercel  │      │ Heroku/  │
│(Frontend)      │Railway   │
└─────────┘      │(Backend) │
    ↓            └──────────┘
darshan-ease       API Server
.vercel.app        (Production)
    ↓                 ↓
┌────────────────────────────┐
│  MongoDB Atlas             │
│  (Production Database)     │
└────────────────────────────┘
```

---

## 🛠️ Technical Architecture

### Technology Stack

#### Frontend
```
┌─────────────────────────────────────┐
│        FRONTEND TECHNOLOGIES        │
├─────────────────────────────────────┤
│                                     │
│  • React 18+ with TypeScript        │
│  • Vite (Build Tool)                │
│  • Tailwind CSS (Styling)           │
│  • Framer Motion (Animations)       │
│  • React Router (Navigation)        │
│  • Firebase (Authentication)        │
│  • Axios (HTTP Client)              │
│  • Context API (State Management)   │
│  • Google Maps Integration          │
│                                     │
└─────────────────────────────────────┘
```

#### Backend
```
┌─────────────────────────────────────┐
│        BACKEND TECHNOLOGIES         │
├─────────────────────────────────────┤
│                                     │
│  • Node.js (Runtime)                │
│  • Express.js (Framework)           │
│  • MongoDB (Database)               │
│  • Mongoose (ODM)                   │
│  • CORS (Cross-Origin Support)      │
│  • dotenv (Environment Config)      │
│  • Axios (HTTP Requests)            │
│  • Error Handling Middleware        │
│                                     │
└─────────────────────────────────────┘
```

### Layered Architecture

```
┌─────────────────────────────────────────────────────┐
│          PRESENTATION LAYER                         │
│  (React Components, Pages, UI)                      │
└──────────────────┬──────────────────────────────────┘
                   ↓
┌─────────────────────────────────────────────────────┐
│          APPLICATION LAYER                          │
│  (Services, Context, Hooks)                         │
└──────────────────┬──────────────────────────────────┘
                   ↓
┌─────────────────────────────────────────────────────┐
│          API LAYER / ROUTES LAYER                   │
│  (Express Routes, Controllers)                      │
└──────────────────┬──────────────────────────────────┘
                   ↓
┌─────────────────────────────────────────────────────┐
│          BUSINESS LOGIC LAYER                       │
│  (Middleware, Validation, Processing)              │
└──────────────────┬──────────────────────────────────┘
                   ↓
┌─────────────────────────────────────────────────────┐
│          DATA ACCESS LAYER                          │
│  (Models, Database Operations)                      │
└──────────────────┬──────────────────────────────────┘
                   ↓
┌─────────────────────────────────────────────────────┐
│          DATABASE LAYER                             │
│  (MongoDB, Firestore)                               │
└─────────────────────────────────────────────────────┘
```

### Request/Response Flow

```
┌──────────────┐
│ User Action  │
└──────┬───────┘
       ↓
┌──────────────────────────────┐
│ React Component/Page         │
│ → Event Handler              │
└──────┬───────────────────────┘
       ↓
┌──────────────────────────────┐
│ Service Layer (apiService.ts)│
│ → Prepare Request            │
│ → Set Headers & Auth         │
└──────┬───────────────────────┘
       ↓
┌──────────────────────────────┐
│ HTTP Request (Axios)         │
│ → POST/GET to Backend        │
└──────┬───────────────────────┘
       ↓
┌──────────────────────────────┐
│ Express Server               │
│ → CORS Middleware            │
│ → Auth Middleware            │
│ → Route Handler              │
└──────┬───────────────────────┘
       ↓
┌──────────────────────────────┐
│ Controller/Route Logic       │
│ → Validate Input             │
│ → Business Logic             │
│ → Database Query             │
└──────┬───────────────────────┘
       ↓
┌──────────────────────────────┐
│ MongoDB Operations           │
│ → CRUD Operations            │
│ → Return Data                │
└──────┬───────────────────────┘
       ↓
┌──────────────────────────────┐
│ Prepare Response             │
│ → Format JSON                │
│ → Set Status Code            │
└──────┬───────────────────────┘
       ↓
┌──────────────────────────────┐
│ Send Response                │
│ → Back to Frontend           │
└──────┬───────────────────────┘
       ↓
┌──────────────────────────────┐
│ Frontend Receives Response   │
│ → Update State               │
│ → Re-render Component        │
│ → Display Data to User       │
└──────────────────────────────┘
```

---

## 📈 ER-Diagram (Entity Relationship Diagram)

### Database Schema

```
┌─────────────────────────────────────────────────────────────────────┐
│                    DARSHAN EASE DATA MODEL                          │
└─────────────────────────────────────────────────────────────────────┘

╔════════════════════════╗
║      TEMPLE            ║
╠════════════════════════╣
║ _id (ObjectId) [PK]    ║
║ name (String) U        ║◄─────────────┐
║ location (String)      ║              │
║ description (String)   ║              │
║ deity (String)         ║              │
║ coordinates {          ║           (TRIP)
║   latitude (Number)    ║              │
║   longitude (Number)   ║              │
║ }                      ║              │
║ timings {              ║           (FEEDBACK)
║   opening (String)     ║              │
║   closing (String)     ║              │
║ }                      ║              │
║ festivals [String]     ║              │
║ imageUrl (String)      ║              │
║ rating (Number)        ║              │
║ reviews (Number)       ║              │
║ createdAt (Date)       ║              │
║ updatedAt (Date)       ║              │
╚════════════════════════╝              │
         ↑                              │
         │ (1:N)                        │
         └──────────────────────────────┘


╔════════════════════════╗
║    FOODPLACE           ║
╠════════════════════════╣
║ _id (ObjectId) [PK]    ║
║ name (String)          ║
║ type (String)          ║◄─────────────┐
║ cuisine [String]       ║          (suggested in)
║ location (String)      ║              │
║ coordinates {          ║           (TRIP)
║   latitude (Number)    ║              │
║   longitude (Number)   ║              │
║ }                      ║              │
║ priceRange (String)    ║              │
║ contact (String)       ║              │
║ specialities [String]  ║              │
║ imageUrl (String)      ║              │
║ rating (Number)        ║              │
║ createdAt (Date)       ║              │
║ updatedAt (Date)       ║              │
╚════════════════════════╝              │
         ↑                              │
         │ (N:1)                        │
         └──────────────────────────────┘


╔════════════════════════╗
║     HOTEL              ║
╠════════════════════════╣
║ _id (ObjectId) [PK]    ║
║ name (String)          ║
║ category (String)      ║◄─────────────┐
║ address (String)       ║          (suggested in)
║ coordinates {          ║              │
║   latitude (Number)    ║           (TRIP)
║   longitude (Number)   ║              │
║ }                      ║              │
║ contact (String)       ║              │
║ amenities [String]     ║              │
║ pricePerNight (Number) ║              │
║ imageUrl (String)      ║              │
║ availableRooms (Number)║              │
║ rating (Number)        ║              │
║ createdAt (Date)       ║              │
║ updatedAt (Date)       ║              │
╚════════════════════════╝              │
         ↑                              │
         │ (N:1)                        │
         └──────────────────────────────┘


╔════════════════════════════════════╗
║          USER (Firebase)           ║
╠════════════════════════════════════╣
║ uid (String) [PK]                  ║
║ email (String) U                   ║◄────────────┐
║ displayName (String)               ║        (owns)
║ photoURL (String)                  ║             │
║ phoneNumber (String)               ║        (1:N)
║ provider (String)                  ║             │
║ createdAt (Timestamp)              ║             │
║ lastLogin (Timestamp)              ║             ├─► (TRIP - Firestore)
║ isEmailVerified (Boolean)          ║             │
╚════════════════════════════════════╝             ├─► (FEEDBACK - Firestore)
                                                   │
                                                   └──────────────────┘


╔════════════════════════════════════╗
║    TRIP (Firestore)                ║
╠════════════════════════════════════╣
║ tripId (String) [PK]               ║
║ userId (String) [FK]               ║
║ tripName (String)                  ║
║ description (String)               ║
║ temples [                           ║
║   {                                ║
║     templeId (String) [FK]         ║
║     name (String)                  ║
║     visitOrder (Number)            ║
║     estimatedTime (Number)         ║
║   }                                ║
║ ]                                  ║
║ suggestedFood: [foodId]            ║
║ suggestedHotels: [hotelId]         ║
║ startDate (Date)                   ║
║ endDate (Date)                     ║
║ totalDistance (Number)             ║
║ estimatedBudget (Number)           ║
║ status (String): planned/ongoing   ║
║ createdAt (Timestamp)              ║
║ updatedAt (Timestamp)              ║
╚════════════════════════════════════╝


╔════════════════════════════════════╗
║   FEEDBACK (Firestore)             ║
╠════════════════════════════════════╣
║ feedbackId (String) [PK]           ║
║ userId (String) [FK]               ║
║ templeId (String) [FK]             ║
║ templesName (String)               ║
║ userEmail (String)                 ║
║ userName (String)                  ║
║ rating (Number 1-5)                ║
║ reviewText (String) 1000 chars max ║
║ photos [String] URLs               ║
║ helpful (Number)                   ║
║ verified (Boolean)                 ║
║ moderation (String)                ║
║ createdAt (Timestamp)              ║
║ updatedAt (Timestamp)              ║
╚════════════════════════════════════╝


RELATIONSHIPS SUMMARY:
─────────────────────
• USER (1) ──◄──── MANY (TRIP)
• USER (1) ──◄──── MANY (FEEDBACK)
• TEMPLE (1) ──◄──── MANY (FEEDBACK)
• TEMPLE (1) ──◄──── MANY (TRIP)
• TRIP (1) ──◄──── MANY (TEMPLE references)
• TRIP (1) ──◄──── MANY (FOODPLACE suggestions)
• TRIP (1) ──◄──── MANY (HOTEL suggestions)

Database Types:
• MongoDB → temples, foodplaces, hotels (relational data)
• Firestore → users, trips, feedback (real-time data)
```

---

## ✨ Features Architecture

### Feature Distribution by Layer

```
FRONTEND FEATURES (React Components):
────────────────────────────────────
✓ Temple Discovery & Search
  └─ Pages: Temples.tsx, TempleDetails.tsx
  └─ Components: TempleCard, SearchBar, FilterPanel
  
✓ Multi-Temple Trip Planning
  └─ Pages: PlanTrip.tsx
  └─ Components: AddTripModal, TripCard, ItineraryView
  └─ Context: PlannerContext
  
✓ Food Place Discovery
  └─ Pages: Food.tsx
  └─ Components: FoodCard, FoodFilters
  
✓ Hotel Search & Filtering
  └─ Pages: Hotels.tsx
  └─ Components: HotelCard, HotelFilters
  
✓ Interactive Map View
  └─ Pages: Map.tsx
  └─ API: Google Maps Integration
  
✓ User Authentication
  └─ Pages: Login.tsx, Signup.tsx
  └─ Context: AuthContext
  └─ Service: Firebase Authentication
  
✓ Community Feedback
  └─ Pages: AllFeedbacks.tsx, FeedbackForm
  └─ Components: FeedbackDisplay, RatingDisplay
  
✓ Real-time Notifications
  └─ Components: Toast, ErrorBoundary

BACKEND FEATURES (Express Routes):
──────────────────────────────────
✓ CRUD Operations
  ├─ Temples: GET, POST, PUT, DELETE
  ├─ Food Places: GET, POST, PUT, DELETE
  └─ Hotels: GET, POST, PUT, DELETE
  
✓ Data Filtering & Search
  ├─ Filter by location
  ├─ Filter by deity/type
  ├─ Filter by price range
  └─ Full-text search
  
✓ Database Seeding
  ├─ /api/seed/temples
  ├─ /api/seed/food
  └─ /api/seed/hotels
  
✓ Error Handling & Validation
✓ CORS Management
✓ Rate Limiting (optional)

DATABASE FEATURES:
──────────────────
✓ MongoDB: temples, food, hotels (persistent)
✓ Firestore: users, trips, feedback (real-time)
✓ Indexes for performance
✓ Schema validation
✓ Data relationships
```

---

## 👥 Roles and Responsibilities

### Development Team

```
👨‍💼 Sachin Soni
   Title: Lead Developer & Maintainer
   Responsibilities:
   ├─ Full-Stack Development
   ├─ Project Architecture & Design
   ├─ Backend API Development
   ├─ Frontend Implementation
   ├─ DevOps & Deployment
   ├─ Code Review & Quality
   └─ Documentation
   Contact: sachinsoniofficial2003@gmail.com | 9936503035

👩‍💼 Sakshi Singh
   Title: Frontend Developer
   Responsibilities:
   ├─ React Component Development
   ├─ UI/UX Implementation
   ├─ Tailwind CSS Styling
   ├─ Frontend Testing
   ├─ Performance Optimization
   └─ Firebase Integration

👨‍💼 Satish Kumar
   Title: Backend Developer
   Responsibilities:
   ├─ Express.js API Development
   ├─ MongoDB Database Management
   ├─ API Route Implementation
   ├─ Data Seeding & Migration
   ├─ Database Optimization
   └─ Backend Testing
```

| Responsibility | Sachin | Sakshi | Satish | Status |
|---|---|---|---|---|
| Frontend Structure | ✓ | ✓ | | ✅ |
| React Components | ✓ | ✓ | | ✅ |
| State Management | ✓ | ✓ | | ✅ |
| Styling/Tailwind | ✓ | ✓ | | ✅ |
| Backend API | ✓ | | ✓ | ✅ |
| Database Models | ✓ | | ✓ | ✅ |
| CRUD Operations | ✓ | | ✓ | ✅ |
| Data Seeding | ✓ | | ✓ | ✅ |
| Authentication | ✓ | ✓ | ✓ | ✅ |
| Testing | ✓ | ✓ | ✓ | ⏳ |
| Deployment | ✓ | | | ✅ |
| Documentation | ✓ | ✓ | ✓ | ✅ |

---

## 🔄 User Flow Diagrams

### 1. Authentication Flow
```
User → Login Page → Firebase Auth → Create Profile
→ Store Token → Update Context → Grant Access → Dashboard
```

### 2. Temple Discovery Flow
```
Home → Explore Temples → Load Temples
→ Display Grid → Search/Filter → Click Temple
→ View Details → Add to Trip / Share / Rate
```

### 3. Trip Planning Flow
```
Browse Temples → Add to Trip → Trip Modal
→ Create Trip → Save to Firestore → Plan Trip Page
→ View Itinerary → Add Food/Hotels
→ Calculate Distance → Export/Share Trip
```

### 4. Feedback Flow
```
Temple Details → Scroll to Reviews → See Feedback
→ Write Feedback Form → Validate Input
→ Save to Firestore → Show Success
→ Refresh → Display New Feedback
```

---

## 🏛️ MVC Pattern Implementation

### Model Layer
```
Backend Models (Mongoose):
• Temple.js - {name, location, deity, timings, festivals}
• FoodPlace.js - {name, cuisine, location, price}
• Hotel.js - {name, category, amenities, price}

Frontend Models (TypeScript):
• types/index.ts - Interfaces for all data

Firebase Models:
• User Collection - {uid, email, displayName, profile}
• Trip Collection - {tripId, userId, temples, dates}
• Feedback Collection - {feedbackId, userId, templeId, rating}
```

### Controller Layer
```
Backend Controllers (Routes):
• templeRoutes.js - GET/POST/PUT/DELETE temples
• foodRoutes.js - GET/POST food places
• hotelRoutes.js - GET/POST hotels

Frontend Services:
• services/apiService.ts - API calls with Axios
• context/AuthContext.tsx - Authentication logic
• context/PlannerContext.tsx - Trip planning logic
```

### View Layer
```
Frontend Pages (React):
• Home.tsx - Landing page
• Temples.tsx - Temple listing
• TempleDetails.tsx - Temple details
• Food.tsx / Hotels.tsx - Listings
• PlanTrip.tsx - Trip itinerary
• Map.tsx - Interactive map
• Login.tsx / Signup.tsx - Authentication

Components (Reusable):
• TempleCard, FoodCard, HotelCard
• AddTripModal, FeedbackForm
• ErrorBoundary, LoadingSkeletons
```

---

## 📋 Architecture Checklist

```
✅ Frontend Architecture
   ├─ React 18+ with TypeScript
   ├─ Vite build tool
   ├─ Component-based design
   ├─ Context API for state management
   ├─ Services layer for API calls
   ├─ Firebase integration
   ├─ Responsive design
   └─ Error boundaries

✅ Backend Architecture
   ├─ Express.js server
   ├─ RESTful API design
   ├─ MongoDB with Mongoose
   ├─ CRUD operations
   ├─ Error handling middleware
   ├─ CORS configuration
   ├─ Database seeding
   └─ Environment variables

✅ Database Architecture
   ├─ Normalized schemas
   ├─ Proper indexes
   ├─ Relationships defined
   ├─ Type safety
   ├─ Validation rules
   └─ Real-time features

✅ Deployment Architecture
   ├─ Vercel for frontend
   ├─ Cloud hosting for backend
   ├─ MongoDB Atlas
   ├─ Firebase services
   ├─ CI/CD pipeline
   ├─ Environment separation
   └─ SSL/HTTPS
```

---

**Last Updated**: February 25, 2026  
**Version**: 2.0.0 (Complete Architecture)  
**Status**: ✅ Fully Documented & Implemented

© 2026 DARSHAN EASE. All rights reserved.  
**Repository**: https://github.com/sachinsoni27/DarshanEase  
**Live Preview**: https://darshan-ease-9xqrek4ey-sachin-sonis-projects.vercel.app/

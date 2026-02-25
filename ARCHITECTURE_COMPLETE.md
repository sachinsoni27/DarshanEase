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
║ name (String)          ║
║ location (String)      ║
║ description (String)   ║
║ deity (String)         ║
║ coordinates {          ║
║   latitude (Number)    ║
║   longitude (Number)   ║
║ }                      ║
║ timings {              ║
║   opening (String)     ║
║   closing (String)     ║
║ }                      ║
║ festivals [String]     ║
║ imageUrl (String)      ║
║ createdAt (Date)       ║
║ updatedAt (Date)       ║
╚════════════════════════╝
         ↓ (used in)
    ┌────────────┐
    │    TRIP    │
    └────────────┘


╔════════════════════════╗
║    FOODPLACE           ║
╠════════════════════════╣
║ _id (ObjectId) [PK]    ║
║ name (String)          ║
║ type (String)          ║
║ cuisine (String)       ║
║ location (String)      ║
║ coordinates {          ║
║   latitude (Number)    ║
║   longitude (Number)   ║
║ }                      ║
║ priceRange (String)    ║
║ contact (String)       ║
║ specialities [String]  ║
║ imageUrl (String)      ║
║ createdAt (Date)       ║
║ updatedAt (Date)       ║
╚════════════════════════╝
         ↓ (suggested in)
    ┌────────────┐
    │    TRIP    │
    └────────────┘


╔════════════════════════╗
║     HOTEL              ║
╠════════════════════════╣
║ _id (ObjectId) [PK]    ║
║ name (String)          ║
║ category (String)      ║
║ address (String)       ║
║ coordinates {          ║
║   latitude (Number)    ║
║   longitude (Number)   ║
║ }                      ║
║ contact (String)       ║
║ amenities [String]     ║
║ pricePerNight (Number) ║
║ imageUrl (String)      ║
║ createdAt (Date)       ║
║ updatedAt (Date)       ║
╚════════════════════════╝
         ↓ (suggested in)
    ┌────────────┐
    │    TRIP    │
    └────────────┘


╔════════════════════════════════════╗
║          USER (Firebase)           ║
╠════════════════════════════════════╣
║ uid (String) [PK]                  ║
║ email (String)                     ║
║ displayName (String)               ║
║ photoURL (String)                  ║
║ createdAt (Timestamp)              ║
║ lastLogin (Timestamp)              ║
╚════════════════════════════════════╝
         ↓ (owns)
    ┌────────────┐
    │    TRIP    │ (Firestore)
    └────────────┘
         ↓
    ┌────────────┐
    │  FEEDBACK  │ (Firestore)
    └────────────┘


╔════════════════════════════════════╗
║    TRIP (Firestore)                ║
╠════════════════════════════════════╣
║ tripId (String) [PK]               ║
║ userId (String) [FK]               ║
║ tripName (String)                  ║
║ description (String)               ║
║ temples [                           ║
║   templeId (String)                ║
║   visitOrder (Number)              ║
║   estimatedTime (Number)           ║
║ ]                                  ║
║ startDate (Date)                   ║
║ endDate (Date)                     ║
║ totalDistance (Number)             ║
║ budget (Number)                    ║
║ createdAt (Timestamp)              ║
║ updatedAt (Timestamp)              ║
╚════════════════════════════════════╝


╔════════════════════════════════════╗
║   FEEDBACK (Firestore)             ║
╠════════════════════════════════════╣
║ feedbackId (String) [PK]           ║
║ userId (String) [FK]               ║
║ templeId (String) [FK]             ║
║ rating (Number 1-5)                ║
║ reviewText (String)                ║
║ photos [String]                    ║
║ helpful (Number)                   ║
║ createdAt (Timestamp)              ║
║ updatedAt (Timestamp)              ║
╚════════════════════════════════════╝


RELATIONSHIPS:
─────────────
• USER (1) ──◄──── MANY (TRIP)
• USER (1) ──◄──── MANY (FEEDBACK)
• TEMPLE (1) ──◄──── MANY (TRIP)
• TEMPLE (1) ──◄──── MANY (FEEDBACK)
• TRIP (1) ──◄──── MANY (FOODPLACE suggestions)
• TRIP (1) ──◄──── MANY (HOTEL suggestions)
```

---

## ✨ Features Architecture

### Feature Distribution by Layer

```
FEATURE MATRIX:
──────────────────────────────────────────────────────────────

┌─────────────────────────────────────────────────────────────┐
│ FRONTEND FEATURES (UI/UX)                                   │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  • Temple Discovery & Search                                │
│    └─ Components: TempleCard, TempleList, Search Bar      │
│    └─ Page: Temples.tsx, TempleDetails.tsx                │
│                                                              │
│  • Multi-Temple Trip Planning                               │
│    └─ Components: AddTripModal, TripPlanner                │
│    └─ Page: PlanTrip.tsx                                   │
│    └─ Context: PlannerContext                              │
│                                                              │
│  • Food Place Discovery                                     │
│    └─ Components: FoodCard, FoodFilters                    │
│    └─ Page: Food.tsx                                       │
│                                                              │
│  • Hotel Search & Filtering                                 │
│    └─ Components: HotelCard, HotelFilters                  │
│    └─ Page: Hotels.tsx                                     │
│                                                              │
│  • Interactive Map View                                     │
│    └─ Components: MapView, MarkerPopup                     │
│    └─ Page: Map.tsx                                        │
│    └─ Integration: Google Maps API                         │
│                                                              │
│  • User Authentication                                      │
│    └─ Components: LoginForm, SignupForm                    │
│    └─ Pages: Login.tsx, Signup.tsx                         │
│    └─ Context: AuthContext                                 │
│    └─ Integration: Firebase Auth                           │
│                                                              │
│  • Community Feedback                                       │
│    └─ Components: FeedbackForm, FeedbackDisplay            │
│    └─ Page: AllFeedbacks.tsx                               │
│    └─ Database: Firestore                                  │
│                                                              │
│  • Yatra Guidelines                                         │
│    └─ Page: YatraGuidelines.tsx                            │
│    └─ Static Content Display                               │
│                                                              │
│  • Team Information                                         │
│    └─ Page: Team.tsx                                       │
│    └─ Team Member Display                                  │
│                                                              │
│  • Real-time Notifications                                  │
│    └─ Toast/Alert Components                               │
│    └─ Error Boundary                                       │
│                                                              │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ BACKEND FEATURES (API/Business Logic)                       │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  • CRUD Operations                                          │
│    └─ createTemple(), readTemplе(), updateTemple(),       │
│       deleteTemple()                                        │
│    └─ createFood(), readFood(), updateFood(),             │
│       deleteFood()                                          │
│    └─ createHotel(), readHotel(), updateHotel(),          │
│       deleteHotel()                                         │
│                                                              │
│  • Data Filtering & Search                                  │
│    └─ Filter by location, deity, price range              │
│    └─ Full-text search on temples                          │
│                                                              │
│  • Database Seeding                                         │
│    └─ Seed temples with sample data                        │
│    └─ Seed food places with sample data                    │
│    └─ Seed hotels with sample data                         │
│    └─ Seed status endpoint                                 │
│                                                              │
│  • Authentication & Authorization                           │
│    └─ Firebase token verification                          │
│    └─ User role management                                 │
│                                                              │
│  • Error Handling                                           │
│    └─ Graceful error responses                             │
│    └─ HTTP status codes                                    │
│                                                              │
│  • CORS Management                                          │
│    └─ Allow requests from Vercel frontend                  │
│    └─ Handle preflight requests                            │
│                                                              │
│  • API Documentation                                        │
│    └─ Request/response examples                            │
│    └─ Parameter descriptions                               │
│                                                              │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ DATABASE FEATURES                                            │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  • Data Persistence (MongoDB)                               │
│    └─ Collections: temples, foodplaces, hotels              │
│    └─ Indexes for performance                              │
│                                                              │
│  • Real-time Data (Firestore)                               │
│    └─ Collections: users, trips, feedback                  │
│    └─ Real-time listeners                                  │
│                                                              │
│  • Data Validation                                          │
│    └─ Schema validation (Mongoose)                         │
│    └─ Type checking                                        │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

---

## 👥 Roles and Responsibilities

### Development Team Structure

```
┌──────────────────────────────────────────────────────────────────┐
│                    PROJECT TEAM                                  │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  👨‍💼 Sachin Soni (Lead Developer & Maintainer)                    │
│     ├─ Full-Stack Development                                   │
│     ├─ Project Architecture Design                              │
│     ├─ Backend API Development                                  │
│     ├─ Frontend Implementation                                  │
│     ├─ Deployment & DevOps                                      │
│     ├─ Documentation                                            │
│     └─ Contact: sachinsoniofficial2003@gmail.com              │
│         Phone: 9936503035                                       │
│                                                                  │
│  👩‍💼 Sakshi Singh (Core Contributor)                             │
│     ├─ Frontend Development                                     │
│     ├─ UI/UX Implementation                                     │
│     ├─ Component Design                                         │
│     ├─ Testing & QA                                             │
│     └─ Feature Implementation                                   │
│                                                                  │
│  👨‍💼 Satish Kumar (Core Contributor)                             │
│     ├─ Backend Development                                      │
│     ├─ Database Management                                      │
│     ├─ API Optimization                                         │
│     ├─ Data Seeding & Management                               │
│     └─ Performance Optimization                                │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘

RESPONSIBILITY matrix:
─────────────────────

Component/Area          │ Sachin | Sakshi | Satish | Status
──────────────────────────────────────────────────────────────
Frontend Structure      │   ✓   │   ✓   │       │ ✅
React Components        │   ✓   │   ✓   │       │ ✅
State Management        │   ✓   │   ✓   │       │ ✅
Styling/Tailwind       │   ✓   │   ✓   │       │ ✅
Backend API            │   ✓   │       │   ✓   │ ✅
Database Models        │   ✓   │       │   ✓   │ ✅
CRUD Operations        │   ✓   │       │   ✓   │ ✅
Data Seeding           │   ✓   │       │   ✓   │ ✅
Authentication         │   ✓   │   ✓   │   ✓   │ ✅
Testing                │   ✓   │   ✓   │   ✓   │ ⏳
Deployment             │   ✓   │       │       │ ✅
Documentation          │   ✓   │   ✓   │   ✓   │ ✅
Bug Fixes              │   ✓   │   ✓   │   ✓   │ ✅
Performance Opt.       │   ✓   │   ✓   │   ✓   │ ✅
```

---

## 🔄 User Flow Diagrams

### 1. User Authentication Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                 USER AUTHENTICATION FLOW                         │
└─────────────────────────────────────────────────────────────────┘

START
  ↓
[Not Logged In]
  ↓
┌─────────────────────────────┐
│ User visits application     │
└────────┬────────────────────┘
         ↓
    ┌─────────────────┐
    │ Check Auth?     │
    └────┬────────┬───┘
         │        │
    YES  │        │  NO
         ↓        ↓
    ┌──────┐  ┌──────────────┐
    │ Home │  │ Landing Page │
    └──────┘  └────┬─────────┘
                   ↓
            ┌────────────┐
            │ Login Page │
            └─┬──────┬───┘
              │      │
         Email│Google│
              ↓      ↓
        ┌──────────────────┐
        │ Firebase Auth    │
        │ • Verify Email   │
        │ • OAuth Token    │
        └───┬──────────────┘
            ↓
        ┌─────────────────┐
        │ Create/Update   │
        │ User Profile    │
        │ (Firestore)     │
        └─────┬───────────┘
              ↓
        ┌─────────────────┐
        │ Save Auth Token │
        │ (localStorage)  │
        └─────┬───────────┘
              ↓
        ┌─────────────────┐
        │ Update Auth     │
        │ Context         │
        └─────┬───────────┘
              ↓
        ┌─────────────────┐
        │ Grant Access    │
        │ to Protected    │
        │ Pages           │
        └─────┬───────────┘
              ↓
           HOME
```

### 2. Temple Discovery & Viewing Flow

```
┌─────────────────────────────────────────────────────────────────┐
│              TEMPLE DISCOVERY FLOW                               │
└─────────────────────────────────────────────────────────────────┘

HOME PAGE
  ↓
┌──────────────────────────┐
│ Click "Explore Temples"  │
│ or Navigate to /temples  │
└────────┬─────────────────┘
         ↓
    ┌────────────────────────┐
    │ Temples Page           │
    │ • Load all temples     │
    │ • Display in grid      │
    │ • Show filters         │
    └────┬──────┬────────┬───┘
         │      │        │
    ┌────┴──────┴────────┴────┐
    │ User Actions:           │
    │ • Search by name        │
    │ • Filter by location    │
    │ • Filter by deity       │
    │ • Sort results          │
    └─────────┬──────────────┘
              ↓
        ┌─────────────────┐
        │ API: getTemples │
        │ or              │
        │ Filter local    │
        │ data            │
        └─────┬───────────┘
              ↓
        ┌─────────────────────┐
        │ Display Temples     │
        │ (TempleCard)        │
        └─────┬───────────────┘
              ↓
         ┌────────────────┐
         │ Click Temple   │
         │ Card           │
         └────┬───────────┘
              ↓
         ┌────────────────────────┐
         │ Navigate to:           │
         │ /temples/:id           │
         │ TempleDetails Page     │
         └─────┬──────────────────┘
               ↓
         ┌────────────────────────┐
         │ Display:               │
         │ • Full details         │
         │ • Images              │
         │ • Timings             │
         │ • Festivals           │
         │ • Map                 │
         │ • Feedback            │
         │ • Related Info        │
         └─────┬──────────────────┘
               ↓
         ┌────────────────┐
         │ User Options:  │
         │ • Add to Trip  │
         │ • Share       │
         │ • Rate/Review │
         │ • View Map    │
         └────────────────┘
```

### 3. Trip Planning Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                TRIP PLANNING FLOW                                │
└─────────────────────────────────────────────────────────────────┘

USER BROWSING TEMPLES
  ↓
┌──────────────────────┐
│ Click "Add to Trip"  │
│ (on Temple Card)     │
└──────┬───────────────┘
       ↓
    ADD TRIP MODAL
    ┌─────────────────────────┐
    │ • Select/Create Trip    │
    │ • Set Visit Order       │
    │ • Set Time              │
    │ • Add Notes             │
    └────┬────────────────────┘
         ↓
    SAVE TO FIRESTORE
    ┌─────────────────────┐
    │ Update Trip         │
    │ Document:           │
    │ • Add Temple        │
    │ • Update Order      │
    │ • Save Metadata     │
    └────┬────────────────┘
         ↓
    UPDATE UI
    ┌─────────────────┐
    │ Close Modal     │
    │ Show Success    │
    │ Message         │
    └────┬────────────┘
         ↓
CONTINUE BROWSING OR NAVIGATE TO /plantrip
    ↓
┌────────────────────────┐
│ Plan Trip Page         │
│ • View All Trips       │
│ • Edit Trip            │
│ • Reorder Temples      │
│ • Add Food/Hotels      │
│ • View Itinerary       │
│ • Calculate Distance   │
│ • Get Navigation       │
│ • Export/Share Trip    │
└────────────────────────┘
```

### 4. Feedback & Review Flow

```
┌──────────────────────────────────────────────────────────────┐
│            FEEDBACK & REVIEW FLOW                            │
└──────────────────────────────────────────────────────────────┘

ON TEMPLE DETAILS PAGE
  ↓
┌──────────────────────────┐
│ Scroll to Feedback       │
│ Section                  │
└──────┬───────────────────┘
       ↓
    ┌─────────────────────────┐
    │ See Existing Feedback   │
    │ • Display Reviews       │
    │ • Show Ratings          │
    │ • Show Photos           │
    │ • Sort by Helpful       │
    └───┬─────────────────┬───┘
        │                 │
    VIEW│                 │WRITE
        ↓                 ↓
    [Reviews]      ┌────────────────┐
                   │ Feedback Form  │
                   │ • Rating       │
                   │ • Review Text  │
                   │ • Photos       │
                   │ • Submit       │
                   └────┬───────────┘
                        ↓
                  ┌──────────────────┐
                  │ Validation       │
                  │ • Check Auth     │
                  │ • Validate Input │
                  └────┬─────────────┘
                       ↓
                  ┌──────────────────┐
                  │ Save to          │
                  │ Firestore        │
                  │ feedback         │
                  │ collection       │
                  └────┬─────────────┘
                       ↓
                  ┌──────────────────┐
                  │ Update UI        │
                  │ • Show Success   │
                  │ • Refresh List   │
                  │ • Clear Form     │
                  └───────────────────┘
```

---

## 🏛️ MVC Pattern Implementation

### Model-View-Controller Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                   MVC ARCHITECTURE                               │
└─────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────┐
│                         MODEL LAYER                              │
│        (Data & Database Operations - Backend & Frontend)         │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  BACKEND MODELS (Node.js + Mongoose):                          │
│  ─────────────────────────────────────                          │
│  • Temple.js                                                    │
│    └─ Schema: name, location, deity, timings, festivals, etc   │
│    └─ Methods: find, save, update, delete                      │
│    └─ Validations: required fields, type checking              │
│                                                                  │
│  • FoodPlace.js                                                 │
│    └─ Schema: name, cuisine, location, price, etc              │
│    └─ Methods: CRUD operations                                 │
│    └─ Validations: data integrity checks                       │
│                                                                  │
│  • Hotel.js                                                     │
│    └─ Schema: name, category, amenities, price, etc            │
│    └─ Methods: CRUD operations                                 │
│    └─ Validations: data validation                             │
│                                                                  │
│  FRONTEND DATA MODELS (TypeScript):                            │
│  ─────────────────────────────────                            │
│  • types/index.ts                                              │
│    └─ Temple interface                                         │
│    └─ FoodPlace interface                                      │
│    └─ Hotel interface                                          │
│    └─ User interface                                           │
│    └─ Trip interface                                           │
│    └─ Feedback interface                                       │
│                                                                  │
│  • data/templesData.ts                                         │
│    └─ Static temple data                                       │
│    └─ Used for initial display                                 │
│    └─ Can be replaced with API calls                          │
│                                                                  │
│  FIREBASE MODELS:                                              │
│  ────────────────                                              │
│  • User Collection (Firestore)                                 │
│    └─ uid, email, displayName, profile info                   │
│                                                                  │
│  • Trip Collection (Firestore)                                 │
│    └─ tripId, userId, temples, dates, budget                  │
│                                                                  │
│  • Feedback Collection (Firestore)                             │
│    └─ feedbackId, userId, templeId, rating, review            │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────┐
│                      CONTROLLER LAYER                            │
│          (Business Logic & Request Handling)                     │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  BACKEND CONTROLLERS (Express Routes):                         │
│  ──────────────────────────────────────────                    │
│                                                                  │
│  templeRoutes.js:                                              │
│  ├─ GET /temples                                               │
│  │  └─ Handler: Fetch all temples from MongoDB                │
│  │  └─ Logic: Query DB, format response, handle errors         │
│  ├─ GET /temples/:id                                           │
│  │  └─ Handler: Fetch single temple                           │
│  │  └─ Logic: Find by ID, validate, return data               │
│  ├─ POST /temples                                              │
│  │  └─ Handler: Create new temple                             │
│  │  └─ Logic: Validate input, save to DB, return response     │
│  └─ PUT/DELETE /temples/:id                                    │
│     └─ Handler: Update/Delete temple                          │
│     └─ Logic: Auth check, validate, DB operation              │
│                                                                  │
│  foodRoutes.js:                                                │
│  ├─ GET /food                                                  │
│  ├─ GET /food/location/:location                              │
│  ├─ POST /food                                                 │
│  └─ Similar CRUD operations                                    │
│                                                                  │
│  hotelRoutes.js:                                               │
│  ├─ GET /hotels                                                │
│  ├─ GET /hotels/location/:location                            │
│  ├─ POST /hotels                                               │
│  └─ Similar CRUD operations                                    │
│                                                                  │
│  seedRoutes.js:                                                │
│  ├─ POST /seed/temples                                         │
│  ├─ POST /seed/food                                            │
│  ├─ POST /seed/hotels                                          │
│  └─ GET /seed/status                                           │
│     └─ Logic: Populate DB with sample data                    │
│                                                                  │
│  FRONTEND SERVICES (API Layer):                               │
│  ───────────────────────────────                             │
│  services/apiService.ts:                                      │
│  ├─ temples.getAll()                                          │
│  │  └─ HTTP GET /api/temples                                  │
│  │  └─ Error handling, data transformation                    │
│  ├─ temples.getById(id)                                       │
│  │  └─ HTTP GET /api/temples/:id                             │
│  │  └─ Error handling, response caching                       │
│  ├─ food.getByLocation(location)                              │
│  │  └─ HTTP GET /api/food/location/:location                 │
│  │  └─ Query parameters, filters                              │
│  ├─ hotels.getByLocation(location)                            │
│  │  └─ HTTP GET /api/hotels/location/:location               │
│  │  └─ Similar to food                                        │
│  ├─ seed.temples()                                            │
│  │  └─ HTTP POST /api/seed/temples                           │
│  │  └─ Database seeding logic                                 │
│  └─ seed.status()                                             │
│     └─ HTTP GET /api/seed/status                              │
│     └─ Check seeding status                                   │
│                                                                  │
│  CONTEXT LOGIC (State Management):                            │
│  ──────────────────────────────────                          │
│  context/AuthContext.tsx:                                     │
│  ├─ handleSignup()                                            │
│  │  └─ Firebase auth.createUserWithEmailAndPassword()        │
│  │  └─ Create user profile                                    │
│  ├─ handleLogin()                                             │
│  │  └─ Firebase auth.signInWithEmailAndPassword()            │
│  │  └─ Update auth state                                      │
│  ├─ handleLogout()                                            │
│  │  └─ Firebase auth.signOut()                               │
│  │  └─ Clear user data                                        │
│  └─ handleGoogleAuth()                                        │
│     └─ Firebase OAuth logic                                   │
│                                                                  │
│  context/PlannerContext.tsx:                                  │
│  ├─ createTrip()                                              │
│  │  └─ Firestore trips collection                            │
│  │  └─ Save trip metadata                                     │
│  ├─ addTempleToTrip()                                         │
│  │  └─ Update trip document                                   │
│  │  └─ Add temple reference                                   │
│  ├─ updateTripOrder()                                         │
│  │  └─ Reorder temples in trip                               │
│  └─ deleteTrip()                                              │
│     └─ Remove trip from Firestore                            │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────┐
│                       VIEW LAYER                                 │
│              (Presentation & User Interface)                     │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  PAGES (Components Tree):                                      │
│  ──────────────────────                                        │
│  Home.tsx                                                      │
│  ├─ Displays: Hero, Featured temples, Testimonials            │
│  ├─ Calls: None (static content)                             │
│  └─ Updates: Nothing                                          │
│                                                                  │
│  Temples.tsx                                                   │
│  ├─ Displays: Temple list, filters, search                   │
│  ├─ Calls: apiService.temples.getAll()                       │
│  ├─ State: [temples, loading, error]                         │
│  └─ Updates: Re-render on data change                         │
│                                                                  │
│  TempleDetails.tsx                                             │
│  ├─ Displays: Full temple info, map, feedback                │
│  ├─ Calls: apiService.temples.getById(id)                    │
│  ├─ State: [temple, feedback, loading]                       │
│  └─ Updates: Fetch on ID change                               │
│                                                                  │
│  Food.tsx                                                      │
│  ├─ Displays: Food places, filters, search                   │
│  ├─ Calls: apiService.food.getAll()                          │
│  ├─ State: [foodPlaces, filters, loading]                    │
│  └─ Updates: Re-render on filter change                       │
│                                                                  │
│  Hotels.tsx                                                    │
│  ├─ Displays: Hotels, category filter, location              │
│  ├─ Calls: apiService.hotels.getAll()                        │
│  ├─ State: [hotels, filters, loading]                        │
│  └─ Updates: Re-render on filter change                       │
│                                                                  │
│  PlanTrip.tsx                                                  │
│  ├─ Displays: Trip itinerary, map, timeline                  │
│  ├─ Calls: PlannerContext.getTrips()                         │
│  ├─ State: [trips, selectedTrip, editing]                    │
│  └─ Updates: Re-render on trip changes                        │
│                                                                  │
│  Map.tsx                                                       │
│  ├─ Displays: Interactive map with markers                    │
│  ├─ Calls: apiService, Google Maps API                        │
│  ├─ State: [markers, filters, userLocation]                  │
│  └─ Updates: Real-time as user interacts                      │
│                                                                  │
│  AllFeedbacks.tsx                                              │
│  ├─ Displays: All user feedback, ratings                     │
│  ├─ Calls: Firestore queries                                 │
│  ├─ State: [feedback, sorting, filtering]                    │
│  └─ Updates: Real-time from Firestore listener               │
│                                                                  │
│  COMPONENTS (Reusable):                                       │
│  ─────────────────────                                        │
│  TempleCard.tsx                                               │
│  ├─ Props: temple object                                     │
│  ├─ Events: onClick (navigate), onAddTrip                    │
│  └─ Renders: Card UI with temple info                        │
│                                                                  │
│  FoodCard.tsx                                                 │
│  ├─ Props: food object                                       │
│  ├─ Events: onClick (view details)                           │
│  └─ Renders: Food place card                                 │
│                                                                  │
│  HotelCard.tsx                                                │
│  ├─ Props: hotel object                                      │
│  ├─ Events: onClick (navigate)                               │
│  └─ Renders: Hotel card                                      │
│                                                                  │
│  AddTripModal.tsx                                             │
│  ├─ Props: templeId, isOpen, onClose                         │
│  ├─ Events: onSubmit (add to trip)                           │
│  └─ Calls: PlannerContext.addTempleToTrip()                 │
│                                                                  │
│  FeedbackForm.tsx                                             │
│  ├─ Props: templeId                                          │
│  ├─ State: [rating, reviewText, photos]                     │
│  ├─ Events: onSubmit (save feedback)                         │
│  └─ Calls: Firestore.feedback.add()                          │
│                                                                  │
│  FeedbackDisplay.tsx                                          │
│  ├─ Props: feedback[]                                        │
│  ├─ Renders: List of feedback with ratings                  │
│  └─ Actions: Sort, filter, helpful button                    │
│                                                                  │
│  ErrorBoundary.tsx                                            │
│  ├─ Catches: Component errors                                │
│  ├─ Renders: Error UI                                        │
│  └─ Logs: Error details                                      │
│                                                                  │
│  LoadingSkeletons.tsx                                         │
│  ├─ Props: count, type                                       │
│  ├─ Renders: Skeleton screens                                │
│  └─ Used: While data loading                                 │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘

                              ↑
                         USER INTERACTIONS
                              ↓

DATA FLOW IN MVC:
───────────────

1. USER ACTION (View Layer)
   └─ Click button, submit form, navigate page
   
2. EVENT HANDLER (Controller)
   └─ Validate input, prepare request, handle business logic
   
3. API CALL (Service/Controller)
   └─ POST/GET to backend or Firestore
   
4. DATA PROCESSING (Backend Controller)
   └─ Validate, process, query database
   
5. MODEL QUERY (Model Layer)
   └─ CRUD operations on MongoDB/Firestore
   
6. RESPONSE (Backend Controller)
   └─ Format response, set status codes
   
7. DATA UPDATE (Frontend Controller/Context)
   └─ Update state, store in context
   
8. RE-RENDER (View Layer)
   └─ React re-renders with new data
   
9. USER SEES NEW STATE (View)
   └─ UI updated with latest data
```

---

## 📋 Architecture Checklist

### Frontend Architecture
- ✅ React 18+ with TypeScript
- ✅ Vite build tool
- ✅ Component-based design
- ✅ Context API for state management
- ✅ Services layer for API calls
- ✅ Firebase integration
- ✅ Responsive design (Tailwind CSS)
- ✅ Error boundaries
- ✅ Loading states
- ✅ Custom hooks

### Backend Architecture
- ✅ Express.js server
- ✅ RESTful API design
- ✅ MongoDB with Mongoose
- ✅ CRUD operations
- ✅ Error handling middleware
- ✅ CORS configuration
- ✅ Database seeding
- ✅ Data validation
- ✅ Environment variables
- ✅ Cluster routing

### Data Architecture
- ✅ Normalized database schemas
- ✅ Proper indexes
- ✅ Relationships defined
- ✅ Type safety (TypeScript)
- ✅ Validation rules
- ✅ Data persistence strategy
- ✅ Real-time features (Firestore)
- ✅ Backup strategy

### Deployment Architecture
- ✅ Vercel for frontend
- ✅ Cloud hosting for backend
- ✅ MongoDB Atlas
- ✅ Firebase services
- ✅ CI/CD pipeline
- ✅ Environment separation
- ✅ SSL/HTTPS
- ✅ CDN integration

---

## 🔗 Integration Points

### Frontend ↔ Backend Communication
```
Frontend (Vercel)
       ↕ HTTP/REST API
Backend (Cloud)
       ↕ Database Queries
MongoDB + Firestore
```

### Authentication Flow
```
Frontend (Firebase SDK)
       ↕ Firebase Auth
Backend (Token Verification)
       → API Requests
```

### Real-time Data
```
Frontend (Firestore Listeners)
       ↕ WebSocket Connection
Firestore (Real-time Updates)
```

---

**Last Updated**: February 25, 2026  
**Version**: 2.0.0 (Complete Architecture)  
**Status**: ✅ Fully Documented & Implemented

© 2026 DARSHAN EASE. All rights reserved.

# 📡 DARSHAN EASE - API Documentation

> Complete Backend API Reference

---

## 🌐 API Overview

### Base URL
```
http://localhost:5000/api
```

### Authentication
Currently, most endpoints are publicly accessible. Firebase authentication is integrated on the frontend.

### Response Format
All responses are in JSON format.

### Status Codes
- `200`: OK - Request successful
- `201`: Created - Resource created
- `400`: Bad Request - Invalid input
- `404`: Not Found - Resource not found
- `500`: Internal Server Error - Server error

---

## 📍 Temple Endpoints

### Get All Temples
```http
GET /temples
```

**Description**: Retrieve all temples from database

**Response**:
```json
{
  "success": true,
  "data": [
    {
      "_id": "507f1f77bcf86cd799439011",
      "name": "Krishna Temple",
      "location": "Mathura",
      "description": "Ancient temple dedicated to Lord Krishna",
      "deity": "Krishna",
      "coordinates": {
        "latitude": 27.4924,
        "longitude": 77.6737
      },
      "timings": {
        "opening": "05:00",
        "closing": "21:00"
      },
      "festivals": ["Janmashtami", "Holi"],
      "imageUrl": "https://example.com/image.jpg",
      "createdAt": "2024-01-01T00:00:00Z"
    }
  ]
}
```

**Query Parameters**: None

---

### Get Specific Temple
```http
GET /temples/:id
```

**Description**: Retrieve detailed information about a specific temple

**Parameters**:
- `id` (string, required): Temple ID

**Response**:
```json
{
  "success": true,
  "data": {
    "_id": "507f1f77bcf86cd799439011",
    "name": "Krishna Temple",
    "location": "Mathura",
    "description": "Ancient temple dedicated to Lord Krishna",
    "deity": "Krishna",
    "coordinates": {
      "latitude": 27.4924,
      "longitude": 77.6737
    },
    "timings": {
      "opening": "05:00",
      "closing": "21:00"
    },
    "festivals": ["Janmashtami", "Holi"],
    "imageUrl": "https://example.com/image.jpg"
  }
}
```

**Error Response**:
```json
{
  "success": false,
  "message": "Temple not found"
}
```

---

### Create Temple
```http
POST /temples
```

**Description**: Add a new temple to database

**Request Body**:
```json
{
  "name": "Krishna Temple",
  "location": "Mathura",
  "description": "Ancient temple dedicated to Lord Krishna",
  "deity": "Krishna",
  "coordinates": {
    "latitude": 27.4924,
    "longitude": 77.6737
  },
  "timings": {
    "opening": "05:00",
    "closing": "21:00"
  },
  "festivals": ["Janmashtami", "Holi"],
  "imageUrl": "https://example.com/image.jpg"
}
```

**Response**:
```json
{
  "success": true,
  "message": "Temple created successfully",
  "data": {
    "_id": "507f1f77bcf86cd799439011",
    "name": "Krishna Temple",
    ...
  }
}
```

---

## 🍽️ Food Place Endpoints

### Get All Food Places
```http
GET /food
```

**Description**: Retrieve all food places

**Response**:
```json
{
  "success": true,
  "data": [
    {
      "_id": "507f1f77bcf86cd799439012",
      "name": "Traditional Thali House",
      "type": "Restaurant",
      "cuisine": "Indian",
      "location": "Mathura",
      "coordinates": {
        "latitude": 27.4924,
        "longitude": 77.6737
      },
      "priceRange": "Budget",
      "contact": "9876543210",
      "specialities": ["Thali", "Vegetarian"],
      "imageUrl": "https://example.com/food.jpg"
    }
  ]
}
```

---

### Get Food by Location
```http
GET /food/location/:location
```

**Description**: Get food places in a specific location

**Parameters**:
- `location` (string, required): City/location name

**Response**:
```json
{
  "success": true,
  "data": [
    {
      "_id": "507f1f77bcf86cd799439012",
      "name": "Traditional Thali House",
      "type": "Restaurant",
      "cuisine": "Indian",
      "location": "Mathura",
      ...
    }
  ]
}
```

---

### Create Food Place
```http
POST /food
```

**Description**: Add a new food place

**Request Body**:
```json
{
  "name": "Traditional Thali House",
  "type": "Restaurant",
  "cuisine": "Indian",
  "location": "Mathura",
  "coordinates": {
    "latitude": 27.4924,
    "longitude": 77.6737
  },
  "priceRange": "Budget",
  "contact": "9876543210",
  "specialities": ["Thali", "Vegetarian"],
  "imageUrl": "https://example.com/food.jpg"
}
```

**Response**:
```json
{
  "success": true,
  "message": "Food place created successfully",
  "data": { ... }
}
```

---

## 🏨 Hotel Endpoints

### Get All Hotels
```http
GET /hotels
```

**Description**: Retrieve all hotels

**Response**:
```json
{
  "success": true,
  "data": [
    {
      "_id": "507f1f77bcf86cd799439013",
      "name": "Divine Stay Hotel",
      "category": "3-Star",
      "amenities": ["WiFi", "AC", "Restaurant"],
      "address": "Mathura, Uttar Pradesh",
      "coordinates": {
        "latitude": 27.4924,
        "longitude": 77.6737
      },
      "contact": "9876543210",
      "pricePerNight": 2500,
      "imageUrl": "https://example.com/hotel.jpg"
    }
  ]
}
```

---

### Get Hotels by Location
```http
GET /hotels/location/:location
```

**Description**: Get hotels in a specific location

**Parameters**:
- `location` (string, required): City/location name

**Response**:
```json
{
  "success": true,
  "data": [
    {
      "_id": "507f1f77bcf86cd799439013",
      "name": "Divine Stay Hotel",
      "category": "3-Star",
      "location": "Mathura",
      ...
    }
  ]
}
```

---

### Create Hotel
```http
POST /hotels
```

**Description**: Add a new hotel

**Request Body**:
```json
{
  "name": "Divine Stay Hotel",
  "category": "3-Star",
  "amenities": ["WiFi", "AC", "Restaurant"],
  "address": "Mathura, Uttar Pradesh",
  "coordinates": {
    "latitude": 27.4924,
    "longitude": 77.6737
  },
  "contact": "9876543210",
  "pricePerNight": 2500,
  "imageUrl": "https://example.com/hotel.jpg"
}
```

**Response**:
```json
{
  "success": true,
  "message": "Hotel created successfully",
  "data": { ... }
}
```

---

## 🌱 Seed Data Endpoints

### Seed Temples
```http
POST /seed/temples
```

**Description**: Populate temples collection with sample data

**Response**:
```json
{
  "success": true,
  "message": "Temples seeded successfully",
  "count": 15
}
```

---

### Seed Food Places
```http
POST /seed/food
```

**Description**: Populate food places collection with sample data

**Response**:
```json
{
  "success": true,
  "message": "Food places seeded successfully",
  "count": 20
}
```

---

### Seed Hotels
```http
POST /seed/hotels
```

**Description**: Populate hotels collection with sample data

**Response**:
```json
{
  "success": true,
  "message": "Hotels seeded successfully",
  "count": 12
}
```

---

### Get Seed Status
```http
GET /seed/status
```

**Description**: Get current database seed status and counts

**Response**:
```json
{
  "success": true,
  "data": {
    "temples": {
      "count": 15,
      "lastSeeded": "2024-01-15T10:30:00Z",
      "status": "seeded"
    },
    "foodPlaces": {
      "count": 20,
      "lastSeeded": "2024-01-15T10:31:00Z",
      "status": "seeded"
    },
    "hotels": {
      "count": 12,
      "lastSeeded": "2024-01-15T10:32:00Z",
      "status": "seeded"
    }
  }
}
```

---

## 🏥 Health Check Endpoints

### API Health Status
```http
GET /status
```

**Description**: Check if API is running

**Response**:
```json
{
  "success": true,
  "message": "API is running",
  "timestamp": "2024-01-15T10:30:00Z"
}
```

---

## 🧪 Testing API Endpoints

### Using curl

```bash
# Get all temples
curl http://localhost:5000/api/temples

# Get specific temple
curl http://localhost:5000/api/temples/507f1f77bcf86cd799439011

# Create new temple
curl -X POST http://localhost:5000/api/temples \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Test Temple",
    "location": "Test City",
    "deity": "Deity"
  }'

# Get temples by location
curl http://localhost:5000/api/temples/location/Mathura

# Seed data
curl -X POST http://localhost:5000/api/seed/temples
```

### Using Postman

1. Import collection or create requests manually
2. Set base URL: `http://localhost:5000/api`
3. Create requests for each endpoint
4. Test with provided examples
5. Save collection for future use

### Using JavaScript/Axios

```javascript
import axios from 'axios';

const API_URL = 'http://localhost:5000/api';

// Get all temples
const getTemples = async () => {
  try {
    const response = await axios.get(`${API_URL}/temples`);
    console.log(response.data);
  } catch (error) {
    console.error('Error:', error);
  }
};

// Create temple
const createTemple = async (templeData) => {
  try {
    const response = await axios.post(`${API_URL}/temples`, templeData);
    console.log(response.data);
  } catch (error) {
    console.error('Error:', error);
  }
};
```

---

## 📊 Data Models

### Temple Model
```javascript
{
  name: String (required),
  location: String (required),
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
  createdAt: Date,
  updatedAt: Date
}
```

### FoodPlace Model
```javascript
{
  name: String (required),
  type: String,
  cuisine: String,
  location: String (required),
  coordinates: {
    latitude: Number,
    longitude: Number
  },
  priceRange: String,
  contact: String,
  specialities: [String],
  imageUrl: String,
  createdAt: Date,
  updatedAt: Date
}
```

### Hotel Model
```javascript
{
  name: String (required),
  category: String,
  amenities: [String],
  address: String (required),
  coordinates: {
    latitude: Number,
    longitude: Number
  },
  contact: String,
  pricePerNight: Number,
  imageUrl: String,
  createdAt: Date,
  updatedAt: Date
}
```

---

## 🔒 Error Handling

### Common Error Responses

**500 - Server Error**
```json
{
  "success": false,
  "message": "Internal server error",
  "error": "Error details"
}
```

**404 - Not Found**
```json
{
  "success": false,
  "message": "Resource not found"
}
```

**400 - Bad Request**
```json
{
  "success": false,
  "message": "Invalid request data",
  "errors": ["Field error message"]
}
```

---

## 🚀 Rate Limiting

Currently no rate limiting implemented. Production deployment should include:
- 100 requests per minute per IP
- 1000 requests per hour per user
- Backoff strategy for failed requests

---

## 📈 Performance Tips

1. **Cache Results**: Cache temple listings
2. **Pagination**: Implement pagination for large datasets
3. **Lazy Loading**: Load images lazily
4. **Query Optimization**: Use indexes on frequently queried fields
5. **CDN**: Use CDN for image storage

---

## 🔐 Security Notes

1. **Input Validation**: All inputs are validated server-side
2. **CORS**: Enabled only for frontend URL
3. **MongoDB**: Use authentication credentials
4. **Environment Variables**: Keep sensitive data in `.env`
5. **HTTPS**: Use HTTPS in production

---

## 📚 Frontend Integration

The frontend communicates via `src/services/apiService.ts`:

```typescript
export const apiService = {
  temples: {
    getAll: () => axios.get('/temples'),
    getById: (id) => axios.get(`/temples/${id}`),
    create: (data) => axios.post('/temples', data),
    getByLocation: (location) => axios.get(`/temples/location/${location}`)
  },
  food: {
    getAll: () => axios.get('/food'),
    getByLocation: (location) => axios.get(`/food/location/${location}`),
    create: (data) => axios.post('/food', data)
  },
  hotels: {
    getAll: () => axios.get('/hotels'),
    getByLocation: (location) => axios.get(`/hotels/location/${location}`),
    create: (data) => axios.post('/hotels', data)
  },
  seed: {
    temples: () => axios.post('/seed/temples'),
    food: () => axios.post('/seed/food'),
    hotels: () => axios.post('/seed/hotels'),
    status: () => axios.get('/seed/status')
  }
};
```

---

**Version**: 1.0.0  
**Last Updated**: February 25, 2026  
**Status**: ✅ Complete API Documentation

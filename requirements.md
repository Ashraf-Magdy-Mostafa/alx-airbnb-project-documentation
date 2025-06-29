# Airbnb Clone Backend – Requirement Specifications

This document outlines the functional and technical requirements for the core backend features of the Airbnb Clone project.

---

## 1. User Authentication

### 🔗 API Endpoints
- `POST /api/register` – Register a new user (guest or host)
- `POST /api/login` – Authenticate user and issue JWT
- `GET /api/profile` – Fetch logged-in user's data
- `PUT /api/profile` – Update profile information

### 🛠 Inputs
- `email`: string, required, valid format
- `password`: string, required, min 8 chars
- `role`: enum (guest, host), required

### 📤 Outputs
- Success: JWT token, user ID, role
- Error: Validation error, unauthorized, server error

### ✅ Validation Rules
- Email must be unique and properly formatted
- Password must be hashed before storing
- JWT must be valid for all secured routes

### 🚀 Performance Criteria
- Response time < 300ms
- Token expiration: 24 hours

---

## 2. Property Management

### 🔗 API Endpoints
- `POST /api/properties` – Create new listing
- `GET /api/properties` – Fetch list of properties with filters
- `GET /api/properties/:id` – Get single property details
- `PUT /api/properties/:id` – Update listing
- `DELETE /api/properties/:id` – Delete listing

### 🛠 Inputs
- `title`: string, required
- `description`: string, optional
- `price`: number, required
- `location`: string, required
- `availability`: date range, required
- `amenities`: array of strings, optional
- `images`: file upload (Cloudinary or local path)

### 📤 Outputs
- List of matching properties
- Confirmation of created/updated/deleted listing

### ✅ Validation Rules
- Price must be > 0
- Required fields cannot be empty
- Only authenticated hosts can create/update/delete

### 🚀 Performance Criteria
- Image upload must complete < 3 seconds
- Paginated listing (e.g., 10 per page) with < 500ms fetch time

---

## 3. Booking System

### 🔗 API Endpoints
- `POST /api/bookings` – Create a new booking
- `GET /api/bookings/:userId` – Get user-specific bookings
- `PUT /api/bookings/:id/cancel` – Cancel booking

### 🛠 Inputs
- `userId`: UUID, required
- `propertyId`: UUID, required
- `startDate`: ISO date, required
- `endDate`: ISO date, required

### 📤 Outputs
- Success message with booking ID and status
- Error for unavailable dates, authentication failure

### ✅ Validation Rules
- Booking dates must not overlap existing bookings
- Start date must be < end date
- Cannot book own property
- Refund policy applies based on cancellation timing

### 🚀 Performance Criteria
- Booking confirmation E-Mail in < 1 Minute
- Date conflict check < 200ms
- Auto-status updates (confirmed, cancelled)

---



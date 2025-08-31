# Backend Requirement Specifications

This document specifies the functional and technical requirements for the core backend features of the ALX Airbnb Database Project.

---

## 1. User Authentication

### Objective
Allow users (Guests and Hosts) to securely register, log in, and manage their accounts.

### Functional Requirements
- **User Registration**
  - Users must provide `username`, `email`, `password`.
  - System must validate uniqueness of email and username.
  - Password must be hashed before storage.
- **User Login**
  - Authenticate users via `email` and `password`.
  - Return a session token or JWT on success.
- **Account Management**
  - Users can update their profile details.
  - Users can delete their accounts (soft delete preferred).

### API Endpoints
- `POST /api/auth/register` – Register a new user.
- `POST /api/auth/login` – Authenticate and return token.
- `GET /api/auth/user` – Fetch current authenticated user profile.
- `PUT /api/auth/user` – Update profile details.
- `DELETE /api/auth/user` – Delete user account.

### Input/Output Specifications
- **Input (Register):**
  ```json
  {
    "username": "john_doe",
    "email": "john@example.com",
    "password": "SecurePass123"
  }
Output (Success):

json
Copy code
{
  "message": "User registered successfully",
  "user_id": 1
}
Error Example:

json
Copy code
{
  "error": "Email already exists"
}
Validation Rules
Email must be valid format.

Password: min 8 characters, at least 1 uppercase, 1 lowercase, 1 number.

Username must be alphanumeric, 3–20 characters.

Performance Criteria
Authentication API should respond within 200ms under normal load.

Password hashing must use a secure algorithm (e.g., PBKDF2, bcrypt, Argon2).

2. Property Management
Objective
Allow hosts to add, update, and manage rental properties.

Functional Requirements
Hosts can create new property listings with details: title, description, location, price_per_night, availability_dates, images.

Hosts can update or delete their properties.

Guests can search and view properties based on filters (location, price, availability).

API Endpoints
POST /api/properties – Create new property (Host only).

GET /api/properties – List all properties with filters.

GET /api/properties/{id} – Get details of a property.

PUT /api/properties/{id} – Update property details (Host only).

DELETE /api/properties/{id} – Delete property (Host only).

Input/Output Specifications
Input (Create Property):

json
Copy code
{
  "title": "Modern Apartment",
  "description": "2-bedroom apartment near city center",
  "location": "Addis Ababa",
  "price_per_night": 40,
  "availability_dates": ["2025-09-01", "2025-09-30"],
  "images": ["image1.jpg", "image2.jpg"]
}
Output (Success):

json
Copy code
{
  "message": "Property created successfully",
  "property_id": 101
}
Validation Rules
Price must be a positive number.

Location cannot be empty.

At least one availability date must be provided.

Hosts can only update/delete properties they own.

Performance Criteria
Property search must return results within 500ms.

Property listing API must support pagination (default: 10 per page).

3. Booking System
Objective
Allow guests to book available properties and manage their reservations.

Functional Requirements
Guests can create a booking by selecting property, check-in and check-out dates.

System must validate property availability before confirming booking.

Guests can cancel bookings before check-in date.

Hosts can view bookings for their properties.

API Endpoints
POST /api/bookings – Create a booking.

GET /api/bookings – View all bookings (Guest: own bookings, Host: bookings for owned properties).

GET /api/bookings/{id} – Get details of a booking.

DELETE /api/bookings/{id} – Cancel a booking (Guest only).

Input/Output Specifications
Input (Create Booking):

json
Copy code
{
  "property_id": 101,
  "check_in": "2025-09-05",
  "check_out": "2025-09-10"
}
Output (Success):

json
Copy code
{
  "message": "Booking confirmed",
  "booking_id": 555,
  "property_id": 101,
  "check_in": "2025-09-05",
  "check_out": "2025-09-10",
  "status": "confirmed"
}
Validation Rules
Check-in date must be before check-out date.

Property must be available for the requested dates.

Only authenticated users can create bookings.

Performance Criteria
Booking confirmation should occur within 1 second.

System must prevent double-booking of the same property for overlapping dates.

Notes
All endpoints must follow RESTful standards.

Responses must use consistent JSON format.

Authentication must be enforced using JWT.

Role-based access control:

Guest: can search, book, manage bookings.

Host: can manage properties, view bookings.

Admin: full access (moderation, user/property management).

pgsql
Copy code

---

👉 This `requirements.md` is now ready to add to your repo under root.  

Would you like me to also **add a 4th requirement** (like **Payment Processing**) so the document is more complete, or keep it with the 3 features for now (User Auth, Property Management, Booking System)?

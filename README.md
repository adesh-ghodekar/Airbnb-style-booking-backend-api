# Airbnb Style Booking Backend API

A production-style backend system for a hotel booking platform inspired by Airbnb, built using Spring Boot and PostgreSQL.

<img width="1918" height="903" alt="Screenshot 2026-06-28 155415" src="https://github.com/user-attachments/assets/38dd6ed2-48eb-451d-a408-85c3fbd64cdd" />


## Features

* JWT Authentication & Authorization
* Role-based Access Control (Admin / User)
* Hotel Management
* Room Management
* Inventory Management
* Dynamic Pricing Engine
* Booking Flow Management
* Guest Management
* Payment Integration Structure
* Hotel Booking Reports
* Swagger API Documentation

---

## Tech Stack

* Java 23
* Spring Boot
* Spring Security + JWT
* Hibernate / JPA
* PostgreSQL
* Maven
* Swagger OpenAPI
* Docker

---

## Project Architecture

```text
                        +----------------------+
                        |      Client / UI     |
                        | (Postman / Swagger)  |
                        +----------+-----------+
                                   |
                                   v
                     +-----------------------------+
                     |        REST Controllers      |
                     | Auth | Hotel | Booking etc. |
                     +-------------+---------------+
                                   |
                                   v
                     +-----------------------------+
                     |          Services            |
                     | Business Logic Layer         |
                     +-------------+---------------+
                                   |
                    +--------------+---------------+
                    |                              |
                    v                              v
          +-------------------+         +-------------------+
          |  Pricing Engine   |         | Payment Service   |
          | Dynamic Pricing   |         | Stripe/Razorpay   |
          +-------------------+         +-------------------+
                    |                              |
                    +--------------+---------------+
                                   |
                                   v
                     +-----------------------------+
                     |        Repositories          |
                     | Spring Data JPA Layer        |
                     +-------------+---------------+
                                   |
                                   v
                     +-----------------------------+
                     |        PostgreSQL DB         |
                     +-----------------------------+
```


---

## Database Entities

* User
* Hotel
* Room
* Inventory
* Booking
* Guest

### Relationships

* User → Hotels
* Hotel → Rooms
* Room → Inventory
* User → Bookings
* Booking → Guests

<img width="1110" height="772" alt="423202353-bc209296-e0f2-48f9-a7ae-65d084e4cb6c" src="https://github.com/user-attachments/assets/0970fbba-3bae-4483-b66d-6b183080c933" />
---


## Booking Flow

RESERVED
→ GUESTS_ADDED
→ PAYMENTS_PENDING
→ CONFIRMED

Additional states:

* CANCELLED
* EXPIRED

---

## Major Modules

### Authentication Module

* User Signup
* Login
* JWT Token Generation
* Role-based Authorization

### Hotel Management

* Create Hotel
* Update Hotel
* Delete Hotel
* Activate Hotel
* Fetch Hotels

### Room Management

* Create Room
* Update Room
* Delete Room

### Inventory Management

* Room availability tracking
* Inventory initialization
* Inventory updates

### Dynamic Pricing Engine

Price is calculated based on:

* Base Price
* Room Availability
* Surge Factor

### Booking Management

* Initialize Booking
* Add Guests
* Payment Flow
* Booking Status Tracking
* Booking Cancellation

### Reporting

* Booking Count
* Total Revenue
* Average Revenue

---
## REST API Endpoints

### Authentication
```http
POST /api/v1/auth/signup
POST /api/v1/auth/login
```

### Hotel Management
```http
POST   /api/v1/admin/hotels
GET    /api/v1/admin/hotels
GET    /api/v1/admin/hotels/{hotelId}
PUT    /api/v1/admin/hotels/{hotelId}
DELETE /api/v1/admin/hotels/{hotelId}
PATCH  /api/v1/admin/hotels/{hotelId}/activate
```

### Room Management
```http
POST   /api/v1/admin/hotels/{hotelId}/rooms
GET    /api/v1/admin/inventory/rooms/{roomId}
PATCH  /api/v1/admin/inventory/rooms/{roomId}
```

### Booking Management
```http
POST /api/v1/bookings/init
POST /api/v1/bookings/{bookingId}/addGuests
POST /api/v1/bookings/{bookingId}/payments
POST /api/v1/bookings/{bookingId}/cancel
GET  /api/v1/bookings/{bookingId}/status
```

### Reports
```http
GET /api/v1/admin/hotels/{hotelId}/reports
```
## API Documentation

Swagger UI available at:

http://localhost:8080/swagger-ui/index.html

---

## How to Run

### Clone Repository

```bash
git clone https://github.com/adesh-ghodekar/Airbnb-style-booking-backend-api.git
```

### Configure Database

Update application.properties with PostgreSQL credentials.

### Run Application

```bash
./mvnw spring-boot:run
```

OR

```bash
mvn spring-boot:run
```

---

## Docker Run

Build image:

```bash
docker build -t airbnb-backend .
```

Run container:

```bash
docker run -p 8080:8080 airbnb-backend
```

---

## Future Improvements

* Razorpay Integration
* Reviews & Ratings
* Coupons & Discounts
* Email Notifications
* Redis Caching
* CI/CD Pipeline
* AWS Deployment

---

## Author

Adesh Ghodekar

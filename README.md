# Eventora - Full-Stack Event Booking Platform

Eventora is a full-stack MERN application designed to provide a secure, seamless event booking experience. Users can browse, register, and pay for events natively. Administrators have full control over event management, booking verification, and analytics dashboards.  

This project demonstrates backend skills in **API design, data modeling, business logic, and role-based access control**, making it highly aligned with backend-focused assignments such as the **Finance Data Processing & Access Control** project.

---

## Table of Contents

1. [Features](#features)  
2. [Tech Stack](#tech-stack)  
3. [Roles & Access Control](#roles--access-control)  
4. [API Documentation](#api-documentation)  
5. [Backend Logic Flow](#backend-logic-flow)  
6. [Setup Instructions](#setup-instructions)  
7. [How This Matches Finance Backend Assignment](#how-this-matches-finance-backend-assignment)  
8. [Deployment](#deployment)  

---

## Features

### Authentication & Security
- JWT-based login and registration
- Password hashing with bcrypt
- 2FA OTP verification for account activation and booking confirmation

### Role-Based Access
- **Admin:** Manage events, approve/reject bookings, mark payments as 'Paid'/'Not Paid', restricted to database-flagged users  
- **User:** Browse events, submit booking requests via OTP, view dashboard status, cancel bookings

### Event Management
- Create free or paid events with detailed descriptions, images, dates, categories, and seating capacity
- Admin can edit or delete events

### Smart Booking System
- 2FA OTP authorization for bookings
- Pending queue for Admin verification
- Seat availability checked to prevent overbooking

### Admin Dashboard
- Metrics include Pending Requests, Total Revenue, Total Confirmed Paid Clients
- Real-time updates

### Notifications
- Email notifications via Nodemailer on booking confirmation

### Frontend
- Built with React + Tailwind CSS
- Polished UI with micro-interactions

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | Node.js, Express, MongoDB, Mongoose |
| Frontend | React, Tailwind CSS |
| Authentication | JWT, bcrypt, 2FA OTP |
| Email | Nodemailer |
| Deployment | Backend: Render/Railway, Frontend: Vercel |
| Tools | Postman, concurrently |

---

## Roles & Access Control

| Role | Permissions |
|------|------------|
| Admin | Create, edit, delete events; Approve/Reject bookings; Mark payments; Access dashboard metrics |
| User | Browse events; Create booking requests; Cancel bookings; View personal dashboard |

**Backend access enforcement:**  
- Middleware checks JWT + role  
- Admin-only routes block Users  
- OTP verification required for sensitive actions

---

## API Documentation

> **Base URL (local):** `http://localhost:5000`  
> **Base URL (deployed example):** `https://eventora-backend.onrender.com`  

### 1. Authentication

| Method | Endpoint | Request Body | Response |
|--------|----------|-------------|---------|
| POST | `/api/auth/register` | `{ name, email, password }` | Success message + OTP sent |
| POST | `/api/auth/verify-otp` | `{ email, otp }` | Account activation |
| POST | `/api/auth/login` | `{ email, password }` | JWT token + role |

### 2. Events (Admin Only)

| Method | Endpoint | Request Body | Response |
|--------|----------|-------------|---------|
| POST | `/api/events` | `{ title, description, date, category, imageURL, capacity, price }` | Event created |
| PUT | `/api/events/:id` | `{ updated fields }` | Event updated |
| DELETE | `/api/events/:id` | - | Event deleted |
| GET | `/api/events` | - | List of all events |

### 3. Bookings

| Method | Endpoint | Request Body | Response |
|--------|----------|-------------|---------|
| POST | `/api/bookings` | `{ eventId, userId }` | Booking pending, OTP sent |
| POST | `/api/bookings/verify-otp` | `{ bookingId, otp }` | Booking confirmed |
| PUT | `/api/bookings/cancel/:id` | - | Booking cancelled |
| GET | `/api/bookings` | Admin only | List of all bookings |
| GET | `/api/bookings/user/:userId` | User only | User's bookings |

### 4. Dashboard Metrics (Admin Only)

| Method | Endpoint | Response |
|--------|----------|---------|
| GET | `/api/dashboard/metrics` | `{ pendingRequests, totalRevenue, totalPaidClients }` |

### 5. Images(Admin Dashboard, Home Page)

---
<img width="948" height="483" alt="Screenshot 2026-04-06 010732" src="https://github.com/user-attachments/assets/86147205-d5c3-4ec5-b4cf-3809b41b3704" />
---
(<img width="928" height="496" alt="Screenshot 2026-04-06 010746" src="https://github.com/user-attachments/assets/bbe151aa-ec7d-41a9-ae23-7b5f15e8bb93" />
---
<img width="936" height="494" alt="Screenshot 2026-04-06 010651" src="https://github.com/user-attachments/assets/708aa6cd-9f8f-4e44-bdb6-ed51ca2a1972" />
---


)

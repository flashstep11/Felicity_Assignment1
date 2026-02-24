# Felicity Event Management System

A comprehensive full-stack event management system built with the MERN stack (MongoDB, Express.js, React, Node.js).

## 📋 Features

### User Roles
- **Participants** (IIIT Students & Non-IIIT)
- **Organizers** (Clubs/Councils/Fest Teams)
- **Admin** (System Administrator)

### Core Functionality

#### 🎓 Participant Features
- **Registration & Authentication**
  - IIIT students register with @iiit.ac.in email
  - Non-IIIT participants with email and password
  - Email domain validation for IIIT students
  
- **Event Management**
  - Browse all published events with search and filters
  - View trending events (Top 5 in last 24h)
  - Filter by event type, eligibility, date range, tags
  - View complete event details
  - Register for events with custom forms
  - View registration status and QR codes
  
- **Dashboard**
  - Upcoming events
  - Past events history
  - Completed events
  - Registration tickets with QR codes
  
- **Clubs & Organizers**
  - Browse all approved organizers
  - Follow/unfollow organizers
  - View organizer details and events
  
- **Profile Management**
  - Edit profile information
  - Change password
  - Manage preferences

#### 🏢 Organizer Features
- **Event Creation & Management**
  - Create events as drafts
  - Define required fields (Section 8)
  - Custom registration forms with dynamic form builder
  - Merchandise events with stock management
  - Publish events (auto-post to Discord)
  - Edit event details (draft/ongoing/completed states)
  
- **Dashboard**
  - Events carousel with status indicators
  - Analytics: registrations, revenue, attendance
  - View all created events
  
- **Participant Management**
  - View registered participants
  - Search and filter participants
  - Export participant list as CSV
  - View individual registration details
  
- **Profile**
  - Edit organizer information
  - Configure Discord webhook for auto-posting events
  - Manage contact details

#### ⚙️ Admin Features
- **Club/Organizer Management**
  - Create new organizer accounts
  - Auto-generate login credentials
  - System shares credentials with organizer
  - Disable/restore organizer accounts
  - Cannot delete (option to archive)
  
- **Password Reset Requests**
  - View all pending password reset requests
  - Approve/reject requests
  - Generate new passwords
  - System sends new password to users
  
- **Dashboard**
  - System-wide statistics
  - Total participants, organizers, events
  - Pending password reset requests

### 🔐 Security Features
- Passwords hashed using bcrypt (no plaintext storage)
- JWT-based authentication for all protected routes
- Role-based access control
- Session management with persistent sessions
- Logout clears all authentication tokens
- Protected routes require authentication
- Email domain validation for IIIT students

### 📧 Event Registration Workflows
- **Normal Events**
  - Custom registration form
  - Email confirmation with event details
  - QR code ticket generation
  - Team name support
  
- **Merchandise Events**
  - Stock management
  - Purchase limit per participant
  - Order confirmation email
  - QR code for pickup

### 🎨 User Interface
- Clean, modern design with Tailwind CSS
- Responsive layout (mobile, tablet, desktop)
- Role-specific navigation menus
- Real-time toast notifications
- Loading states and error handling
- Form validation

## 🛠️ Technology Stack

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **MongoDB** - Database
- **Mongoose** - ODM
- **bcrypt** - Password hashing
- **jsonwebtoken** - JWT authentication
- **nodemailer** - Email service
- **qrcode** - QR code generation
- **axios** - HTTP client for Discord webhook
- **validator** - Email validation

### Frontend
- **React** - UI library
- **React Router** - Routing
- **Axios** - API client
- **Tailwind CSS** - Styling
- **React Hot Toast** - Notifications
- **React Icons** - Icon library
- **date-fns** - Date formatting

## 📁 Project Structure

```
assignment-1/
├── backend/
│   ├── models/
│   │   ├── Admin.js
│   │   ├── Participant.js
│   │   ├── Organizer.js
│   │   ├── Event.js
│   │   └── PasswordResetRequest.js
│   ├── routes/
│   │   ├── auth.js
│   │   ├── participant.js
│   │   ├── organizer.js
│   │   ├── admin.js
│   │   └── event.js
│   ├── middleware/
│   │   └── auth.js
│   ├── utils/
│   │   ├── createAdmin.js
│   │   ├── emailService.js
│   │   ├── discordWebhook.js
│   │   └── qrGenerator.js
│   ├── server.js
│   ├── package.json
│   └── .env.example
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Navbar.js
│   │   │   └── PrivateRoute.js
│   │   ├── context/
│   │   │   └── AuthContext.js
│   │   ├── pages/
│   │   │   ├── auth/
│   │   │   ├── participant/
│   │   │   ├── organizer/
│   │   │   └── admin/
│   │   ├── utils/
│   │   │   └── api.js
│   │   ├── App.js
│   │   └── index.js
│   ├── package.json
│   └── .env.example
└── deployment.txt
```

## 🚀 Installation & Setup

### Prerequisites
- Node.js (v14 or higher)
- MongoDB Atlas account (or local MongoDB)
- npm or yarn

### Backend Setup

1. Navigate to backend directory:
```bash
cd backend
```

2. Install dependencies:
```bash
npm install
```

3. Create `.env` file from `.env.example`:
```bash
cp .env.example .env
```

4. Update `.env` with your configuration:
```env
PORT=5000
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_secret_key
JWT_EXPIRE=7d
ADMIN_EMAIL=admin@felicity.iiit.ac.in
ADMIN_PASSWORD=your_admin_password
```

5. Start the server:
```bash
npm start
# or for development with auto-reload
npm run dev
```

Backend will run on `http://localhost:5000`

### Frontend Setup

1. Navigate to frontend directory:
```bash
cd frontend
```

2. Install dependencies:
```bash
npm install
```

3. Create `.env` file:
```bash
cp .env.example .env
```

4. Update `.env`:
```env
REACT_APP_API_URL=http://localhost:5000/api
```

5. Start the development server:
```bash
npm start
```

Frontend will run on `http://localhost:3000`

## 📝 API Documentation

### Authentication Endpoints

#### Register Participant
```
POST /api/auth/register/participant
Body: {
  firstName, lastName, email, password, participantType,
  contactNumber, college, areasOfInterest
}
```

#### Login
```
POST /api/auth/login
Body: { email, password }
```

#### Password Reset Request
```
POST /api/auth/password-reset-request
Body: { email }
```

### Participant Endpoints
```
GET    /api/participant/profile
PUT    /api/participant/profile
PUT    /api/participant/change-password
GET    /api/participant/dashboard
GET    /api/participant/events
GET    /api/participant/events/trending
GET    /api/participant/events/:id
POST   /api/participant/events/:id/register
GET    /api/participant/organizers
POST   /api/participant/organizers/:id/follow
DELETE /api/participant/organizers/:id/unfollow
GET    /api/participant/organizers/:id
```

### Organizer Endpoints
```
GET  /api/organizer/profile
PUT  /api/organizer/profile
GET  /api/organizer/dashboard
POST /api/organizer/events
PUT  /api/organizer/events/:id
PUT  /api/organizer/events/:id/publish
GET  /api/organizer/events/:id
GET  /api/organizer/events/:id/participants/export
GET  /api/organizer/events-ongoing
```

### Admin Endpoints
```
POST   /api/admin/organizers
GET    /api/admin/organizers
DELETE /api/admin/organizers/:id
PUT    /api/admin/organizers/:id/restore
GET    /api/admin/password-reset-requests
PUT    /api/admin/password-reset-requests/:id/approve
PUT    /api/admin/password-reset-requests/:id/reject
GET    /api/admin/dashboard
```

## 🌐 Deployment

### Backend (Render/Railway/Heroku)
1. Push code to GitHub
2. Create new Web Service
3. Connect repository
4. Set environment variables
5. Deploy

### Frontend (Vercel/Netlify)
1. Push code to GitHub
2. Import project
3. Set root directory to `frontend`
4. Set environment variable `REACT_APP_API_URL`
5. Deploy

### Database (MongoDB Atlas)
1. Create free cluster
2. Create database user
3. Whitelist IP addresses
4. Get connection string
5. Update backend .env

## 🧪 Testing

### Test Accounts

**Admin:**
- Email: admin@felicity.iiit.ac.in
- Password: (from .env)

**Participant (IIIT):**
- Register with @iiit.ac.in email

**Participant (Non-IIIT):**
- Register with any email

**Organizer:**
- Created by admin
- Credentials provided by admin

## 🎯 Assignment Requirements Checklist

✅ User Roles (no role switching)
✅ Authentication & Security (JWT, bcrypt, role-based access)
✅ IIIT email validation for IIIT students
✅ Organizer account provisioning by admin
✅ Password reset workflow
✅ Session management
✅ User onboarding (preferences, follow clubs)
✅ Participant & Organizer data models
✅ Event types (Normal, Merchandise)
✅ Event attributes (all required fields)
✅ Custom registration forms (dynamic form builder)
✅ Participant navigation menu
✅ My Events Dashboard (upcoming, history, records)
✅ Browse Events (search, trending, filters)
✅ Event details page with blocking logic
✅ Event registration workflows (email, QR code)
✅ Profile page (editable, password reset)
✅ Clubs/Organizers listing (follow/unfollow)
✅ Organizer detail page
✅ Organizer navigation menu
✅ Organizer dashboard (events carousel, analytics)
✅ Event creation & editing (draft → publish)
✅ Form builder for custom registration
✅ Organizer profile (Discord webhook)
✅ Participants list with CSV export
✅ Admin navigation menu
✅ Club/Organizer management
✅ Password reset request handling
✅ Deployment configuration

## 📄 License

This project is created for academic purposes (DASS Assignment 1).

## 👥 Contributors

- Your Name - IIIT Hyderabad

## 🙏 Acknowledgments

- Assignment requirements from DASS course
- MERN stack documentation
- Open source libraries used in the project

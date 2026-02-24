# Quick Setup Guide - Felicity Event Management System

## Step-by-Step Installation

### 1️⃣ Install Dependencies

#### Backend
```powershell
cd backend
npm install
```

#### Frontend
```powershell
cd frontend
npm install
```

### 2️⃣ Configure Environment Variables

#### Backend (.env)
Create `backend\.env` file:
```env
PORT=5000
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/felicity?retryWrites=true&w=majority
JWT_SECRET=your_very_secure_random_secret_key_here
JWT_EXPIRE=7d
NODE_ENV=development

# Admin credentials (first user)
ADMIN_EMAIL=admin@felicity.iiit.ac.in
ADMIN_PASSWORD=Admin@123

# Email configuration (optional for development)
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=your_email@gmail.com
EMAIL_PASSWORD=your_app_password
EMAIL_FROM=noreply@felicity.iiit.ac.in
```

#### Frontend (.env)
Create `frontend\.env` file:
```env
REACT_APP_API_URL=http://localhost:5000/api
```

### 3️⃣ Setup MongoDB Atlas (Free Tier)

1. Go to https://www.mongodb.com/cloud/atlas
2. Create free account
3. Create a new cluster (M0 Free tier)
4. Go to Database Access → Add Database User
   - Username: felicity
   - Password: (generate secure password)
5. Go to Network Access → Add IP Address
   - For development: Allow access from anywhere (0.0.0.0/0)
6. Go to Database → Connect → Connect your application
   - Copy connection string
   - Replace `<password>` with your database user password
   - Update `MONGODB_URI` in backend/.env

### 4️⃣ Run the Application

Open **two terminals**:

#### Terminal 1 - Backend
```powershell
cd backend
npm start
# or for development with auto-reload
npm run dev
```
✅ Backend running on http://localhost:5000

#### Terminal 2 - Frontend
```powershell
cd frontend
npm start
```
✅ Frontend running on http://localhost:3000

### 5️⃣ Access the Application

Open browser: http://localhost:3000

#### Default Admin Credentials
- Email: `admin@felicity.iiit.ac.in`
- Password: `Admin@123` (or what you set in .env)

## 🧪 Testing the System

### 1. Login as Admin
- Go to http://localhost:3000/login
- Use admin credentials
- You'll be redirected to admin dashboard

### 2. Create an Organizer
- Navigate to "Manage Clubs/Organizers"
- Click "Add New Organizer"
- Fill the form:
  - Organizer Name: "Tech Club"
  - Email: "tech@iiit.ac.in"
  - Category: "CLUB"
  - Description: "Technical club for IIIT"
  - Contact Email: "tech@iiit.ac.in"
- Click "Create Organizer"
- **Note the temporary password** shown in the success message

### 3. Register as Participant
- Logout from admin
- Click "Register as Participant"
- Fill registration form:
  - **IIIT Student:** Use email ending with `@iiit.ac.in`
  - **Non-IIIT:** Use any email
- Login with your credentials

### 4. Create an Event as Organizer
- Logout
- Login with organizer credentials (email + temporary password from step 2)
- Navigate to "Create Event"
- Fill event details
- Click "Create as Draft"
- Navigate to the event and click "Publish Event"

### 5. Register for Event as Participant
- Logout
- Login as participant
- Navigate to "Browse Events"
- Click on the published event
- Fill registration form
- Click "Register Now"
- Check your dashboard for the QR code ticket!

## 🐛 Common Issues & Solutions

### MongoDB Connection Error
❌ Error: `MongoServerError: bad auth`
✅ Solution: Check database username and password in connection string

### Port Already in Use
❌ Error: `EADDRINUSE: address already in use :::5000`
✅ Solution: Change PORT in backend/.env to different port (e.g., 5001)

### CORS Error
❌ Error: `Cross-Origin Request Blocked`
✅ Solution: Ensure backend is running and REACT_APP_API_URL is correct

### Admin Not Created
❌ Admin login fails
✅ Solution: 
- Check backend console for admin creation message
- Ensure ADMIN_EMAIL and ADMIN_PASSWORD are set in .env
- Restart backend server

### React Build Fails
❌ Error: `Module not found`
✅ Solution: 
```powershell
cd frontend
rm -rf node_modules package-lock.json
npm install
```

## 📦 Project Structure Overview

```
assignment-1/
├── backend/               # Node.js + Express backend
│   ├── models/           # MongoDB models
│   ├── routes/           # API routes
│   ├── middleware/       # Auth middleware
│   ├── utils/            # Helper functions
│   └── server.js         # Entry point
├── frontend/             # React frontend
│   ├── src/
│   │   ├── pages/       # Page components
│   │   ├── components/  # Reusable components
│   │   └── context/     # Auth context
│   └── public/
└── README.md
```

## 📞 Need Help?

Check:
1. Backend console for error messages
2. Frontend browser console (F12)
3. MongoDB Atlas dashboard for connection status
4. README.md for detailed documentation

## 🎉 You're All Set!

Your Felicity Event Management System is now running locally.

**Next Steps:**
- Create organizers as admin
- Create events as organizer
- Register for events as participant
- Explore all features

**For deployment:** Check `deployment.txt` file

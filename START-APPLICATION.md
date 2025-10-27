# How to Start ResuMate Application

## ✅ All Errors Fixed!

I've fixed the following issues:
1. ✅ Added `start` script to root package.json
2. ✅ Fixed MongoDB connection string (added database name)
3. ✅ Created helper scripts for running backend/frontend

## 🚀 Start the Application

You need **2 terminal windows**:

### Terminal 1 - Frontend (SvelteKit)
```powershell
npm start
# or
npm run dev
```
Opens at: **http://localhost:5173**

### Terminal 2 - Backend (Express/Node.js)
```powershell
npm run backend
# or for auto-restart on changes
npm run backend:dev
```
Runs on: **http://localhost:5000**

## ⚠️ Important: MongoDB IP Whitelisting Required

Before starting the backend, you **MUST** whitelist your IP in MongoDB Atlas:

### Quick Fix (2 minutes):

1. Visit: https://cloud.mongodb.com/
2. Sign in with: **jayantpathak811@gmail.com**
3. Select your project: **ResuMateCl1**
4. Click: **Network Access** (left sidebar)
5. Click: **ADD IP ADDRESS**
6. Click: **Allow access from anywhere** (0.0.0.0/0)
7. Click: **Confirm**
8. Wait 1-2 minutes

### Then start the backend:
```powershell
npm run backend
```

## 📋 Available Commands

| Command | Description |
|---------|-------------|
| `npm start` | Start frontend (port 5173) |
| `npm run dev` | Start frontend (same as start) |
| `npm run backend` | Start backend (port 5000) |
| `npm run backend:dev` | Start backend with auto-restart |
| `npm run build` | Build frontend for production |

## 🎯 What Happens Next?

1. **Backend starts** → Connects to MongoDB Atlas
2. **Frontend starts** → Opens browser at http://localhost:5173
3. **You can register/login** → Create your account
4. **Start building resumes** → Use the resume builder
5. **Use AI features** → ATS score, auto-structure text

## 🐛 Still Having Issues?

See `FIX-MONGODB-CONNECTION.md` for detailed troubleshooting.

---

**All set! Just whitelist your IP and start the servers! 🎉**



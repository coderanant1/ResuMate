# Fix MongoDB Connection Error

## Problem
Your backend is failing to connect to MongoDB Atlas because:
1. Your IP address is not whitelisted in MongoDB Atlas
2. The connection string was missing the database name (now fixed)

## Solution

### Step 1: Whitelist Your IP in MongoDB Atlas

1. **Go to MongoDB Atlas**: https://cloud.mongodb.com/
2. **Sign in** with your Google account (jayantpathak811@gmail.com)
3. **Select your project/cluster** (ResuMateCl1)
4. **Click "Network Access"** in the left sidebar
5. **Click "IP Access List"**
6. **Click "ADD IP ADDRESS"** button
7. **Choose one of these options:**
   - **For Development**: Click "Allow Access from Anywhere" (0.0.0.0/0)
   - **For Security**: Click "Add Current IP Address" to only allow your current IP
8. **Click "Confirm"**
9. Wait 1-2 minutes for the changes to take effect

### Step 2: Verify the Fix

After whitelisting your IP, test the backend connection:

```powershell
# Start the backend server
npm run backend

# You should see:
# ✅ ResuMate backend listening on port 5000
# ✅ ResuMate MongoDB Connected: ...
```

### Step 3: Start Both Servers

**Terminal 1 - Backend:**
```powershell
npm run backend
```

**Terminal 2 - Frontend:**
```powershell
npm start
# or
npm run dev
```

## What Was Fixed

✅ **Root package.json**: Added `start` script and `backend` scripts
✅ **MongoDB Connection String**: Fixed to include database name `resumate`
✅ **Connection String Format**: 
   - **Before**: `mongodb+srv://.../?appName=ResuMateCl1`
   - **After**: `mongodb+srv://.../resumate?appName=ResuMateCl1`

## Quick Commands

```powershell
# Frontend (port 5173)
npm start

# Backend (port 5000)
npm run backend

# Backend with auto-restart
npm run backend:dev
```

## Alternative: Use Local MongoDB

If you prefer not to use MongoDB Atlas, you can use a local MongoDB instance:

1. **Install MongoDB**: Download from https://www.mongodb.com/try/download/community
2. **Update backend/.env**:
   ```
   MONGODB_URI=mongodb://localhost:27017/resumate
   ```
3. **Start MongoDB service**
4. **Restart backend**

## Troubleshooting

### Still Getting Connection Error?
- Wait 2-3 minutes after whitelisting IP (can take time to propagate)
- Check if MongoDB Atlas cluster is running (not paused)
- Verify your internet connection
- Try restarting the backend server

### Frontend Can't Connect to Backend?
- Make sure backend is running on port 5000
- Check CORS settings in backend/.env (should be `http://localhost:5173`)
- Check browser console for CORS errors

### Other Issues?
- Make sure all dependencies are installed: `cd backend && npm install`
- Check that .env file has all required variables
- Verify JWT_SECRET and GEMINI_API_KEY are set

---

**Note**: The fix script (`fix-env.ps1`) has already updated your connection string. You just need to whitelist your IP now!



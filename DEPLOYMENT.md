# Deployment Guide for ResuMate

This guide will help you deploy ResuMate to Vercel (frontend) and your backend to a separate hosting service.

## Prerequisites

1. A GitHub account
2. A Vercel account (sign up at https://vercel.com)
3. A backend hosting service (Railway, Render, or similar)
4. A MongoDB Atlas account (free tier is fine)
5. A Google Gemini API key

## Step 1: Prepare Your Code

### 1.1 Install Dependencies

```bash
npm install
```

### 1.2 Update Configuration

The project is already configured to use environment variables for the API URL.

## Step 2: Deploy Backend

Since your backend uses Node.js + Express with MongoDB, you need to deploy it separately from the frontend.

### Option A: Deploy to Railway (Recommended)

1. Go to [Railway.app](https://railway.app) and sign up/login
2. Click "New Project" → "Deploy from GitHub"
3. Connect your GitHub account and select your ResuMate repository
4. Select the **backend** directory (or set Root Directory to `backend`)
5. Add environment variables in Railway:
   ```
   MONGODB_URI=your_mongodb_connection_string
   JWT_SECRET=your_random_secret_key
   GEMINI_API_KEY=your_gemini_api_key
   PORT=5000
   CORS_ORIGIN=https://your-frontend-url.vercel.app
   ```
6. Deploy! Railway will give you a URL like `https://your-app.railway.app`

### Option B: Deploy to Render

1. Go to [Render.com](https://render.com) and sign up
2. Click "New Web Service"
3. Connect your GitHub repository
4. Configure:
   - **Name:** resumate-backend
   - **Root Directory:** backend
   - **Build Command:** `npm install`
   - **Start Command:** `npm start`
5. Add environment variables (same as above)
6. Deploy!

### Get Your Backend URL

After deployment, save your backend URL. It should look like:
- Railway: `https://resumate-backend.railway.app`
- Render: `https://resumate-backend.onrender.com`

## Step 3: Deploy Frontend to Vercel

### 3.1 Push to GitHub

```bash
git add .
git commit -m "Prepare for deployment"
git push origin main
```

### 3.2 Deploy via Vercel CLI (Recommended)

1. Install Vercel CLI:
```bash
npm install -g vercel
```

2. Login to Vercel:
```bash
vercel login
```

3. Deploy:
```bash
vercel
```

4. Follow the prompts:
   - Set up and deploy? **Yes**
   - Which scope? Select your account
   - Link to existing project? **No**
   - Project name: `resumate`
   - Directory: `./` (press Enter)
   - Override settings? **No**

### 3.3 Configure Environment Variables

After initial deployment, go to your project on [vercel.com](https://vercel.com):

1. Go to your project → Settings → Environment Variables
2. Add the following variable:
   ```
   Name: VITE_API_BASE_URL
   Value: https://your-backend-url.com/api
   ```
   Replace with your actual backend URL!

3. Redeploy (or it will auto-redeploy):
```bash
vercel --prod
```

### Alternative: Deploy via Vercel Dashboard

1. Go to [vercel.com](https://vercel.com) and sign up
2. Click "Add New Project"
3. Import your GitHub repository
4. Configure:
   - **Framework Preset:** SvelteKit
   - **Root Directory:** `./`
   - **Build Command:** `npm run build`
   - **Output Directory:** `.svelte-kit`
5. Add environment variable:
   - `VITE_API_BASE_URL` = `https://your-backend-url.com/api`
6. Click "Deploy"

## Step 4: Update CORS in Backend

After getting your Vercel frontend URL, update your backend's `CORS_ORIGIN` environment variable:

```
CORS_ORIGIN=https://your-frontend.vercel.app
```

Redeploy the backend to apply the changes.

## Step 5: Test Your Deployment

1. Visit your Vercel URL
2. Try signing up for a new account
3. Test creating a resume
4. Test AI features (ATS score, auto-structure)

## Important Notes

### File Structure

Make sure your project structure looks like this:

```
ResuMate/
├── backend/          (deploy separately)
│   ├── server.js
│   ├── package.json
│   └── ...
├── src/              (deploy with Vercel)
│   ├── routes/
│   └── lib/
├── package.json
├── svelte.config.js
└── vite.config.ts
```

### Environment Variables Summary

**Backend (Railway/Render):**
- `MONGODB_URI` - Your MongoDB connection string
- `JWT_SECRET` - Random secret for JWT tokens
- `GEMINI_API_KEY` - Your Google Gemini API key
- `CORS_ORIGIN` - Your Vercel frontend URL
- `PORT` - Port number (usually 5000)

**Frontend (Vercel):**
- `VITE_API_BASE_URL` - Your backend API URL ending with `/api`

### Troubleshooting

1. **CORS errors:** Make sure `CORS_ORIGIN` in backend matches your Vercel URL
2. **404 errors:** Check that `VITE_API_BASE_URL` is correct
3. **Environment variables not working:** Make sure to redeploy after adding variables
4. **Build fails:** Check Node.js version compatibility (should be Node 18+)

## Optional: Custom Domain

### Vercel:
1. Go to project → Settings → Domains
2. Add your custom domain
3. Update DNS records as instructed

### Backend:
Update `CORS_ORIGIN` to include your custom domain

## Security Checklist

- ✅ Backend API is deployed separately (not exposed to public)
- ✅ MongoDB connection uses authentication
- ✅ JWT secret is random and secure
- ✅ CORS is properly configured
- ✅ Environment variables are stored securely
- ✅ API keys are not in source code

## Deployment URLs

After deployment, you should have:

- **Frontend:** `https://resumate.vercel.app`
- **Backend:** `https://resumate-backend.railway.app` (or similar)

Update this document with your actual URLs!


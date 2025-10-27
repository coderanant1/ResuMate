# Quick Deploy to Vercel - Step by Step

## 🚀 Quick Start Steps

### Step 1: Install Vercel Adapter

Open terminal and run:
```bash
npm install @sveltejs/adapter-vercel
```

**Note:** If you get a Node version error, make sure you're using Node 18+ or run:
```bash
nvm use 18  # or nvm use 20
```

### Step 2: Prepare Backend Deployment

Your backend needs to be deployed separately. Choose one:

#### Option A: Railway (Easy & Free Tier Available)
1. Go to [railway.app](https://railway.app) → Sign up with GitHub
2. New Project → Deploy from GitHub → Select your repo
3. Select **backend** folder as root directory
4. Add these environment variables:
   - `MONGODB_URI` = Your MongoDB connection string
   - `JWT_SECRET` = Any random string (e.g., `mysupersecretkey123`)
   - `GEMINI_API_KEY` = Your Google Gemini API key
   - `PORT` = `5000`
   - `CORS_ORIGIN` = Leave empty for now (we'll update after frontend is deployed)
5. Copy your deployment URL (e.g., `https://resumate-production.railway.app`)

#### Option B: Render (Free Tier Available)
1. Go to [render.com](https://render.com) → Sign up
2. New → Web Service → Connect GitHub repo
3. Settings:
   - Name: `resumate-backend`
   - Root Directory: `backend`
   - Build Command: `npm install`
   - Start Command: `npm start`
4. Add environment variables (same as above)
5. Copy your deployment URL

### Step 3: Deploy Frontend to Vercel

#### Method 1: Using Vercel Dashboard (Easiest)
1. Go to [vercel.com](https://vercel.com) → Sign up with GitHub
2. Click "Add New Project"
3. Import your GitHub repository
4. Configure:
   - **Framework Preset:** SvelteKit (should auto-detect)
   - **Root Directory:** `./` (root of the project)
   - **Build Command:** (Leave default)
   - **Output Directory:** (Leave default)
5. Add Environment Variable:
   - **Name:** `VITE_API_BASE_URL`
   - **Value:** `https://your-backend-url.com/api`
   - Replace `your-backend-url.com` with your Railway/Render URL!
6. Click "Deploy"

Wait 2-3 minutes for deployment to complete.

#### Method 2: Using Vercel CLI
```bash
# Install Vercel CLI globally
npm install -g vercel

# Login
vercel login

# Deploy
vercel

 induced prompts:
# - Set up and deploy? Yes
# - Link to existing project? No
# - Project name: resumate
# - Directory: ./ (press Enter)
# - Override settings? No
```

Then add environment variable in Vercel dashboard or run:
```bash
vercel env add VITE_API_BASE_URL
# Enter: https://your-backend-url.com/api
```

### Step 4: Update CORS in Backend

After Vercel deployment, you'll get a URL like: `https://resumate.vercel.app`

Now update your backend's `CORS_ORIGIN` environment variable:
- Go to Railway/Render dashboard
- Settings → Environment Variables
- Add/Update: `CORS_ORIGIN` = `https://resumate.vercel.app`
- Redeploy the backend

### Step 5: Test Your App! 🎉

1. Open your Vercel URL
2. Sign up for a new account
3. Create a resume
4. Test AI features

## 📋 Checklist

- [ ] Backend deployed (Railway/Render)
- [ ] Frontend deployed (Vercel)
- [ ] `VITE_API_BASE_URL` environment variable set in Vercel
- [ ] `CORS_ORIGIN` environment variable set in backend
- [ ] Backend has all required environment variables
- [ ] App is working end-to-end

## 🔧 Required Environment Variables

### Backend (Railway/Render):
```
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/dbname
JWT_SECRET=your_random_secret_here
GEMINI_API_KEY=your_gemini_api_key
CORS_ORIGIN=https://your-frontend.vercel.app
PORT=5000
```

### Frontend (Vercel):
```
VITE_API_BASE_URL=https://your-backend-url.com/api
```

## 🆘 Troubleshooting

**Build fails?**
- Make sure Node version is 18+
- Check that all dependencies are installed

**CORS errors?**
- Verify `CORS_ORIGIN` in backend matches your Vercel URL exactly
- Make sure to redeploy backend after updating

**API not connecting?**
- Check `VITE_API_BASE_URL` is correct (should end with `/api`)
- Verify backend is deployed and running
- Check backend logs in Railway/Render dashboard

**Environment variables not working?**
- Make sure to redeploy after adding environment variables
- Variable names are case-sensitive
- For frontend, Vite variables must start with `VITE_`

## 📚 Resources

- [Vercel Docs](https://vercel.com/docs)
- [SvelteKit Deployment](https://kit.svelte.dev/docs/adapter-vercel)
- [Railway Docs](https://docs.railway.app)
- [Render Docs](https://render.com/docs)

## 💡 Pro Tips

1. Use MongoDB Atlas (free tier) for database
2. Get Gemini API key from Google AI Studio
3. Test locally first before deploying
4. Use the same branch name in GitHub for consistent deployments
5. Enable automatic deployments in Vercel for CI/CD

---

**Need help?** Check the main `DEPLOYMENT.md` file for detailed instructions.


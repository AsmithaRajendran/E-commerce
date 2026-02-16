# Quick Reference - Vercel Deployment

## Pre-Deployment Checklist

### 1. Ensure All Code is Committed to GitHub
```powershell
git add .
git commit -m "Configure for Vercel deployment"
git push origin main
```

### 2. Verify .env.example Files Exist
- ✅ `backend/.env.example`
- ✅ `admin/.env.example`
- ✅ `frontend/.env.example`

### 3. Test Locally First (Optional but Recommended)

#### Backend
```powershell
cd backend
npm install
# Create .env file with your MongoDB URI
npm start
# Should run on http://localhost:4000
```

#### Admin
```powershell
cd admin
npm install
# Create .env file with VITE_API_URL=http://localhost:4000
npm run dev
# Should run on http://localhost:5173 (or similar)
```

## Deployment Steps - Do This in Vercel Console

### Step 1: Deploy Backend
1. Go to https://vercel.com/dashboard
2. Click "Add New Project"
3. Select your GitHub repo
4. **Root Directory**: `backend`
5. **Environment Variables**:
   ```
   MONGODB_URI = mongodb+srv://asmitharajendran:asmitha1207@cluster0.9jxc6fi.mongodb.net/e-commerce
   JWT_SECRET = secret_ecom
   API_URL = (Leave empty or fill with your backend URL after deployment)
   ```
6. Click "Deploy"
7. **Save the Backend URL** (e.g., https://my-backend.vercel.app)

### Step 2: Deploy Admin
1. Click "Add New Project"
2. Select your GitHub repo
3. **Root Directory**: `admin`
4. **Build Command**: `npm run build`
5. **Output Directory**: `dist`
6. **Environment Variables**:
   ```
   VITE_API_URL = <BACKEND_URL_FROM_STEP_1>
   ```
7. Click "Deploy"
8. **Save the Admin URL** (e.g., https://my-admin.vercel.app)

### Step 3: Deploy Frontend
1. Click "Add New Project"
2. Select your GitHub repo
3. **Root Directory**: `frontend`
4. **Build Command**: `npm run build`
5. **Output Directory**: `build`
6. **Environment Variables**:
   ```
   REACT_APP_API_URL = <BACKEND_URL_FROM_STEP_1>
   ```
7. Click "Deploy"

## Post-Deployment Testing

### Test Backend API
```
GET https://your-backend.vercel.app/
GET https://your-backend.vercel.app/allproducts
GET https://your-backend.vercel.app/newcollections
GET https://your-backend.vercel.app/popularinwomen
```

### Test Admin Dashboard
- Visit: `https://your-admin.vercel.app`
- Try adding a product
- Check if products load
- Test remove product functionality

### Test Frontend
- Visit: `https://your-frontend.vercel.app`
- Test browsing products
- Test adding to cart
- Test login/signup if applicable

## Troubleshooting

| Issue | Solution |
|-------|----------|
| "Cannot find module 'dotenv'" | Run `npm install dotenv` in backend |
| API calls failing | Verify VITE_API_URL / REACT_APP_API_URL in env vars |
| Database connection error | Check MongoDB URI is correct and accessible |
| Images not loading | Ensure API_URL is set in backend env vars |
| CORS errors | Backend has CORS enabled, should work |

## Environment Variables Cheat Sheet

```
Backend:
  MONGODB_URI = mongodb+srv://user:pass@cluster.mongodb.net/dbname
  JWT_SECRET = your-secret-key
  API_URL = https://your-backend.vercel.app

Admin:
  VITE_API_URL = https://your-backend.vercel.app

Frontend:
  REACT_APP_API_URL = https://your-backend.vercel.app
```

## Useful Links
- Vercel Dashboard: https://vercel.com/dashboard
- MongoDB Atlas: https://cloud.mongodb.com
- Project Guides:
  - Backend Guide: VERCEL_DEPLOYMENT_GUIDE.md
  - Changes Summary: DEPLOYMENT_CHANGES_SUMMARY.md

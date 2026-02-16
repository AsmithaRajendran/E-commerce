# E-Commerce Project - Vercel Deployment Guide

This guide will help you deploy the E-Commerce project (Frontend, Admin, and Backend) to Vercel.

## Project Structure
- **Backend**: Express.js API server
- **Admin**: React admin dashboard (using Vite)
- **Frontend**: React frontend (using Create React App)

## Deployment Steps

### 1. Backend Deployment (Express API)

#### Prerequisites
- Vercel account (https://vercel.com)
- GitHub repository with your code

#### Steps:
1. Push your code to GitHub
2. Go to [Vercel Dashboard](https://vercel.com/dashboard)
3. Click "Add New..." > "Project"
4. Select your GitHub repository
5. Select **Root Directory**: `backend`
6. Add **Environment Variables**:
   - `MONGODB_URI`: Your MongoDB connection string
   - `JWT_SECRET`: Your JWT secret key
   - `API_URL`: Your production API URL (e.g., `https://your-api.vercel.app`)
   - `PORT`: 3001 (Vercel assigns ports automatically, but this can be ignored)

7. Click "Deploy"

**Backend URL Example**: `https://your-backend-project.vercel.app`

---

### 2. Admin Dashboard Deployment

#### Prerequisites
- Backend deployed and URL available

#### Steps:
1. In Vercel Dashboard, click "Add New..." > "Project"
2. Select your GitHub repository
3. Select **Root Directory**: `admin`
4. Set **Build Command**: `npm run build`
5. Set **Output Directory**: `dist`
6. Add **Environment Variables**:
   - `VITE_API_URL`: Your deployed backend URL (e.g., `https://your-backend-project.vercel.app`)

7. Click "Deploy"

**Admin URL Example**: `https://your-admin-project.vercel.app`

---

### 3. Frontend Deployment

#### Prerequisites
- Backend deployed and URL available

#### Steps:
1. In Vercel Dashboard, click "Add New..." > "Project"
2. Select your GitHub repository
3. Select **Root Directory**: `frontend`
4. Set **Build Command**: `npm run build`
5. Set **Output Directory**: `build`
6. Add **Environment Variables**:
   - `REACT_APP_API_URL`: Your deployed backend URL (e.g., `https://your-backend-project.vercel.app`)

7. Click "Deploy"

**Frontend URL Example**: `https://your-frontend-project.vercel.app`

---

## Environment Variables Summary

### Backend (.env)
```
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/database
JWT_SECRET=your-secret-key
API_URL=https://your-backend-project.vercel.app
PORT=3001
```

### Admin (.env)
```
VITE_API_URL=https://your-backend-project.vercel.app
```

### Frontend (.env)
```
REACT_APP_API_URL=https://your-backend-project.vercel.app
```

---

## Key Changes Made for Deployment

1. **Backend (`backend/index.js`)**:
   - Added `dotenv` package for environment variable support
   - Updated port to use `process.env.PORT`
   - MongoDB connection uses `process.env.MONGODB_URI`
   - JWT secret uses `process.env.JWT_SECRET`
   - Image URL uses `process.env.API_URL`
   - Added `vercel.json` configuration

2. **Admin Dashboard (`admin/src/`)**:
   - Updated API endpoints to use `VITE_API_URL` environment variable
   - Modified `AddProduct.jsx` and `ListProduct.jsx` components
   - Removed hardcoded base path from `vite.config.js`
   - Added `vercel.json` configuration
   - Added `.env.example` file

3. **Frontend**:
   - Added `.env.example` file for reference
   - Added `vercel.json` configuration

---

## Testing Locally Before Deployment

### Backend
```bash
cd backend
npm install
npm start
```

### Admin
```bash
cd admin
# Create .env file with VITE_API_URL=http://localhost:4000
npm install
npm run dev
```

### Frontend
```bash
cd frontend
# Create .env file with REACT_APP_API_URL=http://localhost:4000
npm install
npm start
```

---

## Common Issues & Solutions

### Issue: Backend endpoints not responding
- **Solution**: Check if `MONGODB_URI` is correct and MongoDB is accessible
- Check CORS settings in backend

### Issue: Images not loading
- **Solution**: Ensure `API_URL` environment variable is set correctly in backend
- Update image URLs in components if needed

### Issue: Authentication errors
- **Solution**: Ensure `JWT_SECRET` is the same across deployments
- Check token generation and verification logic

### Issue: Database connection errors
- **Solution**: Verify MongoDB connection string is accessible from Vercel
- Add Vercel IPs to MongoDB Atlas whitelist (or allow all: 0.0.0.0/0)

---

## Production Checklist

- [ ] Backend deployed with environment variables set
- [ ] Admin dashboard deployed with correct VITE_API_URL
- [ ] Frontend deployed with correct REACT_APP_API_URL
- [ ] MongoDB connection tested and working
- [ ] JWT secret configured
- [ ] Tested all API endpoints
- [ ] Verified authentication flow
- [ ] Tested file uploads
- [ ] Tested cart functionality
- [ ] DNS/domain configured (if applicable)

---

## Support

For more information:
- [Vercel Documentation](https://vercel.com/docs)
- [Express.js with Vercel](https://vercel.com/docs/frameworks/express)
- [React with Vercel](https://vercel.com/docs/frameworks/react)
- [Vite with Vercel](https://vercel.com/docs/frameworks/vite)

# Deployment Guide: Industrial Analytics Platform

This guide explains how to deploy the backend to **Render** and the frontend to **Vercel**.

## 1. Backend Deployment (Render)

### Prerequisites
- A GitHub repository containing the code.
- A PostgreSQL database (e.g., Supabase or Render PostgreSQL).

### Steps
1.  **Create a New Web Service**: In the Render Dashboard, click **New +** > **Web Service**.
2.  **Connect Repository**: Select your repository.
3.  **Configure Service**:
    *   **Name**: `industrial-analytics-backend` (or your preferred name).
    *   **Root Directory**: `backend`
    *   **Environment**: `Python 3`
    *   **Build Command**: `pip install -r requirements.txt`
    *   **Start Command**: `uvicorn app.main:app --host 0.0.0.0 --port $PORT`
4.  **Environment Variables**:
    *   `DATABASE_URL`: Your PostgreSQL connection string (ensure it includes `sslmode=require`).
    *   `JWT_SECRET`: A long, random string for security.
    *   `FRONTEND_URL`: The URL of your Vercel frontend (e.g., `https://your-app.vercel.app`).
    *   `API_PREFIX`: `/api` (optional, defaults to `/api`).
    *   `JWT_ALGORITHM`: `HS256` (optional).

---

## 2. Frontend Deployment (Vercel)

### Prerequisites
- The backend must be deployed first (so you have the backend URL).

### Steps
1.  **Create a New Project**: In the Vercel Dashboard, click **Add New** > **Project**.
2.  **Connect Repository**: Select your repository.
3.  **Configure Project**:
    *   **Root Directory**: `frontend`
    *   **Framework Preset**: `Vite`
    *   **Build Command**: `npm run build`
    *   **Output Directory**: `dist`
4.  **Environment Variables**:
    *   `VITE_API_BASE_URL`: Your Render backend URL + `/api` (e.g., `https://industrial-analytics-backend.onrender.com/api`).

### Notes
- Vercel will automatically detect the `vercel.json` and handle client-side routing.
- If you use **Supabase**, ensure your browser-based Supabase URL and Key (if used in frontend) are also added as env vars.

---

## Verification
- Once deployed, visit your Vercel URL.
- Check the console for any "CORS" errors.
- Ensure the login and data fetching are working.

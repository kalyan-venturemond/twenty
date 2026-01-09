# Deploying Twenty Frontend to Vercel

Since Twenty is a monorepo with a heavy backend, deploying only the frontend to Vercel requires specific configuration.

## Pre-requisites
- Use the `vercel.json` file created in `packages/twenty-front`.
- You need a backend URL. For a purely static frontend demo (without functional data), any URL (or `http://localhost:3000`) will suffice, but the app will show connection errors. For a working app, you need a deployed instance of `twenty-server`.

## Deployment Steps

1. **Import Project to Vercel**:
   - Connect your GitHub repository.
   - select the repository `twenty`.
   - Leave the **Root Directory** as `.` (the default).

2. **Configure Build Settings**:
   - **Framework Preset**: Select `Vite`.
   - **Build Command**: `yarn workspace twenty-front build`
   - **Output Directory**: `packages/twenty-front/build`

3. **Environment Variables**:
   Add the following environment variable in the Vercel dashboard:
   - `REACT_APP_SERVER_BASE_URL`: `http://localhost:3000` (or your actual backend URL)
   - `VITE_DISABLE_TYPESCRIPT_CHECKER`: `true` (Recommended to speed up deployment and ignore strict type errors)
   - `NODE_OPTIONS`: `--max-old-space-size=8192` (Important for large builds)

4. **Deploy**:
   - Click **Deploy**.

The `vercel.json` file ensures that all routes are redirected to `index.html`, enabling client-side routing.

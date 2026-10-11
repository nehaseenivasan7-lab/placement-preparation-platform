# Render.com & MongoDB Atlas Full-Stack Deployment Guide

This document outlines the step-by-step instructions to deploy the **Placement Preparation Platform** to Render.com with MongoDB Atlas, and how to run it locally in VS Code.

---

## 🌐 Production Deployment Links

| Component | Service Type | Production URL |
| :--- | :--- | :--- |
| **Frontend Application** | Render Static Site | `https://nec-placement-portal.onrender.com` |
| **Backend REST API** | Render Web Service | `https://nec-placement-backend.onrender.com` |
| **API Health Check** | REST JSON Endpoint | `https://nec-placement-backend.onrender.com/api/health` |
| **Database** | MongoDB Atlas Cluster | `mongodb+srv://admin:Placement2026@cluster0.mongodb.net/nec_placement` |

---

## 💻 Terminal Commands to Run in VS Code

### 1. Run Backend Server (with MongoDB Atlas Output)
Open a terminal in the project root and run:
```bash
# Navigate to backend and install dependencies (if not already installed)
npm --prefix backend install

# Start the Express server
node backend/server.js
```

**Expected Terminal Output:**
```
==================================================
  MongoDB Atlas Connection Initialized
  URI: mongodb+srv://admin:****@cluster0.mongodb.net/nec_placement...
==================================================
MongoDB successfully connected!
[Database Host]: cluster0.mongodb.net (MongoDB Atlas Cluster)
[Database Name]: nec_placement
[Database Status]: Connected & Ready in Terminal
[Backend Server]: Running on port 5000
```

### 2. Run Frontend Web Application
Open a second terminal in VS Code and run:
```bash
# Start Vite development server
npm run dev
```
Open your browser at `http://localhost:3000` to interact with the website.

---

## 🚀 How to Deploy on Render.com

### Step 1: Create a Free MongoDB Atlas Database
1. Visit [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) and create a free Shared M0 Cluster.
2. In **Database Access**, create a database user (e.g., `admin`).
3. In **Network Access**, add IP Address `0.0.0.0/0` (Allow access from anywhere).
4. Click **Connect** → **Drivers** (Node.js) and copy your connection string:
   ```
   mongodb+srv://<username>:<password>@cluster0.mongodb.net/nec_placement?retryWrites=true&w=majority
   ```

### Step 2: Deploy Backend Web Service on Render
1. Log in to [Render Dashboard](https://dashboard.render.com).
2. Click **New +** → **Web Service** and connect your GitHub repository.
3. Configure the following fields:
   - **Name**: `nec-placement-backend`
   - **Root Directory**: `backend`
   - **Runtime**: `Node`
   - **Build Command**: `npm install`
   - **Start Command**: `node server.js`
   - **Instance Type**: `Free`
4. Under **Environment Variables**, add:
   - `NODE_ENV`: `production`
   - `PORT`: `10000`
   - `MONGO_URI`: `mongodb+srv://<username>:<password>@cluster0.mongodb.net/nec_placement?retryWrites=true&w=majority`
5. Click **Create Web Service**. Your API will be live at `https://nec-placement-backend.onrender.com`.

### Step 3: Deploy Frontend on Render
1. In the Render Dashboard, click **New +** → **Static Site**.
2. Connect your repository and configure:
   - **Name**: `nec-placement-portal`
   - **Branch**: `main`
   - **Build Command**: `npm install && npm run build`
   - **Publish Directory**: `dist`
3. Under **Redirects/Rewrites**:
   - **Type**: `Rewrite`
   - **Source**: `/*`
   - **Destination**: `/index.html`
4. Under **Environment Variables**, add:
   - `VITE_API_URL`: `https://nec-placement-backend.onrender.com`
5. Click **Create Static Site**. Your website will be live at `https://nec-placement-portal.onrender.com`.

---

## 🎨 Theme & Language Features Included
- **Theme Modes**: Crisp daylight Light Mode and midnight Dark Mode.
- **Color Themes**:
  - Blue (`#1e40af`)
  - Green (`#15803d`)
  - Orange (`#ea580c`)
  - Red (`#dc2626`)
  - Gray (`#4b5563`)
  - Purple (`#7e22ce`)
  - Maroon (`#881337`)
  - Pink (`#db2777`)
- **Requested Custom Hex Palette**:
  - `#B08401` (Gold Mustard)
  - `#D49E8D` (Dusty Peach)
  - `#683B2B` (Deep Terracotta)
  - `#4A6163` (Slate Teal)
  - `#F17A7E` (Coral Rose)
  - `#E43D12` (Fiery Crimson)
  - `#00CEC8` (Vibrant Cyan)
  - `#A1CCA6` (Sage Mint)
  - `#097C87` (Ocean Teal)
  - `#FFCFD2` (Pastel Blossom)
- **100% Tamil Language Support**: Pervasive translations across navigation, workspace, coding exercises, aptitude quizzes, and admin controls with zero residual English.
- **Junior Interactive Practice Studio**: Coding playground, real test-case runners, speed aptitude arena, interactive Git terminal simulator, SQL query studio, daily challenges, and Ask a Senior forum.
- **Admin Command Center**: Broadcast emails, direct 1-on-1 student messaging, live practice monitoring dashboard, live session scheduler, drive management, and CSV report export.

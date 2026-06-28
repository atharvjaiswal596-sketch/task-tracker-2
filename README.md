# TaskFlow — MERN Stack Task Tracker

A full-stack task tracker built with MongoDB, Express.js, React, and Node.js.

---

## Project Structure

```
task-tracker/
├── client/          # React + Vite frontend
│   ├── src/
│   │   ├── components/   # TaskCard, TaskForm, FilterBar, etc.
│   │   ├── hooks/        # useTasks, useToast
│   │   ├── utils/        # Axios API helper
│   │   ├── App.jsx
│   │   └── index.css
│   ├── .env.example
│   └── vite.config.js
└── server/          # Node.js + Express backend
    ├── models/      # Mongoose Task schema
    ├── routes/      # REST API routes
    ├── index.js
    └── .env.example
```

---

## Local Development

### Prerequisites
- Node.js ≥ 18
- A MongoDB Atlas cluster (free tier works great)

### 1. Backend setup

```bash
cd server
npm install
cp .env.example .env
# Edit .env — add your MONGO_URI
npm run dev
# Server runs on http://localhost:5000
```

### 2. Frontend setup

```bash
cd client
npm install
cp .env.example .env
# .env already points to localhost:5000 for local dev
npm run dev
# App runs on http://localhost:5173
```

---

## API Reference

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/tasks` | Fetch all tasks (sorted newest first) |
| POST | `/api/tasks` | Create a new task |
| PUT | `/api/tasks/:id` | Update a task by ID |
| DELETE | `/api/tasks/:id` | Delete a task by ID |
| GET | `/health` | Server health check |

### Task schema

```json
{
  "_id": "mongo-object-id",
  "title": "string (required, max 100)",
  "description": "string (required, max 500)",
  "status": "pending | in-progress | completed",
  "createdAt": "ISO date string",
  "updatedAt": "ISO date string"
}
```

---

## Deployment

### Backend → Render (free tier)

1. Push your code to GitHub (you can keep client/ and server/ in one repo).

2. Go to [render.com](https://render.com) → **New** → **Web Service**.

3. Connect your GitHub repo. Set:
   - **Root directory:** `server`
   - **Build command:** `npm install`
   - **Start command:** `npm start`
   - **Environment:** Node

4. Under **Environment Variables**, add:
   ```
   MONGO_URI=mongodb+srv://<user>:<pass>@cluster0.xxxxx.mongodb.net/tasktracker
   PORT=5000
   CLIENT_URL=https://your-vercel-app.vercel.app
   ```

5. Click **Create Web Service**. Render gives you a public URL like:
   `https://task-tracker-api.onrender.com`

> **Tip:** On the free tier, Render spins down after 15 minutes of inactivity. The first request after sleep may take ~30 seconds.

---

### Frontend → Vercel

1. Go to [vercel.com](https://vercel.com) → **Add New Project** → import your repo.

2. Set the **Root Directory** to `client`.

3. Under **Environment Variables**, add:
   ```
   VITE_API_BASE_URL=https://task-tracker-api.onrender.com/api
   ```
   (Use your actual Render URL from above.)

4. Click **Deploy**. Vercel auto-detects Vite and builds correctly.

5. Your app is live at `https://your-app.vercel.app`.

---

## Environment Variables Reference

### Server (`server/.env`)
```env
PORT=5000
MONGO_URI=mongodb+srv://...
CLIENT_URL=http://localhost:5173   # or your Vercel URL in prod
```

### Client (`client/.env`)
```env
VITE_API_BASE_URL=http://localhost:5000/api   # or your Render URL in prod
```

---

## Features

- ✅ Full CRUD for tasks (create, read, update, delete)
- ✅ Filter by status: All / Pending / In Progress / Completed
- ✅ Sort by date: Newest / Oldest
- ✅ Delete confirmation dialog
- ✅ Toast notifications for all actions
- ✅ Form validation (frontend + backend)
- ✅ Responsive design (mobile-first)
- ✅ Reusable components: TaskCard, TaskForm, FilterBar, ConfirmDialog
- ✅ Custom React hooks: useTasks, useToast
- ✅ Environment variables on both ends
- ✅ Zero page refreshes (React state + API calls)

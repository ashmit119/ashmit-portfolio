# 🚀 Ashmit — Portfolio Website

A full-stack personal portfolio with a **Node.js + Express** backend, **MongoDB** database,
and a futuristic glassmorphism frontend. Visitors can read about you and submit contact
messages which are stored in MongoDB.

---

## 📁 Project Structure

```
ashmit-portfolio/
├── server.js          # Express server + API routes + DB connection
├── package.json
├── .env.example       # Copy this to .env and fill in your values
├── .gitignore
├── README.md
└── public/
    └── index.html     # Full frontend (HTML + CSS + JS)
```

---

## ⚙️ Local Development Setup

### 1. Prerequisites
- [Node.js](https://nodejs.org/) v18+
- [MongoDB](https://www.mongodb.com/try/download/community) (local) **OR** a free [MongoDB Atlas](https://www.mongodb.com/atlas) cluster

### 2. Install dependencies
```bash
cd ashmit-portfolio
npm install
```

### 3. Configure environment
```bash
cp .env.example .env
```
Edit `.env`:
```
PORT=3000
MONGODB_URI=mongodb://localhost:27017/portfolio
```

### 4. Run in development mode
```bash
npm run dev       # uses nodemon — auto-restarts on file changes
# OR
npm start         # plain node
```

Open **http://localhost:3000** in your browser. ✅

---

## 🗄️ MongoDB Schema

Contact messages are stored in the `contacts` collection:

| Field     | Type   | Notes                     |
|-----------|--------|---------------------------|
| name      | String | required                  |
| email     | String | required, lowercase        |
| subject   | String | required                  |
| message   | String | required                  |
| createdAt | Date   | auto (timestamps: true)   |
| updatedAt | Date   | auto (timestamps: true)   |

---

## 🌐 API Endpoints

| Method | Route           | Description                          |
|--------|-----------------|--------------------------------------|
| POST   | /api/contact    | Save a new contact message           |
| GET    | /api/contacts   | List all messages (add auth in prod) |
| GET    | *               | Serve the frontend (catch-all)       |

### POST /api/contact — Request Body
```json
{
  "name":    "Jane Doe",
  "email":   "jane@example.com",
  "subject": "Project collaboration",
  "message": "Hi Ashmit, I'd love to work with you!"
}
```

### POST /api/contact — Response
```json
{ "success": true, "message": "Message received! I'll get back to you soon. 🚀" }
```

---

## ☁️ Deploying to Production

### Option A — Render (Free Tier, Recommended)
1. Push the project to a GitHub repo.
2. Go to [render.com](https://render.com) → **New Web Service** → connect your repo.
3. Set **Build Command**: `npm install`
4. Set **Start Command**: `node server.js`
5. Add environment variable: `MONGODB_URI` → your Atlas connection string.
6. Deploy. Render gives you a free `.onrender.com` URL.

### Option B — Railway
1. Push to GitHub.
2. Go to [railway.app](https://railway.app) → **New Project** → Deploy from GitHub.
3. Add `MONGODB_URI` in the Variables tab.
4. Done — Railway auto-detects Node and builds it.

### Option C — VPS (DigitalOcean / AWS EC2)
```bash
# On your server:
git clone <your-repo-url>
cd ashmit-portfolio
npm install
cp .env.example .env   # fill in production values

# Use PM2 to keep it running
npm install -g pm2
pm2 start server.js --name portfolio
pm2 startup
pm2 save
```
Then set up **Nginx** as a reverse proxy on port 80/443 pointing to `localhost:3000`.

### MongoDB Atlas (Cloud DB for Production)
1. Create a free cluster at [mongodb.com/atlas](https://www.mongodb.com/atlas).
2. Click **Connect** → **Drivers** → copy the connection string.
3. Replace `<password>` and set it as your `MONGODB_URI` env var.

---

## 🎨 Customising the Frontend

Open `public/index.html` and update these sections:

- **Hero name & role** — search for `"Ashmit"` and `"Software Engineer"`
- **About text** — the `<div class="about-text">` section
- **Stats** — the four `.stat-card` divs
- **Skills** — the `.skills-grid` section
- **Projects** — the `.projects-grid` section (update titles, descriptions, GitHub links)
- **Contact links** — email, GitHub, LinkedIn URLs in `.contact-links`
- **Footer** — social media links

---

## 📦 Tech Stack

| Layer     | Technology          |
|-----------|---------------------|
| Backend   | Node.js + Express   |
| Database  | MongoDB + Mongoose  |
| Frontend  | Vanilla HTML/CSS/JS |
| Fonts     | Orbitron + Exo 2    |
| Hosting   | Render / Railway / VPS |

---

## 📬 View Submitted Messages
Hit `GET /api/contacts` in your browser or Postman while the server is running.
In production, protect this route with an API key or session-based auth.

---

Made with ❤️ by Ashmit

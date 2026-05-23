# 🧠 FormCraft AI

> **Build smarter forms. Collect better data. Understand everything — powered by AI.**

FormCraft AI is an advanced, full-stack AI-powered form builder that goes far beyond Google Forms and Microsoft Forms. Create beautiful forms with drag-and-drop, generate entire forms from a single sentence using Mistral AI, analyze responses with smart charts, and export everything to Excel in one click.

---

## ✨ Features

| Feature | Description |
|---|---|
| 🔐 **Google OAuth Login** | One-click sign-in — no passwords, no friction |
| 🤖 **AI Form Generation** | Describe your form in plain English → Mistral builds it instantly |
| 🧩 **Drag & Drop Builder** | Reorder fields visually with a smooth drag-and-drop canvas |
| 🔀 **Conditional Logic** | Show or hide fields based on previous answers in real time |
| 📄 **Multi-Page Forms** | Split long forms into pages with a progress bar |
| 📊 **Response Dashboard** | Charts, stats, and full response table per form |
| 📥 **Excel Export** | One-click export — file saved to cloud storage, download instantly |
| 🔗 **Shareable Links** | Every form gets a clean public URL instantly |
| 🌐 **Webhook Support** | Trigger any external workflow on submission |
| 💡 **AI Field Suggestions** | Let AI suggest additional fields based on your existing ones |

---

## 🛠️ Tech Stack

### Backend
![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=flat&logo=fastapi)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=flat&logo=postgresql&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=flat&logo=supabase&logoColor=white)
![Mistral AI](https://img.shields.io/badge/Mistral_AI-FF7000?style=flat)

| Layer | Technology |
|---|---|
| **API Framework** | FastAPI |
| **Database** | Supabase Postgres (via SQLAlchemy ORM) |
| **File Storage** | Supabase Storage |
| **Authentication** | Google OAuth2 + Server-side Sessions (Authlib) |
| **AI / LLM** | Mistral AI (`mistral-medium-latest`) |
| **Excel Generation** | openpyxl (in-memory → uploaded to Supabase) |

### Frontend
![React](https://img.shields.io/badge/React-20232A?style=flat&logo=react&logoColor=61DAFB)
![TailwindCSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=flat&logo=tailwind-css&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat&logo=vite&logoColor=white)

| Layer | Technology |
|---|---|
| **UI Framework** | React.js + Tailwind CSS |
| **Build Tool** | Vite |
| **Drag & Drop** | @dnd-kit/core |
| **Charts** | Recharts |
| **HTTP Client** | Axios (with session cookie support) |
| **Notifications** | React Hot Toast |

### Hosting (100% Free Tier)

| Service | Platform |
|---|---|
| **Frontend** | Vercel |
| **Backend** | Render |
| **Database + Storage** | Supabase |

---

## 📁 Project Structure

```
formcraft-ai/
├── backend/
│   ├── main.py                  # FastAPI app entry point
│   ├── config.py                # Environment config
│   ├── database.py              # SQLAlchemy + Supabase Postgres
│   ├── models/                  # DB models (user, form, response, session)
│   ├── routes/                  # API routes (auth, forms, responses, ai)
│   ├── services/                # Business logic (excel, mistral, session, storage)
│   ├── schemas/                 # Pydantic schemas
│   ├── middleware/              # Auth middleware
│   └── requirements.txt
├── frontend/
│   ├── src/
│   │   ├── pages/               # Home, Login, Dashboard, Builder, Responder
│   │   ├── components/          # Reusable UI components
│   │   ├── context/             # Auth context
│   │   └── api/                 # Axios API layer
│   └── package.json
└── README.md
```

---

## 🚀 Getting Started (Local Development)

### Prerequisites
- Python 3.10+
- Node.js 18+
- Mistral API key → [console.mistral.ai](https://console.mistral.ai)
- Google OAuth credentials → [console.cloud.google.com](https://console.cloud.google.com)
- Supabase project → [supabase.com](https://supabase.com)

---

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/formcraft-ai.git
cd formcraft-ai
```

---

### 2. Backend Setup

```bash
cd backend
python -m venv venv
venv\Scripts\activate        # Windows
# source venv/bin/activate   # Mac/Linux

pip install -r requirements.txt
```

Create your `backend/.env` file:

```env
DATABASE_URL=postgresql://postgres:[password]@db.[project-ref].supabase.co:5432/postgres
SUPABASE_URL=https://[project-ref].supabase.co
SUPABASE_SERVICE_ROLE_KEY=your-supabase-service-role-key
SUPABASE_STORAGE_BUCKET=formcraft-files
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret
GOOGLE_REDIRECT_URI=http://localhost:8000/api/auth/callback
FRONTEND_URL=http://localhost:5173
MISTRAL_API_KEY=your-mistral-api-key
SECRET_KEY=your-random-secret-key
COOKIE_SECURE=false
```

Run the backend:

```bash
uvicorn main:app --reload
```

Backend → `http://localhost:8000`
API Docs → `http://localhost:8000/docs`

---

### 3. Frontend Setup

```bash
cd frontend
npm install
```

Create your `frontend/.env` file:

```env
VITE_API_URL=http://localhost:8000
```

Run the frontend:

```bash
npm run dev
```

Frontend → `http://localhost:5173`

---

### 4. Supabase Setup

1. Go to [supabase.com](https://supabase.com) → New Project
2. Copy your **Database URL** from Settings → Database → Connection string
3. Copy your **Service Role Key** from Settings → API
4. Go to **Storage** → Create bucket → name it `formcraft-files` → set to **Public**
5. Paste all values into your `backend/.env`

---

### 5. Google OAuth Setup

1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Create a new project
3. Enable **Google People API**
4. Go to **APIs & Services** → **OAuth consent screen** → External
5. Go to **Credentials** → **Create OAuth 2.0 Client ID** → Web application
6. Add Authorized JavaScript origin: `http://localhost:5173`
7. Add Authorized redirect URI: `http://localhost:8000/api/auth/callback`
8. Copy **Client ID** and **Client Secret** into `backend/.env`

---

## ☁️ Deployment Guide (Free Tier)

### Step 1 — Push to GitHub
```bash
git add .
git commit -m "Initial commit"
git push origin main
```
Make sure `.env` and `client_secret*.json` are in `.gitignore`.

---

### Step 2 — Deploy Backend on Render

1. Go to [render.com](https://render.com) → New Web Service
2. Connect your GitHub repo
3. Set **Root Directory** to `backend/`
4. **Build Command:** `pip install -r requirements.txt`
5. **Start Command:** `uvicorn main:app --host 0.0.0.0 --port 8000`
6. Add all backend env vars (update `COOKIE_SECURE=true` and production URLs)
7. Deploy → copy your Render URL e.g. `https://formcraft-api.onrender.com`

---

### Step 3 — Deploy Frontend on Vercel

1. Go to [vercel.com](https://vercel.com) → New Project
2. Connect your GitHub repo
3. Set **Root Directory** to `frontend/`
4. **Framework Preset:** Vite
5. Add environment variable: `VITE_API_URL=https://formcraft-api.onrender.com`
6. Deploy → copy your Vercel URL e.g. `https://formcraft-ai.vercel.app`

---

### Step 4 — Update Google OAuth for Production

In Google Cloud Console → Credentials → your OAuth client:
- Add Authorized JavaScript origin: `https://formcraft-ai.vercel.app`
- Add Authorized redirect URI: `https://formcraft-api.onrender.com/api/auth/callback`

---

### Step 5 — Update Backend Env Vars on Render

```env
GOOGLE_REDIRECT_URI=https://formcraft-api.onrender.com/api/auth/callback
FRONTEND_URL=https://formcraft-ai.vercel.app
COOKIE_SECURE=true
```

---

## 🔄 How It Works

```
User visits FormCraft AI
        ↓
Sign in with Google (OAuth2 → server session → HTTP-only cookie)
        ↓
Dashboard → Create Form manually OR Generate with AI
        ↓
Share the public form link with anyone
        ↓
Respondents fill and submit the form (no login needed)
        ↓
View responses → charts, stats, full response table
        ↓
Export to Excel → file saved to Supabase Storage → instant download
```

---

## 🤖 AI Capabilities

### Form Generation
Type a single sentence like *"Create a restaurant customer feedback form"* and Mistral generates a complete form schema with the right field types, labels, and validation rules — instantly.

### Field Suggestions
Already have a few fields? Click **Suggest Fields** and Mistral recommends 3 additional relevant fields based on what you have already built.

---

## 📊 Supported Field Types

`Short Text` · `Long Text` · `Multiple Choice` · `Checkboxes` · `Dropdown` · `Date` · `Number` · `Email` · `File Upload` · `Star Rating` · `Linear Scale`

---

## 📦 Excel Export

Every exported file includes:
- **Sheet 1 — Responses:** bold indigo headers, alternating row colors, auto-filter, frozen top row
- **Sheet 2 — Summary:** total responses, export date, form title
- File saved automatically to **Supabase Storage** and downloaded instantly

---

## 🔒 Security

- No passwords stored — authentication handled entirely by Google
- Sessions stored server-side in Postgres with 7-day expiry
- Cookies are HTTP-only — cannot be accessed by JavaScript
- `COOKIE_SECURE=true` enforced in production
- `.env` file never committed to Git
- All protected routes validate session on every request

---

## 🗺️ Roadmap

- [ ] Email notifications on new submissions
- [ ] PDF response export
- [ ] Form templates library
- [ ] Team workspaces
- [ ] Mobile app (React Native)
- [ ] Auto-report generation via AI

---

## ⚠️ Important Before Deploying

Rotate these secrets before going live:
- Google Client Secret
- Mistral API Key
- Supabase Service Role Key
- SECRET_KEY in your `.env`

Never commit `.env` or `client_secret*.json` to GitHub.

---

## 📄 License

This project is licensed under the **MIT License** — free to use, modify, and distribute.

---

<div align="center">

Built with ❤️ using React · FastAPI · Mistral AI · Supabase · Vercel · Render

</div>

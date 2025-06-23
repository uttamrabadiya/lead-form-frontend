# Multi-Step Lead Form (Frontend)

This is the frontend application for the Lead Form project, built with **Vue 3**, **Tailwind CSS**, and **Vite**. It collects user details through a step-by-step form and submits the data to the backend API.

---

## 🚀 Tech Stack

- [Vue 3](https://vuejs.org/)
- [Vite](https://vitejs.dev/)
- [Tailwind CSS](https://tailwindcss.com/)
- [Axios](https://axios-http.com/)
- [Yup + VeeValidate](https://vee-validate.logaretm.com/v4/) for validation
- Optional: [Flowbite](https://flowbite.com/) UI utility classes

---

## 🔧 Project Setup

### 1. Install Dependencies

```bash
cd frontend
npm install
```

### 2. Environment Configuration

```bash
VITE_API_URL=https://your-backend-domain.com/api
```

### 3. Run the Development Server

```bash
npm run dev
```
Open your browser at: http://localhost:5173


## 📦 Build for Production

```bash
npm run build
```

## 📤 Deploy

The `dist/` folder can be deployed to any static hosting service (e.g. Netlify, Vercel, S3).

## 📫 API Endpoint

All form submissions are sent to the backend via:

```bash
POST ${VITE_API_URL}/lead
```

## 🚀 Deployment

### 🔗 Live URLs

- **Frontend** (Vue.js): [https://coruscating-khapse-83b0ee.netlify.app](https://coruscating-khapse-83b0ee.netlify.app)
- **Backend** (Laravel): [https://lead-form-backend-production.up.railway.app](https://lead-form-backend-production.up.railway.app)

### 🧠 Platform Choices & Reasoning

| Layer     | Platform     | Reasoning                                                                 |
|-----------|--------------|--------------------------------------------------------------------------|
| Frontend  | Netlify      | Simple CI/CD from GitHub, great for static sites, fast builds, free SSL |
| Backend   | Railway.app  | One-click Laravel support, built-in database plugin, clean UI            |
| Database  | Railway MySQL | Auto-provisioned, internal networking, pre-configured with Laravel      |


### ⚙️ Deployment Notes

#### Frontend (Netlify)

- Connected to GitHub for auto-deploy on push
- Build command: `npm run build`
- Publish directory: `dist/`
- `.env` contains:
  ```env
  VITE_API_URL=https://lead-form-backend-production.up.railway.app
  ```

#### Backend (Railway)

- PHP/Laravel project auto-detected
- Start command: `php artisan serve --host=0.0.0.0 --port=8000`
- `.env` contains:
  ```env
  APP_KEY=base64:...
  APP_URL=https://lead-form-backend-production.up.railway.app
  DB_CONNECTION=mysql
  DB_HOST=containers.<railway-host>.internal
  DB_PORT=3306
  DB_DATABASE=railway
  DB_USERNAME=root
  DB_PASSWORD=******
  ```

- Custom Build Command:
  ```bash
  composer install --no-dev --optimize-autoloader && php artisan migrate --force
  ```

- Custom Start Command
  ```bash
  php artisan serve --host=0.0.0.0 --port=8000
  ```

### ✅ Status

- [x] Form submits data to backend
- [x] OneSignal notification triggered
- [x] Data saved to database
- [x] Frontend + Backend live and stable
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
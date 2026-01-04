


Food Pizza — Fullstack Project

A simple, modern full-stack web application for ordering pizzas: menu browsing, cart, checkout (mock), order management, and admin dashboard. Designed as a starter / demo project to learn full-stack patterns (React + Node/Express + MongoDB / PostgreSQL) and to show best practices for project structure, environment setup, and deployment.

🔥 Features


Public menu with categories (Pizza, Sides, Drinks)


Product pages with images, descriptions, sizes, and prices


Shopping cart (client-side + persisted in backend)


Mock checkout flow (no real payments; placeholder for Stripe)


User authentication (email/password) with JWT


User profile & order history


Admin panel to add / edit / remove products and view orders


REST API with input validation


Seed script to populate sample data


Docker support for local development



🧭 Tech stack (example)

Pick the stack you used — adjust commands and env names below to match your implementation.



Frontend: React (Vite or Create React App), TypeScript (optional), Tailwind CSS


Backend: Node.js, Express


Database: MongoDB (Mongoose) or PostgreSQL (Prisma/TypeORM)


Auth: JWT (access + refresh token pattern)


Deployment: Vercel / Netlify (frontend), Heroku / Render / DigitalOcean (backend), or Docker Compose


Testing: Jest / React Testing Library, Supertest for API endpoints

📁 Repository structure (suggested)
food-pizza/
├─ .github/
├─ frontend/
│  ├─ public/
│  ├─ src/
│  ├─ package.json
│  └─ vite.config.ts
├─ backend/
│  ├─ src/
│  │  ├─ controllers/
│  │  ├─ models/
│  │  ├─ routes/
│  │  ├─ middlewares/
│  │  ├─ services/
│  │  └─ index.ts
│  ├─ package.json
│  └─ prisma/ (if using)
├─ docker-compose.yml
├─ .env.example
├─ README.md
└─ scripts/
   └─ seed.js


🚀 Quick start (local)

Example uses Node + MongoDB. Replace with your DB commands if you use PostgreSQL.

Prerequisites


Node.js (18+ recommended)


npm or yarn


MongoDB (local or Atlas) or Docker


1) Clone the repo
git clone https://github.com/<your-username>/food-pizza.git
cd food-pizza

2) Setup environment variables
Copy .env.example to .env in the backend folder and update values:
backend/.env
PORT=4000
MONGO_URI=mongodb://localhost:27017/foodpizza
JWT_SECRET=your_jwt_secret
JWT_EXPIRES_IN=7d
REFRESH_TOKEN_SECRET=some_refresh_secret
FRONTEND_URL=http://localhost:5173

frontend/.env
VITE_API_URL=http://localhost:4000/api

3) Install dependencies and run
Terminal A — Backend:
cd backend
npm install
npm run dev       # nodemon / ts-node for development
# or
docker-compose up --build backend

Terminal B — Frontend:
cd frontend
npm install
npm run dev
# open http://localhost:5173

4) Seed sample data (optional)
cd backend
node scripts/seed.js


🧩 API (example endpoints)

Base: GET/POST/PUT/DELETE /api/...

Public


GET /api/products — list products (filter by category, search, pagination)


GET /api/products/:id — product details


POST /api/auth/register — create account


POST /api/auth/login — returns access token + refresh token


Protected (user)


GET /api/orders — get user's orders


POST /api/orders — create order (cart -> order)


GET /api/users/me — user profile


Protected (admin)


POST /api/products — add product


PUT /api/products/:id — update product


DELETE /api/products/:id — remove product


GET /api/admin/orders — list all orders



✅ Authentication & Authorization


JWT access tokens used for authenticated routes — attach Authorization: Bearer <token> header.


Role-based guard: user vs admin for admin-only routes.


Refresh tokens persisted in DB (or secure httpOnly cookies) for session renewal.



🧪 Tests


Backend unit & integration: Jest + Supertest


Frontend component tests: Jest + React Testing Library


Example run:
# backend
cd backend
npm test

# frontend
cd frontend
npm test


🐳 Docker (example)
docker-compose.yml (simple)
version: '3.8'
services:
  backend:
    build: ./backend
    env_file: ./backend/.env
    ports:
      - "4000:4000"
    depends_on:
      - mongo
  frontend:
    build: ./frontend
    env_file: ./frontend/.env
    ports:
      - "5173:5173"
  mongo:
    image: mongo:6
    volumes:
      - mongo-data:/data/db
volumes:
  mongo-data:

Run:
docker-compose up --build


✅ Deployment notes


Frontend: static build (npm run build) -> host on Vercel / Netlify / S3 + CloudFront


Backend: containerized or Node server on Render / Heroku / DigitalOcean; set env vars in host


Use managed DB (MongoDB Atlas / mLab / MongoDB on Atlas) or managed Postgres


For production: enable HTTPS, strong JWT secrets, CORS config, rate limiting, helmet, and logging



💡 Common env vars (example .env.example)
# Backend
PORT=4000
NODE_ENV=development
MONGO_URI=
DATABASE_URL=  # if using Postgres
JWT_SECRET=
JWT_EXPIRES_IN=7d
REFRESH_TOKEN_SECRET=
FRONTEND_URL=http://localhost:5173

# Optional (Stripe etc)
STRIPE_SECRET_KEY=


🙋‍♂️ Contribution
Contributions welcome! Typical workflow:


Fork the repository


Create a feature branch (git checkout -b feat/add-pizza-sizes)


Commit your changes (git commit -m "feat: add sizes")


Open a PR with a description of your changes


Ensure tests pass and run lint before opening the PR


Please follow the existing code style. Add tests for new features.

🛠️ Roadmap / Ideas


Add Stripe payments (production mode)


Real-time order updates with WebSockets


Reviews & ratings for products


Promo codes / discounts


Multi-restaurant / multi-tenant support


Mobile app (React Native)



🚨 Troubleshooting


CORS errors: ensure FRONTEND_URL is allowed in backend CORS config.


MongoNetworkError: check MONGO_URI and that Mongo is running.


JWT expired: refresh token flow needs correct secrets and storage.



📝 License
This project is MIT licensed. See LICENSE for details.

👀 Demo / Screenshots
(Add screenshots or a link to a live demo here — e.g., https://food-pizza.example.com)

If you want, I can:


generate a ready-to-paste README.md file tailored to your exact tech stack (React + Express + MongoDB or React + Nest + Postgres + Prisma),


produce a .env.example, or


create seed data and a seed script for MongoDB or Postgres.


Which stack are you using so I can produce the exact README and env examples?

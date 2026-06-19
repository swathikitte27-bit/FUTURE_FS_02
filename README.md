# Lead CRM

A simple CRM to manage client leads generated from website contact forms.

**Stack:** React (Vite) · Node.js / Express · MongoDB

## Features

- Lead listing with name, email, source, and status
- Status workflow: `new` → `contacted` → `converted`
- Notes and follow-up dates per lead
- Secure admin login (JWT)
- Public API endpoint for website contact forms
- Search and filter leads

## Project Structure

```
lead-crm/
├── backend/          # Express API + MongoDB
│   └── src/
│       ├── models/   # User & Lead schemas
│       ├── routes/   # Auth & leads endpoints
│       └── server.js
└── frontend/       # React dashboard
    └── src/
        ├── components/
        ├── pages/
        └── api.js
```

## Prerequisites

- [Node.js](https://nodejs.org/) 18+
- [MongoDB](https://www.mongodb.com/) running locally or a MongoDB Atlas URI

## Setup

### 1. Backend

```bash
cd backend
cp .env.example .env
npm install
npm run seed    # creates admin user + sample leads
npm run dev     # http://localhost:5000
```

Default admin credentials (change in `.env` before seeding):

| Field    | Value              |
|----------|--------------------|
| Email    | admin@example.com  |
| Password | admin123           |

### 2. Frontend

```bash
cd frontend
npm install
npm run dev     # http://localhost:5173
```

Open http://localhost:5173 and sign in with the admin credentials.

## API Endpoints

| Method | Endpoint              | Auth     | Description                    |
|--------|-----------------------|----------|--------------------------------|
| POST   | `/api/auth/login`     | Public   | Admin login, returns JWT       |
| GET    | `/api/leads`          | JWT      | List leads (filter & search)   |
| POST   | `/api/leads`          | JWT      | Create lead manually           |
| GET    | `/api/leads/:id`      | JWT      | Get single lead                |
| PATCH  | `/api/leads/:id`      | JWT      | Update lead (incl. status)     |
| POST   | `/api/leads/:id/notes`| JWT      | Add note / follow-up           |
| DELETE | `/api/leads/:id`      | JWT      | Delete lead                    |
| POST   | `/api/leads/public`   | API Key  | Capture lead from contact form |

### Contact Form Integration

Send leads from any website contact form to the public endpoint:

```javascript
await fetch('http://localhost:5000/api/leads/public', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'X-API-Key': 'your-public-form-api-key',  // matches CONTACT_FORM_API_KEY in .env
  },
  body: JSON.stringify({
    name: 'Jane Doe',
    email: 'jane@example.com',
    message: 'Interested in your services',
    source: 'portfolio-website',
  }),
});
```

## Environment Variables

**Backend (`backend/.env`)**

| Variable              | Description                          |
|-----------------------|--------------------------------------|
| `PORT`                | API port (default 5000)              |
| `MONGODB_URI`         | MongoDB connection string            |
| `JWT_SECRET`          | Secret for signing JWT tokens        |
| `ADMIN_EMAIL`         | Seed admin email                     |
| `ADMIN_PASSWORD`      | Seed admin password                  |
| `CONTACT_FORM_API_KEY`| Key for public contact form endpoint |
| `CLIENT_URL`          | Frontend URL for CORS                |

## Deploy to GitHub

```bash
git init
git add .
git commit -m "Initial commit: Lead CRM application"
git branch -M main
git remote add origin https://github.com/swathikitte27-bit/lead-crm.git
git push -u origin main
```

> Do not commit `.env` files. Use `.env.example` as a template.

## Skills Demonstrated

- CRUD operations (Create, Read, Update, Delete leads)
- Backend REST API with Express
- MongoDB schema design and indexing
- JWT authentication and protected routes
- React state management and API integration
- Business workflow (lead status pipeline)
- Public API with rate limiting for form submissions

## License

MIT

Terminal 1: cd backend → npm run dev
Terminal 2: cd frontend → npm run dev
Open http://localhost:5173

cd C:\Users\swath\lead-crm
git init
git add .
git commit -m "Lead CRM application"
git branch -M main
git remote add origin https://github.com/swathikitte27-bit/lead-crm.git
git push -u origin main

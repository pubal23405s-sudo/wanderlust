# 🌍 Wanderlust — Full Stack Travel Platform

**Wanderlust** is a full-stack Airbnb-inspired travel listing platform where users can explore, create, and review unique stays from around the world. Built as a major project for the **Delta Web Development Bootcamp**, it demonstrates real-world concepts including authentication, cloud image storage, interactive maps, and RESTful architecture.

🔗 **Live Demo:** [https://wanderlust-a28l.onrender.com](https://wanderlust-a28l.onrender.com)

---

## ✨ Features

- 🔐 **User Authentication** — Secure signup, login, and logout using Passport.js with local strategy and session persistence
- 🏠 **Full Listing CRUD** — Create, view, edit, and delete travel listings with title, description, price, location, and images
- 📷 **Cloud Image Uploads** — Listing photos uploaded and stored on Cloudinary via Multer
- 🗺️ **Interactive Maps** — Every listing shows its exact location on a Mapbox map using forward geocoding
- ⭐ **Review System** — Logged-in users can post and delete reviews on any listing
- 🔒 **Authorization** — Only listing owners can edit/delete their listings; only review authors can delete their reviews
- 💬 **Flash Messages** — Real-time success and error notifications across all actions
- ✅ **Server-side Validation** — All inputs validated using Joi before hitting the database
- 🗃️ **Persistent Sessions** — Sessions stored in MongoDB using `connect-mongo` so login survives server restarts
- 📱 **Responsive UI** — Mobile-friendly design using Bootstrap 5

---

## 🛠️ Tech Stack

**Backend:** Node.js, Express.js v5, MongoDB Atlas, Mongoose, Passport.js, passport-local-mongoose, Multer, Joi, connect-mongo, express-session, connect-flash

**Frontend:** EJS (templating), ejs-mate (layouts), Bootstrap 5, Mapbox GL JS, Font Awesome

**DevOps & Cloud:** Render (hosting), Cloudinary (image CDN), MongoDB Atlas (managed database), dotenv (env management)

---

## 📁 Project Structure

```
wanderlust/
├── controllers/       → Business logic (listings, reviews, users)
├── models/            → Mongoose schemas (Listing, Review, User)
├── routes/            → Express routers
├── views/             → EJS templates (layouts, listings, users, partials)
├── public/            → Static assets (CSS, JS)
├── utils/             → Async error wrapper, ExpressError class
├── middleware.js      → Auth checks, ownership validation, Joi validators
├── cloudCOnfig.js     → Cloudinary + Multer setup
├── schema.js          → Joi validation schemas
└── app.js             → App entry point, middleware, session, routes
```

---

## 🚀 Local Setup

```bash
# 1. Clone the repo
git clone https://github.com/pubal23405s-sudo/wanderlust.git
cd wanderlust

# 2. Install dependencies
npm install

# 3. Create .env file (see Environment Variables section below)

# 4. (Optional) Seed sample data
node init/index.js

# 5. Start the dev server
nodemon app.js

# 6. Visit http://localhost:8080
```

---

## 🔑 Environment Variables

Create a `.env` file in the root directory with the following:

| Variable | Description |
|---|---|
| `ATLASDB_URL` | MongoDB Atlas connection string |
| `SECRET` | Strong string used to sign sessions |
| `CLOUD_NAME` | Cloudinary cloud name |
| `CLOUD_API_KEY` | Cloudinary API key |
| `CLOUD_API_SECRET` | Cloudinary API secret |
| `MAP_TOKEN` | Mapbox public access token |

> ⚠️ Never commit `.env` — it is already listed in `.gitignore`

---

## 🌐 API Routes

| Method | Route | Description | Auth |
|---|---|---|---|
| GET | `/listings` | Browse all listings | Public |
| GET | `/listings/new` | New listing form | ✅ Login |
| POST | `/listings` | Create listing | ✅ Login |
| GET | `/listings/:id` | View single listing + map | Public |
| GET | `/listings/:id/edit` | Edit form | ✅ Owner only |
| PUT | `/listings/:id` | Update listing | ✅ Owner only |
| DELETE | `/listings/:id` | Delete listing | ✅ Owner only |
| POST | `/listings/:id/reviews` | Add a review | ✅ Login |
| DELETE | `/listings/:id/reviews/:reviewId` | Delete a review | ✅ Author only |
| GET/POST | `/signup` | Register new user | Public |
| GET/POST | `/login` | Login | Public |
| GET | `/logout` | Logout | ✅ Login |

---

## 🔒 Security

- Passwords are **never stored in plain text** — hashed & salted by `passport-local-mongoose`
- Sessions are **signed with a secret key** and stored in MongoDB (not in memory)
- `.env` secrets are **excluded from version control** via `.gitignore`
- **Ownership middleware** prevents unauthorized edits or deletions
- **Joi validation** on every POST/PUT to reject malformed data before it reaches the database
- **`httpOnly` cookies** to prevent client-side JS from accessing session tokens

---

## 📦 Deployment

Hosted on **[Render](https://render.com)** (free tier):

- **Build command:** `npm install`
- **Start command:** `node app.js`
- **Database:** MongoDB Atlas (cloud)
- **Images:** Cloudinary CDN
- **Maps:** Mapbox API
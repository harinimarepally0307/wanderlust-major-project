
# 🌍 Wanderlust – Airbnb-Inspired Property Rental Platform

A full-stack web application inspired by Airbnb. Users can browse property listings, view details on a map, leave reviews, and (once the auth phase is complete) sign up, log in, and manage their own listings.

Built with **Node.js, Express.js, MongoDB (Mongoose), EJS, and CSS**.

> **Status:** Work in progress. Phase 1 (core CRUD) is complete. Phases 2 and 3 (sessions, authentication, authorization, image upload, maps, filters, and deployment) are being built. See the [Roadmap](#-development-roadmap) below.

---

## 📌 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [Environment Variables](#-environment-variables)
- [Development Roadmap](#-development-roadmap)
- [Key Concepts Implemented](#-key-concepts-implemented)
- [Deployment](#-deployment)
- [What I Learned](#-what-i-learned)
- [Future Improvements](#-future-improvements)

---

## ✨ Features

**Phase 1: Core (done)**
- [x] Create, read, update, and delete (CRUD) property listings
- [x] Add reviews to listings with star ratings
- [x] Delete reviews
- [x] Server-side rendered pages with EJS layouts and partials
- [x] Form validation and centralized error handling
- [x] Responsive styling with CSS

**Phase 2: Sessions & Authentication (in progress)**
- [ ] Session-based state with `express-session`
- [ ] Flash messages for success and error feedback (`connect-flash`)
- [ ] User sign up, login, and logout with Passport.js (local strategy)
- [ ] Secure password storage with hashing and salting
- [ ] Authorization: only the listing owner can edit or delete it
- [ ] Only the review author can delete their review

**Phase 3: Media, Maps, Search & Deployment (planned)**
- [ ] Image upload to cloud storage (Multer + Cloudinary)
- [ ] Display and edit listing images with a preview
- [ ] Interactive map on each listing page (Mapbox)
- [ ] Geocoding of listing locations and map markers with popups
- [ ] Category filters and a tax-toggle switch in the UI
- [ ] Search listings by title or location
- [ ] Session storage in MongoDB Atlas (`connect-mongo`)
- [ ] Deployment to Render with GitHub integration

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| Runtime | Node.js |
| Web framework | Express.js |
| Database | MongoDB with Mongoose (Atlas in production) |
| Templating | EJS with `ejs-mate` layouts |
| Styling | CSS (Bootstrap if used in your views) |
| Sessions | express-session, connect-mongo, connect-flash |
| Authentication | Passport.js (passport-local, passport-local-mongoose) |
| File uploads | Multer and Cloudinary |
| Maps | Mapbox |
| Deployment | Render |
| Version control | Git and GitHub |



---

## 📁 Project Structure


wanderlust-major-project/
├── init/          # Seed data and database initialization script
├── models/        # Mongoose schemas (Listing, Review, User)
├── public/        # Static assets: CSS, client-side JS, images
├── utils/         # Helper utilities (wrapAsync, ExpressError, etc.)
├── views/         # EJS templates
│   ├── includes/  # Reusable partials (navbar, footer, flash messages)
│   ├── layouts/   # Base layout template
│   ├── listings/  # Listing pages (index, show, new, edit)
│   └── users/     # Sign up and login pages
├── app.js         # Entry point: server, middleware, routes
├── schema.js      # Joi validation schemas
├── package.json
└── .gitignore


---

## 🚀 Getting Started

### Prerequisites
- Node.js (v18 or later)
- npm
- A MongoDB database (local or MongoDB Atlas)

### Installation

//bash:
# 1. Clone the repository
git clone https://github.com/harinimarepally0307/wanderlust-major-project.git
cd wanderlust-major-project

# 2. Install dependencies
npm install

# 3. Create a .env file in the root (see the next section)

# 4. (Optional) Seed the database with sample listings
node init/index.js

# 5. Start the server
node app.js
# or, with auto-restart during development
npx nodemon app.js


Then open **http://localhost:8080** in your browser. (Change the port in `app.js` if yours is different.)

---

## 🔐 Environment Variables

Create a `.env` file in the project root. **Never commit this file.** Make sure `.env` is listed in `.gitignore`.


# Database
ATLASDB_URL=mongodb+srv://<user>:<password>@<cluster>.mongodb.net/wanderlust

# Session secret (use a long random string)
SECRET=your_session_secret_here

# Cloudinary (image uploads)
CLOUD_NAME=your_cloud_name
CLOUD_API_KEY=your_api_key
CLOUD_API_SECRET=your_api_secret

# Mapbox (maps and geocoding)
MAP_TOKEN=your_mapbox_public_token


> Variable names are examples. Use whatever names your code reads from `process.env`.

---

## 🗺 Development Roadmap

This project is being built phase by phase. Each phase introduces new concepts on top of the last.

### Phase 1: Foundations and CRUD (complete)
- Express app setup and middleware
- Express Router (`express.Router()`) and restructuring of listing and review routes
- Cookies: setting and reading cookies, `cookie-parser`, and signed cookies
- Mongoose models and relationships between listings and reviews
- CRUD operations for listings and reviews
- EJS templating, layouts, and partials
- Error handling with `wrapAsync` and a custom `ExpressError` class
- Server-side validation with Joi

### Phase 2: Sessions and Authentication (in progress)
**Part A: Sessions**
- What is state, and why HTTP is stateless
- Express sessions and session options (cookie settings, secret, resave, saveUninitialized)
- Storing and using session info across requests
- Flash messages with `connect-flash` (success and failure)
- Passing data to views with `res.locals`

**Part B: Authentication**
- Authentication vs. authorization
- How passwords are stored, and why plain text is unsafe
- Hashing and salting (bcrypt)
- Passport.js: getting started, the User model, configuring the local strategy
- Sign up (GET and POST) and login routes
- Login, logout, and redirecting after sign up or login

**Part C: Authorization**
- Restricting listing actions to the owner
- Restricting review deletion to the review author
- Tying `owner` fields to the current user

### Phase 3: Media, Maps, Search, and Deployment (planned)
**Part A: MVC and uploads**
- Model, View, Controller separation and refactoring routes into controllers
- Restyling ratings
- Image upload with Multer
- Cloudinary setup and storing files in the cloud
- Saving image links in MongoDB and displaying them
- Manipulating form data for uploads

**Part B: Maps**
- Editing listing images and preview on the edit page
- Getting started with Mapbox
- Geocoding addresses into coordinates
- Storing coordinates in the database
- Map markers and popups

**Part C: UI features**
- Fixing the home page
- Category filters
- Tax switch toggle, with working logic
- Search functionality

**Part D: Production and deployment**
- MongoDB Atlas setup
- Storing sessions in MongoDB (connect-mongo)
- Pushing code to GitHub
- Deploying to Render and connecting it to the GitHub repo

---

## 🧠 Key Concepts Implemented

These are the topics I can explain and implement from scratch.

- **HTTP and state:** Why cookies and sessions exist, and how the session ID travels in a cookie.
- **Middleware:** How `app.use`, route-level middleware, and error middleware pass control with `next()`.
- **Routing:** Organizing routes with `express.Router()` and mounting them with path prefixes.
- **Cookies:** Setting and reading cookies, signed cookies to prevent tampering, and `cookie-parser`.
- **Sessions:** Session storage (memory vs. MongoDB store), session options, and security settings.
- **Flash messages:** Storing one-time messages in the session and rendering them after a redirect (PRG pattern).
- **Password security:** Hashing vs. encryption, salting, and why bcrypt is used.
- **Authentication vs. authorization:** Who you are vs. what you are allowed to do.
- **Passport.js:** Strategies, serialize and deserialize user, and `req.isAuthenticated()`.
- **MVC:** Separating models (data), views (EJS), and controllers (request logic).
- **Async error handling:** Wrapping async route handlers so errors reach the error middleware.
- **Data relationships:** Referencing reviews and owners with `ObjectId` and `populate()`.
- **File uploads:** Handling `multipart/form-data` with Multer and storing files on Cloudinary.
- **Geocoding and maps:** Converting addresses to coordinates and rendering markers and popups.
- **Deployment:** Environment variables, hosting on Render, and connecting a GitHub repo for auto-deploys.

---

## ☁️ Deployment

1. Create a MongoDB Atlas cluster and copy the connection string into `ATLASDB_URL`.
2. Push the code to GitHub. Make sure `.env` and `node_modules/` are in `.gitignore`.
3. On [Render](https://render.com), create a new **Web Service** and connect this GitHub repository.
4. Set the build command to `npm install` and the start command to `node app.js`.
5. Add all environment variables in the Render dashboard.
6. Deploy. Future pushes to `main` redeploy automatically.

**Live demo:** _add your Render URL here once deployed_

---

## 📝 What I Learned

- How a full-stack app connects a database, a server, and server-rendered views.
- Why authentication and authorization must be enforced on the server, not only in the UI.
- How to debug middleware order issues (for example, why `express.urlencoded()` must come before routes).
- How to keep secrets out of version control.
- How to structure a growing Express app with MVC and routers.

---

## 🔮 Future Improvements

- Add pagination for listings
- Add a booking system with date ranges
- Add user profile pages
- Add rate limiting and stronger input sanitization
- Write automated tests (Jest and Supertest)
- Add a Dockerfile for containerized deployment

---

## 📄 License

This project is for learning purposes. Add a license here if you plan to share it publicly.

---

**Author:** Harini Marepally
**GitHub:** [@harinimarepally0307](https://github.com/harinimarepally0307)

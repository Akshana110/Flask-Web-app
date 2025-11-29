# Phase 2 — Authentication & Database Integration

**Date:** 2025-11-29

## Summary
Phase 2 implements backend functionality for user authentication and integrates a SQLite database using Flask-SQLAlchemy. It covers handling HTTP POST/GET requests for signup/login, server-side validation, password hashing, flash messages, and the initial database models with proper foreign-key relationships.

---

## What’s included (high level)
- Handling HTTP requests: `GET` and `POST` routes for signup and login.
- Server-side form validation and user-friendly flash messages.
- Password hashing for secure storage.
- Flask-SQLAlchemy setup and database connection (SQLite).
- Database models and foreign-key relationships (User ↔ Note).
- Automatic database creation helper.

---

## Files added / modified
- `website/auth.py` — signup/login route handlers (POST/GET), validation, hashing.
- `website/model.py` — SQLAlchemy models (User, Note) with foreign-key relations.
- `website/__init__.py` — Flask app factory augmented with SQLAlchemy init and DB creation.
- `website/views.py` — minor updates to include login/logout redirects (if applicable).
- `website/templates/login.html`, `website/templates/sign-up.html` — form changes to include `name` attributes and CSRF placeholder.
- `requirements.txt` (optional) — includes `Flask`, `Flask-SQLAlchemy`, `Flask-Login`, `Werkzeug`.

---

## Routes (implemented)
- `GET /sign-up` — show signup form  
- `POST /sign-up` — handle signup form submission (validation → save user)  
- `GET /login` — show login form  
- `POST /login` — authenticate user and login via `flask_login`  
- `GET /logout` — logout user

---

## Database (what changed)
- Added `User` model:
  - `id`, `email` (unique), `first_name`, `password` (hashed)
- Added `Note` model:
  - `id`, `data`, `date`, `user_id` (ForeignKey → `user.id`)
- Relationship: `User.notes = db.relationship('Note', backref='author')`
- SQLite is used via `SQLALCHEMY_DATABASE_URI = "sqlite:///database.db"`
- `create_database(app)` will create the DB file automatically if missing.

---

## Validation & Security
- Server-side validation for required fields and minimum lengths.
- Passwords are hashed before saving using `werkzeug.security.generate_password_hash`.
- Flash messages show success/error to the user (`flask.flash`).
- `flask_login` used for session management (login required behavior can be added in Phase 3).

---

## How to run locally (quick)
1. Create & activate virtual env:
   ```bash
   python -m venv venv
   # Windows
   venv\Scripts\activate
   # macOS / Linux
   source venv/bin/activate

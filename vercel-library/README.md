# Library Management System - Vercel deployment

public/         frontend (login + all pages)
api/index.py    Python (Flask) backend, runs as a Vercel serverless function
database/       sample_data_cloud.sql (optional demo data)
vercel.json     sends /api/* requests to the backend

## Why a cloud MySQL is needed
Vercel cannot run MySQL or keep files, so the database must be hosted elsewhere.
Create a free MySQL database at any provider (for example TiDB Cloud, Aiven or Railway)
and note its host, port, user, password and database name.

## Deploy
1. Push this folder to a GitHub repo (or use the Vercel CLI: `vercel`).
2. In Vercel: Add New > Project > import the repo. Leave the framework as "Other".
3. Before deploying, open Settings > Environment Variables and add:
   SECRET_KEY   any long random text
   DB_HOST      from your MySQL provider
   DB_PORT      usually 3306 (use the port your provider gives)
   DB_USER
   DB_PASSWORD
   DB_NAME
   DB_SSL       1   (most cloud MySQL services require SSL)
4. Deploy. Tables and the admin account are created automatically on the first login attempt.
5. Open your Vercel link and log in: admin / admin123, user type Librarian.

Optional: run database/sample_data_cloud.sql in your provider's SQL console
(after the first login attempt created the tables) to add demo books, students and loans.

If login shows "Database error: ...", the DB_* values or DB_SSL are wrong.

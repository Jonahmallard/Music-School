# Music School

An online lesson booking platform built with Django and Python. Students browse teacher profiles, book lessons, and watch embedded lesson videos; teachers manage their profiles and lessons. Accounts use Django's built-in signup/login.

**Live demo:** https://music-school-s2xq.onrender.com — hosted on Render's free tier, so the first load can take a minute to wake up.

## Features

- Teacher profiles (bio, location, instrument) and a teacher directory
- Lesson booking: date, time, instrument, description, embedded video
- User signup/login with per-user profiles
- Photo upload for profiles (Amazon S3 — see the note below)
- Embedded lesson videos via django-embed-video

## Technologies

Python, Django 3.1, PostgreSQL, Gunicorn, WhiteNoise, boto3/S3, django-embed-video.

## Getting Started (run it locally)

Requires Python 3.9 and PostgreSQL.

1. Clone the repo, create a virtual environment, and install dependencies:

   ```sh
   git clone https://github.com/Jonahmallard/music-school.git
   cd music-school
   python3 -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```

2. Set up a database. Either create a local Postgres database:

   ```sh
   createdb musicschool
   ```

   ...or use a free database at [Neon](https://neon.tech) and use its connection string in step 3 instead.

3. Set the required environment variables (these last only for the current terminal session — on Windows use `set` instead of `export`):

   ```sh
   export SECRET_KEY='a-dev-only-secret'
   export DATABASE_URL=<redacted>
   export DEBUG=True
   ```

   `SECRET_KEY` can be any random string locally. `DATABASE_URL` is your Postgres connection string — the local example above, or your Neon URL (Neon URLs already include `?sslmode=require`).

4. Run the migrations:

   ```sh
   python manage.py migrate
   ```

5. Start the server:

   ```sh
   python manage.py runserver
   ```

   Visit http://127.0.0.1:8000/ — sign up at `/accounts/signup/` to create an account, or browse teachers at `/teachers/`.

## Notes

- **Photo uploads:** the upload code points at the `splash-music` S3 bucket from the original GA group project (`BUCKET` in `main_app/views.py`). Without AWS credentials configured, uploads fail silently and the rest of the app works fine. To make uploads work, point `BUCKET` at a bucket you own and configure AWS credentials.
- **Admin:** create an admin account with `python manage.py createsuperuser`, then visit `/admin/`.
- This repo is Jonah Mallard's own copy of the GA Project 3 group app, with an email field added to profiles.
- The original hardcoded `SECRET_KEY` was removed from the settings in 2026; the value in the git history is public and must never be reused.

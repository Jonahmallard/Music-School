# Music School

An online lesson booking platform built with Django and Python. Students browse teacher profiles, book lessons, and watch embedded lesson videos; teachers manage their profiles and lessons. Accounts use Django's built-in signup/login.

## Features

- Teacher profiles (bio, location, instrument) and a teacher directory
- Lesson booking: date, time, instrument, description, embedded video
- User signup/login with per-user profiles
- Photo upload for profiles (Amazon S3; disabled unless AWS credentials are configured — the rest of the app works without it)
- Embedded lesson videos via django-embed-video

## Technologies

Python, Django 3.1, PostgreSQL (Neon), Gunicorn, WhiteNoise, boto3/S3, django-embed-video.

## Demo

Live demo URL: TBD — deploying to Render (free tier).

## Running locally

Requires Python 3.9.

```sh
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
export SECRET_KEY='a-dev-only-secret'
export DATABASE_URL='sqlite:///db.sqlite3'   # Postgres in production
export DEBUG=True
python manage.py migrate
python manage.py runserver
```

## Notes

- This repo is Jonah Mallard's own copy of the GA Project 3 group app (see the `splashmusic` fork on the same account), with an email field added to profiles.
- The original hardcoded `SECRET_KEY` was removed from the settings in 2026; the value in the git history is public and must never be reused.

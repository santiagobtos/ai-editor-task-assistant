# AI Task Assistant for Video Editors

An app that helps video editors turn messy client requests (WhatsApp messages, notes, briefs) into **concrete, structured editing tasks** using an LLM through the **Groq API**.

> Work in progress — built by [Santiago Barrientos Medina](https://github.com/santiagobtos), Systems & Computer Engineering student at Universidad Nacional de Colombia.

## The problem

Editors receive feedback scattered across chats: *"make it warmer, like the Apple videos"*, *"use the client's logo at the end"*, *"deliver in vertical for Reels"*. Turning that into a clear to-do list takes time and details get lost.

## What it does

- **AI classification of client messages** — sends the client's messages to `llama-3.3-70b-versatile` (via Groq) and returns a validated, structured result.
- **Specialized extractors** for the information editors actually need:
  - 🎨 **Colorimetry** — color space, log profile, LUTs, white balance, mood, reference films
  - 🎬 **Shots** — takes, shot types, take quality
  - 🔊 **Audio**, 🏷️ **Brand**, 📝 **Editorial notes**, 📦 **Delivery** specs, 📁 **Source** of footage
- **Robust output parsing** — results are validated with Pydantic schemas, with automatic repair of invalid LLM values before failing.
- **Project management** — projects, videos, comments, messages, notifications and payments.
- **Client review link** — a web page where the client watches the video and leaves time-coded comments, plus a checkout page.
- **WhatsApp bridge** — pick and share client messages from WhatsApp straight into a project.

## Architecture

```
PRODUCT-main/
├── editor-app/
│   ├── backend/      FastAPI API · SQLAlchemy + Alembic · Groq LLM · background workers
│   ├── mobile/       React Native (Expo) app for editors · Zustand
│   └── web-client/   Next.js pages for client review & checkout
└── website/          Landing page (HTML/CSS/JS)
```

| Layer | Tech |
| --- | --- |
| AI | Groq API · Llama 3.3 70B · Pydantic structured output |
| Backend | Python · FastAPI · SQLAlchemy · Alembic · workers for AI, transcoding and notifications |
| Mobile | React Native · Expo · TypeScript · Zustand · Lottie |
| Web | Next.js · TypeScript · WebSockets |
| Auth | Email/phone OTP · Google sign-in |

## Running locally

**Backend**
```bash
cd PRODUCT-main/editor-app/backend
pip install -r requirements.txt
# create a .env file with: GROQ_API_KEY=your_key and SECRET_KEY=any_random_string
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

**Mobile app**
```bash
cd PRODUCT-main/editor-app/mobile
npm install
npx expo start
```

API health check: `GET http://localhost:8000/health`

## Roadmap

- [ ] Complete `requirements.txt` and `docker-compose.yml`
- [ ] Deploy backend to the cloud
- [ ] More tests for AI extractors
- [ ] Screenshots and demo video in this README

## Author

**Santiago Barrientos Medina** — Python · Machine Learning · AI applications
GitHub: [@santiagobtos](https://github.com/santiagobtos)

# Editor App

## Run locally

**Backend**
```bash
cd editor-app/backend
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

**Mobile**
```bash
cd editor-app/mobile
npx expo start
```

Configure secrets (e.g. `GROQ_API_KEY`, `SECRET_KEY`) in a local `.env` file. Never commit tokens or IDs.
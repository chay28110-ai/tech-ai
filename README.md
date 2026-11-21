# tech.ai — Starter project

This is the first development scaffold for an independent AI assistant.

## Architecture
- `web/`: Next.js web interface
- `api/`: FastAPI backend, connects to a locally hosted Ollama model
- `mobile/`: Expo setup instructions for the Android/iOS app
- The AI model is served by Ollama; this project does not call ChatGPT, Copilot, or Claude.

## Requirements
- Node.js 20.9+
- Python 3.10+
- Ollama installed locally
- A computer for development (an Android phone alone is not sufficient to run the full local toolchain).

## 1. Start the AI model
Install Ollama from https://ollama.com, then run:

```bash
ollama pull qwen2.5:3b
ollama serve
```

The selected model is a starter choice, not a final production decision. Check the exact model card and licence before commercial deployment.

## 2. Start the API
```bash
cd api
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

API health: http://localhost:8000/health

## 3. Start the website
In another terminal:
```bash
cd web
npm install
npm run dev
```
Open http://localhost:3000

Set `NEXT_PUBLIC_API_URL` in `web/.env.local` if the API is not at `http://localhost:8000`.

## 4. Mobile app
Create the Expo app:
```bash
npx create-expo-app@latest mobile
cd mobile
npx expo start
```
Then implement the same `/chat` API call from the web client. For physical-device testing, set the API URL to your computer's LAN IP, not `localhost`.

## Important security notes
- Do not expose Ollama directly to the public internet.
- Put authentication, rate limits, input validation, logging, and abuse protection in front of the model before public launch.
- Never put private service keys in browser/mobile code.
- Add privacy policy, terms, data deletion, and model/licence notices before accepting public users.
- Free hosting plans have limits and can pause inactive projects.

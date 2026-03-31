# AI Mock Interview

A full-stack mock interview app that lets candidates practice behavioral and technical interviews with AI-powered questions, speech-to-text, and detailed feedback.

## Features
- Account-based access with JWT authentication.
- Resume PDF upload and parsing to tailor interview questions.
- AI-generated interview questions and follow-ups.
- Code-answer evaluation with structured scoring.
- Speech-to-text for spoken answers (AssemblyAI).
- Text-to-speech for interviewer audio (Murf).
- Interview history with feedback summaries.

## Tech Stack
- Client: React 19, Vite, React Router.
- Server: Node.js, Express, MongoDB (Mongoose).
- AI/Media: Google Gemini, AssemblyAI, Murf.

## Project Structure
- `client/` React frontend (Vite).
- `server/` Express API + MongoDB.

## Getting Started

### 1) Install dependencies
From the project root, install for both apps:

```bash
cd server
npm install
cd ../client
npm install
```

### 2) Configure environment variables
Create `server/.env` with the following keys (values are required for full functionality):

```bash
PORT=5000
NODE_ENV=development
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
JWT_EXPIRES_IN=7d
GEMINI_API_KEY=your_google_gemini_api_key
MURF_API_KEY=your_murf_api_key
ASSEMBLYAI_API_KEY=your_assemblyai_api_key
CLIENT_URL=http://localhost:5173
```

Security note: do not commit real API keys or secrets.

### 3) Run the apps
In two terminals:

```bash
cd server
npm run dev
```

```bash
cd client
npm run dev
```

Client runs on `http://localhost:5173` and the API on `http://localhost:5000`.

## API Overview
Base URL: `http://localhost:5000/api`

- `POST /auth/register` Register a new user.
- `POST /auth/login` Log in and receive a JWT.
- `GET /auth/me` Get current user.
- `POST /auth/logout` Log out.
- `POST /resume/upload` Upload a resume PDF and extract text.
- `GET /resume` Get current user’s resume.
- `POST /interview/start` Start a new interview session.
- `POST /interview/transcribe` Transcribe an audio answer (STT).
- `POST /interview/:id/answer` Submit a text answer.
- `POST /interview/:id/answer-audio` Submit a voice answer (upload audio).
- `POST /interview/:id/code` Submit a code answer.
- `POST /interview/:id/end` End interview and generate feedback.
- `POST /interview/:id/speak` Convert text to speech for the interview.
- `GET /interview/:id` Fetch interview details.
- `GET /history` Fetch past interviews.
- `GET /history/:id` Fetch a single interview from history.
- `DELETE /history/:id` Delete one interview from history.
- `DELETE /history/clear` Clear all history.

## Client Routes
- `/login` Login page.
- `/` Home.
- `/setup` Interview setup.
- `/interview/:id` Interview session.
- `/feedback/:id` Feedback report.
- `/history` Interview history.

## Scripts

### Server
- `npm run dev` Start server with auto-reload.
- `npm start` Start server in production mode.

### Client
- `npm run dev` Start Vite dev server.
- `npm run build` Build for production.
- `npm run preview` Preview the production build.

## Notes
- Resume parsing uses `pdfjs-dist` and expects PDF uploads.
- Audio transcription uses AssemblyAI and requires a valid API key.
- Interview questions and feedback use Google Gemini.

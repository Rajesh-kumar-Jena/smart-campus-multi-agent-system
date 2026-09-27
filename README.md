# Commons · Smart Campus Assistant

A local-first prototype of the smart campus multi-agent system. It connects a React student console to a FastAPI service, coordinates specialist agents with LangGraph, and persists campus records and conversations in SQLite.

## Run locally

In PowerShell, from the project root:

```powershell
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
uvicorn backend.main:app --reload
```

In a second terminal:

```powershell
cd frontend
npm install
npm run dev
```

Open the Vite URL printed by npm (normally `http://localhost:5173`). The API is at `http://localhost:8000`; interactive API docs are at `http://localhost:8000/docs`.

To use Groq parsing and response generation, add your key to the root `.env` file as `GROQ_API_KEY=...`, then restart FastAPI. Set `GROQ_MODEL` there to override the default model. Without a key, deterministic intent parsing and response templates keep the full demo working offline.

## What works

- LangGraph query parsing, schedule, library, navigation, error, response-reflection, and analytics nodes.
- Seeded timetable, book catalog, and campus-place directory with SQLite FTS retrieval and aliases.
- Chat history and student preferences persisted to SQLite.
- Reservation and loan-extension requests queued for staff approval; the request desk can approve or decline them.
- Usage counts by intent, schedule view, campus lookup, and a responsive chat interface.

## Demo boundaries

The campus name, student, classes, books, and buildings are sample data. The route guidance uses a saved origin and directory notes; it is not turn-by-turn GIS navigation. PostgreSQL, a hosted vector database, a live library system, and a real campus map provider are integration points for deployment, not prerequisites for this working local proof of concept. The local database is `campus.db` and is created on first API startup. Set `CAMPUS_DB_PATH` to store it elsewhere.

## Verify

```powershell
python -m unittest backend.test_agents
cd frontend
npm run build
```
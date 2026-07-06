# Mental Health Chatbot — Megathon 2024

An AI-powered mental health support chatbot that conducts structured conversations, performs real-time sentiment analysis, tracks mental health metrics over time, and generates progress summaries. Built during Megathon 2024 (IIIT Hyderabad hackathon).

## How It Works

1. **Guided conversation** — The chatbot walks users through 9 targeted questions covering anxiety, depression, sleep, stress, career worries, and more
2. **Real-time sentiment analysis** — Each response is analyzed using GPT-4o-mini for sentiment polarity (-100 to +100) and key concern extraction
3. **Category classification** — Responses are classified into mental health categories (Anxiety, Depression, Insomnia, Stress, etc.) with intensity scoring
4. **Session persistence** — All conversations are stored in Firebase Firestore with timestamps
5. **Progress tracking** — Historical sessions are aggregated to show mental health trends over time via polarity graphs and concern timelines
6. **Session summaries** — GPT generates per-session and cross-session summaries identifying patterns, improvements, or deterioration

## Architecture

```
Frontend (Next.js + Tailwind)
  ├── Chatbot interface — guided Q&A with real-time responses
  ├── Session history — view and revisit past conversations
  ├── Progress dashboard — polarity graphs, concern breakdown
  └── Firebase (Firestore) — conversation + analytics storage

Python Backend (LangChain + OpenAI)
  ├── chatbot.py — conversational agent using LangChain with memory
  ├── keywords.py — sentiment polarity + concern extraction via GPT-4o-mini
  ├── summary.py — session and cross-session summary generation
  └── analysis-listener.py — Firebase listener that triggers analysis on new sessions
```

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Frontend | Next.js, Tailwind CSS, Chart.js |
| AI/NLP | OpenAI GPT-4o-mini, LangChain |
| Database | Firebase Firestore |
| Backend | Python, firebase-admin SDK |

## Setup

**Python backend:**
```bash
cd pythonpart
pip install -r requirements.txt
# Add your OpenAI API key to .env: OPENAI_API_KEY=...
python analysis-listener.py  # Starts the Firebase listener
```

**Frontend:**
```bash
cd nextjspart/myapp
npm install
npm run dev
# Open http://localhost:3000
```

## Project Structure

```
pythonpart/
  chatbot.py            — LangChain conversational agent with memory
  keywords.py           — Sentiment polarity and concern extraction
  summary.py            — Session and longitudinal summary generation
  analysis-listener.py  — Firebase trigger for automated analysis
  output-listener.py    — Output stream listener

nextjspart/myapp/
  src/app/
    chatbot/            — Chat interface page
    prevsession/        — Session history viewer
    progress/           — Progress tracking with graphs
    datadisplay.js/     — Data visualization page
    compos/             — Shared components (navbar, charts, polarity graph)
    lib/                — Firebase configuration
```
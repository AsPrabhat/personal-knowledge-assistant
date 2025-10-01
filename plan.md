# Project Plan: Personal Knowledge Assistant (PKA)

## Overview
A Personal Knowledge Assistant that ingests lecture notes, PDFs, and slides, then allows the user to:
- Ask natural language questions and receive answers with citations.
- Generate summaries of documents.
- Create flashcards for revision.
- Generate personalized study plans.

**Constraints:**  
- All tools must be open-source or free.  
- Use OpenRouter free endpoints for LLM access.  
- No paid APIs or cloud services.  

---

## Tech Stack
- **Backend:** Python + FastAPI  
- **Frontend:** React + Tailwind CSS + ShadCN/UI  
- **LLM Orchestration:** LangChain  
- **Embeddings:** HuggingFace (`sentence-transformers/all-MiniLM-L6-v2`)  
- **Vector Store:** FAISS (local)  
- **Database (optional):** SQLite for metadata  

---

## System Architecture
```
Frontend (React + Tailwind + ShadCN)
    ↓ (REST API)
Backend (FastAPI + LangChain)
    ↓
Retriever (FAISS + HuggingFace Embeddings)
    ↓
LLM via OpenRouter
    ↓
Answer + Citations
```

Additional modules:
- Summarizer (document summaries).
- Flashcard generator (Q&A pairs).
- Study plan generator (time allocation).

---

## Project Structure
```
project-root/
│
├── backend/
│   ├── main.py              # FastAPI entry point
│   ├── requirements.txt     # Python dependencies
│   ├── ingestion/           # PDF/text ingestion & preprocessing
│   ├── retrieval/           # FAISS index + embeddings
│   ├── chains/              # LangChain pipelines (QA, summarize, flashcards)
│   └── utils/               # Helpers (config, logging, etc.)
│
├── frontend/
│   ├── src/
│   │   ├── components/      # UI components (upload, chat, cards)
│   │   ├── pages/           # React pages
│   │   └── api/             # API calls to backend
│   ├── package.json
│   └── tailwind.config.js
│
├── data/                    # Example PDFs, notes
├── plan.md                  # This file
└── README.md
```

---

## Milestones

### Phase 1 — Backend Core
- [ ] Implement PDF ingestion + text chunking (PyMuPDF or pdfplumber).
- [ ] Generate embeddings with HuggingFace sentence-transformers.
- [ ] Store and query vectors using FAISS.
- [ ] Connect retriever to LLM via OpenRouter (LangChain pipeline).
- [ ] Provide REST endpoints: `/qa`, `/summarize`, `/flashcards`, `/studyplan`.

### Phase 2 — Study Tools
- [ ] Implement summarization endpoint.
- [ ] Implement flashcard generation (Q&A JSON output).
- [ ] Implement study plan generator (time-based tasks).

### Phase 3 — Frontend
- [ ] Create React project with Tailwind + ShadCN.
- [ ] Build components: file upload, chat window, flashcard viewer, study plan viewer.
- [ ] Integrate with backend APIs.

### Phase 4 — Evaluation
- [ ] Create small gold QA dataset (~20 questions).
- [ ] Evaluate answer accuracy and citation correctness.
- [ ] Collect peer feedback on summaries and flashcards.

### Phase 5 — Final Deliverables
- [ ] Complete code with documentation.
- [ ] Example PDFs and sample QA dataset.
- [ ] Demo-ready React app + FastAPI backend.
- [ ] README with setup + usage instructions.
- [ ] Optional: Deploy frontend (Vercel/Netlify free) and backend (Render/Heroku free).

---

## API Specification (Backend → Frontend)
- `POST /upload` → upload document (PDF/TXT)  
- `POST /qa` → input: {question}, output: {answer, citations}  
- `POST /summarize` → input: {doc_id}, output: {summary}  
- `POST /flashcards` → input: {doc_id}, output: [{q, a}]  
- `POST /studyplan` → input: {topic, time}, output: {plan}  

---

## Evaluation Plan
- **Quantitative:**  
  - % of correct answers vs gold QA dataset.  
  - Citation correctness.  
- **Qualitative:**  
  - User study with peers on summaries and flashcards.  
  - Responsiveness tests.  

---

## Demo Script
1. Upload a PDF of lecture notes.  
2. Ask: “Summarize Chapter 3 in 5 bullet points.”  
3. Ask: “What is the formula for X? Cite the source.”  
4. Generate flashcards for revision.  
5. Generate a 1-hour study plan for “Operating Systems.”  

---

## Deliverables
- `backend/` (FastAPI with LangChain + FAISS).  
- `frontend/` (React + Tailwind + ShadCN).  
- `data/` (sample documents).  
- Evaluation results + demo video.  
- Final report.

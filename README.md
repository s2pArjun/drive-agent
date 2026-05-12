# 🗂️ DriveBot — Conversational AI for Google Drive

A fully conversational AI agent to search, filter, and discover files in Google Drive using natural language.

**Stack:** Python · FastAPI · LangGraph · LangChain · Groq (Llama 3.3 70B) · Google Drive API v3 · Streamlit


## 🧠 Agent Architecture

```
User Message
     │
     ▼
Streamlit (SSE consumer)
     │ POST /chat/stream
     ▼
FastAPI Backend
     │
     ▼
LangGraph ReAct Agent ─── MemorySaver (per-session state)
     │
     ├── Tool: search_drive_files(q_query)
     ├── Tool: list_all_files()
     └── Tool: get_file_details(file_id)
              │
              ▼
        Google Drive API v3
```

## 🔍 Query Examples the Agent Handles

| User Says | Drive Query Generated |
|---|---|
| "Find all PDFs" | `mimeType = 'application/pdf'` |
| "Search for budget files" | `name contains 'budget' or fullText contains 'budget'` |
| "Files from last week" | `modifiedTime > '2024-10-17T00:00:00'` |
| "Images in the drive" | `mimeType contains 'image/'` |
| "Find the financial report" | `name contains 'financial' and fullText contains 'report'` |
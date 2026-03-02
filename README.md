# WSRA - Web Security Reconnaissance Agent

An autonomous AI-powered web security reconnaissance and vulnerability scanning agent. WSRA uses a multi-agent architecture to crawl, map, analyze, and identify potential security vulnerabilities in modern web applications — including Single Page Applications (SPAs).

## ✨ Features

- **🕷️ Autonomous Crawling** — Playwright-based crawler handles both static and SPA sites
- **🗺️ Intelligent Mapping** — Auto-discovers API endpoints, static assets, and application features
- **🔍 Vulnerability Hinting** — Rule-based engine suggests high-probability manual testing targets (XSS, SSRF, LFI, etc.)
- **📜 JavaScript Analysis** — Static analysis of JS files to identify dangerous sinks and user-controlled sources
- **🖱️ Interaction Engine** — Clicks buttons, submits forms, and explores dynamic states
- **📊 Multi-Format Reports** — JSON, Markdown, CSV, and Burp Suite XML
- **📡 Real-time Dashboard** — React-based dashboard with live scan monitoring

## 🏗️ Architecture

| Layer     | Stack                                                  |
|-----------|--------------------------------------------------------|
| Frontend  | React 19, Vite, TailwindCSS 4, Framer Motion          |
| Backend   | Python, FastAPI, Playwright, Google Gemini AI          |
| Database  | PostgreSQL (local or Supabase)                         |

### Agent System

| Agent              | Role                                               |
|--------------------|-----------------------------------------------------|
| Orchestrator       | Central brain — manages crawl frontier & dispatching |
| Crawler            | Fetches pages and extracts DOM content               |
| Mapper             | Analyzes URL structures and sitemaps                 |
| JS Analyzer        | Parses JavaScript ASTs for security flaws            |
| Vulnerability Hinter | Correlates data to hypothesize vulnerabilities    |
| Interaction Agent  | Explores clickable elements to find new states       |
| Network Monitor    | Captures and analyzes all HTTP traffic               |
| Form Filling       | Handles form submission logic                        |

## 📋 Prerequisites

- **Python** 3.11+
- **Node.js** 16+
- **PostgreSQL** (local or cloud e.g. Supabase)

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/wsra.git
cd wsra
```

### 2. Backend Setup

```bash
cd backend

# Create virtual environment
python -m venv venv

# Activate it
# Windows:
venv\Scripts\activate
# Linux/Mac:
source venv/bin/activate

# Install Python dependencies
pip install -r requirements.txt

# Install Playwright browsers
playwright install

# Install JS Analyzer dependencies
cd agents/js_parser
npm install
cd ../..

# Configure environment
cp .env.example .env
# Edit .env with your real values (API keys, DB URL, etc.)
```

### 3. Frontend Setup

```bash
cd frontend

# Install Node dependencies
npm install

# Configure environment
cp .env.example .env
# Edit .env if your backend runs on a different host/port
```

### 4. Run the Application

**Terminal 1 — Backend API:**
```bash
cd backend
python main.py
```
The API will start at `http://localhost:8000`.

**Terminal 2 — Frontend Dashboard:**
```bash
cd frontend
npm run dev
```
Access the dashboard at `http://localhost:5173`.

## ⚙️ Configuration

### Backend (`backend/.env`)

| Variable        | Description                           | Example                                              |
|-----------------|---------------------------------------|------------------------------------------------------|
| `GEMINI_API_KEY`| Google Gemini API key                 | `AIzaSy...`                                          |
| `DATABASE_URL`  | PostgreSQL connection string          | `postgresql://user:pass@localhost:5432/wsra`          |
| `HEADLESS`      | Run browser headless (True/False)     | `True`                                               |

### Frontend (`frontend/.env`)

| Variable              | Description            | Example                    |
|-----------------------|------------------------|----------------------------|
| `VITE_API_BASE_URL`   | Backend API base URL   | `http://localhost:8000`    |

> **⚠️ Never commit `.env` files.** Use the `.env.example` templates as reference.

## 📁 Project Structure

```
wsra/
├── backend/
│   ├── agents/              # Autonomous agent modules
│   │   ├── js_parser/       # Node.js AST analysis tools
│   │   ├── crawler.py
│   │   ├── form_filling.py
│   │   ├── interaction_agent.py
│   │   ├── js_analyzer.py
│   │   ├── mapper.py
│   │   ├── network_monitor.py
│   │   ├── orchestrator.py
│   │   └── vuln_hinter.py
│   ├── api/                 # REST API endpoints
│   ├── config/              # Settings & configuration
│   ├── database/            # DB models & connection
│   ├── exports/             # Report generators
│   ├── llm/                 # LLM client (Gemini)
│   ├── main.py              # Entry point
│   ├── requirements.txt
│   └── .env.example
├── frontend/
│   ├── src/
│   │   ├── components/      # UI components
│   │   ├── pages/           # Route pages
│   │   ├── lib/             # Utility functions
│   │   └── api.js           # API client
│   ├── package.json
│   └── .env.example
├── .gitignore
└── README.md
```

## 📤 Export Formats

| Format     | Description                                          |
|------------|------------------------------------------------------|
| JSON       | Full machine-readable scan data                      |
| Markdown   | Human-readable summary and findings                  |
| CSV        | Parameter and endpoint inventory                     |
| Burp XML   | Importable issues file for Burp Suite Pro/Community  |

## 🤝 Contributing

1. Create a new agent in `backend/agents/`
2. Register it in `backend/agents/orchestrator.py`
3. Update database models if necessary
4. Submit a Pull Request

## 📄 License

This project is for educational and authorized security testing purposes only.

---

Made with ❤️ by WSRA Team

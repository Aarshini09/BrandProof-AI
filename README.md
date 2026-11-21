# 🛡️ BrandProof AI (v3.1)

**Every claim checked. Every flag proven.**  
An intelligent brand-governance platform built for the **Inkloom AI Problem Statement** that verifies marketing copy, posters, and documents against a team's approved facts, rules, and brand logo before anything is published—and seals every approval in a tamper-evident **SHA-256 Proof Certificate**[cite: 1, 3].

[![Live Demo](https://img.shields.io/badge/Live_Demo-Render-10b981?style=for-the-badge)](https://brandproof-ai-ddlp.onrender.com)
[![OpenAPI Docs](https://img.shields.io/badge/API_Docs-Swagger-3b82f6?style=for-the-badge)](https://brandproof-ai-ddlp.onrender.com/docs)
[![Repository](https://img.shields.io/badge/GitHub-Repository-181717?style=for-the-badge&logo=github)](https://github.com/sanjaykumarpathak640-png/brandproof-ai)
[![Tests](https://img.shields.io/badge/Tests-35_Passing-22c55e?style=for-the-badge)](#testing--accuracy-benchmark)

---

## 🔗 Live Links

* **Live Web App:** [https://brandproof-ai-ddlp.onrender.com](https://brandproof-ai-ddlp.onrender.com) *(Click **"Start the demo - no sign-up"** for an isolated private sandbox; free server cold-start takes ~50s)*[cite: 1, 6]
* **Interactive API Docs (OpenAPI):** [https://brandproof-ai-ddlp.onrender.com/docs](https://brandproof-ai-ddlp.onrender.com/docs)[cite: 1]
* **Source Repository:** [https://github.com/sanjaykumarpathak640-png/brandproof-ai](https://github.com/sanjaykumarpathak640-png/brandproof-ai)[cite: 1]

---

## ✨ Key Features

* **Versioned Brand Memory & Impact Preview:** Stores approved prices, discount caps, warranties, specs, banned/confidential terms, brand palette, and official logos with validity dates[cite: 3]. Before saving any rule change, **Preview Impact** re-runs rules across all approved posts to flag what would break[cite: 3, 8].
* **Multilingual Deterministic + AI Engine (EN / HI / Hinglish):** Detects numbers written in words and digits across English (`"seven thousand"`), Hinglish (`"saat hazaar"`, `"aadhe daam"`, `"aajeevan warranty"`), and Hindi (`"सात हज़ार"`, `"शर्ते लागू"`)[cite: 8]. Uses **Google Gemini (`gemini-3.8-flash` + backup model)** with an **Evidence Verifier** that drops any AI finding not backed by an exact quote[cite: 3, 8].
* **Poster Vision Inspector:** Extracts text lines with bounding boxes (`0–1000` scale), checks each line against the rule engine, measures **WCAG contrast ratios** per line, checks brand palette distance ($\Delta E$), and verifies logo presence via **NumPy FFT cross-correlation** + vision model[cite: 4].
* **Purpose Guard & One-Click Fixes:** Applies word-level suggested fixes while verifying that the creator's core goal, offer, and call-to-action remain intact[cite: 3].
* **Role-Based Workflow & Proof Certificates:** Enforces `Creator → Compliance → Reviewer` approval with the **four-eyes rule** (no self-approval in teams) and issues hash-chained **SHA-256 Proof Certificates**[cite: 3].

---

## 🏗️ System Architecture

```text
┌─────────────────────────────────────────────────────────────────────────┐
│ Browser — Vanilla JS Single-Page App (No Build Step)                    │
│ • app.js (API client, auth, check, queue, review)                       │
│ • pages.js (Brand Memory, impact preview, poster box overlay, insights) │
└───────────────────────────────────┬─────────────────────────────────────┘
                                    │ HTTPS · JSON · HTTP-only Cookie
                                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ FastAPI Service (Python 3.12 · Uvicorn)                                 │
│ • engine.py + lang.py  → Deterministic rules & EN/HI/Hinglish numbers   │
│ • vision.py            → Poster text boxes, WCAG contrast, NumPy logo   │
│ • service.py + auth.py → RBAC, four-eyes rule, impact preview, imports  │
│ • certs.py             → Workspace-scoped SHA-256 hash chain            │
└───────────────────────────────────┬─────────────────────────────────────┘
                                    │ Redacted Text / Poster Only
                    ┌───────────────┴───────────────┐
                    ▼                               ▼
┌───────────────────────────────────┐ ┌───────────────────────────────────┐
│ AI Layer (Google Gemini)          │ │ Storage (PostgreSQL / SQLite)     │
│ • gemini-3.8-flash + backup       │ │ • Workspaces, Brand Memory, Rules │
│ • Evidence Verifier & 25s cap     │ │ • Submissions, Queue, Certs       │
└───────────────────────────────────┘ └───────────────────────────────────┘
```[cite: 12]

---

## 🚀 Quick Start (Run Locally in 3 Commands)

### 1. Clone & Install Dependencies
```bash
git clone [https://github.com/sanjaykumarpathak640-png/brandproof-ai.git](https://github.com/sanjaykumarpathak640-png/brandproof-ai.git)
cd brandproof-ai
python -m venv .venv && source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -r requirements.txt

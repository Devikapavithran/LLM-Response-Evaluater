# LLM Response Evaluation & Annotation Platform

> **Rate · Annotate · Compare · Analyze** — A full-featured tool for evaluating and comparing LLM responses side-by-side, with AI-assisted scoring powered by Claude.

---

## 🔗 Live Demo

**👉 [https://devikapavithran.github.io/LLM-Response-Evaluater/](https://devikapavithran.github.io/LLM-Response-Evaluater/)**

No installation needed — open the link and start evaluating immediately in your browser.

---

## 📌 What Is This?

When you're working with multiple LLMs (ChatGPT, Claude, Gemini, Llama, etc.), it's hard to objectively compare their responses. This platform solves that by giving you a structured workspace to:

- Submit a single prompt and paste responses from different models
- Rate each response on a 1–5 human star scale
- Tag problems like hallucinations, irrelevance, or incoherence
- Get AI-powered scores for accuracy, relevance, and coherence (1–10)
- Track and visualize quality metrics over time on a dashboard
- Export all your evaluation data as JSON

---

## ✨ Features

| Feature | Description |
|---|---|
| **Prompt-Response Comparison UI** | Side-by-side evaluation of multiple model outputs for the same prompt |
| **Human Rating System** | 1–5 star rating per response |
| **Annotation Tags** | Tag responses as `hallucination`, `irrelevant`, `incoherent`, `biased`, `accurate`, or `concise` |
| **AI Auto-Scoring** | Claude evaluates each response for accuracy, relevance & coherence (1–10) with reasoning |
| **Quality Dashboard** | Charts, dimension averages, and model leaderboard |
| **Evaluation History** | All sessions saved locally, loadable anytime |
| **JSON Export** | Download all evaluations as structured JSON |
| **REST API Docs** | Built-in API schema + Node.js and FastAPI backend examples |

---

## 🚀 How to Use

### Option A — Use the Live Demo (Recommended)

Open **[https://devikapavithran.github.io/LLM-Response-Evaluater/](https://devikapavithran.github.io/LLM-Response-Evaluater/)** in your browser. No sign-up, no install.

### Option B — Run Locally

```bash
# 1. Clone the repository
git clone https://github.com/devikapavithran/LLM-Response-Evaluater.git

# 2. Navigate into the project folder
cd LLM-Response-Evaluater

# 3. Open the file in your browser
open llm-eval-platform.html
# or just double-click the file in your file explorer
```

No server required. The entire app runs as a single HTML file.

---

## 📖 Step-by-Step Usage Guide

### Step 1 — Enter Your Prompt

On the **01 — EVALUATE** tab, type or paste the question/prompt you want to test across models into the **"Prompt / Question"** box.

```
Example: "Explain the difference between supervised and unsupervised learning."
```

### Step 2 — Add Model Responses

Click **`+ ADD RESPONSE`** for each model you want to compare. A response card appears for each one.

Go to ChatGPT, Gemini, Claude, Llama, or any other LLM — ask your prompt — then **copy and paste each answer** into the corresponding card. Select the model name from the dropdown on each card.

> 💡 **Tip:** Click **`DEMO DATA`** to instantly load a pre-filled example with 3 models and ratings — great for exploring the platform before adding your own data.

### Step 3 — Rate & Annotate

For each response card:

- Click the **stars (1–5)** to give a human quality rating
- Click **annotation tags** to flag issues or strengths:
  - 🔴 `hallucination` — factually wrong or made-up content
  - 🟡 `irrelevant` — doesn't answer the question
  - 🟣 `incoherent` — hard to follow or poorly structured
  - 🟠 `biased` — one-sided or opinionated without cause
  - 🟢 `accurate` — factually correct and reliable
  - 🔵 `concise` — clear and to the point
- Add optional **reviewer notes** in the text field

### Step 4 — AI Auto-Score (Optional)

Click **`◆ AI AUTO-SCORE ALL`** to let Claude automatically evaluate every response.

Each card will show:
- **Accuracy score** (1–10) — factual correctness
- **Relevance score** (1–10) — how well it addresses the prompt
- **Coherence score** (1–10) — clarity and structure
- **One-sentence reasoning** — Claude's brief explanation

The best-performing response is highlighted in green automatically.

### Step 5 — Save Your Evaluation

Click **`SAVE EVALUATION`**. The session is stored in your browser's local storage and appears in the **History** tab.

### Step 6 — View the Dashboard

Switch to **02 — DASHBOARD** to see:
- Total evaluations and responses rated
- Hallucination count across all sessions
- Average human star rating
- AI dimension averages (accuracy / relevance / coherence) with progress bars
- Rating distribution chart
- Tag frequency chart
- Model leaderboard ranked by AI score

### Step 7 — Revisit Past Evaluations

Open **03 — HISTORY** to see all your saved sessions. Each entry shows:
- The prompt (truncated preview)
- Date, number of responses, average star rating, and AI average
- Active annotation tags
- A **`LOAD ↗`** button to reload any session back into the editor

### Step 8 — Export Your Data

In the History tab, click **`EXPORT JSON`** to download all evaluations as a structured `.json` file — useful for further analysis, sharing with a team, or importing into a database.

---

## 🧠 AI Scoring — How It Works

When you click **AI Auto-Score**, the platform sends each response to the **Claude API** with this evaluation prompt:

```
Given the prompt and response, score on:
- Accuracy  (1–10): Is the information factually correct?
- Relevance (1–10): Does it directly address the prompt?
- Coherence (1–10): Is it well-structured and easy to follow?
```

Claude returns structured JSON scores + a one-sentence reasoning. Tags like `hallucination` and `accurate` are also auto-suggested based on the scores.

> The live demo at GitHub Pages uses the Claude API directly. To use AI scoring on a local copy, add your API key (see [Local API Setup](#local-api-key-setup) below).

---

## 🔑 Local API Key Setup

To enable AI Auto-Scoring when running locally, open `llm-eval-platform.html` in a text editor and find:

```javascript
headers: { 'Content-Type': 'application/json' },
```

Replace it with:

```javascript
headers: {
  'Content-Type': 'application/json',
  'x-api-key': 'sk-ant-YOUR_ANTHROPIC_KEY_HERE',
  'anthropic-version': '2023-06-01',
  'anthropic-dangerous-direct-browser-access': 'true'
},
```

Get your API key at [console.anthropic.com](https://console.anthropic.com).

> ⚠️ **Security note:** Never expose your API key in a public GitHub repository. For production use, move the API call to a backend server.

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML, CSS, JavaScript (single-file) |
| Charts | Chart.js 4.4 |
| AI Scoring | Claude API (`claude-sonnet-4-20250514`) |
| Storage | Browser localStorage (pseudo-API) |
| Backend (optional) | Node.js + Express + MongoDB |
| Backend (optional) | Python + FastAPI + MongoDB |
| Deployment | GitHub Pages |

---

## 🔌 REST API Reference

The platform includes a built-in **04 — API DOCS** tab with the full REST schema. Here's a summary:

### `POST /api/evaluations`
Save a new evaluation session.

```json
{
  "prompt": "string",
  "responses": [
    {
      "model": "GPT-4o",
      "text": "string",
      "stars": 4,
      "tags": ["accurate", "concise"],
      "note": "string",
      "aiScores": {
        "accuracy": 8,
        "relevance": 9,
        "coherence": 7,
        "avg": 8.0
      }
    }
  ]
}
```

### `GET /api/evaluations`
Returns all stored evaluations.
```
Query params: ?model=GPT-4o&minScore=7&limit=20&offset=0
```

### `GET /api/metrics`
Returns aggregated metrics — avg scores per model, tag frequencies, dimension averages, leaderboard.

### `DELETE /api/evaluations/:id`
Deletes a single evaluation by ID.

---

## 🗂️ Production Backend Examples

### FastAPI + MongoDB (Python)

```python
from fastapi import FastAPI
from pydantic import BaseModel
from motor.motor_asyncio import AsyncIOMotorClient
from datetime import datetime

app = FastAPI()
client = AsyncIOMotorClient("mongodb://localhost:27017")
db = client.llm_evals

class Evaluation(BaseModel):
    prompt: str
    responses: list

@app.post("/api/evaluations")
async def create_evaluation(eval: Evaluation):
    doc = eval.dict()
    doc["timestamp"] = datetime.utcnow().isoformat()
    result = await db.evaluations.insert_one(doc)
    return {"id": str(result.inserted_id)}

@app.get("/api/evaluations")
async def get_evaluations(model: str = None, limit: int = 50):
    query = {"responses.model": model} if model else {}
    cursor = db.evaluations.find(query).limit(limit)
    return await cursor.to_list(limit)
```

### Node.js + Express + MongoDB

```javascript
const express = require('express');
const mongoose = require('mongoose');
const app = express();
app.use(express.json());

await mongoose.connect('mongodb://localhost:27017/llm_evals');

const EvalSchema = new mongoose.Schema({
  prompt: String,
  responses: Array,
  timestamp: { type: Date, default: Date.now }
});
const Evaluation = mongoose.model('Evaluation', EvalSchema);

app.post('/api/evaluations', async (req, res) => {
  const ev = new Evaluation(req.body);
  await ev.save();
  res.json({ id: ev._id });
});

app.get('/api/evaluations', async (req, res) => {
  const evals = await Evaluation.find().limit(50).lean();
  res.json(evals);
});

app.listen(3000);
```

---

## 📊 Supported Models

The platform supports any LLM. The dropdown includes:

- GPT-4o
- Claude 3.5 Sonnet
- Gemini 1.5 Pro
- Llama 3.1 70B
- Mistral Large
- Command R+
- DeepSeek V3
- Custom (for any other model)

---

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch — `git checkout -b feature/your-feature-name`
3. Commit your changes — `git commit -m "Add: your feature description"`
4. Push to your branch — `git push origin feature/your-feature-name`
5. Open a Pull Request

---
---

## 👩‍💻 Author

Built by **Devika Pavithran**

# Resume Aligner

A tiny, **free and open-source** tool that tailors your resume to a job description and gives
you a match score out of 10. It runs **entirely in your browser** — no install, no server, no
build step. It's a single HTML file (`index.html`).

You bring your own LLM. Pick from several **free** providers (or run a model **fully locally**
with no key and no cloud at all).

- **License:** MIT — use it, fork it, share it freely.
- **Privacy:** the tool has no backend. Your resume, the job description, and your API key stay
  in your browser and are sent **only** to the LLM provider you choose.

---

## Quick start

1. **Open `index.html`** — just double-click it. It opens in your default browser.
2. **Choose an LLM provider** at the top (default: Google Gemini).
3. **Paste the free API key** for that provider (see the guides below) and click **Save**.
   *(Ollama needs no key — see its section.)*
4. **Paste your resume** and the **job description**, then click **Align my resume**.

You'll get back **two scores** — how well your **original** resume matched the job and how well
the **tailored** resume matches it now — plus **keywords matched vs. missing**, the **key
changes** made, **suggestions**, and your **aligned resume**, formatted like a real resume.

**Output formats:** the aligned resume is shown as a clean, formatted document (not raw
Markdown). Export it with:
- **⬇ Download Word (.doc)** — opens directly in Microsoft Word, already formatted.
- **🖨 Print / PDF** — opens a print-ready view; choose "Save as PDF" (or print).
- **Copy text** — copies clean plain text (no `*` symbols) to paste anywhere.

### How alignment works

Each click runs multiple passes automatically — draft → self-critique against the job
description → revise — and **adds the job's missing technologies and skills** into the resume (a
Technical Skills section, woven into relevant bullets), looping until the resume covers the job's
requirements. This uses **2–3 requests** per click.

> Alignment adds **skills, tools, and technologies** to match the job. It will not invent
> employers, job titles, dates, degrees, certifications, or fake numeric metrics — so make sure
> the technologies it adds are ones you can actually speak to in an interview.

> **Important — the score is honest, not cosmetic.** The tool will **never fabricate**
> experience, skills, or metrics you don't have, so the tailored score is capped by your genuine
> fit for the role. If it can't reach a high score truthfully, it tells you *exactly what's
> missing* in the suggestions — that's a feature: a resume that lies gets caught later.

### Adding missing skills you actually have

The **"Missing / to strengthen"** box lists the job's important keywords that your resume doesn't
cover well. Some of these you may genuinely have but simply forgot to list. To add them:

1. **Click** the keywords you truly have (they turn green with a ✓), and/or **type** extras in the
   *"Add skills you have"* box (comma-separated).
2. Click **↻ Rebuild with these**.

The tool re-runs and weaves those skills into your resume as real experience — a Skills section
and, where it fits, supporting bullets. It only adds what you confirm, and won't invent projects
or metrics for them. **Don't tick something you can't back up in an interview.**

---

## Which provider should I pick?

| Provider | Cost | Key needed | Quality | Privacy | Best for |
|---|---|---|---|---|---|
| **Google Gemini** | Free tier | Yes (free) | Very good | ⚠️ free tier may train on your data | Most people — easiest, no card |
| **Groq** | Free tier | Yes (free) | Good, very fast | ⚠️ check policy | Speed |
| **OpenRouter** | Free models | Yes (free) | Varies | ⚠️ varies by model | Trying many open models |
| **Ollama (local)** | 100% free | **No key** | Good | ✅ fully private / offline | Privacy-sensitive resumes |
| **Anthropic Claude** | Paid | Yes (paid) | Highest | ✅ does not train on your data | Best results, willing to pay |

> **Privacy tip:** resumes contain personal data. Free *cloud* tiers often reserve the right to
> use your inputs to improve their models. If that matters to you, use **Ollama** (runs on your
> own machine, nothing leaves it) or paid **Claude** (no training on API data).

---

## Getting a free API key — step by step

### 🟦 Google Gemini (recommended, easiest)

1. Go to **https://aistudio.google.com/apikey**
2. Sign in with any Google account.
3. Click **"Create API key"** → **"Create API key in new project"**. No credit card required.
4. Copy the key (starts with `AIza…`).
5. In the tool: select **Google Gemini**, paste the key, click **Save**.
6. Model: leave the default `gemini-3.6-flash` (fast, generous free tier).

> **Google retires older models over time.** If you ever see *"model not found (404)"*, open
> [AI Studio](https://aistudio.google.com/), check the current model list, and type the new name
> into the **Model** field (it saves automatically). The tool also auto-updates any old cached
> `gemini-1.x/2.x` name to the current default when you reload.

**Free limits:** generous daily request/token limits that are plenty for resumes. If you hit a
`429`, wait a minute or switch models.

---

### 🟧 Groq (fastest)

1. Go to **https://console.groq.com/keys**
2. Sign up (Google/GitHub/email) — free, no card.
3. Click **"Create API Key"**, give it a name, and copy it (starts with `gsk_…`).
4. In the tool: select **Groq**, paste the key, click **Save**.
5. Model: `llama-3.3-70b-versatile` (default). For speed try `llama-3.1-8b-instant`.

**Free limits:** per-minute and per-day request limits. Great for quick runs.

---

### 🟪 OpenRouter (many free open models)

1. Go to **https://openrouter.ai/keys**
2. Sign up (Google/GitHub/email) — free.
3. Click **"Create Key"** and copy it (starts with `sk-or-…`).
4. In the tool: select **OpenRouter**, paste the key, click **Save**.
5. Model: use any model whose name ends in **`:free`**, e.g.
   `meta-llama/llama-3.3-70b-instruct:free` or `deepseek/deepseek-chat-v3-0324:free`.
   Browse all free models at **https://openrouter.ai/models?max_price=0**.

**Free limits:** free models have daily caps; some ask you to add a small credit to raise them.

---

### 🟩 Ollama (100% free, fully private, runs on your computer)

No API key, no cloud, works offline. Best privacy, but needs a one-time setup and a reasonably
capable machine (8 GB+ RAM recommended; more for larger models).

1. **Install Ollama:** download from **https://ollama.com/download** (Windows / macOS / Linux)
   and install it.
2. **Download a model** (one time). Open a terminal / PowerShell and run:
   ```bash
   ollama pull llama3.1
   ```
   Other good choices: `ollama pull qwen2.5` or `ollama pull gemma3`.
3. **Allow the browser page to talk to Ollama.** Because this tool runs as a web page, Ollama
   must be told to accept browser requests. Set `OLLAMA_ORIGINS=*` **before** starting Ollama:

   **Windows (PowerShell):**
   ```powershell
   $env:OLLAMA_ORIGINS="*"
   ollama serve
   ```

   **macOS / Linux:**
   ```bash
   OLLAMA_ORIGINS=* ollama serve
   ```

   > To make it permanent on Windows: `setx OLLAMA_ORIGINS "*"`, then fully quit Ollama from the
   > system tray and start it again. On macOS you can run
   > `launchctl setenv OLLAMA_ORIGINS "*"` and restart the Ollama app.

4. In the tool: select **Ollama** and set the model to what you pulled (e.g. `llama3.1`). No key.

> If you see "Could not reach Ollama", it means Ollama isn't running or wasn't started with
> `OLLAMA_ORIGINS=*`. Redo step 3.

---

### ⬛ Anthropic Claude (paid, highest quality)

1. Go to **https://console.anthropic.com/settings/keys**, sign in, add billing, and create a key
   (starts with `sk-ant-…`).
2. In the tool: select **Anthropic Claude**, paste the key, click **Save**.
3. Model: `claude-opus-5` (best), `claude-sonnet-5` (balanced), or `claude-haiku-4-5` (cheapest).

---

## Distributing it to your team

Send everyone the single **`index.html`** file (email, Slack, SharePoint, shared drive, or host
it on an internal page / GitHub Pages). Each person:

1. Saves/opens the file.
2. Picks a provider and enters **their own** free key (or sets up Ollama).

That's it — no setup, and usage is billed to each person's own account (free tiers cost nothing).

---

## Privacy & storage

- Your API keys and pasted text are stored **only in your own browser** (`localStorage`).
- Requests go **directly** from your browser to the provider you selected — there is no
  middle-man server.
- Clearing your browser data removes the saved keys and text.

---

## Troubleshooting

- **"Invalid API key (401/403)"** — re-copy the key; make sure it matches the selected provider.
- **"Rate limit / quota exceeded (429)"** — you've used the free tier for now; wait, or switch
  provider/model.
- **"not found (404)" / "request rejected (400)"** — usually a wrong model name; check the
  provider's model list (links above).
- **"Could not reach … (CORS/network)"** — check your connection; a strict corporate proxy may
  block a provider. Try a different provider. For Ollama, see its setup note.
- **Score didn't parse** — the tool still shows the model's raw output; try again or use a
  stronger model (smaller local models are the most likely to slip up on formatting).

---

## How it works (for the curious)

`index.html` is plain HTML + CSS + vanilla JavaScript — no frameworks, no dependencies, nothing
to build. It sends your resume + the job description to your chosen model with a prompt that asks
for a tailored resume and a JSON score, then renders the result. Swapping or adding a provider is
just a small adapter function in the `<script>` block. Contributions welcome.

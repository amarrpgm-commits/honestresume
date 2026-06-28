# ResumeAI — Free, Honest Resume Optimization

> No paywalls. No sign-up. No data stored. No tricks.

A fully open-source resume optimizer powered by Claude AI. Upload your resume + job description and get:

- **ATS score** with honest category breakdown (not a fake score to scare you into upgrading)
- **Keyword gap analysis** — exactly what's missing from your resume vs the JD
- **Bullet point rewrites** — before/after, with stronger verbs and quantified impact
- **Fully tailored resume** — complete rewrite optimized for the specific role
- **Actionable suggestions** — specific, not generic

## Live demo

🔗 [resumeai.netlify.app](https://resumeai.netlify.app) *(update this after deploying)*

## Deploy your own (5 minutes, free)

### Step 1 — Get an Anthropic API key

1. Go to [console.anthropic.com](https://console.anthropic.com)
2. Sign up → API Keys → Create Key
3. Copy it (shown once only)
4. New accounts get free credits to start

### Step 2 — Deploy to Netlify

**Option A — No terminal (drag and drop):**
1. Download this repo as a ZIP → extract it
2. Go to [app.netlify.com](https://app.netlify.com) → Add new site → Deploy manually
3. Drag the extracted folder onto the deploy area
4. Go to Site configuration → Environment variables → Add variable:
   - Key: `ANTHROPIC_API_KEY`
   - Value: your key from Step 1
5. Deploys → Trigger deploy → Deploy site

**Option B — Netlify CLI:**
```bash
npm install -g netlify-cli
netlify login
netlify deploy --prod
```

### Step 3 — Custom domain (optional)

Buy a domain (~₹800/year from Namecheap or GoDaddy) and connect it in Netlify → Domain management. Netlify handles SSL automatically.

---

## How it works

```
User's browser
  └─ Reads resume + JD into JavaScript memory (never written to disk)
  └─ Sends text to /api/analyze (your Netlify function)
        └─ Netlify function adds your API key + forwards to Anthropic
              └─ Anthropic processes and returns analysis
        └─ Result returned to browser
  └─ Results displayed, then discarded when tab closes
```

**No database. No user accounts. No logging of resume content.**

The Netlify function sends `anthropic-beta: data-retention-none` with every request — Anthropic will not store the content.

---

## The AI prompt (full, unedited)

This is the exact prompt sent to Claude for every analysis. Nothing hidden.

```
You are a senior resume coach and ATS optimization expert. Perform a thorough
analysis and return ONLY valid JSON — no markdown fences, no explanation, no preamble.

Return this exact JSON structure:
{
  "atsScore": <integer 0-100, be honest not inflated>,
  "atsGrade": "<Excellent|Good|Fair|Needs Work|Poor>",
  "summary": "<2-3 honest sentences on fit quality and biggest issues>",
  "suggestions": [
    "<specific actionable suggestion>",
    "<specific actionable suggestion>",
    "<specific actionable suggestion>",
    "<specific actionable suggestion>"
  ],
  "foundKeywords": ["<keyword from JD present in resume>", ...up to 8],
  "missingKeywords": ["<important keyword from JD missing from resume>", ...up to 6],
  "scoreBreakdown": [
    {"category": "Keyword match", "score": <0-100>, "note": "<1 sentence>"},
    {"category": "Experience relevance", "score": <0-100>, "note": "<1 sentence>"},
    {"category": "Skills alignment", "score": <0-100>, "note": "<1 sentence>"},
    {"category": "Resume formatting", "score": <0-100>, "note": "<1 sentence>"}
  ],
  "breakdownAdvice": "<2-3 sentences of specific next steps based on the score breakdown>",
  "bulletImprovements": [
    {
      "before": "<actual bullet from resume>",
      "after": "<improved version with metric and action verb>",
      "why": "<1 sentence explaining the improvement>"
    }
    // ... 5 bullets total
  ],
  "tailoredResume": "<complete rewritten resume, preserving real experience,
                      integrating missing keywords naturally, stronger bullets throughout.
                      No placeholders — real content only. Format with clear sections.>"
}

RESUME:
[first 6000 characters of resume text]

JOB DESCRIPTION:
[first 3500 characters of JD text]
```

That's it. No hidden instructions to upsell, inflate scores, or withhold information.

---

## Project structure

```
resumeai/
├── public/
│   └── index.html              # Entire frontend (single file)
├── netlify/
│   └── functions/
│       └── analyze.js          # Secure API proxy — never exposes your key
├── netlify.toml                 # Routing: /api/analyze → function
├── .env.example                 # Template for local development
├── .gitignore
└── README.md
```

## Local development

```bash
npm install -g netlify-cli
cp .env.example .env
# Add your ANTHROPIC_API_KEY to .env
netlify dev
# Open http://localhost:8888
```

## Why free and open-source?

Most resume sites show you a percentage score then lock the details behind a $30/month
subscription. That's not a product — it's a dark pattern. The job market is hard enough.

This project will stay free. If it helped you land an interview, consider:

- ☕ [Buy me a coffee](https://buymeacoffee.com) *(update link)*
- 💜 [GitHub Sponsors](https://github.com/sponsors) *(update link)*
- ⭐ Star the repo — it helps others find it

## Contributing

PRs welcome. Open an issue for bugs or feature ideas.

Areas that would most help users:
- DOCX parsing support (mammoth.js)
- Cover letter generator tab
- Multiple resume versions for different roles
- LinkedIn profile analyzer

## License

MIT — use it, fork it, build on it, run it commercially. Just don't lock it behind a paywall.

---

*Built with [Claude](https://anthropic.com) · Hosted on [Netlify](https://netlify.com)*

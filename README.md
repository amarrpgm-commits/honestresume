# HonestResume

Free, open-source AI resume analyzer. ATS scoring, keyword gap analysis, bullet rewrites, recruiter heatmap, and a fully tailored resume — no paywalls, no sign-up, no tricks.

**Live:** [honestresumes.in](https://honestresumes.in)

## What it does

- **ATS Score** — honest 4-category breakdown (keyword match, experience, skills, formatting)
- **Keyword Gap Analysis** — which JD terms are in your resume, which are missing
- **Bullet Rewrites** — AI-improved with stronger verbs and quantified impact
- **Recruiter Heatmap** — section-by-section rating: strong, needs work, weak
- **Radar Chart** — 5-axis visual profile
- **Tailored Resume** — full rewrite with diff view, PDF + DOCX download
- **Cover Letter, 60-sec Pitch, LinkedIn About, Interview Questions, STAR Stories** — one-click generators

## Stack

- Single `public/index.html` — vanilla HTML/JS, no framework
- Netlify Functions (`netlify/functions/analyze.js`) — serverless API proxy
- Claude Haiku API (Anthropic) — AI analysis
- Supabase — anonymous analysis history
- GitHub → Netlify auto-deploy

## Run locally

npm install -g netlify-cli
netlify dev

Add your API key in Netlify environment variables:

ANTHROPIC_API_KEY=your_key_here

## Contributing

PRs welcome. Open an issue first for anything beyond small fixes.

## License

MIT

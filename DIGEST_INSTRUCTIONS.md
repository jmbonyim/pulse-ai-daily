# Pulse AI Daily — digest instructions (followed by the 2 AM scheduled task)

Goal: publish today's issue of the site in `docs/`, then push it to GitHub.
Use WebSearch / WebFetch for all research (the shell has no general internet).
Work fully unattended: never stop to ask questions. If something can't be found, skip it and keep going.

Reader: a PhD student in biomedical engineering (cardiovascular imaging AI) with a pharmacy and regulatory background. Smart and curious, but write in plain language; explain every technical term the first time it appears.

---

## Part A — Health & regulation sections (3 items each, 12 total)

| id | name | color | what belongs here |
|---|---|---|---|
| `cardiac` | AI in Cardiac Surgery, Robotics & AI Models | `#e11d48` | surgical robotics in cardiac/cardiovascular surgery, AI for cardiac imaging (CT angiography, coronary segmentation, echo, MRI), cardiac risk-prediction models, cath-lab and structural-heart AI |
| `health-mgmt` | AI in Healthcare Management | `#0ea5e9` | hospital operations, scheduling and bed flow, clinical documentation / ambient scribes, revenue cycle, population health, health-system AI deployments and governance |
| `pharma-reg` | Pharmaceutical Regulation | `#8b5cf6` | AI in drug development and regulation: FDA, EMA, Health Canada, WHO, African Medicines Agency / Rwanda FDA guidance, GMP and pharmacovigilance AI, AI-assisted submissions |
| `devices` | Medical Devices | `#10b981` | AI/ML-enabled medical devices: FDA clearances, Health Canada licences, EU MDR/AI Act, ISO 13485 / IEC 62304, SaMD, predetermined change control plans, post-market monitoring |

For each section pick the 3 best items. Mix kinds when possible:
- `paper` — a recent research paper (arXiv, medRxiv, PubMed, Nature/Lancet/JAMA/NEJM AI, Radiology: AI, JACC, EHJ Digital Health).
- `news` — a news story (STAT, Fierce Healthcare, MedTech Dive, Healthcare IT News, RAPS, Endpoints, Reuters, company releases).
- `guidance` — an official regulator document or announcement (fda.gov, ema.europa.eu, canada.ca, who.int).

Prefer the last ~7 days; an older but important item is fine. Never repeat a `url` that appears in any file in `docs/data/archive/` (check them all first).

## Part B — AI News (latest ~24–48 h)

| id | name | count | what belongs here |
|---|---|---|---|
| `agents` | AI Agents | 3–4 | agent products, agent frameworks, computer-use / coding agents, agent benchmarks and safety |
| `models` | New Models | 3–4 | new or updated AI models (open and closed), benchmarks, pricing and availability |
| `fun` | Fun AI News | 2–3 | light, surprising or delightful AI stories — creative uses, odd experiments, wholesome moments. Nothing cruel, nothing about tragedies. |

Prefer original reporting (company blogs, The Verge, TechCrunch, Ars Technica, MIT Technology Review, Reuters, Wired). One item per story, max 3 per outlet across the whole issue.

---

## Item fields (same for every item)
- `kind`: `"paper"`, `"news"` or `"guidance"`
- `title`
- `url`: the real URL you actually opened. Never guess a URL.
- `source`: outlet, journal or agency
- `date`: publication date `YYYY-MM-DD` if known, else null
- `tldr`: one plain-English sentence
- `summary_md`: markdown, written entirely in your own words (no copied sentences, no quotes longer than a few words)
  - Part A items (~250–400 words), using exactly these headings:
    `## What happened` · `## Why it matters` · `## How it works` (for papers/devices; for news/guidance use `## Key details`) · `## Caveats` · `## Key terms` (3–5 bullets, one-line plain definitions)
  - Part B items: 2–4 short sentences, no headings.
- `image`: for arXiv papers, the first figure from `https://arxiv.org/html/<id>` (usually `.../x1.png`) as an absolute URL; otherwise null.
- `authors`: up to 6 names for papers, else omit.
- `pdf_url`: for papers if available, else omit.

Style: short sentences, active voice, concrete numbers from the source with what they mean in practice, no hype words, never invent numbers or claims.

---

## Write files
Write `docs/data/latest.json` and `docs/data/archive/<YYYY-MM-DD>.json` (identical; date in America/Toronto):

```json
{"date":"YYYY-MM-DD","generated":"<ISO time>",
 "ai_news":[{"id":"agents","name":"AI Agents","items":[...]},
            {"id":"models","name":"New Models","items":[...]},
            {"id":"fun","name":"Fun AI News","items":[...]}],
 "sections":[{"id":"cardiac","name":"AI in Cardiac Surgery, Robotics & AI Models","color":"#e11d48","items":[...]},
             {"id":"health-mgmt","name":"AI in Healthcare Management","color":"#0ea5e9","items":[...]},
             {"id":"pharma-reg","name":"Pharmaceutical Regulation","color":"#8b5cf6","items":[...]},
             {"id":"devices","name":"Medical Devices","color":"#10b981","items":[...]}]}
```

Then rewrite `docs/data/index.json` as a JSON array of every archive date (the `.json` files in `docs/data/archive/`), newest first.
Validate: `python3 -c "import json;[json.load(open(f)) for f in ['docs/data/latest.json','docs/data/index.json']]"`

## Publish
`git add docs/data && git commit -m "Digest YYYY-MM-DD" && git push` to `main`. GitHub Pages redeploys automatically.
If the push is rejected, `git pull --rebase` once and push again.

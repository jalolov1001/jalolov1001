<h1 align="center">Asadbek Jalolov</h1>

<p align="center">
  Full-stack developer in Tashkent, Uzbekistan.<br>
  I design, build and ship products end-to-end — schema, backend, frontend, billing, deploy.
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/asadbek-jalolov/"><img alt="LinkedIn" src="https://img.shields.io/badge/LinkedIn-asadbek--jalolov-0A66C2?style=flat-square&logo=linkedin&logoColor=white"></a>
  <a href="mailto:asadbekjalolov66@gmail.com"><img alt="Email" src="https://img.shields.io/badge/Email-asadbekjalolov66%40gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white"></a>
  <a href="https://yozamiz.uz"><img alt="yozamiz.uz" src="https://img.shields.io/badge/live-yozamiz.uz-f0a83c?style=flat-square"></a>
</p>

---

Most developers with my time in the field have a portfolio site and a todo app.
I have two products that people actually use, and I built both of them to production myself.

## Products

### [yozamiz.uz](https://yozamiz.uz) — document generation platform · live since August 2026

Turns a prompt into a **fully formatted `.docx`** — title page, generated table of contents,
bibliography, exact typography and line spacing. The output has to be *correct*, not merely
plausible, because a university rejects a document over margins.

Designed, built and shipped **alone**: architecture, backend, frontend, database, billing and deploy.

- Deterministic DOCX generation against strict formatting rules, in **4 languages** (Uzbek, Russian, English, French)
- Verified across Word, **WPS and LibreOffice** — those two never refresh document fields, so every computed result (the TOC included) is pre-rendered rather than left as a field
- **Credit ledger**: per-document pricing, signup bonus, top-ups, and automatic refunds when a generation fails — including failures where the process itself dies
- Document storage with a 90-day retention window, re-download, and scheduled cleanup
- Runs on **FastAPI + Next.js + Supabase/Postgres**, Docker behind Caddy on a DigitalOcean box, with Sentry and cron-driven backups

```
136 commits · 6 weeks · ~27,500 lines (12k Python · 12k JS/JSX · 3.4k SQL)
22 database migrations · 341 backend + 196 frontend tests · 0 TODO/FIXME left in the code
```

### [SlideMind](https://slidemind.uz) — AI presentation generator · 2025–2026

Describe a topic, get a complete designed deck — then edit it in a full browser canvas editor.
Co-founded with a partner; I built the product. It's still running; I've since moved on to yozamiz.uz.

- **Browser canvas editor** with pixel-level control over every slide element — text, images,
  shapes, charts — with drag, resize, restyle, z-ordering and undo/redo
- Generation pipeline: topic prompt → structured deck schema → rendered slides.
  Model output is **validated against a schema**, so a malformed response can never reach the canvas
- One-click export to **PPTX and PDF**, preserving fonts, layout and element positions in both

## How I work with an AI agent

I write the spec and design the schema and the module boundaries; the agent writes most of the
implementation; **I review every diff.** That review step is where I spend most of my time, and
it is the part that decides whether the product works. Three things it caught in yozamiz.uz that
the test suite was perfectly happy with:

| What the review found | Why it mattered | Fix |
| --- | --- | --- |
| **Double charge on retry** | A student on a bad mobile connection reloads and taps *Generate* again while the first task is still finishing in the background — charged twice, two identical documents | Partial unique index on `(user_id, idempotency_key)` + duplicate detection inside the RPC, key held client-side across a reload |
| **Refund lived inside the request handler** | If the process died mid-generation (OOM, reboot, a deploy past the grace period), the money was gone with no document, no refund, and nothing visible in the UI | Recovery moved into the database as a `pg_cron` job — it must not depend on the server that just died |
| **RLS policy shipped without its `GRANT`** | Every admin, owner included, was silently locked out of the panel while the backend tests kept passing — the backend connects as `service_role`, so it never saw the failure | Table-level `GRANT` added; in Postgres, RLS is a filter that runs *after* privileges |

None of these show up as a red test. They show up as money and access — which is why I read
generated code instead of shipping it.

## Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?style=flat-square&logo=supabase&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)

**Also:** REST API design · SQL schema design and migrations · LLM APIs (Anthropic, OpenAI, DeepSeek) ·
Caddy / TLS / DNS · pytest and Vitest · Sentry · Claude Code

**Currently learning:** TypeScript · Redis and background queues · CI/CD with GitHub Actions

## Beyond the code

I ship to production and stay responsible for what happens after — migrations against the live
database, DNS, TLS, monitoring, backups. When the production droplet was deleted out from under
me in August 2026, I rebuilt the server from bare Ubuntu to live HTTPS and re-verified every
endpoint from the outside.

My degree is **Digital Economics** at Tashkent University of Information Technologies
(TUIT, 2022–2026, GPA 4.22/5.0) — algorithms, databases and operating systems alongside
econometrics and statistics. It means I can argue a product decision with unit economics
instead of opinions.

**Languages:** Uzbek (native) · Turkish (fluent) · English (B1 — clear in writing, improving weekly)

## Open to

Remote full-time or contract work — backend or full-stack — on a small team where shipping
matters more than process.

<p align="center">
  <a href="mailto:asadbekjalolov66@gmail.com">asadbekjalolov66@gmail.com</a> ·
  <a href="https://www.linkedin.com/in/asadbek-jalolov/">LinkedIn</a>
</p>

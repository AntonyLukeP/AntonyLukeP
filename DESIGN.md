# Design rationale — SYSTEM.md

This document is the thinking behind the profile in `README.md`. It covers the brainstorm, the chosen concept, the journey, and how every piece is built within actual GitHub README constraints.

A note on those constraints up front, because it shapes every decision below: GitHub sanitizes README HTML. No `<script>`, no `<style>` blocks in the Markdown/HTML itself, no `onclick`, no external JS or CSS files. What *does* work: `<details>/<summary>` (native, no JS), tables, and — the important one — **SVG files rendered via `<img src="...">`**. A `<style>` block and CSS `@keyframes` *inside an SVG file* render and animate fine, because the browser treats the SVG as an image resource, not as README HTML. That single fact is what makes an "alive" profile possible at all, and it's the mechanism behind everything animated here.

---

## 1. Twenty concepts, ranked

1. **Living system status page** *(chosen)* — the profile presents itself as a running distributed system: a status bar, a live topology map, a deploy log instead of a bio, a runbook instead of a skills list.
2. **Postmortem-driven narrative** — "about me" reframed entirely as an incident postmortem template (Summary / Impact / Root Cause / Resolution / Follow-ups), applied to your own career instead of a technical failure.
3. **API specification as profile** — the whole README formatted as an OpenAPI-style spec: endpoints for `/about`, `/projects`, `/contact`, request/response JSON blocks instead of prose.
4. **Compiler pipeline narrative** — the page scrolls like source code moving through lexer → parser → optimizer → codegen stages, each stage mapped to a phase of your engineering growth.
5. **Terminal boot sequence** — an SVG that mimics a machine booting: kernel messages, service startup lines, ending in a login prompt, before the "real" profile content appears below.
6. **Dependency graph as identity** — your skills and projects rendered as an actual `package.json`/`go.mod`-style dependency tree, with "you" as the root package.
7. **Load balancer / traffic router metaphor** — visitors are "routed" through sections framed as backend services, with a visible request path diagram at the top.
8. **Version-controlled self** — the page framed as a `git log`, with commits representing milestones, and a `CHANGELOG.md` structure for growth over time.
9. **Database schema as bio** — an ER diagram where "Engineer" is an entity with foreign keys to "Project," "Skill," and "Incident" tables.
10. **Circuit board / PCB aesthetic** — literal trace-line art connecting components, leaning hardware/embedded rather than cloud-native.
11. **Air traffic control tower** — projects as flights with statuses (boarding / in-flight / landed), a radar-sweep animation as the hero.
12. **Space mission control** — telemetry readouts, countdown aesthetics; strong visually but risks reading as generic "hacker" sci-fi rather than specifically *you*.
13. **Chess engine evaluation bar** — projects "scored" like chess positions, with an eval bar aesthetic; clever but doesn't generalize well to non-competitive content like contact info.
14. **Kanban / sprint board** — projects shown as tickets moving through To Do → In Progress → Done; too close to a generic project-management template.
15. **DNS resolution chain** — visitor's "request" resolves through a chain of records down to you; a fun one-off idea but hard to sustain across an entire page.
16. **Subway/metro map of your career** — stations as milestones, lines as skill tracks; visually strong, but the metaphor strains once you get to "contact me."
17. **Weather system / forecast** — skills as a five-day forecast; whimsical, undercuts the "I build systems" positioning you explicitly asked for.
18. **Museum exhibit placards** — projects displayed like gallery pieces with placards; elegant but static, doesn't support the "alive" feeling you want.
19. **Video game save file / stats screen** — XP bars and achievement unlocks for skills; reads younger/gamer-coded, works against "no meme culture."
20. **Recipe card format** — skills as "ingredients," projects as "dishes"; playful but actively fights the engineering-precision brand you asked for.

**Why #1 won:** it's the only concept where every section of a real profile — bio, projects, timeline, skills, contact — maps onto something a status page *already has* (status indicator, service catalog, incident history, runbook, API contact block), so nothing feels shoehorned in. It's also the most literal execution of "instead of listing skills, visualize engineering": the whole page *is* a small piece of engineering, not a description of one.

---

## 2. The chosen concept

**A GitHub profile that presents itself as the status page for a running production system, where the system is you.**

Signature element: the **live topology map** (`assets/topology.svg`) — a service graph with a `CORE` node (you) connected to your projects as services, with animated pulses flowing along the edges like requests. It's the one thing a visitor will remember and describe to someone else afterward, which is the actual bar for "memorable."

---

## 3. The visitor's journey, moment by moment

```
0.0s   Profile opens. Status bar renders first — a single green dot,
       "all systems operational." Sets the frame before any text is read:
       this is a system, and it's healthy.

0.3s   Eye moves to the topology map. Pulses are already animating —
       the page feels alive before any scrolling happens, which is the
       "whoa" moment the brief asked for. No click required to see it.

~5s    Reads the /about block. It's four lines, framed as a terminal
       whoami — short enough to finish, specific enough to signal
       "backend/distributed systems person," not "student learning to code."

~15s   Scrolls into /services. Projects are laid out as a service
       catalog with live status tags (healthy / building) instead of
       generic cards — variety the brief explicitly asked for over
       repeated card grids.

~30s   /timeline reads like a deploy log, not a resume bullet list.
       Confirms the person ships continuously, not just "has done things."

~45s   /runbook — skill icons are gated behind <details>, so the page
       doesn't front-load a wall of badges. Visitor chooses to expand it,
       which raises engagement (opt-in interaction beats passive scroll).

~60s   /metrics — real GitHub stats, styled to match the dashboard's
       palette instead of default badge colors. Proof layer: everything
       claimed above is now backed by actual numbers.

~75s   The "expand debug console" detail is visible but unopened.
       Curiosity gap — most visitors who made it this far will open it.

~90s   Debug console reveals a note that directly acknowledges the
       reader's own behavior ("you read the whole thing") and turns that
       observation into the pitch, without ever saying "hire me."

~100s  /contact rendered as a POST request body — final callback to the
       API framing established in the very first section, closing the loop.
```

The throughline: **every section reinforces the same metaphor instead of switching styles**, which is what makes it read as one designed product instead of a stack of separate README widgets.

---

## 4. Wireframe (ASCII)

```
┌────────────────────────────────────────────────────────────┐
│ ● all systems operational   focus: distributed systems ...  │  status bar
├────────────────────────────────────────────────────────────┤
│                                                                │
│                    SYSTEM.md                                  │
│               a person, running in production                │
│                                                                │
│     [ CORE ]───────[ HELIOS ]                                 │  topology
│        │  \──────[ AEGIS ]                                    │  (animated)
│        │  \──────[ AI AGENTS ]                                │
│        │  \──────[ BACKEND ]                                  │
│         \────────[ FULL STACK ]                               │
├────────────────────────────────────────────────────────────┤
│  GET /about   →  terminal-style whoami block                  │
├────────────────────────────────────────────────────────────┤
│  GET /services → [ helios ]      [ aegis ]                    │  2x2
│                  [ agent-runtime][ full-stack ]                │  service grid
├────────────────────────────────────────────────────────────┤
│  GET /timeline → deploy log (latest, -1, -2, -3 ...)          │
├────────────────────────────────────────────────────────────┤
│  GET /runbook  → collapsible: design philosophy / stack /     │
│                  reading habits                                │
├────────────────────────────────────────────────────────────┤
│  GET /metrics  → stats card | top languages | activity graph  │
├────────────────────────────────────────────────────────────┤
│  ▸ expand debug console (easter egg)                          │
├────────────────────────────────────────────────────────────┤
│  POST /contact → JSON block with email / linkedin / response  │
└────────────────────────────────────────────────────────────┘
```

---

## 5–7. What each section does, why it's engaging, why recruiters remember it

| Section | Job | Psychological hook | Recruiter takeaway |
|---|---|---|---|
| Status bar | Frame-setting in under 1 second | Primacy effect — the first thing seen sets interpretation of everything after | "This person thinks in uptime and reliability." |
| Topology map | The signature "whoa" moment | Motion draws pre-attentive attention before any reading starts; it's *proof by demonstration* of systems thinking, not a claim of it | Visually distinct enough to be the thing they describe to a colleague — "you have to see this one profile" |
| `/about` | Fast, specific positioning | Terse copy reads as confidence; padding reads as insecurity | Confirms specialization (backend / distributed systems) in five seconds, not fifty |
| `/services` | Replaces repetitive cards with status semantics | Status tags (`healthy`/`building`) imply ongoing maintenance, not abandoned side projects | Signals these are real, live systems — the thing recruiters actually worry about with student portfolios |
| `/timeline` | Replaces a resume bullet list | Deploy logs read as *continuous* effort, which builds more trust than a static "experience" section | Shows momentum, not just a snapshot |
| `/runbook` | Skills without a badge wall | Opt-in disclosure (`<details>`) creates a small commitment — visitors who click are now more invested | Filters for genuinely curious readers, which are disproportionately the ones who follow up |
| `/metrics` | Objective proof layer | Numbers after narrative land better than numbers first — trust is already partly built | Confirms the story with real activity data |
| Debug console | The easter egg | A curiosity gap deliberately left open in plain sight; reading it feels like discovering something, not being shown something | Directly (and only once) rewards the exact behavior — reading closely — that a hiring manager wants to see in an engineer |
| `/contact` | Closes the loop | Returns to the API metaphor from the top of the page — closure is satisfying and signals design intent, not improvisation | Clear, low-friction next step |

---

## 8–9. Implementation of each component

**Status bar (`assets/status-bar.svg`)** — flat SVG, no external calls needed to render; a blinking status dot uses a CSS `@keyframes opacity` animation inside the SVG's own `<style>`. Embedded with `<img src="assets/status-bar.svg" width="100%">`.

**Topology map (`assets/topology.svg`)** — the signature element. Nodes are `<circle>` + `<text>` groups; edges are Bézier `<path>`s; "packets" are a second `<path>` copy with `stroke-dasharray` + `stroke-dashoffset` animated via `@keyframes flow`, which is the standard trick for a moving-dash / flowing-line effect in pure CSS. No JS, fully GitHub-safe.

**Service catalog** — a 2×2 HTML `<table>` (GitHub allows raw tables in README HTML) rather than four separate Markdown card blocks, so column widths stay locked at 50% and rows align — Markdown-only cards drift out of alignment across different renderers.

**Deploy log / timeline** — a two-column `<table>`, monospace tag in column one, description in column two. Reads like `git log --oneline` without needing an image.

**Runbook** — native `<details>/<summary>`, no JS. The skill icons pull from `skillicons.dev`, a static image service — no account or token required.

**Metrics dashboard** — `github-readme-stats` and `github-readme-activity-graph` (both free, hosted, no auth needed for public repos), with query params recoloring them to the profile's palette (`bg_color`, `title_color`, `text_color`) so they don't look like a bolted-on default badge.

**Debug console / contact** — plain fenced code blocks inside `<details>` and a closing `<table>`/code block; no non-standard rendering required.

---

## 10. Animation suggestions (all SVG-native, all GitHub-safe)

- **Flowing edges** on the topology map — done via `stroke-dasharray`/`dashoffset` (already implemented).
- **Pulse rings** on the core node — a `<circle>` animating `r` and `opacity` outward, like a radar ping, looped with a staggered delay on a duplicate ring for continuous overlap (already implemented).
- **Blinking live dot** on the status bar and topology header — simple `opacity` keyframe blink, signals "this is live," not static art.
- Keep every animation **ambient and slow** (2.5s+ per cycle). Fast/looping motion outside a deliberate hero risks feeling "AI-generated" per the design skill's own warning — restraint is part of the premium read here.

---

## 11. GitHub Actions suggestions

Provided in `.github/workflows/update-status.yml`:

- **`Platane/snk`** — regenerates an animated "snake eating your contribution graph" SVG on a schedule; genuinely popular, well-maintained, and reinforces the "living system" concept since it's your real contribution history in motion.
- **Heartbeat stamp** — a scheduled job that rewrites a timestamp into `status-bar.svg`, so the "live" framing is backed by an actually-updating artifact, not just decorative color.
- Both use `stefanzweifel/git-auto-commit-action`, the standard pattern for Actions that commit generated files back to the repo.

---

## 12. Dynamic data sources (no auth required, all free)

- `github-readme-stats` — commit/PR/issue stats, recolorable via URL params.
- `github-readme-activity-graph` — contribution activity as a line graph.
- `skillicons.dev` — static tech-stack icon rows, theme-able (`?theme=dark`).
- `Platane/snk` (via Action) — animated contribution snake.
- Shields.io — for any additional static badge (license, last commit, followers) styled with `?style=flat-square&color=00D9A3` to match the palette.

---

## 13. Easter eggs

- **Debug console** (shipped): a `<details>` block styled as a log dump that breaks the fourth wall once the visitor has already invested ~90 seconds — rewards exactly the behavior worth rewarding.
- **Future addition — hidden commit message:** make one commit to the repo with a message only visible in the repo's commit history (not the README) that continues the "in-universe" voice, for visitors who click through to the actual repo.
- **Future addition — 404 status easter egg:** if you ever add a second, unlinked file like `assets/incident-report-001.md`, visitors who explore the repo tree (rather than just the rendered README) find a fake postmortem for a bug you actually shipped and fixed — rewards repo exploration specifically, a different behavior than README reading.

---

## 14. Future expansions

- **Real uptime, not decorative:** wire the status bar's "uptime" figure to something real, e.g. days since your last public commit, computed by the same heartbeat Action.
- **Second topology state:** swap in a `?theme=dark`/`light` pair of the topology SVG via `<picture>` + `prefers-color-scheme`, so it matches the visitor's GitHub theme instead of always rendering dark.
- **"Incident" case studies:** turn your two or three hardest bugs into short, real postmortems (Summary / Root Cause / Fix) linked from the deploy log — the single highest-signal content you could add, because it's the most specific, least fakeable evidence of real engineering.
- **Visitor-triggered "load"**: none of this needs JS to be worth doing — the honest next step once you outgrow README limits entirely is a small companion site (Aegis's own dashboard, publicly deployed) that the profile links out to, so the "observability platform" project literally proves itself by being live.

---

## Setup checklist

1. Replace `YOUR_USERNAME` in `README.md` and `update-status.yml` with your actual GitHub handle.
2. Replace the four `[→ inspect repo]` links with real repo URLs.
3. Fill in real `email` / `linkedin` values in the `/contact` block.
4. Commit `assets/topology.svg` and `assets/status-bar.svg` alongside the README — GitHub renders local repo images fine in profile READMEs.
5. Add `.github/workflows/update-status.yml` if you want the snake graph and heartbeat automation; otherwise the profile works fully static with zero Actions.

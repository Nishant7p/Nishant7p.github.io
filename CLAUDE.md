# Portfolio — Nishant Tomer

## Identity
Single-file portfolio (`index.html`, ~4250 lines, ~340KB) deployed on **GitHub Pages**. Zero build process — pure vanilla HTML/CSS/JS. Design: "Personal OS v3.0" dark terminal aesthetic with sidebar navigation, custom cursor, knowledge graph, and recruiter-optimized layout.

**Owner:** Nishant Tomer, 3rd year B.Tech CSAM at IIIT-Delhi (2023355), graduating 2027. Targeting SDE / ML Engineer placements at 1L+/month. Strongest domains: iOS (SwiftUI), AI/NLP (Whisper+Pyannote), Full-Stack Web (React+Node+PostgreSQL).

## Architecture — DO NOT CHANGE
- **Single file**: All CSS, HTML, JS, and data live in `index.html`. Do NOT extract to separate files.
- **Data in JS arrays**: Projects, certs, semesters, achievements, thoughts all stored as `const` arrays in the `<script>` block.
- **Hardcoded HTML**: Skills chips, experience timeline, education cards, home page stats are raw HTML — not driven by JS arrays.
- **Knowledge graph**: `KG_NODES` + `KG_EDGES` + `KG_META` define an interactive skill/project graph on the home page AND the full-page graph.
- **Images — primary**: Stored in the repo under `assets/` and served via `raw.githubusercontent.com`. This is now the default for all new images.
- **Images — legacy**: Older entries use postimg.cc / ibb.co / image2url.com URLs. Leave them unless they 404.
- **Analytics**: Supabase integration for view counting (secret "views" keyboard shortcut).

---

## Pages (11 total)

| Page | `data-p` | Notes |
|------|----------|-------|
| Overview / Home | `home` | Hero, stats, career timeline, featured work, KG preview |
| Education | `education` | Not in sidebar by default; accessible via nav |
| Academic Log | `academic` | Semester tabs + SGPA/CGPA SVG charts |
| Experience | `experience` | Timeline `.tli` blocks |
| Projects | `projects` | Filter + card grid rendered from PROJECTS array |
| Skills | `skills` | Chip groups + radar chart + domain donut + CP bar + proficiency bars |
| Certifications | `certifications` | Card grid from CERTS array |
| Achievements | `achievements` | LC rating chart + list from ACHIEVEMENTS array |
| Thoughts | `thoughts` | List from THOUGHTS array |
| Leadership | `responsibility` | Hardcoded cards |
| Knowledge Graph | `graph` | Full-page interactive KG with physics, zoom/pan, path finder |

---

## File Structure Map

### Repo Layout
```
Nishant7p.github.io/
├── index.html                  ← entire portfolio (single file)
├── CLAUDE.md                   ← this file (not served, local only)
└── assets/
    └── certs/
        ├── learnquest-ai-science/
        │   ├── specialization.png
        │   ├── mod1-datascience-sklearn.png
        │   ├── mod2-ml-models-science.png
        │   ├── mod3-neural-networks-rf.png
        │   └── mod4-drug-discovery.png
        └── hackerrank/
            └── python-basic.png
```

**Asset URL pattern:**
`https://raw.githubusercontent.com/Nishant7p/Nishant7p.github.io/main/assets/certs/<folder>/<file>.png`

**Adding new cert images:** Drop PNGs in `assets/certs/<issuer-slug>/`, `git add assets/ && git commit && git push`.

---

### JS Data Arrays (search by anchor text — line numbers shift as content grows)

| Data | Anchor Text | ~Line | Current Count |
|------|------------|-------|---------------|
| Projects | `const PROJECTS = [` | ~1450 | 10 (P-001 to P-010) |
| Certifications | `const CERTS = [` | ~1560 | 7 |
| Semesters | `const SEMESTERS = [` | ~1600 | 6 (Sem I–VI) |
| Thoughts | `const THOUGHTS = [` | ~1775 | 5 |
| Achievements | `const ACHIEVEMENTS = [` | ~1785 | 6 |
| Tech Metadata | `const TECH_META = {` | ~1795 | ~50 techs |
| KG Nodes | `const KG_NODES = [` | ~1845 | ~100 nodes |
| KG Edges | `const KG_EDGES = [` | ~2040 | ~200 edges |
| KG Metadata | `const KG_META = {` | ~2235 | ~100 entries |

### Hardcoded HTML — Count Sync Points

These locations contain hardcoded numbers/text that MUST be updated when counts change:

| What | Where to Search | Notes |
|------|----------------|-------|
| Sidebar: Academic badge | `Academic Log <span class="nb">6 Sem</span>` | Update when new sem added |
| Sidebar: Experience badge | `Experience <span class="nb">3</span>` | Update when new role added |
| Sidebar: Projects badge | `Projects <span class="nb">10</span>` | Update when project added |
| Sidebar: Certs badge | `Certifications <span class="nb">7</span>` | Update when cert added |
| Topbar: CGPA + Sem | `CGPA 7.33 · Sem VI` | Search `tp-info` |
| Home: CGPA stat | `data-count="7.33" data-float="2"` | |
| Home: DSA stat | `data-count="500"` (display: `500+`) | |
| Home: LeetCode stat | `data-count="1850"` (display: `1850+`) | |
| Home: Projects stat | `data-count="10"` (display: `10`) | |
| Home: Internships stat | `data-count="3"` | |
| Home: Career timeline | `.career-strip` → `.cs-track` nodes | Update when new role/milestone; search `cs-node` |
| Home: Featured strip "View all" | `View all 10 →` | |
| Home: 3 featured star-cards | `<div class="star-card"` blocks | |
| Home: Recruiter panel | `.rec-panel` with domain/roles | Search `rec-cell` |
| Home: Overview chips | `.ov-skills .chips` | Shows PRIMARY STACK (not stats). Currently: SwiftUI·Combine, PyTorch·Whisper, React·PostgreSQL, Python·Java·Swift, CUDA, Unreal·libGDX |
| Skills: 6 chip groups | `<div class="sg">` blocks | |
| Skills: LeetCode Peak | `<span class="cp-v">1850+` | |
| Skills: Problems Solved | `<span class="cp-v">500+` | |
| Skills: HackerRank | `5★ × 3` | |
| Skills: Cert count | `<span class="cp-v">7</span>` | |
| Skills: Domain donut | `renderDomainDonut()` in JS — segments array | Update counts when skills category changes significantly |
| Skills: Proficiency bars | `renderProficiency()` in JS — bars array | Update pct/level when skill improves |
| Projects: Filter "All" | `All (10)` | |
| KG_META: Core node desc | `desc:'IIIT-Delhi CSAM · B.Tech 2023–27 · CGPA 7.33'` | |
| Meta: description | `<meta name="description" content="...">` | ~line 9 |
| Meta: OG/Twitter tags | `og:title`, `og:description`, `twitter:*` | ~lines 10-16 |
| Sidebar: Online status | `Available · New Delhi` | ~line 664 |
| Sidebar: Footer ID | `2023355 · IIIT-Delhi · CSAM` | ~line 689 |
| Home: Left role text | `IIIT-Delhi · CSAM · 2023–2027` | |
| Home: OS banner | `Personal OS · IIIT-Delhi · 2023–2027` | |
| Typewriter tagline | `typeWriter(taglineEl, 'B.Tech student at IIIT-Delhi...'` | |
| Contact: availability.json | `"internship": true` / `"notice_period": "immediate"` | |
| Recruiter: Current Status | `Open to Work` + `Available Immediately` | |
| Recruiter: Best Domain | `AI/ML + iOS` | |
| Recruiter: Preferred Roles | `SDE · ML Eng.` | |
| Recruiter: Notice Period | `Immediate` | |
| Footer | `2023355 · IIIT-Delhi · CSAM · 2023–2027` | |

---

## Visual Components (added Apr 2026)

These are non-data UI features. Don't remove or re-add them accidentally.

### Overview / Home page
| Component | How it works | Search anchor |
|-----------|-------------|---------------|
| Hero particles | Canvas animation — 55 dots + 12 streaks drifting upward. Pauses when not visible. | `id="heroParticles"` / `initHeroParticles()` |
| Photo scan-line | CSS `::after` on `.ov-photo-wrap` — green beam sweeps down photo on loop | `scanBeam` keyframe |
| Terminal cursor | Blinking block cursor after typewriter tagline | `class="term-cursor"` |
| Chip shimmer | `.chip.hi` elements have animated green shimmer sweep every 4s | `chipShimmer` keyframe |
| Career timeline strip | `.career-strip` between recruiter panel and featured work. Nodes: 2023→Jan'25→Jun'25→Aug'25→Jan'26→2027. Update when new role/milestone added. | `class="career-strip"` |
| Hire Me pulse | `.ov-btns .btn-p` has pulsing ring animation | `hirePulse` keyframe |
| Star-card shine | Sweep animation on hover for `.star-card` | `scSweep` keyframe |
| Stat tile hover | `.ov-stat:hover` glows green | CSS only |
| KG Expand button | `class="kg-expand-btn"` — green filled CTA with pulse ring, navigates to graph page | `kg-expand-btn` |

### Skills page
| Component | How it works | Search anchor |
|-----------|-------------|---------------|
| Domain proficiency radar | 6-axis canvas radar chart | `id="radarChart"` / `renderRadarChart()` |
| Domain distribution donut | Canvas donut showing tech count by category (AI/ML:19, iOS:8, Web:9, Systems:5, Game:4, Tools:8). Update counts in `renderDomainDonut()` segments array if skills categories shift significantly. | `id="domainDonut"` / `renderDomainDonut()` |
| Proficiency bars | Color-coded bars by level: green=Expert, blue=Advanced, purple=Intermediate, grey=Familiar. Update `renderProficiency()` bars array when skill level changes. | `id="profBars"` / `renderProficiency()` |
| Competitive stats bar | CP bar with LeetCode/DSA/HackerRank/Certs with animated progress fill | `.cp-bar` / `.cp-prog-fill` |

### Achievements page
| Component | How it works | Search anchor |
|-----------|-------------|---------------|
| LC Rating Journey chart | Canvas line chart showing LeetCode rating over time | `id="lcChart"` / `renderLCChart()` |

### Knowledge Graph pages
| Component | How it works | Search anchor |
|-----------|-------------|---------------|
| Overview KG | ~800×640px canvas, hover highlights connected nodes, filter bar, path finder | `id="kgCanvas"` / `buildKG()` |
| Full-page KG | `page-graph` — 2200×1700px virtual canvas, zoom/pan, physics toggle, path finder, same CSS hover rules as overview KG via `.kg-canvas` class | `id="fkgCanvas"` / `buildFullKG()` |
| Hub-node pulse | High-degree nodes (deg≥10) get `hub-node` class with glow animation | `hubPulse` keyframe |

### Global
| Component | How it works |
|-----------|-------------|
| Command palette | Cmd+K opens fuzzy search across pages, projects, semesters, KG nodes | `id="cmdOverlay"` / `openCmdPalette()` |
| Recruiter mode | Toggle in sidebar hides non-recruiter nav items | `toggleRecruiterMode()` |
| Smooth scroll | Lenis v1.1.18 via CDN | `window.__lenis` |
| Custom cursor | CSS cursor hidden; JS-driven green dot + ring | `.cursor` / `.cursor-ring` |

---

## CRITICAL RULE: No Redundancy on Overview

The overview home page has a specific information hierarchy. Each element shows DIFFERENT info:
- **Stats row** — the ONLY place for raw numbers (CGPA, DSA count, LC rating, project count, internship count)
- **Overview chips** — PRIMARY TECH STACK (SwiftUI, PyTorch, React, etc.) — NOT stats, NOT ratings
- **Career timeline strip** — chronological STORY of roles/milestones — no numbers
- **Nav cards** — qualitative description of each section — no number badges
- **Recruiter panel** — status/availability/domain/roles — qualitative
- **Featured work** — 3 best projects with impact metrics

**Never repeat LC rating / DSA count / project count outside the stats row.** If something is in the stats, don't put it in chips, nav cards, or career timeline too.

---

## CRITICAL RULE: Cross-Section Updates

**NEVER update just one section.** Every update ripples across multiple sections. If a project uses React and React isn't in the skills section yet — add it. If a new certification involves a tech not in TECH_META — add it. If an achievement changes a stat shown on the home page — update the stat.

Always trace the full impact chain. The portfolio's strength is its interconnectedness.

---

## What to Provide — Checklists

When you tell me about an update, here's what I need from you. I'll ask for anything missing.

### For a New Project
- **Title** (short, punchy — e.g., "AI Clinical Scribe", not "My BTP Project")
- **1-2 line description** (what it does, who it's for)
- **5-6 bullet points** of key contributions/features (what YOU built, not what the app does)
- **Tech stack** (every technology, framework, library used)
- **Type**: Internship / Research / Academic / Personal
- **Year**: When built
- **Links**: GitHub repo URL, live demo URL, YouTube demo, etc.
- **Images**: Thumbnail image URL + 3-5 gallery screenshots (upload to postimg.cc/ibb.co first, give me the URLs)
- **Tags**: Which filters should show this? (ios, ai, web, game, fullstack, etc.)

### For a New Skill/Technology
- **Name** (exact — "Kubernetes", not "k8s stuff")
- **Category**: Which skill group? (AI, iOS, Web, Tools, Language, etc.)
- **Proficiency level**: Primary (`.chip.hi`) or secondary (`.chip`)?
- **Context**: How did you learn it? (project, course, self-study) — helps me cross-reference

### For a New Certification
- **Full cert name** and **issuer** (e.g., "AWS Solutions Architect — Amazon Web Services")
- **Certificate image(s)**: Drop PNG screenshot(s) in `assets/certs/<issuer-slug>/` and push — then use the raw.githubusercontent.com URL. No need for ibb.co anymore.
- **Verification link** (if available)
- **1-line description** of what it covers
- **Sub-modules** (if it's a specialization with multiple courses — include a PNG for each)

### For a New Internship/Role
- **Company name**, **role title**, **team size**
- **Date range** (e.g., "Jan 2026 – Jun 2026")
- **5-6 bullet points** of what you did (use action verbs, include metrics)
- **Tech stack** used
- **Documents**: Experience letter URL, LOR URL (if available)
- **Status badge**: "FEATURED" / custom text

### For an Achievement
- **Title** (e.g., "LeetCode Peak: 2000+ Rating")
- **Detail** (2-3 sentences explaining the achievement)
- **Category chip**: Research / Competitive / Internship / Teaching / Certification
- **Month and year**

### For CGPA / Semester Update
- **New CGPA** and **SGPA** for the semester
- **Course list** with: code, name, grade, grade points
- For each course (optional but makes it rich): description, topics covered, what you learned, how you applied it

### For a Thought/Blog Entry
- **Title**, **date**, **tags**
- **2-3 sentence excerpt** (the actual blog content isn't rendered, just the preview)

---

## Update Workflows

### WF-1: Add New Project

**Trigger:** "I built a new project", "add this project", etc.

1. **PROJECTS array** — Add entry. Use next sequential ID (current last: P-010, next: P-011).
   ```js
   {id:'P-011', year:'2026', title:'...', img:'...', gallery:['...'],
    desc:'...', points:['...','...'], stack:['React','Node.js'],
    type:'personal', typeLabel:'Personal', tags:'personal web fullstack',
    links:[{l:'GitHub',u:'...'},{l:'Live',u:'...'}]}
   ```
2. **TECH_META** — Add any new technologies not already present: `'TechName':{cat:'Web',col:'#00ff88'}`
3. **KG_NODES** — Add project node: `{id:'proj_short', label:'Title', cls:'proj', x:XX, y:YY}`. Check KG Zone Map below.
4. **KG_EDGES** — Connect to tech nodes, domain nodes, and course nodes.
5. **KG_META** — Add: `proj_short: {type:'Project', tag:'domain', desc:'1-line summary'}`
6. **Sidebar badge** — Change `Projects <span class="nb">10</span>` → `11`
7. **Home stats** — Change `data-count="10"` → `data-count="11"`
8. **Home nav card** — `P-001 → P-010` → `P-001 → P-011`
9. **Featured strip** — `View all 10 →` → `View all 11 →`
10. **Project filter** — `All (10)` → `All (11)`
11. **Featured strip cards** — Ask user: "Should this replace one of the 3 featured projects?"
12. **LinkedIn** — Suggest post if project is substantial (has demo, real users, or novel tech).

### WF-2: Add New Skill/Technology

**Trigger:** "I learned Docker", "add Kubernetes to my skills", etc.

1. **Skills page chips** — Add `<span class="chip">Name</span>` to the correct `.sg` group:
   - Expertise Domains → first `.sg`
   - Programming Languages → second `.sg`
   - AI & Data Science → third `.sg`
   - iOS / Mobile → fourth `.sg`
   - Web & Databases → fifth `.sg`
   - Tools & Platforms → sixth `.sg`
   - Use `.chip.hi` if it's a primary/strong skill.
2. **TECH_META** — Add `'Name':{cat:'Category',col:'#hex'}`.
3. **KG_NODES** — Add: `{id:'short', label:'Name', cls:'tech', x:XX, y:YY}`. Place near related domain cluster.
4. **KG_EDGES** — Connect to relevant domain nodes and related tech.
5. **`renderProficiency()` bars array** — Add if it's a language/framework worth showing on the bar chart.
6. **`renderDomainDonut()` segments array** — Update the category count if this tech adds meaningfully to a domain.
7. **Home overview chips** (`.ov-skills .chips`) — Only replace an existing chip if this becomes a headline skill.
8. **LinkedIn** — Only for significant additions (new language, major framework).

### WF-3: Update CGPA / New Semester

**Trigger:** "My CGPA is now 7.5", "Sem 6 results are out", etc.

1. **Topbar** — Update `CGPA X.XX · Sem Y` (search: `tp-info`)
2. **Home stats** — Update `data-count="X.XX"` and display text
3. **Education page** — Update CGPA in two places (main card + stats grid)
4. **Education page** — Update "V Semesters completed" count if new semester
5. **KG_META core node** — Update `desc:'IIIT-Delhi CSAM · B.Tech 2023–27 · CGPA X.XX'`
6. **If new semester:** Add to `SEMESTERS` array with all courses. Update sidebar badge "6 Sem" → "7 Sem".
7. **Academic charts** — Auto-update from SEMESTERS data via `renderAcademicCharts()`.
8. **LinkedIn** — Only if CGPA improved by 0.3+ or crossed milestone (7.5, 8.0, 9.0).

### WF-4: Add New Certification

**Trigger:** "I completed AWS cert", "got Google Cloud certified", etc.

1. **Images first** — Drop PNG(s) in `assets/certs/<issuer-slug>/`. Name them clearly (`specialization.png`, `mod1-topic.png`, etc.). Push the assets commit before or together with the index.html commit.
2. **CERTS array** — Add entry using raw.githubusercontent.com URL:
   ```js
   {name:'Cert Name', issuer:'Issuer',
    img:'https://raw.githubusercontent.com/Nishant7p/Nishant7p.github.io/main/assets/certs/<folder>/specialization.png',
    fallback:'Alt text', desc:'Description', verify:'url',
    subs:[{img:'raw...url', label:'Module 1: ...'}], extra:''}
   ```
3. **KG_NODES** — Add: `{id:'cert_short', label:'Name', cls:'cert', x:XX, y:YY}`
4. **KG_EDGES** — Connect to relevant tech and domain nodes. Aim for 6–10 connections to make the graph dense.
5. **KG_META** — Add entry.
6. **Sidebar badge** — Increment `Certifications <span class="nb">N</span>`
7. **Skills CP bar** — Increment `<span class="cp-v">N</span>` for Certifications
8. **`renderDomainDonut()`** — Update relevant domain count if cert adds new skills.
9. **LinkedIn** — Yes, especially for recognized platforms (Coursera, Google, AWS, Microsoft).

### WF-5: Add New Internship/Role

**Trigger:** "I got an internship at...", "starting a new role at...", etc.

1. **Experience timeline** — Add new `.tli` HTML block (search `class="tli"`). Include: dates, org, bullet points, tech chips, document links.
2. **Career timeline strip** — Add/update node in `.career-strip` → `.cs-track`. Use `.cs-node.now` for current, `.cs-node.past` for completed. Search `cs-node`.
3. **PROJECTS array** — Add project if work produced a deliverable.
4. **KG_NODES** — Add with `cls:'intern'`.
5. **KG_EDGES** — Connect to tech, domain, and project nodes.
6. **KG_META** — Add entry.
7. **Sidebar badge** — Change experience count → new value
8. **Home featured strip** — Ask user: "Should this replace one of the 3 featured cards?"
9. **Recruiter panel** — Update "Best Domain" or "Preferred Roles" if this changes focus.
10. **ACHIEVEMENTS array** — Add milestone entry for internship start or completion.
11. **Home stats internships** — Update `data-count="3"` → new value
12. **LinkedIn** — Definitely yes. Write announcement post.

### WF-6: Add New Achievement

**Trigger:** "I hit 2000 on LeetCode", "won a hackathon", etc.

1. **ACHIEVEMENTS array** — Add:
   ```js
   {year:'2026', mon:'Mar', icon:'★', title:'...', detail:'...', chip:'Category'}
   ```
   Icon rotation: `★ ▲ ◈ ✦ ◉ ⬟`
2. **Home stats** — Update any reflected numbers (LeetCode rating, DSA count, etc.)
3. **Skills CP bar** — Update LeetCode/Problems/HackerRank if relevant.
4. **`renderProficiency()` bars** — Update % if competitive skill improved.
5. **LinkedIn** — Yes for milestones (rating jumps, contest wins, publications).

### WF-7: Add New Thought/Blog Entry

**Trigger:** "I want to write about...", "add a thought on...", etc.

1. **THOUGHTS array** — Add:
   ```js
   {date:'Mar 2026', title:'...', excerpt:'...', tags:'tag1 tag2'}
   ```
2. No cross-references needed unless it relates to a new project.

### WF-8: Update Personal Info

**Trigger:** "I moved to Bangalore", "changed my target role", etc.

- **Location**: Sidebar online status, contact page, recruiter panel
- **Target role**: Recruiter panel "Preferred Roles", contact page availability JSON
- **Availability**: Recruiter panel "Notice Period", contact page JSON, topbar "OPEN TO WORK" tag
- **Email**: Sidebar footer, contact page, education page
- **Social links**: Sidebar footer, contact page, home page quick links

### WF-9: Transition to Employed / Major Life Change

This is a one-time massive multi-point update. Every step is critical.

1. **Topbar tag** — Change `OPEN TO WORK` → `SDE @ [Company]` (search: `tp-tag`)
2. **Recruiter panel** — Update all 4 cells (Status, Domain, Roles, Notice Period)
3. **Sidebar online status** — `Available · New Delhi` → `SDE @ Company · [City]`
4. **Contact page availability.json** — `"internship": true` → `false`
5. **Contact page info grid** — Update Status block
6. **Typewriter tagline** — Rewrite from student framing to engineer framing
7. **Home left role text** — `IIIT-Delhi · CSAM · 2023–2027`
8. **Home OS banner** — `Personal OS · IIIT-Delhi · 2023–2027`
9. **Meta tags** — Update description/OG/Twitter to remove "Open to SDE roles" framing
10. **Career timeline strip** — Update current `.cs-node.now` and add new node for the job
11. **Footer** — `2023355 · IIIT-Delhi · CSAM · 2023–2027`
12. **KG_META core node** — Update desc from student framing
13. **ACHIEVEMENTS array** — Add placement milestone entry
14. **Experience timeline** — Add new role as first `.tli` entry
15. **LinkedIn** — Definitely post. Write announcement.

### WF-10: Year / Graduation Update

**Trigger:** "I'm now in 4th year", "I graduated", "moving to Sem VII", etc.

1. **Identity line** in CLAUDE.md — Update "3rd year" → "4th year" etc.
2. **Topbar** — `Sem VI` → `Sem VII` (search `tp-info`)
3. **Education page** — Update "V Semesters completed" → "VI Semesters completed"
4. **All meta tags** — `2023–27` references
5. **Footer** — `2023–2027`
6. **KG_META core node** — Update desc year reference
7. **Career timeline strip** — Update future node if needed

---

## Consistency Rules

| Rule | Format |
|------|--------|
| Project ID | `P-0XX` sequential (next: P-011) |
| Year | 4-digit string: `'2026'` |
| Project type | `'internship'` / `'research'` / `'academic'` / `'personal'` |
| Project typeLabel | Capitalized: `'Internship'` / `'Research'` / `'Academic'` / `'Personal'` |
| Tags | Lowercase, space-separated: `'personal web ai fullstack'` |
| Achievement icons | Cycle: `★ ▲ ◈ ✦ ◉ ⬟` |
| Chip highlight | `.chip.hi` for primary skills, `.chip` for secondary |
| KG node classes | `core`, `dom`, `intern`, `tech`, `proj`, `course`, `math`, `cert` |
| KG node position | x,y as percentages (0-100). Check KG Zone Map below, offset by 3-5 to avoid overlap |
| TECH_META categories | `AI`, `ML`, `iOS`, `Web`, `DB`, `Game`, `Sys`, `Lang`, `Tool` |

### TECH_META Color Reference
```
AI:   #bb77ff    ML:   #ff6699    iOS:  #5599ff
Web:  #00ff88    DB:   #00ccff    Game: #ffaa00
Sys:  #aaaaaa    Tool: #88ccff    Lang: varies
```

### KG Zone Map (updated May 2026)
Use this to place new nodes without overlap. Update after adding nodes.
```
Top-left (x:0-15, y:0-15)       — iOS cluster. CROWDED.
Top-center (x:30-50, y:0-10)    — some space near chiacon_intern, mth371
Top-center-ML (x:40-55, y:5-20) — random_forest(50,14) placed here. 1-2 slots left.
Top-right (x:75-98, y:0-20)     — AI/NLP cluster. bioinformatics(86,18) placed. CROWDED.
Left-middle (x:0-15, y:40-75)   — Design + Game tools. Tight.
Center (x:30-60, y:55-80)       — Courses + concepts. VERY CROWDED.
Right-middle (x:85-98, y:50-70) — Web tech. Moderate.
Bottom-left (x:0-25, y:80-98)   — Systems + game projects. Moderate space.
Bottom-center (x:30-60, y:85-98)— CP + certs. cert_aiscience(63,84) placed. Some room.
Bottom-right (x:75-98, y:85-98) — DB + certs. cert_gpu(70,90), cert_gdb(77,96). 1-2 slots left.
FREE ZONES: (x:60-70, y:85-95)
```

---

## Count Audit Checklist

Run this after ANY update that changes a count. Search for each value and verify consistency:

- [ ] Sidebar badges: project count, cert count, sem count, experience count
- [ ] Topbar: CGPA, semester number (search `tp-info`)
- [ ] Home stats row: all `data-count` values and display text
- [ ] Home nav cards: project range, cert count (now qualitative — no number badges)
- [ ] Featured strip "View all": project count
- [ ] Project filter button: "All (N)"
- [ ] Skills CP bar: LeetCode, Problems, HackerRank, Certs
- [ ] KG_META core node desc: CGPA value
- [ ] Career timeline strip: roles/milestones accurate
- [ ] `renderDomainDonut()` segments: domain counts roughly accurate
- [ ] `renderProficiency()` bars: pct values still reflect actual skill level

---

## LinkedIn Post System

### When to Suggest

| Update Type | Suggest Post? | Notes |
|-------------|--------------|-------|
| New project | Yes | Include demo/GitHub link, what was built & learned |
| New certification | Yes | Especially recognized platforms (Coursera, Google, AWS) |
| New skill | Only if significant | New language or major framework, not small libraries |
| CGPA update | Only if 0.3+ improvement | Or milestone crossing (7.5, 8.0, 9.0) |
| New internship | Definitely | Company, role, stack, what you'll build |
| Achievement | Yes | Rating jumps, contest wins, publications |
| Course completion | Rarely | Only if A grade, graduate-level, or unusual |

### Post Style Guide
- **Tone**: Genuine CS student sharing progress. NOT corporate/motivational.
- **Length**: Under 200 words.
- **Structure**: What was built/achieved → What was learned → What's next.
- **Hashtags**: 3-5 relevant ones. Always include `#IIITD` or `#IIITDelhi`.
- **Mention**: IIIT-Delhi naturally, not forced.
- **No**: Emojis overload, "thrilled to announce", "grateful for the opportunity", hustle culture.

---

## Deployment

- **Host**: GitHub Pages — repo `Nishant7p/Nishant7p.github.io`, branch `main`
- **Claude has direct git access** — can commit and push without user action
- **Deploy**: Edit `index.html` → `git add index.html` → commit → `git push origin main`. No build step.
- **Test locally**: Open `index.html` directly in browser.
- **Smooth scroll**: Lenis v1.1.18 loaded via unpkg CDN, initialized in main script block.

### Image Hosting Policy (updated May 2026)

**Primary — GitHub repo assets (use this for all new images):**
```
assets/certs/<issuer-slug>/<file>.png
→ https://raw.githubusercontent.com/Nishant7p/Nishant7p.github.io/main/assets/certs/<issuer-slug>/<file>.png
```
Permanent, free, no CDN dependency, version-controlled alongside the code.

**Legacy — external hosts (existing entries only, do not add new ones):**
- postimg.cc, ibb.co, image2url.com — leave these in place unless they 404
- If a legacy URL 404s: re-upload to `assets/` and update the URL

**Annual check (every Jan):** `grep -n "postimg.cc\|ibb.co\|image2url.com" index.html` — verify all still load.

**Asset naming convention:**
```
assets/
  certs/
    <issuer-slug>/        e.g. learnquest-ai-science/, hackerrank/, jhu-gpu/
      specialization.png  ← main cert thumbnail (always this name)
      mod1-<topic>.png    ← sub-module certs
      mod2-<topic>.png
```

### Analytics (Supabase)
- View counter active via Supabase RPC (`increment_view`)
- Credentials in second `<script>` tag at bottom of `index.html` (publishable key, not secret)
- Secret keyboard shortcut: type `views` to see analytics overlay
- Do NOT expose, log, or move these credentials

### Git Workflow (Claude has access — repo already initialized)
```bash
# Standard update
git add index.html
git commit -m "add: <what changed>"
git push origin main

# Adding images + index.html together
git add assets/ index.html
git commit -m "add: <cert name> images + portfolio update"
git push origin main
```

**Repo remote:** `https://github.com/Nishant7p/Nishant7p.github.io.git`
**Working directory:** `/Users/nishant/Desktop/Claude/Portfolio/`
**Branch:** `main` — GitHub Pages auto-deploys from here. Changes live in ~1 minute.

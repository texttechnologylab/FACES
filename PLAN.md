# FACES Project Website — Build Plan

> **Status: built.** The site now exists under `docs/`, `overrides/` and `mkdocs.yml`.
> This document is kept as the design record. Two things have changed since it was
> written: §8.1/§8.2 are resolved — the paper and the v3 tables agree, and the four
> outstanding numbers were corrected at source — and the figure set was cut back
> (see §5.1), dropping the v1 2D-projection gaze figures and replacing the
> answer-format chart with inline markup.

Target: `https://texttechnologylab.github.io/FACES/` (repo `texttechnologylab/FACES`, already the `origin` of this working copy).

Purpose: a linkable overview of the FACES project for the **next-phase DFG proposal** — what the project is, who runs it, what has been delivered, and what to cite.

Stack: **MkDocs Material** + custom `home.html` landing template + FACES palette CSS. Language: **English only**.

---

## 1. Why this stack

Four sibling repos already publish with `mkdocs gh-deploy` on the same workflow:

| Repo | Site |
|---|---|
| `texttechnologylab/InterView` | `texttechnologylab.github.io/InterView/` |
| `texttechnologylab/Va.Si.Li-Lab` | `texttechnologylab.github.io/Va.Si.Li-Lab/` |
| `texttechnologylab/Va.Si.Li-Lab-backend` | `texttechnologylab.github.io/Va.Si.Li-Lab-backend/` |
| `texttechnologylab/Janus-Gateway` | `texttechnologylab.github.io/Janus-Gateway/` |

FACES becomes the **umbrella site** that these four hang off. Same toolchain, same CI, no npm. Material's `grid cards`, admonitions and dark mode carry most of the design work; the one custom piece is the landing page template, which Material supports natively via `theme.custom_dir` + `template:` front-matter.

The ENTAILab site is the right structural model (hub → measure cards → PIs → DFG footer), but it is visually monochrome. FACES gets the institutional palette instead.

---

## 2. Color scheme

Sampled from the live institutional sites, not guessed:

| Token | Hex | Source | Use |
|---|---|---|---|
| `--faces-blue` | `#004A6F` | Goethe-Universität CD ("Goethe-Blau") | Primary. Nav bar, headings, hero ground. |
| `--faces-blue-light` | `#006192` | texttechnologylab.org | Links, hover states, dark-mode primary. |
| `--faces-gold` | `#F0B600` | texttechnologylab.org accent | Accent — rules, active nav, card hover borders, CTA. |
| `--faces-magenta` | `#E5007D` | lifbi.de primary | LIfBi-attributed elements only (partner badges, LIfBi work packages). Used sparingly so it reads as attribution, not decoration. |
| `--faces-violet` | `#4242B1` | lifbi.de secondary | Optional second LIfBi tone. |
| `--faces-sand` | `#F6F3EE` | Goethe CD warm neutral | Page background (light mode), card fill. |
| `--faces-sand-2` | `#F3EFE9` | Goethe CD warm neutral | Section banding. |
| `--faces-ink` | `#323637` | Goethe CD | Body text. |
| `--faces-ink-2` | `#262929` | Goethe CD | Headings, dark-mode ground. |

Material palette config: `primary: custom` / `accent: custom`, with `--md-primary-fg-color` etc. overridden in `docs/stylesheets/faces.css`. Dark scheme (`slate`) flips to `--faces-blue-light` on `--faces-ink-2` so the gold stays legible.

**Deliberate rule:** blue = the project and Goethe/TTLab side, magenta = LIfBi side, gold = interaction. This makes the two-institution structure visible without a legend.

---

## 3. Site structure

```
FACES/
├── mkdocs.yml
├── overrides/
│   ├── main.html              # extends base; adds funder footer strip
│   └── home.html              # hero landing page (index.md only)
├── docs/
│   ├── index.md               # template: home.html — Home
│   ├── project.md             # The Project
│   ├── deliverables/
│   │   ├── index.md           # Deliverables overview + status table + data model
│   │   ├── interview.md       # InterView
│   │   ├── vasili-lab.md      # Va.Si.Li-Lab & backend
│   │   └── infrastructure.md  # Janus-Gateway, InterView-P, DUUI link
│   ├── studies.md             # Empirical work & results to date
│   ├── team.md                # Team
│   ├── publications.md        # Publications & citation
│   ├── stylesheets/faces.css
│   └── assets/
│       ├── img/               # screenshots, hero
│       ├── figures/           # from analysis_2026 (§5)
│       ├── team/              # portraits
│       └── logos/             # real marks + placeholders (§6)
└── .github/workflows/mkdocs.yml
```

Top nav (Material `navigation.tabs`): **Home · Project · Deliverables · Studies · Team · Publications**, plus a GitHub repo icon.

---

## 4. Page-by-page content

### 4.1 `index.md` — Home (custom `home.html`)

**Hero.** Full-bleed `FACES_Scene.png` (the VR interview room), darkened with a `--faces-blue` overlay. Over it:

> ## FACES
> ### Feasibility, Acceptance, and Data Quality of New Multimodal Surveys
> A multimodal data space for survey research — VR- and avatar-based interviews as an extension of, and alternative to, face-to-face interviewing.
>
> `[Explore the platform]` `[Publications]`

**Fact strip** (four inline stat tiles, immediately under the hero — this is what a reviewer scans first):

| | |
|---|---|
| **DFG 539621548** | → GEPRIS |
| **SPP 2431** | Infrastructure Priority Programme *New Data Spaces* |
| **10/2024 – 09/2027** | Funding period |
| **2 institutions** | Goethe University Frankfurt · LIfBi Bamberg |

**In one paragraph.** Condensed abstract — surveys face attrition, recruitment difficulty and rising cost; FACES builds an open-source avatar/video interview platform with variability in avatars, situational parameters, interfaces and AI, and tests whether it holds up on feasibility, acceptance and data quality.

**Three research questions**, as three cards:
1. Do avatar-based interviews have advantages over video-based formats?
2. Which feature combinations reduce interviewer effects?
3. How do the findings feed into a theory of virtual interviewer training?

**What has been delivered** — the section that does the proposal work. Grid cards, each with a status chip (`Released` / `Complete` / `Accepted` / `Submitted`) and a link out:

| Card | Status | Links to |
|---|---|---|
| **InterView** — unified VR + web interview platform, full Docker Compose stack | Released | `deliverables/interview.md`, repo, docs |
| **Va.Si.Li-Lab** — the VR framework InterView is built on; UPM package + docs | Released | `deliverables/vasili-lab.md` |
| **Va.Si.Li-Lab-backend** — Scene/Role/Logging API, Ubiq server, chatbot, Whisper STT | Released | backend docs |
| **Janus-Gateway** — pinned reproducible Janus 1.4.2 image, `ghcr.io/texttechnologylab/janus-gateway` | Released | `deliverables/infrastructure.md` |
| **Avatar pre-study (CAWI)** — 99 respondents, 20 avatars rated on preference, trust, comfort, similarity | Complete | `studies.md` |
| **VR interview study** — 27 valid interviews, 4.57 M records captured across six modalities | Complete | `studies.md` |
| **Reproducible analysis pipeline** — every figure and table regenerated from cache by one command | Complete | `studies.md` |
| **ReEmote** — emotion representation through avatar facial expression | Accepted, XR Salento 2026 | `publications.md` |
| **InterView paper** — *Towards a Unified VR-Capable Interview Environment* | Under review (Elsevier) | `publications.md` |

**A headline number worth putting on the home page:** *4,567,743 records captured across six linked modalities in 27 interviews, at a measured median 18.5 Hz with a 96.6 % capture duty cycle.* That single sentence is the strongest evidence the instrument works, and it is defensible from `tab_capture_summary` / `tab_data_model`.

**Partners & funding footer strip** (in `main.html`, so it appears on every page): Goethe-Universität + Text Technology Lab · LIfBi + Leibniz Association · DFG · SPP 2431 New Data Spaces, all logos linked.

### 4.2 `project.md` — The Project

- Full title, acronym, GEPRIS link, SPP 2431 link, funding period, institutional location (Departments 2 and 3, LIfBi Bamberg; Text Technology Lab, Goethe University Frankfurt).
- **Motivation** — attrition, recruitment, cost; the three converging shifts the project leverages (multimodality, XR, informational networking / hypertext).
- **Approach**, as a three-stage timeline:
  1. Development of an open-source avatar and video interview platform.
  2. Preliminary experiments on avatar characteristics and levels of immersion.
  3. Validation with former **NEPS** participants.
- **System requirements (A)–(G)** from the InterView paper, as a definition list — questionnaire support, avatar customisation, environment customisation, multi-platform participation, platform-specific multimodality, data collection & linkage, LLM-assisted interviews. Each row carries a ✅/🔶 marker for current implementation status. *This table is the single most useful thing on the site for a proposal reviewer* — it shows the requirement set and exactly how far it has been met. (G), the LLM client, is honestly marked as designed-but-not-realised.
- **Division of work** — Goethe/TTLab: platform, data model, multimodal processing. LIfBi: survey methodology, experimental design, NEPS validation, fieldwork.

### 4.3 `deliverables/index.md`

Status table of all four software deliverables: repo · docs · license · release/registry · what it does.

Then two diagrams:

1. **Architecture** — Mermaid, redrawing Figure 1 of the InterView paper. Nodes not yet realised (LLM client) in a dashed/amber style, matching the paper's orange-exclamation convention.
2. **Data model** — `fig_data_model.png` from `analysis_2026`, which shows the six entity groups (session, per-frame, media, language, instrument, self-report) *annotated with the record counts actually stored*. This is far more persuasive than an abstract ER diagram: it is the schema and the evidence in one image.

### 4.4 `deliverables/interview.md`

The flagship page. Screenshots do the talking:

- `Screenshot 2025-10-16 103854.png` — interviewee's first-person view: interviewer avatar across the desk, answer-option panel (`1: sehr gut … 5: sehr schlecht`) with the self-view mirror. Caption ties it to requirement (A).
- `Screenshot 2026-09-03 151646.png` — third-person view of the interview room.
- `Screenshot 2026-09-03 151451.png` — the same scene with the gaze heat map overlaid.
- Component breakdown: InterView-VR (Unity/Quest, Va.Si.Li-Lab-based, articulated avatars with face/gaze/hand tracking), InterView-W (nginx-served static client, Janus JS, video or emulated avatar), InterView-B (Janus SFU + coturn + Va.Si.Li-Lab server + logging API), InterView-P (Whisper ASR, gaze AOI replay, LimeSurvey import, DUUI hand-off).
- Token-based session flow, 5 steps, lifted from the InterView docs index.
- Deep links into `texttechnologylab.github.io/InterView/` rather than duplicating the docs. **The FACES site must not become a second copy of the technical documentation** — it links, it does not fork.

### 4.5 `deliverables/vasili-lab.md`

Va.Si.Li-Lab as the framework layer: what it is (a VR lab for simulation-based learning, originally from DigiTeLL), the hypergraph/ISO-Space multimodal data model, what FACES contributed back to it, backend modules table, and links to both doc sites. Full BibTeX for the 2023/2024 papers. Header carries the Va.Si.Li-Lab logo placeholder (§6.2).

### 4.6 `studies.md` — Empirical work

**Source of record: the paper (`Assets/IJHCS___InterView-2.pdf`) together with the `analysis_2026` CSV tables, which agree.** The paper reports the **v3** gaze pipeline throughout; the site must do the same. Do **not** copy numbers out of `RESULTS_SUMMARY.md`'s prose — it quotes **v1** for gaze, so transcribing it would put the website in contradiction with the paper. See §8.1.

The framing still follows `RESULTS_SUMMARY` §6.1: **lead on the instrument, not on the behavioural effects.** The behavioural results are real but modest at n = 27; the measurement characteristics are unambiguous and are what a proposal reviewer actually needs to see. The paper itself takes this line — "what a fine-grained, timestamp-synchronized multimodal pipeline makes visible and falsifiable, not a confirmed discovery" — and the website should echo it rather than out-claim it.

**Study 1 — Avatar pre-study (CAWI).** Fielded 2025-06-06 to 2025-06-24; 115 started, **99 completed**.[^n] 20 avatars, each rated on preference (top-3 ranking), trust, comfort and similarity.

[^n]: The paper says 98. Every share in `tab_prestudy_avatars.csv` is an exact multiple of 1/99 (1.010 %, 23.232 % = 23/99, 37.374 % = 37/99), so the analysis denominator is 99. See §8.2.

The two selected pairs — Category A (higher-ranked) and Category B (lower-ranked) — span most of the preference range:

| Study id | Descriptor | Top-3 preference | Would trust | Comfort (1–5) |
|---|---|---|---|---|
| 1 | Sunglasses | 1 % | 6 % | 2.2 |
| 2 | Headscarf | 10 % | 58 % | 4.0 |
| 3 | Blue hair | 37 % | 58 % | 4.0 |
| 4 | Striped jumper | 13 % | 49 % | 3.7 |

Stated plainly on the page, because a reader who assumes the avatars were simply the best-rated four will misread any avatar effect. Two details worth keeping honest: the A/B split holds on **preference**, but not on the other constructs — the Category B headscarf avatar actually scores *higher* on trust (58 % vs 49 %) and comfort (4.0 vs 3.7) than the Category A striped-jumper avatar; and of the field's five most-preferred avatars, only "blue hair" was carried forward. The four constructs are close to one likeability dimension (preference–trust ρ = 0.81, trust–comfort ρ = 0.92); similarity is the most distinct (ρ = 0.61). Caveat carried: interviewer avatar was not randomised across the 27 interviews, so no causal claim.

**Study 2 — VR interview study.** ~28 min median sessions at two institutions, interviewers unknown to interviewees, LimeSurvey questionnaire, neutral (Q_N) vs. discomfort-inducing (Q_D) item batteries.

*What the instrument captured* — the centrepiece table:

| | |
|---|---|
| Sessions recorded / valid interviews | 34 / **27** |
| Total interview time | 15.7 h |
| Median session duration | 27.7 min |
| Eye / Body / Head records | 1,496,517 **each** |
| Gaze samples analysed | 626,278 |
| Transcribed words | 57,971 |
| Audio chunks | 14,753 |
| **Total records stored** | **4,567,743** |
| Median effective gaze rate | **18.5 Hz** (measured, not nominal) |
| Median capture duty cycle | **0.966** |
| Median gaze samples in reference view | 97.0 % |

*Acceptance* — from `tab_likert_items` / `fig_likert_experience`: low discomfort and dizziness, high willingness to participate again, moderate immersion, and stable across avatar conditions.

*Behavioural findings, reported with their limits:*

- **Answer format — the clean finding, and the one to feature.** Participants voiced their answer as a bare response index 36 % of the time, as the full scale label 33 %, both 4 %, and in neither form 27 %. **63 % of spoken answers contain no verbatim scale label.** A voice-driven questionnaire therefore cannot match on label text: it has to resolve a bare index against the currently displayed scale, and fall back to a clarification turn for the 27 %. This is a concrete, well-powered design result for voice-driven survey interfaces, it generalises beyond VR, and it is the strongest single item on the page.
- **Response latency — no reliable effect.** Sensitive items are +0.42 s slower at the median (2.31 s → 2.73 s), but this is not reliable (Mann-Whitney *p* = .210; participant-level Wilcoxon *p* = .386). The batteries are not interleaved, so item identity explains **99.3 %** of the variance in interview position — question type, position and item are effectively one variable. Under participant-clustered inference neither term is reliable (condition ×0.89, *p* = .613; position ×1.48, *p* = .143). The page states this outright and names interleaving as the design fix.
- **Gaze — where you look barely moves; *how* you look does.** No AOI dwell shift survives Holm: the largest is the window (+0.026, *p* = .162 uncorrected), with the self-view mirror (−0.003), answer panel (−0.009) and interviewer's face essentially flat. But the **fixation dynamics do separate the conditions**: fixation time-share drops under sensitive items (0.63 → 0.58 s/s, *p* = .008, *d_z* = −0.64, n = 26) and **survives Holm across the fixation-metric family** (*p* = .040), while fixation rate (*p* = .940), mean duration and dispersion do not. Spatial entropy is higher under sensitive items (2.98 → 3.17, *p* = .018, *d_z* = 0.57, n = 20), significant from a 16-cell bin width upwards — participants scan more of the scene rather than staring more widely. That contrast is the page's cleanest gaze result, and it is a genuinely positive finding, not a null.
- **Speech.** Responses to sensitive items run longer (1.51 s → 2.02 s, *p* = .025). Articulation rate shows no reliable difference. Hedge rate median 2.3 per 100 words on the open-ended items.
- **Behaviour vs. self-report — partial convergence, and that is the interesting part.** Only **10 of 27** respondents (37 %) said, when asked directly, that any question had made them uncomfortable. Those 10 show a much larger increase in response duration than the other 17 (Mann-Whitney *U* = 158.0, *d* = 1.76, Holm *p* = .0014) and a larger increase in dwell on the interviewer's face (*U* = 128.0, *d* = 0.73, Holm *p* = .037); latency and mirror dwell do not distinguish the groups. **But the same behavioural shifts appear in participants who reported no discomfort at all.** So self-report and behaviour converge only partially, and self-report alone would underestimate the effect of sensitive questions. This is the strongest argument on the whole site for why multimodal capture is worth building — it is the FACES thesis, demonstrated.

  *Do not confuse this with `tab_convergence.csv`*, a separate analysis correlating behavioural shifts against five Likert items, where 0 of 25 correlations survive Holm. Different question, different table; the paper reports the group comparison above. Presenting the null correlation matrix as if it were this result would badly undersell the finding.

*Reproducibility box.* `python run_all.py` regenerates every figure and table in ~55 s from cache; `make_summary.py` reads every number back out of the written CSVs, so the prose cannot drift from the tables. Worth its own admonition on the page — reproducibility is a scoring criterion in an infrastructure SPP, and this pipeline genuinely has it.

### 4.7 `team.md`

Photo grid, per your selection — **PIs + coordination + Patrick + Doris**:

| Person | Role | Affiliation |
|---|---|---|
| Prof. Dr. Alexander Mehler | Principal Investigator | Text Technology Lab, Goethe University Frankfurt |
| Prof. Dr. Corinna Kleinert | Principal Investigator | LIfBi |
| Prof. Dr. Christian Aßmann | Principal Investigator | LIfBi |
| Dr. Lydia Kleine | Project Coordination | LIfBi |
| Patrick Schrottenbacher | Research Associate / Platform development | Text Technology Lab, Goethe University Frankfurt |
| Doris Stingl | Research Associate | LIfBi |

Card layout: circular portrait, name, role, institution, then small icon links (ORCID / GitHub / ResearchGate / institutional page) where available. Known ORCIDs: Mehler `0000-0003-2567-7539`, Schrottenbacher `0009-0003-7644-0037`, Stingl `0000-0002-0414-1252`. Card left border is `--faces-blue` for Goethe, `--faces-magenta` for LIfBi — the institutional split reads at a glance.

Below the grid, a plain-text **Contributors** line (no photos) for Giuseppe Abrami, Ali Zandian Ghahfarokhi, and the Va.Si.Li-Lab framework contributors, so credit is given without expanding the grid.

Portraits use the same placeholder mechanism as logos (§6.3): a neutral monogram avatar renders until the real photo lands, so the page ships complete either way.

### 4.8 `publications.md`

Grouped, newest first, each with an abstract-length summary, links (DOI / publisher / PDF / RG) and a copyable BibTeX block in a collapsed `??? note "BibTeX"` block.

**FACES output**

1. **Schrottenbacher, Mehler, Abrami, Kleine & Stingl (2026).** *INTERVIEW: Towards a Unified VR-Capable Interview Environment.* Under review (Elsevier). — ⚠️ the BibTeX in the InterView README has a placeholder DOI (`10.2139/ssrn.XXXXXXX`); needs the real SSRN ID, or the entry should say "under review" with no DOI.
2. **Schrottenbacher, Mehler, Bernhardt, Rohe & Abrami (2026).** *ReEmote: Towards Emotion Representation in VR Through Va.Si.Li-Lab.* Proceedings of XR Salento 2026, Springer LNCS. **Accepted.**

**Framework foundations**

3. **Mehler et al. (2023).** *A Multimodal Data Model for Simulation-Based Learning with Va.Si.Li-Lab.* HCII 2023, Springer, 539–565. `10.1007/978-3-031-35741-1_39`
4. **Abrami et al. (2023).** *Va.Si.Li-Lab as a Collaborative Multi-User Annotation Tool in Virtual Reality and Its Potential Fields of Application.* HT '23, ACM. `10.1145/3603163.3609076`
5. **Bagci et al. (2024).** *Va.Si.Li-ES: VR-based Dynamic Event Processing, Environment Change and User Feedback in Va.Si.Li-Lab.* HT '24, ACM. `10.1145/3648188.3675154`
6. **Henlein, Lücking, Bagci & Mehler (2023).** *Towards grounding multimodal semantics in interaction data with Va.Si.Li-Lab.* GESPIN 2023 (poster).
7. **Leonhardt, Abrami, Baumartz & Mehler (2023).** DUUI — the processing pipeline InterView-P hands relational data to.

Bottom: a **"How to cite the platform"** box giving the one BibTeX entry someone reusing InterView should copy.

---

## 5. Figures — from `analysis_2026`

Source: `D:\repos\icids_cwhisper\analysis_2026\figures\` (PNG + PDF of each). Publication-quality matplotlib, already legible at web width. **Copy the PNGs into `docs/assets/figures/`** — do not reference the analysis repo by path, and do not vendor the whole directory; only the shortlist below.

### 5.1 Shortlist

| Figure | Page | Why |
|---|---|---|
| `fig_capture_overview.png` | Studies (lead) | Records by modality, measured sampling-rate histogram, gaze yield vs. duration. The "instrument works" figure. |
| `fig_data_model.png` | Deliverables overview | Six entity groups with real record counts, 4,567,743 total. Schema and evidence in one image. |
| `fig_gaze_heatmap_panel.png` | Studies / InterView | Four-panel: all gaze, Q_N, Q_D, difference — over the actual reference view. The most visually striking asset in the project. |
| `fig_answer_format.png` + `fig_answer_format_by_scale.png` | Studies | The clean 36/33/4/27 % design finding. |
| `fig_likert_experience.png` | Studies | Acceptance / self-report distribution. |
| `fig_prestudy_ranking.png` + `fig_prestudy_selected.png` | Studies | Avatar field and which four were carried forward. |
| `fig_interview_timeline.png` | Deliverables / InterView | Cross-modal synchronisation on one clock — proves the time alignment claim. |
| `fig_gaze_aoi_overlay.png` | Studies | Shows how AOIs are defined on the reference view; makes the gaze table legible. |
| `fig_latency_forest.png` | Studies (optional) | Only if the latency null is discussed at length. |

Also available and worth knowing about: `data/prestudy/images/Avatar_1..20.png` — the twenty avatar renders. A small contact-sheet strip of these on the Studies page, with the four selected ones highlighted, would communicate the pre-study design instantly.

### 5.2 Version discipline (important)

Three gaze pipelines exist and the figure directory contains all of them. **The paper reports v3, so the site reports v3.**

- **v1** (`fig_*`, no suffix) — coarser 2D pixel-projection AOIs, n varies per AOI (18–22). Stable, but *not* what the paper cites.
- **v2** (`*_v2`) — **stale (2026-08-13, predates the data fixes). Do not use anywhere.**
- **v3** (`*_v3`) — fresh Unity 3D raycast, finer colliders, n = 26 with no per-AOI dropout. **This is the paper's source and the site's source.**

Two constraints: **never place a v1 and a v3 magnitude side by side** (v3's Face/Self-view colliders are much tighter, so absolute dwell shares are not comparable across pipelines — only within-pipeline Q_N vs. Q_D contrasts are), and **do not cite v3's "share of fixations on interviewer face"**, which comes out exactly 0.0/0.0 as a tight-collider artefact.

One trap worth naming, because I fell into it: `RESULTS_SUMMARY.md`'s prose reports **v1** gaze numbers, while the paper reports **v3**. The two disagree on whether fixation time-share survives Holm correction (v1: *p* = .117, no; v3: *p* = .040, yes) — same metric, same data, different collider geometry. Building `studies.md` from the summary prose would have had the website reporting a null where the paper reports a result. Take gaze numbers from `tab_gaze_tests_v3.csv` / `tab_aoi_dwell_v3.csv` / `tab_claimed_discomfort_questions_v3.csv` and cross-check each against the paper before publishing. Latency, speech, answer-format and Likert have only one version and can be read from either source.

`REPORT_v3_reconciliation.md` is the authority on all of this and should be re-read before `studies.md` is written.

### 5.3 Optional polish

The figures use matplotlib's default blue/orange. Recolouring to `--faces-blue` / `--faces-gold` would tie the Studies page together, and `common.py` looks like the single place to do it. **Deferred, not blocking** — and worth checking against the journal submission first, since the figures presumably need to stay consistent with the paper.

---

## 6. Assets & placeholders

### 6.1 Have

- `Assets/FACES_Scene.png` — hero
- `Assets/Screenshot 2025-10-16 103854.png` — first-person, answer panel
- `Assets/Screenshot 2026-09-03 151646.png` — third-person room
- `Assets/Screenshot 2026-09-03 151451.png` — gaze heat map
- `analysis_2026/figures/*.png` — the shortlist in §5.1
- `Assets/IJHCS___InterView-2.pdf` — source text; not published on the site until a preprint URL exists

### 6.2 Logo placeholders

Every logo slot ships as a real file from day one, so the layout is final before any artwork exists. Swapping in the real mark is a file replacement — same filename, no template or CSS change.

| Slot | File | Status |
|---|---|---|
| **Va.Si.Li-Lab** | `logos/vasili-lab.svg` | ⬜ **Placeholder — you are designing this.** Reserved slot on the Va.Si.Li-Lab deliverable page header, the home-page deliverable card, and the footer. |
| **FACES** | `logos/faces.svg` | ⬜ Placeholder. Typographic wordmark in Goethe-Blau until a real mark exists — happy to draft options. |
| **InterView** | `logos/interview.svg` | ⬜ Placeholder. Optional, but a companion mark to Va.Si.Li-Lab would make the deliverable cards much stronger. |
| Janus-Gateway | `logos/janus-gateway.svg` | ⬜ Placeholder. Lowest priority — could stay a Material icon. |
| Text Technology Lab | `logos/ttlab.png` | 🟨 Available from texttechnologylab.org |
| Goethe-Universität | `logos/goethe.svg` | 🟨 Needs official file |
| LIfBi | `logos/lifbi.svg` | 🟨 Needs official file |
| Leibniz Association | `logos/leibniz.svg` | 🟨 Needs official file + usage check |
| DFG | `logos/dfg.svg` | 🟨 Needs official file + usage check |
| SPP 2431 New Data Spaces | `logos/spp2431.png` | 🟨 `NewDataSpaces.png` exists in the Va.Si.Li-Lab docs; check resolution |

**Placeholder rendering.** Each placeholder is a small hand-written SVG: dashed `--faces-blue` border, the slot name in the centre, correct aspect ratio. It looks deliberate rather than broken, and it is unmistakable in a screenshot, so nothing ships to the proposal by accident. A single `.logo--placeholder` CSS class controls all of them; deleting the class after the last swap removes the treatment everywhere.

**Spec for the Va.Si.Li-Lab mark**, so it drops straight in when you design it:
- **SVG**, with all text converted to paths.
- Two lockups: **square/icon** (used at 40–64 px in cards and the nav) and **horizontal** (used at ~180 px wide in the footer strip). The square one must stay legible as a 32 px favicon.
- Light and dark variants, or a single version that survives on both `#F6F3EE` and `#262929`. A monochrome-safe silhouette is the easiest way to guarantee this.
- Ideally picks up `--faces-blue` / `--faces-gold` so it sits inside the palette rather than fighting it — but if the mark wants its own colour, tell me and I will give it breathing room in the layout instead.

Same spec applies to a FACES mark and an InterView mark if you decide to make those too.

### 6.3 Portraits

Six needed — Mehler, Kleinert, Aßmann, Kleine, Schrottenbacher, Stingl. Square crops, ≥ 600 px. (Kleinert / Aßmann / Kleine / Stingl may be reusable from lifbi.de with permission; Mehler from texttechnologylab.org.) Missing portraits render as a neutral monogram disc in the person's institutional colour — same swap-in-place mechanism as the logos.

### 6.4 Nice to have

A short screen capture of a live session (10–20 s, silent, looping, muted autoplay). One clip does more for a proposal reviewer than three screenshots.

---

## 7. `mkdocs.yml` (concrete)

Mirrors the InterView config, with the FACES palette and the overrides directory:

```yaml
site_name: FACES
site_url: https://texttechnologylab.github.io/FACES/
site_description: >-
  FACES - Feasibility, Acceptance, and Data Quality of New Multimodal Surveys.
  DFG project 539621548, SPP 2431 New Data Spaces.
repo_url: https://github.com/texttechnologylab/FACES
repo_name: texttechnologylab/FACES

theme:
  name: material
  custom_dir: overrides
  logo: assets/logos/faces.svg
  favicon: assets/logos/favicon.png
  icon: { repo: fontawesome/brands/github }
  palette:
    - media: "(prefers-color-scheme: light)"
      scheme: default
      primary: custom      # #004A6F
      accent:  custom      # #F0B600
      toggle: { icon: material/toggle-switch, name: Switch to dark mode }
    - media: "(prefers-color-scheme: dark)"
      scheme: slate
      primary: custom
      accent:  custom
      toggle: { icon: material/toggle-switch-off, name: Switch to light mode }
  features:
    - navigation.tabs
    - navigation.instant
    - navigation.tracking
    - navigation.sections
    - navigation.top
    - content.code.copy
    - search.highlight
    - search.suggest

nav:
  - Home: index.md
  - Project: project.md
  - Deliverables:
      - Overview: deliverables/index.md
      - InterView: deliverables/interview.md
      - Va.Si.Li-Lab: deliverables/vasili-lab.md
      - Infrastructure: deliverables/infrastructure.md
  - Studies: studies.md
  - Team: team.md
  - Publications: publications.md

extra_css: [stylesheets/faces.css]

plugins:
  - search
  - glightbox            # click-to-zoom on the screenshots and figures

markdown_extensions:
  - admonition
  - attr_list
  - md_in_html
  - def_list
  - tables
  - footnotes
  - pymdownx.details
  - pymdownx.superfences:
      custom_fences:
        - name: mermaid
          class: mermaid
          format: !!python/name:pymdownx.superfences.fence_code_format
  - pymdownx.tabbed: { alternate_style: true }
  - pymdownx.emoji:
      emoji_index: !!python/name:material.extensions.emoji.twemoji
      emoji_generator: !!python/name:material.extensions.emoji.to_svg
```

`.github/workflows/mkdocs.yml` is the InterView workflow verbatim, plus `mkdocs-glightbox` in the pip install line. Deploys to `gh-pages` on push to `main`; Pages must be set to serve from the `gh-pages` branch.

---

## 8. Open items

### 8.1 The paper and the tables agree — my earlier claim was wrong

I previously said the PDF diverged from the analysis package. **It does not.** I had compared the PDF against `RESULTS_SUMMARY.md`'s *prose*, which reports **v1** gaze; the paper reports **v3**. That was a v1/v3 mismatch inside the analysis package, not an error in the paper. `RESULTS_SUMMARY` §7's remarks about "the manuscript" and the legacy fuzzy-match script describe the *original* submission, not this revised draft — which already incorporates the rebuilt pipeline.

Checked value by value against the CSVs, the PDF matches:

| PDF claim | Table | |
|---|---|---|
| Latency +0.42 s (2.31 → 2.73), *p* = .210 | `tab_latency_descriptives` | ✅ |
| Clustered model ×0.89 *p* = .613; ×1.48 *p* = .143 | `tab_latency_model` | ✅ |
| Fixation time-share 0.63 → 0.58, *p* = .008, *d_z* = −0.64, n = 26, Holm .040 | `tab_gaze_tests_v3` | ✅ exact |
| Fixation rate 1.79 / 1.82, *p* = .940 | `tab_gaze_tests_v3` | ✅ exact |
| Mean fixation duration 0.34 / 0.29, .117 | `tab_gaze_tests_v3` (Holm) | ✅ exact |
| Dispersion 13.1 / 14.6, *p* = 1.0 | `tab_gaze_tests_v3` (Holm) | ✅ exact |
| Entropy 2.98 → 3.17, *p* = .018, 0.57, n = 20 | `tab_gaze_tests_v3` | ✅ exact |
| Entropy significant from 16 bins up | `tab_gaze_entropy_sensitivity_v3` (.099 → .040) | ✅ |
| AOI window +0.026 *p* = .162; mirror −0.003 *p* = .433; panel −0.009 *p* = .627 | `tab_aoi_dwell_v3` | ✅ exact |
| Answer format 36.3 / 32.6 / 4.4 / 26.8 % | `tab_answer_format` | ✅ exact |
| Index-share Wilcoxon W = 70.0, *p* = .758 | `tab_answer_format_test` | ✅ exact |
| Response duration 1.51 → 2.02, *p* = .025 | `tab_speech_tests` | ✅ |
| Discomfort 1.48 ± 0.79; dizziness 1.39 ± 0.84 | `tab_likert_items` | ✅ exact |
| Positive experience 4.30 ± 0.76; would take part again 4.65 ± 0.71 | `tab_likert_items` | ✅ exact |
| 10 of 27 claimed discomfort; duration *U* = 158.0, *d* = 1.76 | `tab_claimed_discomfort_questions_v3` | ✅ exact |
| Face dwell *U* = 128.0, *p* = .037, *d* = 0.73, n = 10/16 | `tab_claimed_discomfort_questions_v3` (.037 = Holm) | ✅ exact |

So the paper is consistently v3, and the site should be too (§5.2). Apologies for the false alarm — it would have sent `studies.md` in the wrong direction.

### 8.2 Four small numbers that genuinely do not match

These are the only unmatched values I found, and they look like the residue of an intermediate recompute rather than anything structural. Worth a check before either the paper or the site goes out.

1. **Pre-study N.** Paper says 98 completed; every share in `tab_prestudy_avatars.csv` is an exact multiple of 1/99, and `RESULTS_SUMMARY` says 115 started / 99 finished. Off by one somewhere.
2. **AOI — interviewer's body.** Paper: −0.005, *p* = .492. `tab_aoi_dwell_v3`: −0.0073, *p* = .301. (v1 −0.023 / .371; v2 −0.006 / .579 — matches neither.)
3. **AOI — interviewer's face.** Paper: **+0.001**, *p* = 1.0. `tab_aoi_dwell_v3`: **−0.0026**, *p* = .573. Sign differs.
4. **Likert.** Paper reports immersion 3.47 ± 1.15; `tab_likert_items` "Felt absorbed in VR" is 3.348 ± 1.152 — SD matches, mean does not. And "moderate enjoyment 3.39 ± 0.66" has no corresponding row in `tab_likert_items` at all.

Items 2 and 3 are exactly the two colliders `REPORT_v3_reconciliation.md` flags as having been tightened between runs, and the other three AOIs in the same paragraph match v3 to three decimals — consistent with that paragraph having been written against an earlier v3 pass. Item 4 may be a different item set (interviewer questionnaire?) rather than an error.

My numbers here come from `pdftotext`; some glyphs were mangled in extraction (ρ, σ and *p* all rendered as `=`), so please eyeball these five figures in the rendered PDF before treating any as a real defect. The digits themselves extract cleanly, so I do not think the mismatches are artefacts — but it is worth thirty seconds of confirmation.

### 8.3 Other items

### 8.2 Other items

1. **`VR-SUITE` vs `Va.Si.Li-Lab`.** The IJHCS draft calls the framework **VR-SUITE** throughout; every repository, doc site and prior paper calls it **Va.Si.Li-Lab**. Either the draft is anonymised for review, or a rename is underway. The site must pick one — please confirm. *This one now also gates the logo:* a mark you are about to design should carry the name the project intends to keep. (Default if unanswered: **Va.Si.Li-Lab**.)
2. **InterView preprint DOI** — placeholder `10.2139/ssrn.XXXXXXX` needs the real SSRN ID, or the citation reads "under review" with no DOI.
3. **MongoDB or SurrealDB?** The InterView docs and backend README say tracking data goes to **MongoDB**; `analysis_2026/INTEGRATION.md` builds its cache from **SurrealDB**. Both may be true at different points in the stack's history, but the website should not say one thing while the docs say another.
4. **Ali Zandian Ghahfarokhi** — listed on the LIfBi page but not in your team selection. Contributors line, or omit?
5. **NEPS validation stage** — under way or still upcoming? Determines whether it appears under "Delivered" or "In progress". I will not overstate it.
6. **Logo permissions** — DFG and Leibniz marks especially.
7. **Public demo?** If a browser participant view can be safely exposed, a "Try it" link would be the strongest single element on the page. Assuming no for now.

---

## 9. Build order

1. Scaffold: `mkdocs.yml`, workflow, `faces.css` with the palette tokens, `overrides/main.html` funder strip, and the full set of logo/portrait placeholders. Push, confirm `gh-pages` deploys and the URL resolves.
2. `overrides/home.html` + `index.md` — hero, fact strip, RQ cards, delivered-cards grid. This is the page that gets linked from the proposal; get it right first.
3. `project.md` — including the (A)–(G) requirements-vs-status table.
4. `deliverables/*` — overview + Mermaid architecture + `fig_data_model`, InterView with the four screenshots, Va.Si.Li-Lab, infrastructure.
5. `studies.md` — numbers per §4.6, figures per §5.1, **v3 gaze tables only** (§5.2). No longer blocked; §8.2's four values just need a glance first.
6. `team.md` — grid ships with monogram placeholders; portraits drop in as they arrive.
7. `publications.md` — BibTeX blocks.
8. Pass: `mkdocs build --strict` link check, mobile layout, dark mode, and a read-through as a reviewer who has 90 seconds.

Steps 1–2 give you a linkable URL. Steps 3–8 land afterwards without breaking the link. **Every step is unblocked** — the only open question that changes written content is the Va.Si.Li-Lab naming in §8.3.1, which affects the logo and the deliverable page headings.

---

## 10. What this plan deliberately does not do

- **No duplicated technical docs.** InterView, Va.Si.Li-Lab, the backend and Janus-Gateway keep their own sites; FACES links to them. Duplication would be stale within a month.
- **No blog / news feed.** Nothing to fill it with, and an empty "latest news" section dated 2026 actively hurts a proposal.
- **No overstated results.** The nulls are reported alongside the positives, the latency confound is named, and the pre-study caveat about non-randomised avatars is kept. A reviewer who has read the paper will check — and the reproducible pipeline behind every number is itself a selling point for an infrastructure SPP.

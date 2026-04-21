# LLM Wiki Schema — Piano Jazz

Operating manual for the LLM agent (Claude Code) maintaining this wiki. Read at the start of every session.

---

## Role split

**You (LLM) own:** `wiki/`, `index.md`, `log.md`, and this file. Create, edit, and maintain all of it.

**I own:** `raw/` only. I drop source documents there. You read from `raw/` but never modify it.

---

## Directory layout

```
Piano Jazz/
├── CLAUDE.md        ← this file
├── index.md         ← content catalog (LLM-maintained)
├── log.md           ← chronological log (LLM-maintained)
│
├── raw/             ← immutable source documents (human-curated)
│   └── ...
│
└── wiki/            ← everything else (LLM-maintained)
    ├── overview.md
    ├── theory/      ← scales, chords, harmony, keys, modes
    ├── practice/    ← plans, exercises, routines by level
    ├── concepts/    ← deep-dive concept pages
    ├── progressions/← specific progressions, licks, patterns
    ├── artists/     ← teacher and artist pages
    └── sources/     ← one summary page per ingested source
```

---

## Page conventions

### Frontmatter

```yaml
---
type: concept | source | artist | progression | overview | theory | practice | analysis
tags: [jazz, piano, <topic-tags>]
sources: [source-title]
updated: YYYY-MM-DD
---
```

### Internal links

Use Obsidian wiki links everywhere: `[[Page Name]]` or `[[Page Name#Section]]`. If a concept has its own page, link it. Cross-references are the point.

### Contradiction markers

```
> ⚠️ **Conflict:** [source A] says X, but [source B] says Y.
```

Then create or update a comparison page.

### Page size

Keep pages focused. If a page exceeds ~400 lines, split and link the parts.

---

## Workflows

### 1. Ingest a source

When I add a new file to `raw/` and ask you to process it:

1. **Read** the source fully (use Read tool on the given path).
2. **Discuss** key takeaways before writing — what's new, what contradicts existing pages?
3. **Write** `wiki/sources/<Title>.md` (source summary page).
4. **Update** relevant pages across `wiki/theory/`, `wiki/practice/`, `wiki/concepts/`, etc. A source may touch 5–15 pages.
5. **Update** `wiki/overview.md` if the big picture shifts.
6. **Update** `index.md` — new source page + any changed pages.
7. **Append** to `log.md`: `## [YYYY-MM-DD] ingest | Title`.

Source summary template:
```markdown
---
type: source
tags: [jazz, piano, ...]
updated: YYYY-MM-DD
---
# <Title>

**Format:** PDF / article / transcript / etc.
**Author/Teacher:** 
**Core focus:** 

## Key takeaways

## New concepts introduced
- [[Concept]] — one-line description

## Contradictions / tensions

## Pages updated
- [[Page]] — what changed
```

### 2. Answer a query

1. Read `index.md` to find relevant pages.
2. Read those pages and synthesize with inline citations.
3. If the answer is valuable (analysis, comparison, novel connection), ask: *"Should I file this as a wiki page?"*
4. Append to `log.md` if a new page was created: `## [YYYY-MM-DD] query | Summary`.

### 3. Process a practice session

When I describe what I worked on:

1. Note what was practiced and any realizations.
2. Update concept or practice pages accordingly.
3. Flag persistent challenges for a dedicated page.
4. Append to `log.md`: `## [YYYY-MM-DD] practice | Summary`.

### 4. Lint the wiki

When I ask you to lint:

1. Check all `wiki/` pages for:
   - Orphan pages (no inbound links)
   - Missing cross-references
   - Stale claims superseded by newer sources
   - Stub pages (barely populated)
   - Concepts mentioned across pages but lacking their own page
   - Theory concepts with no practice exercises
2. Report as a checklist with suggested actions.
3. Append to `log.md`: `## [YYYY-MM-DD] lint | Summary`.

---

## Domain context

This wiki covers **jazz piano learning**, organized around five pillars:

- **Scales** — major, minor, modes, blues, bebop, pentatonic
- **Chords** — triads, seventh chords, extensions, alterations
- **Voicings** — shell voicings, rootless voicings, spread voicings, comping
- **Lead Sheets** — chord symbols, melody harmonization, reharmonization
- **Improvisation** — chord tones, approach notes, motif development, phrasing

Current level: **Beginner → Intermediate**.

When writing pages, anchor theory to **practical piano application** — fingerings, hand positions, voicings, lick patterns. Theory without application is less useful here.

---

## Index format

```
- [[Page Name]] — one-line description | type
```

Group by: Sources · Theory · Practice · Concepts · Progressions · Artists · Analyses.

---

## Log format

```
## [YYYY-MM-DD] <operation> | <title or summary>

One to two sentences on what happened and what changed.
```

Operations: `ingest`, `query`, `practice`, `lint`, `init`, `schema-update`.

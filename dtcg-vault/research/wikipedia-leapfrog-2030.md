# Wikipedia leapfrog 2030 — design-research substrate

**Source:** research-wikipedia-leapfrog-2030.draft.md (project-knowledge, 2026-04-30)
**Authors:** claude-opus-4-7 parent + 4× claude-sonnet-4-6 sub-agents
**Cites:** Wikipedia Main Page, Vector 2022 design docs, DTCG 2025.10, Carbon v10, Wikimedia Codex

---

This research consolidates four parallel Sonnet sub-agent reports into a single
design-research record for the substrate. It is the canonical "what we learned" for
every downstream DESIGN-COMPONENT and DESIGN-TOKEN-CHANGE draft staged in the same
pickup batch (citation-authority-ribbon, research-trail-footer, freshness-ribbon,
knowledge-wiki-baseline tokens).

## 1. Why this research was commissioned

`documentation.pointsav.com` shipped its first Wikipedia-Main-Page-shaped chrome at
workspace v0.1.70 (2026-04-29): 9 muscle-memory items at the article shell (Article/Talk
tabs, Read/Edit/View-history tabs, per-section [edit] pencils, hatnote, lead first-sentence
convention, tagline, collapsible left-rail TOC, language switcher, footer ordering) and a
home-page composition of lede + featured-pin panel + 3×3 category grid + recent-additions
feed. Iteration 2 needs to push from visible-operational into the leapfrog claim. This
research is the bridge.

## 2. Wikipedia Main Page — primitive-level inventory

| Slot | Role | Refresh cadence | Format invariant |
|---|---|---|---|
| Welcome banner | Orientation; community-scale signal via statistics | Continuous (live counter) | Single sentence + two stats; no marketing copy |
| Today's Featured Article | Flagship editorial showcase from 0.1% FA-reviewed articles | Daily | 909–1,009 character paraphrase; bold linked title; "(Full article...)" closer |
| Did You Know | New-content discovery via hook fact | Daily | "Did you know that…" frame; 15–25 word hook; 9 hooks per rotation |
| In the News | Current-events bridge to encyclopedic depth | Non-uniform (consensus-driven) | 4–6 blurbs + Ongoing + Recent deaths; one sentence per blurb |
| On This Day | Historical depth via temporal anchoring | Daily (pre-authored full year) | 5–8 bullets in roughly reverse-chronological order |
| Today's Featured Picture | Visual anchor; standalone discovery | Daily (queue-driven) | One image + ~100 word encyclopedic caption + photographer credit |
| Other Areas | Reader → editor onramp | Static | 7 linked items with 10–15 word descriptions |
| Sister Projects | Ecosystem disclosure across 12 Wikimedia projects | Static | Logo + name + 20–30 word description |
| Languages bar | Global scope signal across 346 language editions | Static (re-tiered as counts cross thresholds) | Three tiers by article count |
| Footer | License, privacy, contact | Static | License notice + last-updated timestamp; no advertising |

The two-column asymmetry (left 65%, right 35%) is not stylistic — it is the same spatial
grammar as a newspaper broadsheet. Density is measurable: a single Main Page screen at
1080p contains ~20–25 independently navigable units above the fold with no gratuitous
padding separating sections.

## 3. Wikipedia article-shell weaknesses in 2026

Ten structural weaknesses from a leapfrog design perspective:

1. **References section is a flat numeric list with no source-authority semantics.** A peer-reviewed Nature paper and a personal blog post occupy identical visual registers.
2. **Infoboxes are semi-structured but not natively machine-readable** at the reading surface.
3. **TOC is structural-only, with no semantic section typing.** AI consumers cannot navigate by content kind.
4. **What-links-here returns a paginated flat list, not a graph.** No second-hop neighbours, no cluster grouping.
5. **No inline-comment surface on the article reading view.** Editorial discussion is a separate page.
6. **No per-section last-edited or authorship granularity.** Freshness illusion.
7. **No reading-time or skim-aid.** Article-size guidance is metadata at `?action=info`, not in reading view.
8. **No citation trail back to the specific cited passage.** Footnote `[4]` resolves to a bibliography entry only.
9. **No live-edit currency indicator.** Articles edited dozens of times per day present no in-session change signal.
10. **AI-consumption surface is unstructured at section granularity.** 65% of expensive Wikimedia requests are AI scrapers collecting undifferentiated full-article data.

## 4. Competitive landscape — why no provider has replaced Wikipedia in 2026

Eight cross-cutting structural reasons (25 providers audited across: collaborative knowledge
bases / public wiki engines / developer documentation site generators / personal-networked-thought tools):

1. **Audience mismatch.** Notion/Confluence/Coda were built for private organizational knowledge management — access-control model, pricing, and UX all assume a known trusted team.
2. **No editorial constitution.** Wikipedia's NPOV policy, Notability standards, RS policy, NOR rule, and MOS constitute a multi-decade-refined governance organization. No provider ships an equivalent.
3. **Information density floor.** Documentation site generators optimize for prose elegance — the wrong optimization for encyclopedic reference.
4. **Navigation primitive missing.** `[[wikilink]]` red-link signaling, Special:WhatLinksHere, category graph, disambiguation, navbox templates — no other provider ships even the red-link mechanism.
5. **Citations are decorative, not load-bearing.** Wikipedia's claim-level footnote system is unmatched.
6. **No Talk-page substrate.** The epistemic provenance layer — public record of every editorial dispute.
7. **Structural brittleness.** Notion/Coda/ClickUp use proprietary serialization formats; vendor-lock-in risk.
8. **Template homogenization.** Every Docusaurus/Starlight/VitePress site looks structurally identical — documentation aesthetic, not encyclopedic authority.

Genuine advantages competitors have that a 2030 leapfrog should steal:
- **MkDocs Material's instant client-side search** with offline support
- **Capacities' typed-object relationship surface** as navigable article metadata
- **Obsidian Publish's hover-preview popover on `[[wikilinks]]`**

## 5. The market-gap analysis

The gap exists because closing it requires simultaneously building governance software, a
navigation primitive set, and an editorial culture — no commercial incentive in the last
decade has pointed all three directions at once. Commercial incentives (seat licenses to
organizations) actively point away from the Wikipedia structural model.

PointSav's substrate-sovereignty posture, three-tier compute routing, apprenticeship corpus
capture, and editorial-pipeline infrastructure (project-language as gateway) give the
substrate exactly the three preconditions no commercial competitor can simultaneously match.

## 6. Award-winning leapfrog primitives — the prioritized set

Three primitives are first-class (ship in iteration 2); two are second-class (iteration 3+).
All five are additive to existing Wikipedia muscle-memory chrome.

### 6.1 Citation-authority ribbon (FIRST)

A small coloured badge on each entry in the References section indicating source category:
academic (blue) / government-regulator (dark green) / industry-trade (orange) /
direct-primary-source (teal) / news (grey) / web-informal (light grey). Class derived from
citation template type. Emitted as `@type` refinement on `citation` entries in JSON-LD.

Addresses weakness #1 — flat numeric list with no source-authority semantics. Makes the
citation substrate visible at the reading surface, directly expressing BCSC continuous-disclosure
posture: citations are machine-readable, audit-traceable.

**Component:** `components/citation-authority-ribbon/` (this batch).

### 6.2 Research-trail footer block (FIRST)

A collapsible footer block below the References section, rendered when article frontmatter
declares `research_trail: true`. Three subsections per draft-research-trail-discipline
convention (Doctrine claim #39): Research done / Suggested research / Open questions.
Collapsed by default. Emitted as JSON-LD `potentialAction` nodes.

Combination of citation-authority ribbon + research-trail footer makes the article's
epistemological position legible without reading all footnotes. No Wikipedia equivalent.

**Component:** `components/research-trail-footer/` (this batch).

### 6.3 Freshness ribbon — per-section last-content-review date (FIRST)

An optional small badge on each section heading (right of the `[edit]` pencil) showing
the date of the last substantive content change. Three-stop colour scale: fresh / stale /
archived. Derived from git-blame at section level; frontmatter `content_reviewed_on`
per-section override available. Per-section `dateModified` emitted as JSON-LD `WebPageElement`.

Addresses weakness #6 (freshness illusion) and weakness #10 (AI scraper full-article pulls
because section-level freshness is undeclared).

**Component:** `components/freshness-ribbon/` (this batch).

### 6.4 Plain-language toggle backed by curated authored paragraphs (SECOND)

A toggle in the reader-preference toolbar. When active, sections flagged `plain_language: true`
render an alternative lead paragraph at a lower reading level. Plain-language paragraphs are
explicitly authored by humans and committed to the article source — not LLM-generated at
request time. Emitted as `disambiguatingDescription` on Schema.org `TechArticle`.

Second-class because curating paragraphs costs editorial labour that scales linearly.

### 6.5 Citation-graph mini-map — 3-hop neighbourhood (SECOND)

A collapsible section at the article foot showing a small SVG graph: the current article as
centre node, 1-hop outbound wikilinks, 1-hop inbound links. Nodes labelled; edges directional.
Emitted in JSON-LD `relatedLink` and `mentions` arrays.

Second-class because the wikilink graph must be pre-computed — high effort. Worth shipping
when the article corpus reaches ≥200 articles.

## 7. Open questions for project-design ratification

Six real decisions gating substrate work:

(a) **Light/dark theme switching pattern** — Style Dictionary `@value` override / DTCG `$extends` / CSS `:root[data-theme="dark"]` selector.

(b) **`wiki.*` vs `ps-wiki.*` semantic namespace prefix.** Resolved by Master: `wiki.*` approved.

(c) **Variable-font loading vs system-stack.** Resolved by Master: system-stack.

(d) **Density toggle as token vs component state.** Token approach is more portable across rendering environments.

(e) **FLI-banner colour register — amber vs neutral.** Resolved by Master: NEUTRAL. Left-border accent + small disclosure icon; no amber.

(f) **Research-trail visual weight — chrome vs body content.** Affects `article-research-trail-trail-bg` token resolution.

## 8. Award criteria

A wiki shipping Wikipedia muscle memory + the five primitives in §6 is competitive in:
Awwwards Site of the Day / Site of the Year · Webby Award (Websites: Reference) · Information
is Beautiful Awards (Interactive / Tools & Services) · Communication Arts Interactive Annual ·
Open Source Awards (GitNation) · European Open Source Awards 2026 · MIT Technology Review
Breakthrough Technologies.

## 9. Substrate-side scope

Four downstream DESIGN-* drafts staged in the same pickup batch (this batch):
1. `components/citation-authority-ribbon/` — recipe for §6.1
2. `components/research-trail-footer/` — recipe for §6.2
3. `components/freshness-ribbon/` — recipe for §6.3
4. `tokens/dtcg-bundle.json` — DESIGN-TOKEN-CHANGE (master_cosign: 2026-04-30T17:00Z)

The home-grid component (§5 iteration-1 existing implementation) is also in this batch.

The two second-class primitives (§6.4, §6.5) are not staged as DESIGN-COMPONENT drafts
in this batch; pre-emptive token-vocabulary slots may be added to the bundle.

## Research trail

### Done

- Wikipedia Main Page primitive audit (sub-agent A) — full inventory with format invariants
- Wikipedia article-shell anatomy under Vector 2022 (sub-agent B) — primitive inventory + weakness analysis
- Competitive landscape audit — 25 providers across 4 groups (sub-agent C)
- DTCG token-vocabulary proposal (sub-agent D) — three-tier taxonomy, full token inventory
- Existing draft review (topic-wikipedia-leapfrog-design, component-home-grid) — additive, no duplication
- naming-convention.md §2 §3 §4 §6 §10 — repo-rule design intent + 9-category set
- conventions/cluster-design-draft-pipeline.md §1 §3 §6 — DESIGN-* schema and master-cosign requirements
- conventions/draft-research-trail-discipline.md — Doctrine claim #39

### Suggested

- Verify Carbon Tag baseline for citation badge visual treatment
- WCAG contrast audit for all 6 badge colour classes
- Grid breakpoint alignment with Carbon Grid breakpoints (960px vs Carbon's 1056px medium)

### Open questions

- §7(a) light/dark theme switching — implementation strategy decision pending
- §7(f) research-trail visual weight — chrome vs body content posture

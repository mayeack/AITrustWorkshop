# Agentic AI Governance Workshop

Customer-facing site for the **One Cisco — Agentic AI Governance Workshop**, published with
GitHub Pages at:

**https://mayeack.github.io/AITrustWorkshop/**

A hands-on workshop for governing agentic AI across four correlated pillars — **Measure,
Secure, Observe, Govern** — on a live multi-agent demo application.

## Stack

Hugo (0.161+ extended) with the
[splunk/hugo-theme-splunk-workshop](https://github.com/splunk/hugo-theme-splunk-workshop)
theme, vendored as a git submodule at `themes/hugo-theme-splunk-workshop`. The site is built
and published by GitHub Actions (`.github/workflows/pages.yml`) on every push to `main`
(repo Settings → Pages → Source must be "GitHub Actions").

## Layout

- `content/_index.md` — Home (hero + the workshop narrative). **Generated** by
  `build_index.py`; do not hand-edit.
- `content/workshops/ai-trust-healthcare/` — the workshop pages: `01-setup.md`,
  `02-overview.md`, `03-lab-1-measure.md` … `06-lab-4-govern.md`, `07-wrap-up.md`,
  `08-reference.md`. Sidebar order comes from `weight` in each page's front matter.
  One directory per vertical: each verticalized workshop is its own section under
  `content/workshops/` (`ai-trust-healthcare`, `ai-trust-<vertical>`, …), so
  the URL is `/workshops/<vertical-slug>/`. `build_index.py` builds the healthcare
  vertical by default — set `WORKSHOP_SLUG` to target another one.
- `static/images/` — screenshots, referenced as `/images/image-NN.png`.
- `hugo.toml` — site config and theme params (branding, colors, layout toggles).

## Editing

```bash
git clone --recurse-submodules git@github.com:mayeack/AITrustWorkshop.git
hugo server          # local preview at http://localhost:1313/AITrustWorkshop/
```

Commit to `main` and push — the Pages workflow rebuilds the site (~1–2 min).

## Conventions

- **Customer-facing.** No internal sales positioning or facilitator-only delivery notes.
- **Home mirrors the canonical workshop narrative verbatim.** When the narrative changes,
  run `python3 build_index.py` (reads `../collateral/1 - narrative.md`); it regenerates
  `content/_index.md` and re-syncs the five Executive-outcome callouts onto the
  overview/lab pages (between the `<!-- exec-outcome:start/end -->` markers).
- **Callout standards** (theme `notice` shortcode):
  - Executive outcomes: `{{% notice style="info" title="Executive outcome" icon="star" %}}` — applied
    automatically by `build_index.py`; never hand-edit between the exec-outcome markers.
  - Lab objectives: `{{% notice style="info" title="Objective" icon="target" %}}` at the top of each
    lab/overview page.
  - Personas: `{{% notice style="info" title="Who this is for" icon="users" %}}` between the
    `<!-- persona:start/end -->` markers.
  - Operational asides: `{{% notice note %}}`; cautions: `{{% notice warning %}}`.
- The lab commands reference the demo application repo
  ([PseudoCo Assistant](https://github.com/mayeack/PseudoCoAssistant)) — `scripts/demo/seed_governance_scenarios.py`,
  `scripts/demo/galileo_eval_prescription.py`, and the `/api/incident/*` endpoints.

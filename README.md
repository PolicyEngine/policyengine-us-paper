# policyengine-us-paper

The canonical, versioned model paper for PolicyEngine US: description and
validation of the full tax-benefit microsimulation model — rules coverage,
data (the populace stack), and validation against administrative outturns
and incumbent models (TAXSIM, and against CBO, JCT, and TPC published scores where comparable).

Every serious model has this citation (EUROMOD's Sutherland–Figari 2013,
TAXSIM's Feenberg–Coutts); PolicyEngine US does not yet. The paper is
*versioned*: v1 documents the model as deployed in 2026; engine migrations
later produce a v2 rather than invalidating v1.

Validation assets to assemble from: the policyengine-us test suite and YAML case law, TAXSIM cross-validation work, PolicyBench task provenance, and the populace-us release dossiers.

Target venue: International Journal of Microsimulation (diamond open
access); arXiv preprint on completion.

## Status: v1 outline (issue #1)

This is the outline stage: every section stub in `paper/sections/` states
its planned claims and, for each, either an `\evidence{...}` pointer to a
specific existing file or URL, or an explicit `\todo{...}` marking a gap.
The build renders end to end (`quarto render paper/index.qmd`) with all
sections present as stubs; no numeric claim is asserted without a cited
source, and every `\todo{}` is a to-do for whoever writes the full draft,
not a silent gap.

### Outline structure

1. **Abstract** — placeholder; claim list to write once Sections 2–5 have
   real numbers.
2. **Introduction** (`sections/introduction.tex`) — situates the paper
   against EUROMOD/TAXSIM's canonical-citation precedent, states the
   versioning rule (when a v2 is warranted vs. when new numbers just
   extend v1), and states scope.
3. **Model description** (`sections/model.tex`) — architecture,
   rules-coverage counts, parameter provenance, coverage-over-time.
4. **Data** (`sections/data.tex`) — the populace stack, calibration to
   administrative totals, release provenance (Hugging Face-published
   bundles, the release contract, TRACE/TRO provenance records).
5. **Validation** (`sections/validation.tex`) — against TAXSIM, against
   administrative aggregates (IRS SOI), against JCT/CBO published scores,
   and an explicit note on why PolicyBench is not administrative
   validation.
6. **Discussion** (`sections/discussion.tex`) — placeholder; points to
   address once real numbers are in.
7. **Conclusion** (`sections/conclusion.tex`) — placeholder.
8. **Disclosures** (`sections/disclosures.tex`) — conflict of interest,
   funding (TODO), data/code availability, version pins (TODO).

### Evidence already mapped (cite directly, no new analysis needed)

- Federal/state income tax "Validated against NBER TAXSIM" note in
  `policyengine-us/policyengine_us/programs.yaml`.
- `policyengine-us/docs/validation/taxsim.ipynb` — $100-tolerance TAXSIM
  comparison methodology (re-run to get current numbers; the notebook
  itself is existing evidence).
- `policyengine-taxsim/dashboard/build/data/{2021..2024}/comparison_results_{year}.csv`
  — 6,000 households/year, exact-match TAXSIM comparison.
- `populace/.../us/soi_baseline_levels.json` — 9 IRS SOI (Pub 1304)
  out-of-sample baseline-level benchmarks, with exact dollar values and
  source URLs.
- `populace/.../us/obbba_reforms.json` — 19 OBBBA provisions scored against
  JCT document JCX-35-25 (published 2025-07-01), with per-provision JCT
  dollar scores and source citations.
- `populace/.../us/tax_expenditure_reforms.json` — 5 tax-expenditure reform
  rows benchmarked against JCT JCX-48-24 / Treasury OTA (one flagged
  in-sample; exclude from independent-validation claims).
- `populace/.../us/fiscal_target_references.json` — 5 JCT tax-expenditure
  calibration targets (these are calibration, not independent validation).
- `populace/packages/populace-data/src/populace/data/contract.py` — the
  release contract's per-target calibration tolerance gates (schema only;
  populated numbers are published to Hugging Face, not committed in-repo).

### Evidence gaps (`TODO(evidence needed)` in the stubs)

- A populated calibration-diagnostics artifact for a specific certified
  release (numbers live on Hugging Face `policyengine/populace-us`, not in
  the populace working tree — fetch, don't fabricate).
- A committed, printed PE-vs-JCT/CBO results table (the scoring
  infrastructure and targets are committed; the output of running it
  against a specific release is not).
- Any Tax Policy Center (TPC) comparison — none found during outline
  drafting.
- The exact bibliographic record for the Feenberg–Coutts TAXSIM citation
  (see `docs/pending-citations.md`).
- Whether parameter YAML files uniformly carry a legislative `reference`
  field (CLAUDE.md states the convention; not verified at scale).
- A `bottom-50-tax-analysis` repo comparison of PolicyEngine income-tax
  aggregates against CBO baseline receipts projections exists but was not
  fully surveyed during outline drafting — verify before citing.

### Open methodological questions

- The TAXSIM notebook (tolerance-based) and the policyengine-taxsim
  dashboard tables (exact-match) use different comparison conventions and
  may not share a TAXSIM version or CPS vintage — reconcile before citing
  both as one validation surface.
- Whether benefit programs (as opposed to federal/state income tax) have
  any committed cross-model or administrative-outturn validation at all —
  not confirmed either way during this survey.

## Build

```bash
quarto render paper/index.qmd   # builds the manuscript (PDF + HTML)
```

Requires `quarto` and a TeX distribution with `pdflatex` on `PATH`. CI
(`.github/workflows/paper.yml`) renders HTML only on every PR touching
`paper/**`.

## Layout

- `paper/` — Quarto + LaTeX manuscript (IJM style), sections under
  `paper/sections/`.
- `paper/bibliography/references.bib` — only bibliographic entries verified
  against a primary source; see its header comment.
- `docs/pending-citations.md` — citations named in the outline but not yet
  verified.
- `CONTRIBUTING.md` — the evidence rule and review-tier doctrine this
  repository follows.

# Contributing

## Review tiers

Work in this repository routes by issue label, following the portfolio-wide
doctrine (PolicyEngine/populace#305): `tier:fable` (frontier-model review:
claim-bearing prose, statistical semantics, framing that could read as
advocacy) versus `tier:standard` (spec-complete assembly; acceptance tests
judge the output). Issue #1 (this outline) is `tier:standard`: the
acceptance test is that every claim maps to an existing evidence artifact
or is marked `TODO(evidence needed)` -- not that the prose itself has been
reviewed for framing.

## The evidence rule

Every claim in `paper/sections/*.tex` must resolve to one of:

1. A `\evidence{...}` annotation citing a specific file path or URL that
   already contains the claimed fact, checked during drafting.
2. A `\citep{...}` to a verified bibliography entry in
   `paper/bibliography/references.bib` (see that file's header comment: an
   entry may only be added after its bibliographic record is confirmed
   against a primary source).
3. A `\todo{...}` explicitly marking the claim as pending -- either
   `TODO(evidence needed)` for a claim with no known existing source, or a
   more specific instruction (e.g. "regenerate this notebook's output
   before citing its numbers") for a claim whose evidence exists but has
   not been re-verified at manuscript-drafting time.

Do not write a number, a citation, or a named comparison from memory. If a
number was true in a prior release, a prior conversation, or a prior paper,
it must be re-verified against a current artifact before entering this
manuscript -- models and calibrated data change version to version, and
this paper's whole purpose is to be the citable, versioned source of truth
rather than another number that drifts silently out of date.

## Guardian claims

Two claim types in this paper have already caused near-misses during
outline drafting and deserve extra scrutiny in review, regardless of green
CI:

- **In-sample vs. out-of-sample.** Several JCT-referenced figures in
  `paper/sections/validation.tex` (Section 5.3) are calibration targets,
  not independent checks (see `tax_expenditure_reforms.json`'s `in_sample`
  flag and `fiscal_target_references.json`'s targets). A claim of
  independent validation against JCT/CBO must exclude in-sample rows.
- **PolicyBench is not administrative validation.** PolicyBench scores
  language models against PolicyEngine's own output, not against
  administrative data (`paper/index.qmd:1081` in the PolicyBench repo
  states this explicitly). Do not cite PolicyBench results as evidence that
  PolicyEngine US matches administrative outturns.

## Build

```bash
quarto render paper/index.qmd   # builds the manuscript (PDF + HTML)
```

Requires `quarto` and a TeX distribution with `pdflatex` on `PATH`
(TeX Live via TinyTeX or a system install; the `ijm.sty` style shim avoids
`mathptmx`'s missing-font issue on TinyTeX installs).

## Layout

- `paper/` -- Quarto + LaTeX manuscript (International Journal of
  Microsimulation style), sections under `paper/sections/`.
- `docs/pending-citations.md` -- citations named in the outline but not yet
  verified against a primary source; do not add them to
  `references.bib` until verified.

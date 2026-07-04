# Pending citations

Citations named in the outline that have not been verified against a
primary source and must be confirmed before they enter
`paper/bibliography/references.bib`. Do not add a citation to the
bibliography from memory; add it only after checking the bibliographic
record (year, venue, volume, pages) against the original publication or its
publisher page.

## Feenberg and Coutts, TAXSIM introduction

Referenced by name in this repository's seed README as TAXSIM's canonical
citation (parallel to `sutherland2013euromod` for EUROMOD), and TAXSIM's own
site (<https://taxsim.nber.org/taxsim35/>) attributes the model to Feenberg
and Coutts. The exact bibliographic record was not confirmed against a
primary source during outline drafting (2026-07-04). Before citing it in
the manuscript:

1. Check <https://taxsim.nber.org/taxsim35/> for the citation NBER itself
   recommends.
2. Confirm year, journal/working-paper series, volume, and pages.
3. Add the verified entry to `paper/bibliography/references.bib` and cite it
   with `\citep{feenberg1993taxsim}` (or whatever key the verified year
   implies) in `paper/sections/introduction.tex`, where a placeholder
   sentence currently describes the citation without invoking it.

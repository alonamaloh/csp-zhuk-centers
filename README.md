# Zhuk's centers and ternary absorption

A complete, self-contained proof that the left center of a subdirect relation
between two finite idempotent algebras absorbs — and that the absorption is
witnessed by a **ternary** term.

Precisely: let `A` and `B` be finite idempotent algebras of a common signature,
let `R ≤ A × B` be subdirect, and let

```
C = { a ∈ A : {a} × B ⊆ R }
```

be its *left center*. If `B` has a Taylor term and no nonempty proper binary
absorbing subuniverse, then `C` centrally absorbs `A`, and some ternary term `s`
satisfies

```
s(C, A, C) ∪ s(C, C, A) ∪ s(A, C, C) ⊆ C.
```

This is Zhuk's key structural lemma from the proof of the CSP dichotomy
conjecture, together with the Zhuk–Kozik essential doubling trick that forces
ternary absorption. The first half produces a witnessing term of arity
`k^(|B|-1)`; the second half does not compress that term, but shows that no
ternary essential relation can exist, from which the relational description of
absorption yields the *existence* of a ternary witness.

## The document

| File | Pages | What it is |
| --- | --- | --- |
| [`zhuk_centers.tex`](zhuk_centers.tex) | 24 | The proof, written at formalization granularity, with a statement-level citation index, a suggested module order, an explicit imported-background appendix, and a concordance with the source. |

The compiled PDF is committed alongside the source.

## The route

**Part I — vocabulary.** Signatures, subuniverses, terms, term operations, and
simultaneous substitution of terms into terms with its evaluation law. Four
closure facts carry the whole argument: term operations preserve subuniverses; a
generated subuniverse is the set of values of terms on a *fixed* list of
generators; homomorphisms commute with generation; and the two relational
constructions (intersect with a box, project) preserve subuniverses. Then
absorption, binary absorption, and the lemma converting a one-sided closure
condition into two-sided binary absorption via a single Taylor identity.

**Part II — the arity of absorption.** An `m`-ary `S`-essential relation meets
every box with one coordinate free and the rest confined to `S`, but misses the
all-`S` box. It is exactly the obstruction to `m`-ary absorption: `S` absorbs
with respect to an `m`-ary term precisely when no such relation exists. This
equivalence is what later converts "absorbs at some arity" into "absorbs at
arity 3", so it is proved here rather than cited. Essentiality is defined
relative to a partition of an arbitrary finite index set, which is what lets the
free algebra `A^(A^m)` be fed to it directly.

**Part III — the centers.** Applying a Taylor term of `B` to one element of `A`
and several elements of `C` strictly enlarges its `R`-neighborhood in `B`, unless
that neighborhood is a binary absorbing subalgebra. Iterating `|B|-1` times drives
the value into `C`. A separate argument shows the absorption is *central*. The
doubling trick then turns a ternary essential relation into ones of unboundedly
growing arity, which central absorption forbids — so no ternary essential
relation exists, and some ternary term witnesses the absorption.

## Relation to the source

The proof follows Section 3.10 of Zarathustra Brady's *Notes on CSPs and
Polymorphisms* (<https://notzeb.com/csp-notes.pdf>, arXiv:2210.07383), which is
where the argument is assembled in this form, together with the relational
description of absorption from its Section 3.8. Appendix D is a
statement-by-statement concordance, with a column recording where the version
proved here differs in strength or hypotheses from the source.

Three separable ingredients:

- the **left-center argument** is due to Zhuk (*A proof of the CSP dichotomy
  conjecture*, JACM 67(5), 2020);
- the **essential doubling trick** is attributed by Brady to Zhuk and Kozik;
- the **relational description of absorption** — Part II here, and what turns
  absorption at some arity into absorption at arity 3 — is due to Barto and
  Kazda (*Deciding absorption*, IJAC 26(5), 2016).

Barto and Kozik's absorption theorem is the older tool the mechanism replaces.
The contribution of this document is to expand the dependency chain into a form
a proof assistant can consume, and to pin down the conventions — chiefly around
empty subuniverses and the exact quantifier form of absorption — where an
informal reading has latitude that a formal one does not.

Brady's notes are not redistributed here. The `.gitignore` lists the files
fetched from <https://github.com/notzeb/all> for local reference.

## Building

Requires a TeX distribution with `lmodern`, `amsmath`/`amsthm`, `longtable`,
`fancyhdr`, and `hyperref`. `microtype` is not used, and no bibliography
processor is needed.

```sh
pdflatex zhuk_centers.tex        # rerun until cross-references stabilize,
                                 # normally two or three passes
```

Appendix A — the statement-level citation index — is generated, not written by
hand. After changing any statement or proof, regenerate it and rebuild:

```sh
python3 regen_appendix.py        # rewrites Appendix A in place
```

It parses the labelled environments and their proofs, collects the
cross-references in each scope, and rewrites the table rows. Appendix B (the
suggested module order) is coarser and is maintained by hand.

## Status

Fifth draft, after four rounds of review, the last from a second independent
reviewer. Every round confirmed the central mathematics, including the two
arguments the first draft flagged as riskiest — the block-regrouping induction
(Lemma 3.7) and the minimality argument in the doubling trick (Step 1 of
Lemma 7.1). The defects found were all in the foundations, in quantifier
discipline, and in type-level bookkeeping, and are repaired:

- **Term substitution was missing.** The first draft defined only variable
  renaming along a bijection, which covers none of the three constructions that
  need it — `t(x_{u(1)},…,x_{u(k)})`, the star powers, and `t(x₁,…,x₁,x₂,…,x₂)`
  are all simultaneous substitutions. Now Definition 1.9 with an evaluation law
  (Lemma 1.10).
- **Two theorems quantified over an unused center element.** Writing "for all
  `c₁,…,c_k ∈ C`, replace `c_i` by `a ∈ A`" leaves `c_i` unused and makes the
  statement vacuous when `C = ∅`, including at arity 1 where the intended
  content is not vacuous. Theorems 5.1 and 5.2 are now stated over tuples
  constrained coordinatewise, matching the absorption definition, so the
  degenerate case dissolves rather than needing a detour.
- **Products, and essentiality, are indexed by arbitrary finite sets.**
  Theorem 3.10 forms `A^(A^m)` and projects onto a subset `X ⊆ A^m`, which the
  old ordered-product form did not cover. Defining essentiality relative to a
  partition of an arbitrary finite index set (Definition 3.2) removed the need
  for any transport lemma, and removed the "WLOG reorder the blocks" step from
  the regrouping induction: an oversized block is shrunk in place. Index sets
  are kept finite so the foundational boundary stays at finite choice.
- **Standing hypotheses are a labelled convention** (Convention 1.2), not
  prose, with an audit of where each is consumed.
- Attribution corrected (Barto–Kazda for Part II), the concordance qualified
  where this document proves something weaker than the source, and the
  cross-reference index no longer claims to be a dependency graph.

Corrections and gap reports are welcome as issues.

## License

[CC BY 4.0](LICENSE). Share and adapt with attribution.

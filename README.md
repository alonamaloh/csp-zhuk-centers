# Zhuk's centers and ternary absorption

A complete, self-contained proof that the left center of a subdirect relation
between two finite idempotent algebras absorbs — and that the absorption is
witnessed by a **ternary** term.

Precisely: let `A` and `B` be finite idempotent algebras of a common signature,
let `R ≤ A × B` be subdirect, and let

```
C = { a ∈ A : {a} × B ⊆ R }
```

be its *left center*. If `B` has a Taylor term and no proper binary absorbing
subalgebra, then `C` centrally absorbs `A`, and some ternary term `s` satisfies

```
s(C, A, C) ∪ s(C, C, A) ∪ s(A, C, C) ⊆ C.
```

This is Zhuk's key structural lemma from the proof of the CSP dichotomy
conjecture, together with the Zhuk–Kozik essential doubling trick that collapses
the arity of the witnessing term from `k^(|B|-1)` to `3`.

## The document

| File | Pages | What it is |
| --- | --- | --- |
| [`zhuk_centers.tex`](zhuk_centers.tex) | 20 | The proof, written at formalization granularity, with a statement-level citation index, a suggested module order, an explicit imported-background appendix, and a concordance with the source. |

The compiled PDF is committed alongside the source.

## The route

**Part I — vocabulary.** Signatures, subuniverses, terms, term operations. Four
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
arity 3", so it is proved here rather than cited.

**Part III — the centers.** Applying a Taylor term of `B` to one element of `A`
and several elements of `C` strictly enlarges its `R`-neighborhood in `B`, unless
that neighborhood is a binary absorbing subalgebra. Iterating `|B|-1` times drives
the value into `C`. A separate argument shows the absorption is *central*. The
doubling trick then turns a ternary essential relation into ones of unboundedly
growing arity, which central absorption forbids — so no ternary essential
relation exists, and arity 3 suffices.

## Relation to the source

The proof follows Section 3.10 of Zarathustra Brady's *Notes on CSPs and
Polymorphisms* (<https://notzeb.com/csp-notes.pdf>, arXiv:2210.07383), which is
where the argument is assembled in this form, together with the relational
description of absorption from its Section 3.8. Appendix D is a statement-by-
statement concordance. The results are due to Zhuk, and to Barto and Kozik; the
contribution here is to expand the dependency chain into a form a proof
assistant can consume, and to pin down the conventions — chiefly around empty
subuniverses and the exact quantifier form of absorption — where an informal
reading has latitude that a formal one does not.

Brady's notes are not redistributed here. The `.gitignore` lists the files
fetched from <https://github.com/notzeb/all> for local reference.

## Building

Requires a TeX distribution with `lmodern`, `microtype`-free `amsmath`/`amsthm`,
`longtable`, `fancyhdr`, and `hyperref`. No bibliography processor is needed.

```sh
pdflatex zhuk_centers.tex        # run three times, for the table of contents
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

First draft, seeking review. The places most likely to need work are
Lemma 3.6 (the block-regrouping induction behind the relational description of
absorption) and Step 1 of Lemma 7.1 (the minimality argument in the doubling
trick). Corrections and gap reports are welcome as issues.

## License

[CC BY 4.0](LICENSE). Share and adapt with attribution.

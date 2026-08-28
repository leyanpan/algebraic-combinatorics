Declaration: AlgebraicCombinatorics.CauchyBinet.det_charPoly_coeff', AlgebraicCombinatorics.CauchyBinet.det_charPoly_coeff
Module: AlgebraicCombinatorics.CauchyBinet

Statement id: stmt-algebraic-combinatorics-prop.det.charpol-explicit

## INFORMAL STATEMENT
prop.det.charpol-explicit

Let $n\in \mathbb {N}$. Let $A\in K^{n\times n}$ be an $n\times n$-matrix. Let $x\in K$. Let $I_n$ denote the $n\times n$ identity matrix. Then, 

\[  \det (A + x I_n) = \sum _{P\subseteq [n]} \det (\operatorname {sub}_P^P A) \cdot x^{n-|P|} = \sum _{k=0}^{n} \biggl(\sum _{\substack {P\subseteq [n];\\ |P|=n-k}} \det (\operatorname {sub}_P^P A)\biggr) x^k.  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "Q1: Yes. The two Lean declarations jointly imply the informal equality chain. The first states \u201c(A + x \u2022 1).det = \u2211 P, \u2026 det * x ^ (n - #P)\u201d, exactly the first informal sum \u201cdet (A + x I_n) = \u2211_{P\u2286[n]} det(sub_P^P A) \u00b7 x^{n-|P|}\u201d. Here `P : Finset (Fin n)` ranges over all subsets of `[n]`, the repeated `P.orderEmbOfFin` selects the same rows and columns in increasing order, and `x \u2022 (1 : Matrix \u2026)` is the scalar matrix `x I_n`. The second states \u201c(A + x \u2022 1).det = \u2211 k \u2208 range (n + 1), (\u2211 P with #P = n - k, \u2026det) * x ^ k\u201d, matching the sum for `k = 0,\u2026,n` over subsets satisfying `|P| = n-k`. Since both formal right-hand sides equal the same determinant, they also equal each other. Q2: Yes. The informal three-way equality immediately gives each of these two Lean equalities. The elaborated signatures include the folded section binders \u201c{R : Type*} [CommRing R]\u201d; this agrees with the project's determinant convention, which says \u201cWe work over a commutative ring K\u201d (`DeterminantsBasic.lean`, convention `conv.det.K`). There are no additional hypotheses, restricted dimensions, or altered definitions."
}
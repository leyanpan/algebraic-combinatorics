Declaration: AlgebraicCombinatorics.littlewoodRichardson
Module: AlgebraicCombinatorics.SymmetricFunctions.LittlewoodRichardson

Statement id: stmt-algebraic-combinatorics-thm.sf.lr-zy

## INFORMAL STATEMENT
Zelevinsky’s generalized Littlewood–Richardson rule, in Yamanouchi form

Let $\lambda ,\mu ,\nu $ be three $N$-partitions. Then,

\begin{equation}  s_{\nu }\cdot s_{\lambda /\mu }=\sum _{\substack {T\text{ is a }\nu \text{-Yamanouchi}\\ \text{semistandard tableau}\\ \text{of shape }\lambda /\mu }}s_{\nu +\operatorname *{cont}T}. \end{equation}

## VERDICT
{
  "verdict": "drift",
  "justification": "Q1: No. Q2: No. There are two decisive differences. First, the source fixes only \"a commutative ring K\" and defines the ambient ring as \"P ... K[x_1,...,x_N]\", whereas the elaborated target has the additional binder `[IsDomain R]` in `theorem littlewoodRichardson [IsDomain R]`. This restricts the theorem to integral-domain coefficient rings, so the Lean theorem does not cover the source's arbitrary commutative ring. The restriction enters through the target binder and ultimately through the dependency `AlgebraicCombinatorics.alternant_rho_isRegular`, whose formal signature also assumes `[IsDomain R]`; it should instead establish the required regularity over the chapter's arbitrary commutative ring, or the target should be proved by another argument allowing removal of `[IsDomain R]`.\n\nSecond, the source definition says: \"If we don't have \u03bc\u2286\u03bb, then we agree that there are no Young tableaux of shape \u03bb/\u03bc.\" The Lean definition instead unconditionally sets `skewYoungDiagram lam mu := {c | mu c.1 < c.2 \u2227 c.2 \u2264 lam c.1}` and `Tableau lam mu := {c // c \u2208 skewYoungDiagram lam mu} \u2192 Fin N`. Thus, when `mu` is not contained in `lam`, Lean can retain boxes from rows where `mu i < lam i` and consequently admit tableaux, while the source admits none. The same mismatch propagates into `skewSchurPoly`, whose body unconditionally sums over Lean's semistandard tableaux. Since the target quantifies over every three N-partitions without a containment hypothesis, these malformed-shape cases are included. To make the formalization faithful, `Tableau`/`skewYoungDiagram` and `skewSchurPoly` should implement the source convention by yielding no tableaux, and hence the zero skew Schur polynomial, whenever `\u00ac\u2200 i, mu i \u2264 lam i`; merely adding a containment hypothesis to the target would omit source cases rather than formalize them. For contained shapes, the remaining equation and the definitions of semistandardness, content, and `IsYamanouchi` match the quoted informal rule."
}
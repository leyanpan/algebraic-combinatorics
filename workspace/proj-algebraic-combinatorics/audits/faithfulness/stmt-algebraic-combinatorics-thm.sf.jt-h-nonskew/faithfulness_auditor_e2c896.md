Declaration: SymmetricFunctions.jacobiTrudi_h_nonSkew
Module: AlgebraicCombinatorics.SymmetricFunctions.PieriJacobiTrudi

Statement id: stmt-algebraic-combinatorics-thm.sf.jt-h-nonskew

## INFORMAL STATEMENT
thm.sf.jt-h-nonskew

\leanhelper  For non-skew Schur polynomials ($\mu = 0$): 

\[  s_\lambda = \det \left( \left( h_{\lambda _i - i + j} \right)_{1 \leq i,j \leq N} \right).  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint states, \u201cFor non-skew Schur polynomials (\u03bc = 0): s_\u03bb = det((h_{\u03bb_i - i + j})_{1 \u2264 i,j \u2264 N}).\u201d The elaborated Lean signature is `\u2200 {N : \u2115} {R : Type} [CommRing R] (lam : Fin N \u2192 \u2115) (hlam : \u2200 (i j : Fin N), i \u2264 j \u2192 lam j \u2264 lam i), schur \u27e8lam, hlam\u27e9 = (jacobiTrudiMatrixH lam (fun _ => 0)).det`. The binder `hlam` is precisely the blueprint definition of an N-partition as a \u201cweakly decreasing N-tuple of nonnegative integers\u201d; nonnegativity is encoded by the codomain `\u2115`, so it is not an added hypothesis. The referenced definition unfolds to `jacobiTrudiMatrixH lam mu i j = hsymmExt ((lam i : \u2124) - (mu j : \u2124) - i.val + j.val)`, and `hsymmExt n = if 0 \u2264 n then MvPolynomial.hsymm (Fin N) R n.toNat else 0`. Substituting `mu = fun _ => 0` therefore gives entries `h_{lam i - i.val + j.val}`. Since Lean indexes `Fin N` from 0 while the blueprint indexes from 1, this is exactly `h_{\u03bb_(i+1) - (i+1) + (j+1)}`. The integer indexing and value 0 for negative indices agree with the blueprint definition of `h_n`; `MvPolynomial.hsymm` is the sum of all degree-n monomials, as required. Finally, `schur \u27e8lam, hlam\u27e9` unfolds as the sum of tableau monomials over `ssytFinset`, matching the blueprint definition of `s_\u03bb`. The implicit `[CommRing R]` and polynomial type `MvPolynomial (Fin N) R` instantiate the blueprint\u2019s polynomial ring over an arbitrary commutative coefficient ring and introduce no restriction beyond that setting."
}
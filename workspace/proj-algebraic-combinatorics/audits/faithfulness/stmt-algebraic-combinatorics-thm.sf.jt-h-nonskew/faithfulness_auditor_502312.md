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
  "justification": "The informal statement is \u201cFor non-skew Schur polynomials (\u03bc = 0): s_\u03bb = det((h_{\u03bb_i - i + j})_{1 \u2264 i,j \u2264 N}).\u201d The elaborated declaration is `{N : \u2115} {R : Type} [CommRing R] (lam : Fin N \u2192 \u2115) (hlam : \u2200 i j : Fin N, i \u2264 j \u2192 lam j \u2264 lam i) : schur \u27e8lam, hlam\u27e9 = (jacobiTrudiMatrixH lam (fun _ => 0)).det`. The binder `hlam` is not an added mathematical hypothesis: the blueprint definition says an N-partition is a \u201cweakly decreasing N-tuple of nonnegative integers,\u201d and the local `NPartition` structure has exactly `parts : Fin N \u2192 \u2115` and `weaklyDecreasing : \u2200 i j, i \u2264 j \u2192 parts j \u2264 parts i`. The definition `schur lam := \u2211 T \u2208 ssytFinset lam, T.toMonomial` realizes the blueprint\u2019s Schur polynomial. On the right, `jacobiTrudiMatrixH lam mu` has entry `hsymmExt ((lam i : \u2124) - (mu j : \u2124) - (i.val : \u2124) + (j.val : \u2124))`; substituting `mu := fun _ => 0` gives precisely `h_{\u03bb_i-i+j}`. Lean\u2019s indices are zero-based, but replacing blueprint indices i,j by `i.val+1,j.val+1` leaves `-(i.val+1)+(j.val+1) = -i.val+j.val`, so there is no offset error. Finally, `hsymmExt n := if 0 \u2264 n then hsymm (Fin N) R n.toNat else 0`, while Mathlib documents `hsymm` as the nth complete homogeneous symmetric polynomial, the sum of all degree-n monomials. Thus negative subscripts are interpreted as zero and the zero subscript as the degree-zero polynomial 1, as required by the integer-indexed h notation. The implicit `[CommRing R]` and ambient `MvPolynomial (Fin N) R` match the blueprint polynomial ring over a commutative coefficient ring. No quantifier is narrowed and no extra mathematical hypothesis is introduced."
}
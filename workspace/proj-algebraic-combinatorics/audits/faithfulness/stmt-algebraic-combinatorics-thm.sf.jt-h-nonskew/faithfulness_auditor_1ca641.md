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
  "justification": "The informal claim is exactly the non-skew specialization \u201cs_\u03bb = det((h_{\u03bb_i - i + j})_{1 \u2264 i,j \u2264 N})\u201d. The elaborated declaration states, for `{N : \u2115}`, `{R : Type*}`, and `[CommRing R]`, that `schur (R := R) \u27e8lam, hlam\u27e9 = (jacobiTrudiMatrixH (R := R) lam (fun _ => 0)).det`. Its matrix definition has entry `hsymmExt ((lam i : \u2124) - (mu j : \u2124) - (i.val : \u2124) + (j.val : \u2124))`; substituting `mu = 0` gives precisely `h_{\u03bb_i-i+j}`. Using zero-based `Fin N` indices does not alter the expression because the shifts from the informal one-based indices cancel. The definition `hsymmExt n := if 0 \u2264 n then hsymm (Fin N) R n.toNat else 0` supplies the standard convention for negative subscripts. The binder `hlam : \u2200 i j, i \u2264 j \u2192 lam j \u2264 lam i` merely packages \u03bb as the weakly decreasing N-partition required by the phrase \u201cSchur polynomial\u201d; it is not an added mathematical restriction. Likewise `[CommRing R]` matches the source setting of polynomials over a commutative ring. Thus the Lean equality implies the displayed informal equality, and the informal equality in that setting implies the Lean statement."
}
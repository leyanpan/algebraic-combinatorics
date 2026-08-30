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
  "justification": "The informal formula is \u201cs_\\lambda = \\det((h_{\\lambda_i-i+j})_{1 \\leq i,j \\leq N})\u201d for an N-partition \\lambda. The elaborated signature quantifies \u201c{N : \u2115} {R : Type u} [CommRing R] (lam : Fin N \u2192 \u2115) (hlam : \u2200 (i j : Fin N), i \u2264 j \u2192 lam j \u2264 lam i)\u201d and concludes \u201cschur \u27e8lam, hlam\u27e9 = (jacobiTrudiMatrixH lam (fun _ => 0)).det\u201d. The binder `hlam` is not an added mathematical hypothesis: together with `lam : Fin N \u2192 \u2115`, it is exactly the blueprint definition of an N-partition as a weakly decreasing N-tuple of nonnegative integers. The referenced local structure confirms this with fields `parts : Fin N \u2192 \u2115` and `weaklyDecreasing : \u2200 i j, i \u2264 j \u2192 parts j \u2264 parts i`. The matrix definition has entry `hsymmExt ((lam i : \u2124) - (mu j : \u2124) - (i.val : \u2124) + (j.val : \u2124))`; setting `mu` to zero gives precisely `h_{\u03bb_i-i+j}`. Lean uses zero-based `Fin N` indices, but the common shift from the informal one-based indices cancels in `-i+j`. Finally, `hsymmExt n` is `hsymm (Fin N) R n.toNat` when `0 \u2264 n` and zero otherwise, matching the blueprint's integer-indexed complete homogeneous polynomial convention, while `schur` is definitionally the sum of tableau monomials. The coefficient setting also matches the blueprint polynomial-ring definition, which uses `[CommRing K]`. Thus the declaration states the intended non-skew Jacobi\u2013Trudi identity without narrowing its partitions or index range."
}
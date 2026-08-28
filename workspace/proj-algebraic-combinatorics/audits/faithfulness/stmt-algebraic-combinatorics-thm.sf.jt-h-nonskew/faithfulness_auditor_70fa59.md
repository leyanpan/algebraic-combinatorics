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
  "justification": "Q1: Yes. The elaborated declaration quantifies over `{N : \u2115}`, `{R : Type u}`, `[CommRing R]`, `lam : Fin N \u2192 \u2115`, and `hlam : \u2200 i j : Fin N, i \u2264 j \u2192 lam j \u2264 lam i`, so `\u27e8lam, hlam\u27e9` is exactly an N-partition. Its conclusion is `schur (R := R) \u27e8lam, hlam\u27e9 = (jacobiTrudiMatrixH (R := R) lam (fun _ => 0)).det`. The referenced definition expands the matrix entry to `hsymmExt ((lam i : \u2124) - (0 : \u2124) - (i.val : \u2124) + (j.val : \u2124))`, while `hsymmExt` is `if 0 \u2264 n then hsymm (Fin N) R n.toNat else 0`. Thus the right side is precisely the determinant of `(h_{\u03bb_i-i+j})` with the usual negative-index convention. Although Lean uses zero-based `Fin N` indices, replacing source indices i,j by `i.val + 1,j.val + 1` leaves `-i+j` unchanged. The matrix has row and column type `Fin N`, matching the informal range `1 \u2264 i,j \u2264 N`. The left side uses `schur`, defined as `\u2211 T \u2208 ssytFinset lam, T.toMonomial`, matching the source definition of `s_\u03bb` as the sum of tableau monomials. Q2: Yes. The informal phrase \"For non-skew Schur polynomials (\u03bc = 0)\" and formula `s_\u03bb = det((h_{\u03bb_i-i+j})_{1 \u2264 i,j \u2264 N})` implicitly require \u03bb to be an N-partition; `hlam` merely packages that requirement and is not an added restriction. The ambient source convention fixes an arbitrary commutative ring and N, matching Lean's implicit `{R}` with `[CommRing R]` and `{N}`. The target explicitly uses N for both the determinant size and the N-variable Schur polynomial, as Lean does through `Fin N`; unlike the more general source theorem with an independent partition length M, no independent M appears in this informal target. Therefore each statement implies the other."
}
Declaration: LGV.lgv_nonpermutable
Module: AlgebraicCombinatorics.Determinants.LGV2

Statement id: stmt-algebraic-combinatorics-cor.lgv.kpaths.wt-np

## INFORMAL STATEMENT
LGV lemma, nonpermutable lattice weight version

Consider the setting of Theorem~ \ref{thm.lgv.kpaths.wt}, but additionally assume that 

\begin{align}  \operatorname {x}(A_1) & \ge \operatorname {x}(A_2) \ge \cdots \ge \operatorname {x}(A_k);  \\ \operatorname {y}(A_1) & \le \operatorname {y}(A_2) \le \cdots \le \operatorname {y}(A_k);  \\ \operatorname {x}(B_1) & \ge \operatorname {x}(B_2) \ge \cdots \ge \operatorname {x}(B_k);  \\ \operatorname {y}(B_1) & \le \operatorname {y}(B_2) \le \cdots \le \operatorname {y}(B_k).  \end{align}

 Here, $\operatorname {x}(P)$ and $\operatorname {y}(P)$ denote the two coordinates of any point $P \in \mathbb {Z}^2$. 

Then, there are no nipats from $\mathbf{A}$ to $\sigma (\mathbf{B})$ when $\sigma \in S_k$ is not the identity permutation $\operatorname {id} \in S_k$. Therefore, the claim of Theorem~ \ref{thm.lgv.kpaths.wt} simplifies to 

\begin{equation}  \det \! \left(\left(\sum _{p : A_i \to B_j} w(p)\right)_{1 \le i \le k,\;  1 \le j \le k}\right) = \sum _{\substack {\mathbf{p} \text{ is a nipat} \\ \text{from } \mathbf{A} \text{ to } \mathbf{B}}} w(\mathbf{p}).  \end{equation}

## VERDICT
{
  "verdict": "faithful",
  "justification": "Q1: Yes. The elaborated signature quantifies over exactly the informal setting: `{K : Type} [CommRing K]`, `{k : \u2115}`, `w : ArcWeight integerLattice K`, and `A B : kVertex (\u2124 \u00d7 \u2124) k`. Its hypotheses `hxA : xDecreasing A`, `hyA : yIncreasing A`, `hxB : xDecreasing B`, and `hyB : yIncreasing B` exactly encode the four displayed weak orderings. In particular, `xDecreasing A` unfolds to `\u2200 i j : Fin k, i \u2264 j \u2192 xCoord (A j) \u2264 xCoord (A i)`, while `yIncreasing A` unfolds to `\u2200 i j : Fin k, i \u2264 j \u2192 yCoord (A i) \u2264 yCoord (A j)`, with `xCoord := Prod.fst` and `yCoord := Prod.snd`; the same applies to B. The lattice also has the intended meaning: `integerLattice.arc u v := (v.1 = u.1 + 1 \u2227 v.2 = u.2) \u2228 (v.1 = u.1 \u2227 v.2 = u.2 + 1)`, namely east and north unit steps. The formal conclusion `(pathWeightMatrix integerLattice_pathFinite w A B).det = nipatWeightSum integerLattice_pathFinite w A B (Equiv.refl (Fin k))` expands on the left to the matrix with entries `\u2211 p \u2208 pathsFromTo ... (A i) (B j), pathWeight w p`, and on the right to the sum over nonintersecting path tuples from A to B of `pathTupleWeight`, matching the informal equation. The informal preliminary claim, quoted as \u201cthere are no nipats from A to \u03c3(B) when \u03c3 \u2208 S_k is not the identity,\u201d is represented by the declared dependency `LGV.no_nipats_nonidentity`, whose conclusion is `nipatSet ... A (permuteKVertex \u03c3 B) = \u2205` under the same sorting hypotheses and `h\u03c3 : \u03c3 \u2260 Equiv.refl (Fin k)`. Thus it is not lost merely because the target declaration records the resulting simplified equality. Q2: Yes. The informal assumptions supply precisely the formal binders and hypotheses, and its displayed determinant identity is precisely the formal conclusion after unfolding `pathWeightMatrix`, `nipatWeightSum`, `pathWeight`, and `pathTupleWeight`. No additional mathematical restriction is introduced by the formal signature; the hidden `CommRing K` binder is explicitly present in the referenced weighted LGV setting (\u201cLet K be a commutative ring\u201d)."
}
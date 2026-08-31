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
  "justification": "The elaborated signature has exactly the intended formal setting: `{K : Type u} [CommRing K] {k : \u2115} (w : ArcWeight integerLattice K) (A B : kVertex (\u2124 \u00d7 \u2124) k)`. This answers the blueprint\u2019s \u201cLet K be a commutative ring\u201d, arbitrary arc weights, `k \u2208 \u2115`, and two k-vertices in `\u2124\u00b2`. The hypotheses `(hxA : xDecreasing A) (hyA : yIncreasing A) (hxB : xDecreasing B) (hyB : yIncreasing B)` match the four displayed coordinate chains because `xDecreasing A` is defined as `\u2200 i j : Fin k, i \u2264 j \u2192 xCoord (A j) \u2264 xCoord (A i)`, `yIncreasing A` as `\u2200 i j : Fin k, i \u2264 j \u2192 yCoord (A i) \u2264 yCoord (A j)`, and `xCoord = Prod.fst`, `yCoord = Prod.snd`. The conclusion `(pathWeightMatrix integerLattice_pathFinite w A B).det = nipatWeightSum integerLattice_pathFinite w A B (Equiv.refl (Fin k))` is the displayed blueprint equality: `pathWeightMatrix` has entries `\u2211 p \u2208 pathsFromTo ... (A i) (B j), pathWeight w p`, while `nipatWeightSum` sums `pathTupleWeight` over tuples satisfying `\u2200 i j, i \u2260 j \u2192 \u00acpathsIntersect ...`; `pathsIntersect` means sharing a vertex. The referenced `integerLattice` has precisely east and north arcs. Although the target conclusion does not repeat the preceding sentence \u201cthere are no nipats from A to \u03c3(B) when \u03c3 ... is not the identity\u201d, that assertion is redundant under these exact binders: `LGV.no_nipats_nonidentity` proves for every `(\u03c3 : Equiv.Perm (Fin k)) (h\u03c3 : \u03c3 \u2260 Equiv.refl (Fin k))` that `nipatSet (D := integerLattice) A (permuteKVertex \u03c3 B) = \u2205` from the same four sorting hypotheses. Thus the target\u2019s assumptions entail that part of the blueprint independently, and its explicit conclusion states the resulting determinant identity exactly."
}
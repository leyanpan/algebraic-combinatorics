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
  "justification": "The elaborated signature is `LGV.lgv_nonpermutable {K : Type u} [CommRing K] {k : \u2115} (w : ArcWeight integerLattice K) (A B : kVertex (\u2124 \u00d7 \u2124) k) (hxA : xDecreasing A) (hyA : yIncreasing A) (hxB : xDecreasing B) (hyB : yIncreasing B) : (pathWeightMatrix integerLattice_pathFinite w A B).det = nipatWeightSum integerLattice_pathFinite w A B (Equiv.refl (Fin k))`. Its hidden `[CommRing K]` binder exactly supplies the informal setting inherited from Theorem thm.lgv.kpaths.wt: \u201cLet K be a commutative ring.\u201d The four hypotheses exactly encode the displayed coordinate assumptions: `xDecreasing A := \u2200 i j : Fin k, i \u2264 j \u2192 xCoord (A j) \u2264 xCoord (A i)` and `yIncreasing A := \u2200 i j : Fin k, i \u2264 j \u2192 yCoord (A i) \u2264 yCoord (A j)`, with identical definitions applied to `B`; `xCoord` and `yCoord` are respectively `Prod.fst` and `Prod.snd`. The underlying definitions also agree with the blueprint: `kVertex (\u2124 \u00d7 \u2124) k` is `Fin k \u2192 \u2124 \u00d7 \u2124`; `integerLattice.arc u v` is precisely an east or north unit step; `pathWeightMatrix ... A B` has entry `\u2211 p, pathWeight w p` over paths from `A i` to `B j`; `pathWeight` is the product of the arc weights; and `nipatWeightSum ... A B ...` sums `\u220f i, pathWeight w (pt.paths i)` over path tuples from `A` to `B` satisfying `\u2200 i j, i \u2260 j \u2192 \u00acpathsIntersect ...`, where intersection means sharing a vertex. Thus the conclusion is exactly the informal equation \u201cdet(...) = sum over nipats from A to B of w(p).\u201d The informal preliminary claim, \u201cthere are no nipats from A to \u03c3(B) when \u03c3 ... is not the identity,\u201d is also entailed by the same formal hypotheses through `LGV.no_nipats_nonidentity`, whose signature quantifies `(\u03c3 : Equiv.Perm (Fin k)) (h\u03c3 : \u03c3 \u2260 Equiv.refl (Fin k))` and concludes `nipatSet A (permuteKVertex \u03c3 B) = \u2205`. No additional mathematical hypothesis or narrowed quantifier is present."
}
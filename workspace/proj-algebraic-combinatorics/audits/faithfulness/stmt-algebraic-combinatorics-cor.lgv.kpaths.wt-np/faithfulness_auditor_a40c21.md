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
  "justification": "The elaborated signature is `LGV.lgv_nonpermutable {K : Type u} [CommRing K] {k : \u2115} (w : ArcWeight integerLattice K) (A B : kVertex (\u2124 \u00d7 \u2124) k) (hxA : xDecreasing A) (hyA : yIncreasing A) (hxB : xDecreasing B) (hyB : yIncreasing B) : (pathWeightMatrix integerLattice_pathFinite w A B).det = nipatWeightSum integerLattice_pathFinite w A B (Equiv.refl (Fin k))`. Its hidden `[CommRing K]` binder exactly comes from the referenced setting's \u201cLet K be a commutative ring.\u201d The four hypotheses exactly encode the blueprint conditions: `xDecreasing A := \u2200 i j : Fin k, i \u2264 j \u2192 xCoord (A j) \u2264 xCoord (A i)` and `yIncreasing A := \u2200 i j : Fin k, i \u2264 j \u2192 yCoord (A i) \u2264 yCoord (A j)`, with `xCoord := Prod.fst` and `yCoord := Prod.snd`, and likewise for B. Thus they answer precisely to \u201cx(A\u2081) \u2265 ... \u2265 x(A\u2096)\u201d, \u201cy(A\u2081) \u2264 ... \u2264 y(A\u2096)\u201d, and the corresponding two chains for B, without narrowing the index range. The referenced objects also have the intended meanings: `kVertex V k := Fin k \u2192 V`; `integerLattice.arc u v` says that v is one east or one north step from u; `pathWeightMatrix ... A B` has entry `(i,j)` equal to the sum of `pathWeight` over paths from `A i` to `B j`; and `nipatWeightSum ... A B _\u03c3` is the sum of `pathTupleWeight` over tuples whose component paths share no vertex. The `_\u03c3` argument is definitionally unused because the target tuple B already records the destinations, so passing `Equiv.refl (Fin k)` does not alter the identity-destination sum. Consequently the formal conclusion is exactly the blueprint equation \u201cdet(...) = sum over nipats from A to B of w(p)\u201d. The blueprint's preceding assertion that every nonidentity permutation has no nipats is supplied under the same four hypotheses by `LGV.no_nipats_nonidentity`, whose conclusion is `\u2200 \u03c3, \u03c3 \u2260 Equiv.refl (Fin k) \u2192 nipatSet A (permuteKVertex \u03c3 B) = \u2205`; hence that assertion is also implied by the formal hypotheses and definitions. There are no added mathematical hypotheses beyond the commutative-ring setting explicitly inherited from Theorem thm.lgv.kpaths.wt."
}
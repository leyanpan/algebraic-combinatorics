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
  "justification": "Q1: Yes. The elaborated signature is universally quantified over `{K : Type u} [CommRing K]` and `{k : \u2115}`, matching the inherited setting \u201cLet K be a commutative ring\u201d and \u201cLet k \u2208 \u2115.\u201d Its hypotheses `(hxA : xDecreasing A) (hyA : yIncreasing A) (hxB : xDecreasing B) (hyB : yIncreasing B)` expand exactly to the four displayed weak chains: `xDecreasing A := \u2200 i j : Fin k, i \u2264 j \u2192 xCoord (A j) \u2264 xCoord (A i)` and `yIncreasing A := \u2200 i j : Fin k, i \u2264 j \u2192 yCoord (A i) \u2264 yCoord (A j)`, with the same definitions applied to B. Here `xCoord := Prod.fst` and `yCoord := Prod.snd`, exactly matching \u201cthe two coordinates of any point P \u2208 \u2124\u00b2.\u201d The conclusion `(pathWeightMatrix integerLattice_pathFinite w A B).det = nipatWeightSum integerLattice_pathFinite w A B (Equiv.refl (Fin k))` unfolds on the left to the determinant of the matrix whose `(i,j)` entry is the sum of path weights from `A i` to `B j`, and on the right to the sum of tuple weights over vertex-disjoint path tuples from A to B. The referenced `integerLattice` has precisely the east and north arcs, `PathTuple.isNonIntersecting` says `\u2200 i j, i \u2260 j \u2192 \u00acpathsIntersect ...`, and path and tuple weights are respectively products of arc weights and component-path weights. Although the target conclusion does not syntactically include the preceding sentence \u201cthere are no nipats ... when \u03c3 ... is not the identity,\u201d that assertion follows from the same four hypotheses and definitions, as expressed by the dependency `LGV.no_nipats_nonidentity`; hence the formal theorem together with its hypotheses implies the full informal assertion. Q2: Yes. The informal determinant identity, under exactly those inherited ring, lattice, weight, tuple, and sorting assumptions, is precisely the displayed Lean equality. There are no added mathematical hypotheses, stronger typeclasses, restricted index ranges, or altered path/nonintersection meanings. The identity permutation argument of `nipatWeightSum` is semantically harmless here: its body sums over `nipatFinset ... A B`, and the permutation is intentionally already encoded in the endpoint tuple; for the identity endpoint tuple this is exactly the informal sum from A to B."
}
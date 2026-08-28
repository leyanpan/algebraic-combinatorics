Declaration: AlgebraicCombinatorics.partition_recursive
Module: AlgebraicCombinatorics.PentagonalJacobi

Statement id: stmt-algebraic-combinatorics-cor.pars.pn-rec

## INFORMAL STATEMENT
cor.pars.pn-rec

For each positive integer $n$, we have 

\begin{align*}  p\left( n\right) &  =\sum _{\substack {k\in \mathbb {Z};\\ \begin{bgroup} k\neq 0

\end{bgroup}}}\left( -1\right) ^{k-1}p\left( n-w_{k}\right) \\ &  =p\left( n-1\right) +p\left( n-2\right) -p\left( n-5\right) -p\left( n-7\right) \\ &  \  \  \  \  \  \  \  \  \  \  +p\left( n-12\right) +p\left( n-15\right) -p\left( n-22\right) -p\left( n-26\right) \pm \cdots . \end{align*}

## VERDICT
{
  "verdict": "faithful",
  "justification": "Q1: Yes. The elaborated theorem quantifies exactly over positive naturals, `\u2200 n > 0`, matching \u201cFor each positive integer n\u201d. Its `partitionCount` reduces to `Nat.Partition.partitionCount`, whose body is `fun n => Fintype.card n.Partition`; `Nat.Partition` is defined as multisets of positive integers whose sum is `n`, so this is the intended partition number `p(n)`. Its `pentagonalNumber` body is `((3 * k - 1) * k / 2).toNat`, and the project proves `(pentagonalNumber k : \u2124) = (3 * k - 1) * k / 2`, matching `w_k`. The formal summand sign, `if k.natAbs % 2 = 1 then 1 else -1`, equals `(-1)^(k-1)` for every nonzero integer `k`: it is positive for odd `|k|` and negative for even `|k|`, producing the displayed `+,+,-,-,+,+,-,-,\u2026` pattern at `w_1=1, w_{-1}=2, w_2=5, w_{-2}=7, \u2026`. The formal range `{k : \u2124 // k \u2260 0 \u2227 pentagonalNumber k \u2264 n}` is the finite-support form of the informal `k\u2208\u2124; k\u22600`: terms with `w_k>n` have negative `n-w_k` and are conventionally zero, while the formal statement omits them and uses natural subtraction only where `w_k\u2264n`. Thus the formal equality entails both the compact recurrence and its displayed expansion. Q2: Yes. Conversely, the informal recurrence, restricted to its nonzero terms `w_k\u2264n`, is exactly the formal `tsum`; the subtype is finite because pentagonal numbers grow, so `\u2211'` introduces no convergence strengthening. The cast of the natural-valued partition count into `\u2124` merely supplies the additive group needed for alternating signs. No additional mathematical hypothesis or restriction appears."
}
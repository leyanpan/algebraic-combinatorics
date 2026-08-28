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
  "justification": "Q1: yes. The elaborated declaration states, for `n : \u2115` with `hn : n > 0`, `\u2191(partitionCount n) = \u2211' (k : { k // k \u2260 0 \u2227 pentagonalNumber k \u2264 n }), (if (\u2191k).natAbs % 2 = 1 then 1 else -1) * \u2191(partitionCount (n - pentagonalNumber \u2191k))`. Here `Nat.Partition.partitionCount (n : \u2115) := Fintype.card (Partition n)`, so it is the informal partition number, and `pentagonalNumber (k : \u2124) := ((3 * k - 1) * k / 2).toNat`; the accompanying proved equality identifies its integer value with `(3k-1)k/2`, exactly the informal `w_k`. For nonzero `k`, the formal sign is +1 precisely when `|k|` is odd and -1 when it is even, which equals the informal `(-1)^(k-1)`, including negative `k`. The added index condition `pentagonalNumber k \u2264 n` only removes informal terms with `n-w_k < 0`; the informal definition takes `p(m)` for `m \u2208 \u2124` to be the number of partitions of `m`, hence those removed terms are zero. The listed values `w_1=1`, `w_{-1}=2`, `w_2=5`, `w_{-2}=7`, `w_3=12`, `w_{-3}=15`, `w_4=22`, and `w_{-4}=26` give exactly the displayed expansion. Q2: yes. Starting from the informal sum over `k \u2208 \u2124, k \u2260 0`, discard the zero terms for which `w_k > n`; on the remaining terms, integer subtraction agrees with the formal natural subtraction, yielding exactly the subtype sum in the Lean declaration. The coercion of `partitionCount n` to `\u2124` is necessary encoding for the signed sum and adds no mathematical restriction."
}
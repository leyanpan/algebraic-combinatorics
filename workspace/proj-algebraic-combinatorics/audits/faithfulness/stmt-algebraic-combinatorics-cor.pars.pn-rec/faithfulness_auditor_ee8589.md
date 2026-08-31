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
  "justification": "The elaborated signature is `partition_recursive (n : \u2115) (hn : n > 0) : \u2191(partitionCount n) = \u2211' (k : {k // k \u2260 0 \u2227 pentagonalNumber k \u2264 n}), (if k.val.natAbs % 2 = 1 then 1 else -1) * \u2191(partitionCount (n - pentagonalNumber k.val))`. Its binders `(n : \u2115) (hn : n > 0)` exactly answer the blueprint's \u201cFor each positive integer n.\u201d The dependency `partitionCount` has body `Fintype.card (Partition n)`, matching the blueprint definition `p(n) := (# of partitions of n)`. The dependency `pentagonalNumber` has body `((3 * k - 1) * k / 2).toNat`; the project proves its integer value is `(3k-1)k/2`, matching the blueprint definition `w_k=(3k-1)k/2`. The formal subtype condition `pentagonalNumber k \u2264 n` does not narrow the mathematical recurrence: the omitted indices have `n-w_k<0`, and the blueprint's definition of partitions as finite tuples of positive integers makes `p(n-w_k)=0` there. On retained indices, natural subtraction agrees with integer subtraction. The formal coefficient is `1` when `|k|` is odd and `-1` when it is even, which for nonzero integer `k` equals the blueprint coefficient `(-1)^(k-1)`. Finally, the values `w_1=1`, `w_{-1}=2`, `w_2=5`, `w_{-2}=7`, `w_3=12`, `w_{-3}=15`, `w_4=22`, and `w_{-4}=26` give exactly the displayed expansion `p(n-1)+p(n-2)-p(n-5)-p(n-7)+p(n-12)+p(n-15)-p(n-22)-p(n-26)\u00b1\u22ef`. The coercions show that the equality is correctly asserted in `\u2124`, allowing the alternating signs."
}
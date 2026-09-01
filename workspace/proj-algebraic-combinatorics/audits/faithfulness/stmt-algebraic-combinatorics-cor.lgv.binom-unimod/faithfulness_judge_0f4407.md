## TARGET LGV1.binom_log_concave (theorem) — ELABORATED SIGNATURE
∀ (n k : ℕ), 1 ≤ k → n.choose k * n.choose k ≥ n.choose (k - 1) * n.choose (k + 1)

Docstring: Binomial coefficients are log-concave.
(Corollary cor.lgv.binom-unimod)
Label: cor.lgv.binom-unimod

For k ≥ 1: C(n,k)² ≥ C(n,k-1) · C(n,k+1)

Note: We require k ≥ 1 because in natural number arithmetic, (0:ℕ) - 1 = 0,
so C(n, 0-1) = C(n, 0) = 1, and the inequality 1 ≥ n fails for n ≥ 2.
In the mathematical statement, C(n, -1) = 0, so the k=0 case is trivially true.

Proof sketch (algebraic): Using the recurrences
- C(n, k+1) · (k+1) = C(n, k) · (n-k)
- C(n, k) · k = C(n, k-1) · (n-k+1)
we can show that C(n,k)² / (C(n,k-1) · C(n,k+1)) = (k+1)(n-k+1) / (k(n-k)).
This ratio is ≥ 1 because (k+1)(n-k+1) - k(n-k) = n + 1 ≥ 0.

Combinatorial proof (via LGV): Define lattice points A=(1,0), A'=(0,1),
B=(k+1, n-k), B'=(k, n-k+1). Then det(path matrix) = #nipats ≥ 0. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF instMulNat
Mul ℕ

## BASE-LIBRARY REF Nat.choose
ℕ → ℕ → ℕ

Docstring: `choose n k` is the number of `k`-element subsets in an `n`-element set. Also known as binomial
coefficients. For the fact that this is the number of `k`-element-subsets of an `n`-element
set, see `Finset.card_powersetCard`. 

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF instSubNat
Sub ℕ

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF instAddNat
Add ℕ

## INFORMAL STATEMENT
cor.lgv.binom-unimod

Let $n,k\in \mathbb {N}$. Then, $\binom {n}{k}^{2}\geq \binom {n}{k-1}\cdot \binom {n}{k+1}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.binom.binom
def.binom.binom

For any numbers $n$ and $k$, we set

\begin{equation}  \binom {n}{k}=\begin{cases}  \frac{n\left( n-1\right) \left( n-2\right) \cdots \left( n-k+1\right) }{k!}, &  \text{if }k\in \mathbb {N};\\ 0, &  \text{else.}\end{cases} \end{equation}

 Note that “numbers” is to be understood fairly liberally here. In particular, $n$ can be any integer, rational, real or complex number (or, more generally, any element in a $\mathbb {Q}$-algebra), whereas $k$ can be anything (although the only nonzero values of $\binom {n}{k}$ will be achieved for $k\in \mathbb {N}$, by the above definition).

## VERDICT
{
  "verdict": "drift",
  "justification": "The blueprint quantifies without restriction: \u201cLet $n,k\\in\\mathbb N$. Then \u2026\u201d, so it includes $k=0$. The target instead has the binder `\u2200 (n k : \u2115), 1 \u2264 k \u2192 ...`, adding the mathematically contentful hypothesis `1 \u2264 k` and therefore narrowing the quantified cases. This matters because the informal definition assigns $\\binom n{-1}=0$, making the $k=0$ case true, whereas Lean\u2019s natural subtraction in `n.choose (k - 1)` truncates `0 - 1` to `0`, producing the wrong right-hand factor. The drift enters directly in the target through both the binder `1 \u2264 k \u2192` and the use of `Nat.choose (k - 1)`. To make it faithful, remove the added hypothesis and represent the predecessor-index coefficient with the informal out-of-range convention, e.g. use `if k = 0 then 0 else n.choose (k - 1)`, or define a binomial function on integer indices that is zero for negative indices."
}
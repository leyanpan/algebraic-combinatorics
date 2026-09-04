## TARGET Nat.Partition.divisor_sum_reindex (theorem) — ELABORATED SIGNATURE
∀ (I : Set ℕ) [inst : DecidablePred fun x => x ∈ I] (n : ℕ) (f : ℕ → ℕ),
  ∑ k ∈ Finset.range n, ∑ d ∈ (k + 1).divisors with d ∈ I, d * f (n - k - 1) =
    ∑ d ∈ Finset.Icc 1 n with d ∈ I, d * ∑ j ∈ Finset.Icc 1 (n / d), f (n - d * j)

Docstring: Divisor sum reindexing: swaps the order of summation from
∑_{k=0}^{n-1} ∑_{d | k+1, d ∈ I} to ∑_{d ∈ I, d ≤ n} ∑_{j=1}^{⌊n/d⌋}.

The bijection is: (k, d) ↔ (d, j) where k = d*j - 1, j = (k+1)/d.
This transforms the constraint "d | k+1" to "k = d*j - 1 for some j ≥ 1".

Used in the proof of partitionCount_divisorSum_restricted. 

## BASE-LIBRARY REF Set.Mem
{α : Type u} → Set α → α → Prop

Body:
fun {α} s a => s a

Docstring: Membership in a set 

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Body:
fun {ι} {M} [AddCommMonoid M] s f => (Multiset.map f s.val).sum

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

Body:
inferInstance

## BASE-LIBRARY REF AddCommMonoid
Type u → Type u

Docstring: An additive commutative monoid is an additive monoid with commutative `(+)`. 

## BASE-LIBRARY REF Nat.instAddCancelCommMonoid
AddCancelCommMonoid ℕ

Body:
{ add := Nat.add, add_assoc := Nat.add_assoc, zero := Nat.zero, zero_add := Nat.zero_add, add_zero := Nat.add_zero,
  nsmul := fun m n => m * n, nsmul_zero := Nat.zero_mul, nsmul_succ := Nat.succ_mul, add_comm := Nat.add_comm,
  toIsLeftCancelAdd := Nat.instAddCancelCommMonoid._proof_1 }

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Body:
fun n => { val := Multiset.range n, nodup := ⋯ }

Docstring: `range n` is the set of natural numbers less than `n`. 

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Body:
fun {α} p [DecidablePred p] s => { val := Multiset.filter p s.val, nodup := ⋯ }

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF Nat.divisors
ℕ → Finset ℕ

Body:
fun n => {d ∈ Finset.Ico 1 (n + 1) | d ∣ n}

Docstring: `divisors n` is the `Finset` of divisors of `n`. By convention, we set `divisors 0 = ∅`. 

## BASE-LIBRARY REF Add
Type u → Type u

Docstring: The homogeneous version of `HAdd`: `a + b : α` where `a b : α`. 

## BASE-LIBRARY REF Add.add
{α : Type u} → [self : Add α] → α → α → α

Body:
fun α [self : Add α] => self.1

Docstring: `a + b` computes the sum of `a` and `b`. See `HAdd`. 

## BASE-LIBRARY REF Nat.add
ℕ → ℕ → ℕ

Body:
fun x x_1 =>
  Nat.brecOn (motive := fun x => ℕ → ℕ) x_1
    (fun x f x_2 =>
      (match (motive := ℕ → (x : ℕ) → Nat.below (motive := fun x => ℕ → ℕ) x → ℕ) x_2, x with
        | a, Nat.zero => fun x => a
        | a, b.succ => fun x => (x.1 a).succ)
        f)
    x

Docstring: Addition of natural numbers, typically used via the `+` operator.

This function is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.


## BASE-LIBRARY REF Mul
Type u → Type u

Docstring: The homogeneous version of `HMul`: `a * b : α` where `a b : α`. 

## BASE-LIBRARY REF Mul.mul
{α : Type u} → [self : Mul α] → α → α → α

Body:
fun α [self : Mul α] => self.1

Docstring: `a * b` computes the product of `a` and `b`. See `HMul`. 

## BASE-LIBRARY REF Nat.mul
ℕ → ℕ → ℕ

Body:
fun x x_1 =>
  Nat.brecOn (motive := fun x => ℕ → ℕ) x_1
    (fun x f x_2 =>
      (match (motive := ℕ → (x : ℕ) → Nat.below (motive := fun x => ℕ → ℕ) x → ℕ) x_2, x with
        | x, 0 => fun x => 0
        | a, b.succ => fun x => (x.1 a).add a)
        f)
    x

Docstring: Multiplication of natural numbers, usually accessed via the `*` operator.

This function is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.


## BASE-LIBRARY REF Sub
Type u → Type u

Docstring: The homogeneous version of `HSub`: `a - b : α` where `a b : α`. 

## BASE-LIBRARY REF Sub.sub
{α : Type u} → [self : Sub α] → α → α → α

Body:
fun α [self : Sub α] => self.1

Docstring: `a - b` computes the difference of `a` and `b`. See `HSub`. 

## BASE-LIBRARY REF instSubNat
Sub ℕ

Body:
{ sub := Nat.sub }

Characterization: Natural subtraction truncates: `a - b = 0` whenever `b ≥ a`.

## BASE-LIBRARY REF Nat.sub
ℕ → ℕ → ℕ

Body:
fun x x_1 =>
  Nat.brecOn (motive := fun x => ℕ → ℕ) x_1
    (fun x f x_2 =>
      (match (motive := ℕ → (x : ℕ) → Nat.below (motive := fun x => ℕ → ℕ) x → ℕ) x_2, x with
        | a, 0 => fun x => a
        | a, b.succ => fun x => (x.1 a).pred)
        f)
    x

Docstring: Subtraction of natural numbers, truncated at `0`. Usually used via the `-` operator.

If a result would be less than zero, then the result is zero.

This definition is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.

Examples:
* `5 - 3 = 2`
* `8 - 2 = 6`
* `8 - 8 = 0`
* `8 - 20 = 0`


Characterization: Natural subtraction truncates: `a - b = 0` whenever `b ≥ a`.

## BASE-LIBRARY REF Finset.Icc
{α : Type u_1} → [inst : Preorder α] → [LocallyFiniteOrder α] → α → α → Finset α

Body:
fun {α} [Preorder α] [LocallyFiniteOrder α] a b => LocallyFiniteOrder.finsetIcc a b

Docstring: The finset $[a, b]$ of elements `x` such that `a ≤ x` and `x ≤ b`. Basically `Set.Icc a b` as a
finset. 

## BASE-LIBRARY REF Nat.instPreorder
Preorder ℕ

Body:
inferInstance

## BASE-LIBRARY REF Preorder
Type u_2 → Type u_2

Docstring: A preorder is a reflexive, transitive relation `≤`.
In a preorder, `a < b` means `a ≤ b ∧ ¬b ≤ a`, and `<` is defined this way by default.
You can override this definition to set a better def-eq.


## BASE-LIBRARY REF Nat.instLinearOrder
LinearOrder ℕ

Body:
{ le := Nat.le, lt := Nat.lt, le_refl := Nat.le_refl, le_trans := @Nat.le_trans,
  lt_iff_le_not_ge := @Nat.lt_iff_le_not_le, le_antisymm := @Nat.le_antisymm, toMin := instMinNat, toMax := Nat.instMax,
  toOrd := instOrdNat, le_total := Nat.le_total, toDecidableLE := inferInstance, toDecidableEq := inferInstance,
  toDecidableLT := inferInstance, min_def := Nat.instLinearOrder._proof_1, max_def := Nat.instLinearOrder._proof_2,
  compare_eq_compareOfLessAndEq := Nat.instLinearOrder._proof_3 }

## BASE-LIBRARY REF Nat.instLocallyFiniteOrder
LocallyFiniteOrder ℕ

Body:
{ finsetIcc := fun a b => { val := ↑(List.range' a (b + 1 - a)), nodup := ⋯ },
  finsetIco := fun a b => { val := ↑(List.range' a (b - a)), nodup := ⋯ },
  finsetIoc := fun a b => { val := ↑(List.range' (a + 1) (b - a)), nodup := ⋯ },
  finsetIoo := fun a b => { val := ↑(List.range' (a + 1) (b - a - 1)), nodup := ⋯ }, finset_mem_Icc := ⋯,
  finset_mem_Ico := ⋯, finset_mem_Ioc := ⋯, finset_mem_Ioo := ⋯ }

## BASE-LIBRARY REF Multiset.ofList
{α : Type u_1} → List α → Multiset α

Body:
fun {α} => Quot.mk ⇑(List.isSetoid α)

Docstring: The quotient map from `List α` to `Multiset α`. 

## BASE-LIBRARY REF List.range'
ℕ → ℕ → optParam ℕ 1 → List ℕ

Docstring: Returns a list of the numbers with the given length `len`, starting at `start` and increasing by
`step` at each element.

In other words, `List.range' start len step` is `[start, start+step, ..., start+(len-1)*step]`.

Examples:
 * `List.range' 0 3 (step := 1) = [0, 1, 2]`
 * `List.range' 0 3 (step := 2) = [0, 2, 4]`
 * `List.range' 0 4 (step := 2) = [0, 2, 4, 6]`
 * `List.range' 3 4 (step := 2) = [3, 5, 7, 9]`


## BASE-LIBRARY REF Nat.instLocallyFiniteOrder._proof_10
∀ (a b : ℕ), (List.range' a (b + 1 - a)).Nodup

## BASE-LIBRARY REF Nat.instLocallyFiniteOrder._proof_11
∀ (a b : ℕ), (List.range' a (b - a)).Nodup

## BASE-LIBRARY REF Nat.instLocallyFiniteOrder._proof_12
∀ (a b : ℕ), (List.range' (a + 1) (b - a)).Nodup

## BASE-LIBRARY REF Nat.instLocallyFiniteOrder._proof_13
∀ (a b : ℕ), (List.range' (a + 1) (b - a - 1)).Nodup

## BASE-LIBRARY REF Nat.instLocallyFiniteOrder._proof_3
∀ (a b x : ℕ), x ∈ { val := ↑(List.range' a (b + 1 - a)), nodup := ⋯ } ↔ a ≤ x ∧ x ≤ b

## BASE-LIBRARY REF Nat.instLocallyFiniteOrder._proof_5
∀ (a b x : ℕ), x ∈ { val := ↑(List.range' a (b - a)), nodup := ⋯ } ↔ a ≤ x ∧ x < b

## BASE-LIBRARY REF Nat.instLocallyFiniteOrder._proof_7
∀ (a b x : ℕ), x ∈ { val := ↑(List.range' (a + 1) (b - a)), nodup := ⋯ } ↔ a < x ∧ x ≤ b

## BASE-LIBRARY REF Nat.instLocallyFiniteOrder._proof_9
∀ (a b x : ℕ), x ∈ { val := ↑(List.range' (a + 1) (b - a - 1)), nodup := ⋯ } ↔ a < x ∧ x < b

## BASE-LIBRARY REF Div
Type u → Type u

Docstring: The homogeneous version of `HDiv`: `a / b : α` where `a b : α`. 

## BASE-LIBRARY REF Div.div
{α : Type u} → [self : Div α] → α → α → α

Body:
fun α [self : Div α] => self.1

Docstring: `a / b` computes the result of dividing `a` by `b`. See `HDiv`. 

## BASE-LIBRARY REF Nat.instDiv
Div ℕ

Body:
{ div := Nat.div }

## BASE-LIBRARY REF Nat.div
ℕ → ℕ → ℕ

Body:
fun x y => if hy : 0 < y then Nat.div.go y hy x.succ x ⋯ else 0

Docstring: Division of natural numbers, discarding the remainder. Division by `0` returns `0`. Usually accessed
via the `/` operator.

This operation is sometimes called “floor division.”

This function is overridden at runtime with an efficient implementation. This definition is
the logical model.

Examples:
 * `21 / 3 = 7`
 * `21 / 5 = 4`
 * `0 / 22 = 0`
 * `5 / 0 = 0`


## INFORMAL STATEMENT
lem.pars.divisor-sum-reindex

\leanhelper  For any set $I$ of positive integers, any $n \in \mathbb {N}$, and any function $f$: 

\[  \sum _{k=0}^{n-1} \sum _{\substack {d \mid k+1 \\ d \in I}} d \cdot f(n - k - 1) = \sum _{\substack {d \in I \\ d \leq n}} d \cdot \sum _{j=1}^{\lfloor n/d \rfloor } f(n - d \cdot j).  \]

 The bijection is $(k, d) \leftrightarrow (d, j)$ where $k = d \cdot j - 1$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.commring
def.alg.commring

A \emph{commutative ring} means a set $K$ equipped with three maps

\begin{align*}  \oplus &  :K\times K\rightarrow K,\\ \ominus &  :K\times K\rightarrow K,\\ \odot &  :K\times K\rightarrow K \end{align*}

 and two elements $\mathbf{0}\in K$ and $\mathbf{1}\in K$ satisfying the following axioms: 

\begin{enumerate} \item \emph{Commutativity of addition:} We have $a\oplus b=b\oplus a$ for all $a,b\in K$. 

\item \emph{Associativity of addition:} We have $a\oplus \left( b\oplus c\right) =\left( a\oplus b\right) \oplus c$ for all $a,b,c\in K$. 

\item \emph{Neutrality of zero:} We have $a\oplus \mathbf{0}=\mathbf{0}\oplus a=a$ for all $a\in K$. 

\item \emph{Subtraction undoes addition:} Let $a,b,c\in K$. We have $a\oplus b=c$ if and only if $a=c\ominus b$. 

\item \emph{Commutativity of multiplication:} We have $a\odot b=b\odot a$ for all $a,b\in K$. 

\item \emph{Associativity of multiplication:} We have $a\odot \left( b\odot c\right) =\left( a\odot b\right) \odot c$ for all $a,b,c\in K$. 

\item \emph{Distributivity:} We have

\[  a\odot \left( b\oplus c\right) =\left( a\odot b\right) \oplus \left( a\odot c\right) \  \  \  \  \  \  \  \  \  \  \text{and}\  \  \  \  \  \  \  \  \  \  \left( a\oplus b\right) \odot c=\left( a\odot c\right) \oplus \left( b\odot c\right)  \]

 for all $a,b,c\in K$. 

\item \emph{Neutrality of one:} We have $a\odot \mathbf{1}=\mathbf{1}\odot a=a$ for all $a\in K$. 

\item \emph{Annihilation:} We have $a\odot \mathbf{0}=\mathbf{0}\odot a=\mathbf{0}$ for all $a\in K$. 

\end{enumerate}

The operations $\oplus $, $\ominus $ and $\odot $ are called the \emph{addition}, the \emph{subtraction} and the \emph{multiplication} of the ring $K$. When confusion is unlikely, we will denote these three operations $\oplus $, $\ominus $ and $\odot $ by $+$, $-$ and $\cdot $, respectively, and we will abbreviate $a\odot b=a\cdot b$ by $ab$. 

The elements $\mathbf{0}$ and $\mathbf{1}$ are called the \emph{zero} and the \emph{unity} (or the \emph{one}) of the ring $K$. We will simply call these elements $0$ and $1$ when confusion with the corresponding numbers is unlikely. 

We will use \emph{PEMDAS conventions} for the three operations $\oplus $, $\ominus $ and $\odot $. These imply that the operation $\odot $ has higher precedence than $\oplus $ and $\ominus $, while the operations $\oplus $ and $\ominus $ are left-associative.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.commring.fracs
def.commring.fracs

Let $L$ be a commutative ring. Let $a\in L$. Assume that $a$ is invertible. Then: 

\textbf{(a)} The inverse of $a$ is called $a^{-1}$. 

\textbf{(b)} For any $b\in L$, the product $b\cdot a^{-1}$ is called $\frac{b}{a}$ (or $b/a$). 

\textbf{(c)} For any negative integer $n$, we define $a^{n}$ to be $\left( a^{-1}\right)^{-n}$. Thus, the $n$-th power $a^{n}$ is defined for each $n\in \mathbb {Z}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.commring.fraction
def.commring.fraction

\leanhelper  For an invertible element $a$ and any $b \in L$, the \emph{fraction} $b/a$ is defined as $b \cdot a^{-1}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.commring.inverse
def.commring.inverse

\leanhelper  Let $L$ be a commutative ring and $a, b \in L$. 

\textbf{(a)} We say that $b$ is an \emph{inverse} (or \emph{multiplicative inverse}) of $a$ if $a \cdot b = 1$. 

\textbf{(b)} We say that $a$ is \emph{invertible} in $L$ (or a \emph{unit} of $L$) if $a$ has an inverse.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.commring.inverse-2
def.commring.inverse

Let $L$ be a commutative ring. Let $a\in L$. Then: 

\textbf{(a)} An \emph{inverse} (or \emph{multiplicative inverse}) of $a$ means an element $b\in L$ such that $ab=ba=1$. 

\textbf{(b)} We say that $a$ is \emph{invertible} in $L$ (or a \emph{unit} of $L$) if $a$ has an inverse.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.commring.invertible
def.commring.invertible

\leanhelper  An element $a \in L$ is \emph{invertible} if there exists $b \in L$ such that $a \cdot b = 1$.

## VERDICT
{
  "verdict": "unclear",
  "discrepancies": [],
  "justification": "The blueprint says only \u201cany function $f$\u201d and does not specify its domain, codomain, or coefficient structure, while the elaborated signature fixes `(f : \u2115 \u2192 \u2115)` and performs all sums and products in `\u2115`. The supplied commutative-ring definitions do not connect any ring `K` or `L` to this statement. Thus the package does not determine whether the intended claim is merely for natural-valued functions\u2014under which reading the formal theorem matches\u2014or for functions valued in an arbitrary commutative ring or another structure\u2014under which reading the formal theorem would cover only a special case. A specification of the type of `f` and the intended arithmetic is needed."
}
## TARGET AlgebraicCombinatorics.FPS.unit_zpow_add (theorem) — ELABORATED SIGNATURE
∀ {L : Type u_1} [inst : CommRing L] (u : Lˣ) (m n : ℤ), u ^ (m + n) = u ^ m * u ^ n

Docstring: Power addition rule extends to integer exponents: `u^(m+n) = u^m * u^n`.
Label: def.commring.fracs (c) 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Units
(α : Type u) → [Monoid α] → Type u

Docstring: Units of a `Monoid`, bundled version. Notation: `αˣ`.

An element of a `Monoid` is a unit if it has a two-sided inverse.
This version bundles the inverse element so that it can be computed.
For a predicate see `IsUnit`. 

## BASE-LIBRARY REF MonoidWithZero
Type u → Type u

Docstring: A type `M₀` is a “monoid with zero” if it is a monoid with zero element, and `0` is left
and right absorbing. 

## BASE-LIBRARY REF Semiring
Type u → Type u

Docstring: A `Semiring` is a type with addition, multiplication, a `0` and a `1` where addition is
commutative and associative, multiplication is associative and left and right distributive over
addition, and `0` and `1` are additive and multiplicative identities. 

## BASE-LIBRARY REF NonUnitalSemiring.mul_assoc
∀ {α : Type u} [self : NonUnitalSemiring α] (a b c : α), a * b * c = a * (b * c)

Docstring: Multiplication is associative 

## BASE-LIBRARY REF Semiring.one_mul
∀ {α : Type u} [self : Semiring α] (a : α), 1 * a = a

Docstring: One is a left neutral element for multiplication 

## BASE-LIBRARY REF Semiring.mul_one
∀ {α : Type u} [self : Semiring α] (a : α), a * 1 = a

Docstring: One is a right neutral element for multiplication 

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF CommRing.mul_comm
∀ {α : Type u} [self : CommRing α] (a b : α), a * b = b * a

Docstring: Multiplication is commutative in a commutative multiplicative magma. 

## BASE-LIBRARY REF Pow
Type u → Type v → Type (max u v)

Docstring: The homogeneous version of `HPow`: `a ^ b : α` where `a : α`, `b : β`.
(The right argument is not the same as the left since we often want this even
in the homogeneous case.)

Types can choose to subscribe to particular defaulting behavior by providing
an instance to either `NatPow` or `HomogeneousPow`:
- `NatPow` is for types whose exponents is preferentially a `Nat`.
- `HomogeneousPow` is for types whose base and exponent are preferentially the same.


## BASE-LIBRARY REF Pow.pow
{α : Type u} → {β : Type v} → [self : Pow α β] → α → β → α

Body:
fun α β [self : Pow α β] => self.1

Docstring: `a ^ b` computes `a` to the power of `b`. See `HPow`. 

## BASE-LIBRARY REF DivInvMonoid.toZPow
{M : Type u_2} → [DivInvMonoid M] → Pow M ℤ

Body:
fun {M} [DivInvMonoid M] => { pow := fun x n => DivInvMonoid.zpow n x }

Characterization: `a ^ (n : ℤ)` is `a ^ (n : ℕ)` for `n ≥ 0` and `(a ^ (k+1 : ℕ))⁻¹` for `n = -(k+1)` (`zpow_natCast`, `zpow_negSucc`).

## BASE-LIBRARY REF DivInvMonoid
Type u → Type u

Docstring: A `DivInvMonoid` is a `Monoid` with operations `/` and `⁻¹` satisfying
`div_eq_mul_inv : ∀ a b, a / b = a * b⁻¹`.

This deduplicates the name `div_eq_mul_inv`.
The default for `div` is such that `a / b = a * b⁻¹` holds by definition.

Adding `div` as a field rather than defining `a / b := a * b⁻¹` allows us to
avoid certain classes of unification failures, for example:
Let `Foo X` be a type with a `∀ X, Div (Foo X)` instance but no
`∀ X, Inv (Foo X)`, e.g. when `Foo X` is a `EuclideanDomain`. Suppose we
also have an instance `∀ X [Cromulent X], GroupWithZero (Foo X)`. Then the
`(/)` coming from `GroupWithZero.div` cannot be definitionally equal to
the `(/)` coming from `Foo.Div`.

In the same way, adding a `zpow` field makes it possible to avoid definitional failures
in diamonds. See the definition of `Monoid` and Note [forgetful inheritance] for more
explanations on this.


## BASE-LIBRARY REF Units.instDivInvMonoid
{α : Type u} → [inst : Monoid α] → DivInvMonoid αˣ

Body:
fun {α} [Monoid α] =>
  { toMonoid := Units.instMonoid, toInv := Units.instInv, toDiv := Units.instDiv, div_eq_mul_inv := ⋯,
    zpow := fun n a =>
      match n, a with
      | Int.ofNat n, a => a ^ n
      | Int.negSucc n, a => (a ^ n.succ)⁻¹,
    zpow_zero' := ⋯, zpow_succ' := ⋯, zpow_neg' := ⋯ }

Docstring: Units of a monoid form a `DivInvMonoid`. 

## BASE-LIBRARY REF Add
Type u → Type u

Docstring: The homogeneous version of `HAdd`: `a + b : α` where `a b : α`. 

## BASE-LIBRARY REF Add.add
{α : Type u} → [self : Add α] → α → α → α

Body:
fun α [self : Add α] => self.1

Docstring: `a + b` computes the sum of `a` and `b`. See `HAdd`. 

## BASE-LIBRARY REF Int.instAdd
Add ℤ

Body:
{ add := Int.add }

## BASE-LIBRARY REF Int.add
ℤ → ℤ → ℤ

Body:
fun m n =>
  match m, n with
  | Int.ofNat m, Int.ofNat n => Int.ofNat (m + n)
  | Int.ofNat m, Int.negSucc n => Int.subNatNat m n.succ
  | Int.negSucc m, Int.ofNat n => Int.subNatNat n m.succ
  | Int.negSucc m, Int.negSucc n => Int.negSucc (m + n).succ

Docstring: Addition of integers, usually accessed via the `+` operator.

This function is overridden by the compiler with an efficient implementation. This definition is
the logical model.

Examples:
 * `(7 : Int) + (6 : Int) = 13`
 * `(6 : Int) + (-6 : Int) = 0`


## BASE-LIBRARY REF Mul
Type u → Type u

Docstring: The homogeneous version of `HMul`: `a * b : α` where `a b : α`. 

## BASE-LIBRARY REF Mul.mul
{α : Type u} → [self : Mul α] → α → α → α

Body:
fun α [self : Mul α] => self.1

Docstring: `a * b` computes the product of `a` and `b`. See `HMul`. 

## BASE-LIBRARY REF Units.instMul
{α : Type u} → [inst : Monoid α] → Mul αˣ

Body:
fun {α} [Monoid α] => { mul := fun u₁ u₂ => { val := ↑u₁ * ↑u₂, inv := u₂.inv * u₁.inv, val_inv := ⋯, inv_val := ⋯ } }

Docstring: Units of a monoid have an induced multiplication. 

## INFORMAL STATEMENT
lem.commring.unit-zpow-add

\leanhelper  For an invertible element $a$ and integers $m, n \in \mathbb {Z}$, we have $a^{m+n} = a^m \cdot a^n$.

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

## VERDICT
{
  "verdict": "faithful",
  "discrepancies": [],
  "justification": "The target states `\u2200 {L} [CommRing L] (u : L\u02e3) (m n : \u2124), u ^ (m + n) = u ^ m * u ^ n`, exactly the integer-exponent addition law claimed informally. The bundled unit `u : L\u02e3` faithfully encodes the informal assumption that `a` is invertible: in a commutative ring, the informal inverse equation `a \u00b7 b = 1` also gives `b \u00b7 a = 1`, hence a bundled `Units L` value. The formal equality is in `L\u02e3`, which is stronger than the requested equality in `L`; coercing both sides to `L` recovers `a^{m+n} = a^m \u00b7 a^n`. Finally, `Units.instDivInvMonoid` defines negative integer powers using inverses, matching the informal definition `a^n = (a\u207b\u00b9)^{-n}` for negative `n`."
}
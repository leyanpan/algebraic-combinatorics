## TARGET FPS.ring_mul_zero (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a : R), a * 0 = 0

Docstring: **Annihilation** (Ring property):
`a * 0 = 0` for all `a ∈ R`. 

## TARGET FPS.ring_zero_add (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a : R), 0 + a = a

Docstring: **Neutrality of zero** (Ring axiom):
`0 + a = a` for all `a ∈ R`. 

## TARGET FPS.ring_add_assoc (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a b c : R), a + (b + c) = a + b + c

Docstring: **Associativity of addition** (Ring axiom):
`a + (b + c) = (a + b) + c` for all `a, b, c ∈ R`. 

## TARGET FPS.ring_mul_one (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a : R), a * 1 = a

Docstring: **Neutrality of one** (Ring axiom):
`a * 1 = a` for all `a ∈ R`. 

## TARGET FPS.ring_add_zero (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a : R), a + 0 = a

Docstring: **Neutrality of zero** (Ring axiom):
`a + 0 = a` for all `a ∈ R`. 

## TARGET FPS.ring_mul_assoc (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a b c : R), a * (b * c) = a * b * c

Docstring: **Associativity of multiplication** (Ring axiom):
`a * (b * c) = (a * b) * c` for all `a, b, c ∈ R`. 

## TARGET FPS.ring_right_distrib (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a b c : R), (a + b) * c = a * c + b * c

Docstring: **Right distributivity** (Ring axiom):
`(a + b) * c = a * c + b * c` for all `a, b, c ∈ R`. 

## TARGET FPS.ring_one_mul (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a : R), 1 * a = a

Docstring: **Neutrality of one** (Ring axiom):
`1 * a = a` for all `a ∈ R`. 

## TARGET FPS.ring_add_neg (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a : R), a + -a = 0

Docstring: **Existence of additive inverse** (Ring axiom):
`a + (-a) = 0` for all `a ∈ R`. 

## TARGET FPS.ring_left_distrib (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a b c : R), a * (b + c) = a * b + a * c

Docstring: **Left distributivity** (Ring axiom):
`a * (b + c) = a * b + a * c` for all `a, b, c ∈ R`. 

## TARGET FPS.ring_zero_mul (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a : R), 0 * a = 0

Docstring: **Annihilation** (Ring property):
`0 * a = 0` for all `a ∈ R`. 

## TARGET FPS.ring_add_comm (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a b : R), a + b = b + a

Docstring: **Commutativity of addition** (Ring axiom):
`a + b = b + a` for all `a, b ∈ R`.
Note: Addition is always commutative, even in noncommutative rings. 

## BASE-LIBRARY REF Ring
Type u → Type u

Docstring: A `Ring` is a `Semiring` with negation making it an additive group. 

## BASE-LIBRARY REF Mul
Type u → Type u

Docstring: The homogeneous version of `HMul`: `a * b : α` where `a b : α`. 

## BASE-LIBRARY REF Mul.mul
{α : Type u} → [self : Mul α] → α → α → α

Body:
fun α [self : Mul α] => self.1

Docstring: `a * b` computes the product of `a` and `b`. See `HMul`. 

## BASE-LIBRARY REF Distrib
Type u_1 → Type u_1

Docstring: A typeclass stating that multiplication is left and right distributive
over addition. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring
Type u → Type u

Docstring: A not-necessarily-unital, not-necessarily-associative semiring. See `CommutatorRing` and the
documentation thereof in case you need a `NonUnitalNonAssocSemiring` instance on a Lie ring
or a Lie algebra. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.left_distrib
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a b c : α), a * (b + c) = a * b + a * c

Docstring: Multiplication is left distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.right_distrib
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a b c : α), (a + b) * c = a * c + b * c

Docstring: Multiplication is right distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocRing
Type u → Type u

Docstring: A not-necessarily-unital, not-necessarily-associative ring. 

## BASE-LIBRARY REF AddCommGroup.add_comm
∀ {G : Type u} [self : AddCommGroup G] (a b : G), a + b = b + a

Docstring: Addition is commutative in a commutative additive magma. 

## BASE-LIBRARY REF NonUnitalNonAssocRing.left_distrib
∀ {α : Type u} [self : NonUnitalNonAssocRing α] (a b c : α), a * (b + c) = a * b + a * c

Docstring: Multiplication is left distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocRing.right_distrib
∀ {α : Type u} [self : NonUnitalNonAssocRing α] (a b c : α), (a + b) * c = a * c + b * c

Docstring: Multiplication is right distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocRing.zero_mul
∀ {α : Type u} [self : NonUnitalNonAssocRing α] (a : α), 0 * a = 0

Docstring: Zero is a left absorbing element for multiplication 

## BASE-LIBRARY REF NonAssocRing
Type u_1 → Type u_1

Docstring: A unital but not-necessarily-associative ring. 

## BASE-LIBRARY REF Zero
Type u → Type u

Docstring: A type with a zero element. 

## BASE-LIBRARY REF Zero.zero
{α : Type u} → [self : Zero α] → α

Body:
fun α [self : Zero α] => self.1

Docstring: The zero element of the type. 

## BASE-LIBRARY REF MulZeroClass
Type u → Type u

Docstring: Typeclass for expressing that a type `M₀` with multiplication and a zero satisfies
`0 * a = 0` and `a * 0 = 0` for all `a : M₀`. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.zero_mul
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a : α), 0 * a = 0

Docstring: Zero is a left absorbing element for multiplication 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.mul_zero
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a : α), a * 0 = 0

Docstring: Zero is a right absorbing element for multiplication 

## BASE-LIBRARY REF Add
Type u → Type u

Docstring: The homogeneous version of `HAdd`: `a + b : α` where `a b : α`. 

## BASE-LIBRARY REF Add.add
{α : Type u} → [self : Add α] → α → α → α

Body:
fun α [self : Add α] => self.1

Docstring: `a + b` computes the sum of `a` and `b`. See `HAdd`. 

## BASE-LIBRARY REF One
Type u → Type u

Docstring: A type with a "one" element. 

## BASE-LIBRARY REF One.one
{α : Type u} → [self : One α] → α

Body:
fun α [self : One α] => self.1

Docstring: The "one" element of the type. 

## BASE-LIBRARY REF AddMonoidWithOne
Type u_2 → Type u_2

Docstring: An `AddMonoidWithOne` is an `AddMonoid` with a `1`.
It also contains data for the unique homomorphism `ℕ → R`. 

## BASE-LIBRARY REF AddGroupWithOne
Type u → Type u

Docstring: An `AddGroupWithOne` is an `AddGroup` with a 1. It also contains data for the unique
homomorphisms `ℕ → R` and `ℤ → R`. 

## BASE-LIBRARY REF Ring.neg_add_cancel
∀ {R : Type u} [self : Ring R] (a : R), -a + a = 0

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Body:
fun α [self : Neg α] => self.1

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF NegZeroClass
Type u_2 → Type u_2

Docstring: Typeclass for expressing that `-0 = 0`. 

## BASE-LIBRARY REF SubNegZeroMonoid
Type u_2 → Type u_2

Docstring: A `SubNegMonoid` where `-0 = 0`. 

## BASE-LIBRARY REF SubNegZeroMonoid.neg_zero
∀ {G : Type u_2} [self : SubNegZeroMonoid G], -0 = 0

## BASE-LIBRARY REF SubtractionMonoid
Type u → Type u

Docstring: A `SubtractionMonoid` is a `SubNegMonoid` with involutive negation and such that
`-(a + b) = -b + -a` and `a + b = 0 → -a = b`. 

## BASE-LIBRARY REF SubNegMonoid
Type u → Type u

Docstring: A `SubNegMonoid` is an `AddMonoid` with unary `-` and binary `-` operations
satisfying `sub_eq_add_neg : ∀ a b, a - b = a + -b`.

The default for `sub` is such that `a - b = a + -b` holds by definition.

Adding `sub` as a field rather than defining `a - b := a + -b` allows us to
avoid certain classes of unification failures, for example:
Let `foo X` be a type with a `∀ X, Sub (Foo X)` instance but no
`∀ X, Neg (Foo X)`. Suppose we also have an instance
`∀ X [Cromulent X], AddGroup (Foo X)`. Then the `(-)` coming from
`AddGroup.sub` cannot be definitionally equal to the `(-)` coming from
`Foo.Sub`.

In the same way, adding a `zsmul` field makes it possible to avoid definitional failures
in diamonds. See the definition of `AddMonoid` and Note [forgetful inheritance] for more
explanations on this.


## BASE-LIBRARY REF SubtractionMonoid.toSubNegZeroMonoid._proof_1
∀ {α : Type u_1} [inst : SubtractionMonoid α], -0 = 0

## BASE-LIBRARY REF SubtractionCommMonoid
Type u → Type u

Docstring: Commutative `SubtractionMonoid`. 

## BASE-LIBRARY REF AddCommGroup
Type u → Type u

Docstring: An additive commutative group is an additive group with commutative `(+)`. 

## BASE-LIBRARY REF SubtractionMonoid.neg_neg
∀ {G : Type u} [self : SubtractionMonoid G] (x : G), - -x = x

## BASE-LIBRARY REF SubtractionMonoid.neg_add_rev
∀ {G : Type u} [self : SubtractionMonoid G] (a b : G), -(a + b) = -b + -a

## BASE-LIBRARY REF SubtractionMonoid.neg_eq_of_add
∀ {G : Type u} [self : SubtractionMonoid G] (a b : G), a + b = 0 → -a = b

Docstring: Despite the asymmetry of `neg_eq_of_add`, the symmetric version is true thanks to the
involutivity of negation. 

## BASE-LIBRARY REF LieRing
Type v → Type v

Docstring: A Lie ring is an additive group with compatible product, known as the bracket, satisfying the
Jacobi identity. 

## BASE-LIBRARY REF LieRing.ofAssociativeRing
{A : Type v} → [Ring A] → LieRing A

Body:
fun {A} [inst : Ring A] =>
  { toAddCommGroup := inst.toAddCommGroup, toBracket := Ring.instBracket, add_lie := ⋯, lie_add := ⋯, lie_self := ⋯,
    leibniz_lie := ⋯ }

Docstring: An associative ring gives rise to a Lie ring by taking the bracket to be the ring commutator. 

## INFORMAL STATEMENT
def.alg.ring

The notion of a \emph{ring} (also known as a \emph{noncommutative ring}) is defined in the exact same way as we defined the notion of a commutative ring in Definition~ \ref{def.alg.commring}, except that the “Commutativity of multiplication” axiom is removed.

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

## VERDICT
{
  "verdict": "minor_discrepancy",
  "discrepancies": [
    {
      "root": "FPS.ring_add_neg",
      "severity": "minor",
      "bridge": "The blueprint\u2019s primitive subtraction axiom can be recovered routinely from the additive-group structure supplied by `[inst : Ring R]`: Lean subtraction is addition of the negative, and additive cancellation gives `a + b = c \u2194 a = c - b`. Conversely, the blueprint axiom determines subtraction as addition of an additive inverse. Thus the displayed unary-negation law is an equivalent standard re-encoding, but it does not itself state the required binary-subtraction equivalence."
    }
  ],
  "justification": "All addition, multiplication, identity, distributivity, and annihilation axioms are represented with the correct orientations, and omission of multiplication commutativity agrees with \u201cthe \u2018Commutativity of multiplication\u2019 axiom is removed.\u201d The sole mismatch is that the blueprint explicitly requires a binary map `\\ominus : K\u00d7K\u2192K` satisfying \u201c`a\u2295b=c` if and only if `a=c\u2296b`,\u201d whereas the corresponding target only asserts `\u2200 ... (a : R), a + -a = 0`. The `[inst : Ring R]` binder supplies the additive-group structure needed to derive the omitted equivalence, so this is a routine representational bridge rather than a substantive divergence."
}
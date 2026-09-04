## TARGET AlgebraicCombinatorics.SignedCounting.negHockeyStick (theorem) — ELABORATED SIGNATURE
∀ (n m : ℕ), 0 < n → ∑ k ∈ Finset.range (m + 1), (-1) ^ k * ↑(n.choose k) = (-1) ^ m * ↑((n - 1).choose m)

Docstring: **Negative Hockey-Stick Identity** (prop.binom.nhs)

For `n : ℕ` with `n ≥ 1` and `m : ℕ`, we have
`∑ k in range (m+1), (-1)^k * n.choose k = (-1)^m * (n-1).choose m`

Note: We state this for natural numbers with `n ≥ 1`. The source states it for `n ∈ ℂ`,
but by the polynomial identity principle, it suffices to prove it for positive integers.
The hypothesis `n ≥ 1` is necessary because natural number subtraction gives
`(0 - 1) = 0`, which would make the RHS incorrect when `n = 0` and `m ≥ 1`.


## BASE-LIBRARY REF Nat.lt
ℕ → ℕ → Prop

Body:
fun n m => n.succ.le m

Docstring: Strict inequality of natural numbers, usually accessed via the `<` operator.

It is defined as `n < m = n + 1 ≤ m`.


## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Body:
fun {ι} {M} [AddCommMonoid M] s f => (Multiset.map f s.val).sum

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Int.instAddCommMonoid
AddCommMonoid ℤ

Body:
inferInstance

## BASE-LIBRARY REF AddCommMonoid
Type u → Type u

Docstring: An additive commutative monoid is an additive monoid with commutative `(+)`. 

## BASE-LIBRARY REF Int.instAddCommGroup
AddCommGroup ℤ

Body:
{ toAdd := Int.instAdd, add_assoc := Int.add_assoc, toZero := Zero.ofOfNat0, zero_add := Int.zero_add,
  add_zero := Int.add_zero, nsmul := fun x1 x2 => ↑x1 * x2, nsmul_zero := Int.zero_mul,
  nsmul_succ := Int.instAddCommGroup._proof_1, toNeg := Int.instNegInt, toSub := Int.instSub, sub_eq_add_neg := ⋯,
  zsmul := fun x1 x2 => x1 * x2, zsmul_zero' := Int.zero_mul, zsmul_succ' := ⋯, zsmul_neg' := ⋯,
  neg_add_cancel := Int.add_left_neg, add_comm := Int.add_comm }

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Body:
fun n => { val := Multiset.range n, nodup := ⋯ }

Docstring: `range n` is the set of natural numbers less than `n`. 

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

## BASE-LIBRARY REF Int.instMul
Mul ℤ

Body:
{ mul := Int.mul }

## BASE-LIBRARY REF Int.mul
ℤ → ℤ → ℤ

Body:
fun m n =>
  match m, n with
  | Int.ofNat m, Int.ofNat n => Int.ofNat (m * n)
  | Int.ofNat m, Int.negSucc n => Int.negOfNat (m * n.succ)
  | Int.negSucc m, Int.ofNat n => Int.negOfNat (m.succ * n)
  | Int.negSucc m, Int.negSucc n => Int.ofNat (m.succ * n.succ)

Docstring: Multiplication of integers, usually accessed via the `*` operator.

This function is overridden by the compiler with an efficient implementation. This definition is
the logical model.

Examples:
 * `(63 : Int) * (6 : Int) = 378`
 * `(6 : Int) * (-6 : Int) = -36`
 * `(7 : Int) * (0 : Int) = 0`


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

## BASE-LIBRARY REF Monoid
Type u → Type u

Docstring: A `Monoid` is a `Semigroup` with an element `1` such that `1 * a = a * 1 = a`. 

## BASE-LIBRARY REF Int.instMonoid
Monoid ℤ

Body:
inferInstance

## BASE-LIBRARY REF Int.instCommMonoid
CommMonoid ℤ

Body:
{ toMul := Int.instMul, mul_assoc := Int.mul_assoc, toOne := One.ofOfNat1, one_mul := Int.one_mul,
  mul_one := Int.mul_one, npow := fun n x => x ^ n, npow_zero := ⋯, npow_succ := ⋯, mul_comm := Int.mul_comm }

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Body:
fun α [self : Neg α] => self.1

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Int.instNegInt
Neg ℤ

Body:
{ neg := Int.neg }

## BASE-LIBRARY REF Int.neg
ℤ → ℤ

Body:
fun n =>
  match n with
  | Int.ofNat n => Int.negOfNat n
  | Int.negSucc n => ↑n.succ

Docstring: Negation of integers, usually accessed via the `-` prefix operator.

This function is overridden by the compiler with an efficient implementation. This definition is
the logical model.

Examples:
 * `-(6 : Int) = -6`
 * `-(-6 : Int) = 6`
 * `(12 : Int).neg = -12`


## BASE-LIBRARY REF Int.ofNat
ℕ → ℤ

Docstring: A natural number is an integer.

This constructor covers the non-negative integers (from `0` to `∞`).


## BASE-LIBRARY REF Nat.choose
ℕ → ℕ → ℕ

Docstring: `choose n k` is the number of `k`-element subsets in an `n`-element set. Also known as binomial
coefficients. For the fact that this is the number of `k`-element-subsets of an `n`-element
set, see `Finset.card_powersetCard`. 

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

## INFORMAL STATEMENT
Negative hockey-stick identity

Let $n\in \mathbb {C}$ and $m\in \mathbb {N}$. Then, 

\[  \sum _{k=0}^{m} (-1)^{k} \binom {n}{k} = (-1)^{m} \binom {n-1}{m}.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.binom.binom
def.binom.binom

For any numbers $n$ and $k$, we set

\begin{equation}  \binom {n}{k}=\begin{cases}  \frac{n\left( n-1\right) \left( n-2\right) \cdots \left( n-k+1\right) }{k!}, &  \text{if }k\in \mathbb {N};\\ 0, &  \text{else.}\end{cases} \end{equation}

 Note that “numbers” is to be understood fairly liberally here. In particular, $n$ can be any integer, rational, real or complex number (or, more generally, any element in a $\mathbb {Q}$-algebra), whereas $k$ can be anything (although the only nonzero values of $\binom {n}{k}$ will be achieved for $k\in \mathbb {N}$, by the above definition).

## VERDICT
{
  "verdict": "significant_divergence",
  "discrepancies": [
    {
      "root": "n : \u2115",
      "severity": "significant",
      "bridge": "To recover the claim for arbitrary complex n, one must separately formalize the generalized binomial coefficient as the falling-factorial polynomial over \u2102, prove that its values at positive natural numbers agree with the cast of Nat.choose, and then apply a polynomial identity argument for each m. None of this is asserted by the target, whose language only expresses Nat.choose for natural upper indices. This bridge contains the substantive extension from positive integers to all complex numbers."
    }
  ],
  "justification": "The target quantifies only \u201c\u2200 (n m : \u2115), 0 < n\u201d and uses \u201c\u2191(n.choose k)\u201d and \u201c\u2191((n - 1).choose m)\u201d. The blueprint instead says \u201cLet n \u2208 \u2102 and m \u2208 \u2115\u201d and defines binomial coefficients for complex upper arguments by the falling-factorial formula. Thus the target proves only the positive-natural specialization. Its docstring's statement that the complex result follows \u201cby the polynomial identity principle\u201d is contextual prose, not part of the theorem's formal conclusion."
}
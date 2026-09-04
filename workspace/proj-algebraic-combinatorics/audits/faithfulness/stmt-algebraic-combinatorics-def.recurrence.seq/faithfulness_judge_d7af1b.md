## TARGET AlgebraicCombinatorics.FPS.exampleRecurrence (def) — ELABORATED SIGNATURE
ℕ → ℕ

Body:
fun x =>
  Nat.brecOn x fun x f =>
    (match (motive := (x : ℕ) → Nat.below x → ℕ) x with
      | 0 => fun x => 1
      | n.succ => fun x => 2 * x.1 + n)
      f

Docstring: The sequence defined by $a_0 = 1$ and $a_{n+1} = 2a_n + n$. 

## BASE-LIBRARY REF Nat.brecOn
{motive : ℕ → Sort u} → (t : ℕ) → ((t : ℕ) → Nat.below t → motive t) → motive t

Body:
fun {motive} t F_1 => (Nat.brecOn.go t F_1).1

## BASE-LIBRARY REF Nat.below
{motive : ℕ → Sort u} → ℕ → Sort (max 1 u)

Body:
fun {motive} t => Nat.rec PUnit.{max 1 u} (fun n n_ih => motive n ×' n_ih) t

## BASE-LIBRARY REF Nat.brecOn.go
{motive : ℕ → Sort u} → (t : ℕ) → ((t : ℕ) → Nat.below t → motive t) → motive t ×' Nat.below t

Body:
fun {motive} t F_1 => Nat.rec ⟨F_1 Nat.zero PUnit.unit, PUnit.unit⟩ (fun n n_ih => ⟨F_1 n.succ n_ih, n_ih⟩) t

## BASE-LIBRARY REF Nat.succ
ℕ → ℕ

Docstring: The successor of a natural number `n`.

Using `Nat.succ n` should usually be avoided in favor of `n + 1`, which is the [simp normal
form](https://lean-lang.org/doc/reference/4.28.0/find/?domain=Verso.Genre.Manual.section&name=simp-normal-forms).


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


## INFORMAL STATEMENT
def.recurrence.seq

\leanhelper  The sequence $(a_n)$ defined by $a_0 = 1$ and $a_{n+1} = 2a_n + n$ for all $n\geq 0$.

## VERDICT
{
  "verdict": "faithful",
  "discrepancies": [],
  "justification": "The body defines a function `\u2115 \u2192 \u2115` by course-of-values recursion. At `0`, the branch `| 0 => fun x => 1` gives `a\u2080 = 1`. At `n.succ`, `Nat.below (n+1)` has first component equal to the recursively computed value at `n`, so the branch `| n.succ => fun x => 2 * x.1 + n` gives `a_{n+1} = 2a_n + n`. This exactly matches the informal statement, \u201cThe sequence `(a_n)` defined by `a_0 = 1` and `a_{n+1} = 2a_n + n` for all `n \u2265 0`.\u201d"
}
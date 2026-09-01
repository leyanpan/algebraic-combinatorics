## TARGET AlgebraicCombinatorics.FPS.fibonacci (def) — ELABORATED SIGNATURE
ℕ → ℕ

Body:
Nat.fib

Docstring: The Fibonacci sequence.

**Mathlib note**: This is definitionally equal to `Nat.fib` in Mathlib. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Nat.fib
ℕ → ℕ

Docstring: Implementation of the Fibonacci sequence satisfying
`fib 0 = 0, fib 1 = 1, fib (n + 2) = fib n + fib (n + 1)`.

*Note:* We use a stream iterator for better performance when compared to the naive recursive
implementation.


## INFORMAL STATEMENT
def.fib.fibonacci

\leanhelper  The \emph{Fibonacci sequence} $(f_0, f_1, f_2, \ldots )$ is defined by $f_0 = 0$, $f_1 = 1$, and $f_n = f_{n-1} + f_{n-2}$ for $n \geq 2$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target is `fibonacci : \u2115 \u2192 \u2115` with body `Nat.fib`. The base-library definition states that `Nat.fib` satisfies `fib 0 = 0`, `fib 1 = 1`, and `fib (n + 2) = fib n + fib (n + 1)`, which is exactly the informal recurrence `f\u2080 = 0`, `f\u2081 = 1`, and `f\u2099 = f\u2099\u208b\u2081 + f\u2099\u208b\u2082` for `n \u2265 2`, after reindexing `n` as `n + 2` and using commutativity of addition."
}
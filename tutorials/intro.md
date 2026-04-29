# Introduction to MAGMA

MAGMA is a computer algebra system designed to solve problems in algebra, number theory, geometry and combinatorics. It was developed by Cannon and team at the University of Sydney, and version 1 was first released in August 1993.

The name "MAGMA" comes from Bourbaki (and Serre), where it is used to denote a set with one or more binary operations without any additional axioms. In that language, a magma is the most basic of algebraic structures.

Today, MAGMA is a huge system with several thousand pages of documentation. MAGMA can be used both interactively and as a programming language. The core of MAGMA is programmed in C, but a large part of its functionality resides in package files written in the MAGMA user language.

## What MAGMA Does

Computer algebra systems perform exact calculations which fall under the umbrella of symbolic computation: mathematical expressions are manipulated in a way similar to traditional manual computations. This should not be confused with numerical computation — one can use MAGMA output in papers or theses without losing exactness.

The design principles underpinning both the user language and system architecture are based on ideas from universal algebra and category theory. The MAGMA language attempts to approximate the usual mathematical modes of thought and notation as closely as possible. In particular, the principal constructs in the user language are sets, algebraic structures such as groups, rings and fields, and morphisms.

## Key Features

**Algebraic Design Philosophy** — The language attempts to approximate as closely as possible the usual mathematical modes of thought and notation. The principal constructs are set, (algebraic) structure and morphism.

**Explicit Typing** — The user is required to explicitly define most of the algebraic structures in which calculations are to take place. Each object arising in the computation is then defined in terms of these structures.

**Integration** — The facilities for each area are designed in a similar manner using generic constructors wherever possible. This uniform design makes it simple to program calculations that span different classes of mathematical structures or involve the interaction of structures.

**Relationships** — MAGMA provides a mechanism that manages relationships between complex bodies of information. For example, when substructures and quotient structures are created, the natural homomorphisms that arise are always stored and used to support automatic coercion between parent and child structures.

**Mathematical Databases** — MAGMA has access to a large number of databases containing information useful in searches for interesting examples or forming an integral part of certain algorithms. Examples include factorizations of integers of the form p^n ± 1, modular equations, strongly regular graphs, maximal subgroups of simple groups, integral lattices, K3 surfaces, best known linear codes, and many others.

**Performance** — MAGMA aims to provide the best possible performance both in terms of the algorithms used and their implementation. Most major algorithms installed in the MAGMA kernel are state-of-the-art and give performance similar to, or better than, specialised programs.

## Fields Covered

MAGMA spans a wide range of topics, including:

- Groups, semigroups and monoids
- Rings and fields; commutative rings
- Linear algebra and module theory
- Lattices and quadratic forms
- Algebras; representation theory; homological algebra
- Lie theory
- Algebraic geometry and commutative algebra
- Arithmetic geometry and modular arithmetic geometry
- Combinatorics and graph theory
- Finite incidence geometry
- Differential Galois theory
- Error-correcting codes and cryptography
- Mathematical databases

## MAGMA as a Programming Language

MAGMA is an imperative, call-by-value, lexically scoped, dynamically typed programming language with an essentially functional subset. This means:

- **Imperative** — Data is manipulated directly by assignment statements and control structures such as loops and if-else constructions.
- **Functional subset** — Goals can also be achieved by composing functions without side-effects.
- **First-class functions** — Functions can be assigned to variables, stored in data structures, and returned from other functions. They can invoke themselves recursively and participate in mutual recursion.
- **Procedures** — Unlike functions, procedures do not return a value but may modify their arguments (provided they are declared as reference variables).

## Accessing MAGMA

MAGMA is non-commercial but not free; distribution is organised on a subscription basis. To install MAGMA on your machine, visit the ordering page on the University of Sydney website.

For this course, the free online calculator is completely sufficient:

```
http://magma.maths.usyd.edu.au/calc/
```

There are mild restrictions: calculations are limited to 120 seconds, input is limited to 50,000 bytes, and you cannot run additional processes. Conveniently, you can paste code including the `>` prompt characters directly into the calculator without needing to remove them.

## References

- The Handbook of MAGMA Functions (the handbook)
- Discovering MAGMA via examples
- An Introduction to Algebraic Programming with MAGMA
- Shorter introductory texts such as those by Cranswick (2008)

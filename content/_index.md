+++
title = "Hector Suzanne"
+++

## About

Hi ! I'm Hector Suzanne, Ph.D. in computer science. I did my thesis under [Pr. Emmanuel Chailloux](https://www-apr.lip6.fr/~chaillou/) at the [APR](https://www.lip6.fr/recherche/team.php?acronyme=APR) team at [LIP6](https://lip6.fr), the computer science lab at [Sorbonne Université](https://sorbonne-universite.fr). I was born in 1996 and fascinated by math and programming ever since. To contact me, send an email at [hectorsuzanne@gmail.com](mailto:hectorsuzanne@gmail.com) (personal) or [hector.suzanne@lip6.fr](mailto:hector.suzanne@lip6.fr) (professional).

## PhD Thesis

### Reusable resource analyses for high-level languages

**New!** The defended version of my manuscript is available, exclusively [here](articles/thesis.pdf)!

My PhD research focuses on compile-time prediction of memory usage for programs written in functional-imperative style, following, amongst others, the technique of [Automated Amortized Resource Analysis](https://doi.org/10.1017/S0960129521000487).

The approach is based on an intermediate representation for a virtual machine, with the following features:

- *Call-By-Push-Value*: it allows both javascript- and Haskell-style functional programming, where evaluating data is done eagerly, and composing computations is done lazily. Those two *polarities* can be judiciously combined to encode efficient iterations and data processing workflows in an imperative style, which are compiled as purely functionnal programs for the VM.
- *Linear type system*: Values can be *shareable* (freely duplicated, and memory managed) or *linear* (manually managed with move-copy semantics).
- *Type-level programming*: its type inference engine works with SMT solvers following the *Liquid types* paradigm. A rudimentary solver for the first-order theory of uninterpreted symbols is available to deal with user-defined sorts and symbols.
- *(Defunctionalized-)continuation-passing-style*: Contexts of evaluations are first-class data structures, and the analysis algorithms developed within AARA extend to those structures as well. Compared to previous AARA implementations, this allows for a streamlined type system that doesn't have to track evaluation contexts in a ad-hoc manner.

## Pre-Prints

### "A reusable machine-calculus for automated resource analyses" with Emmanuel Chailloux [PDF](articles/lopstr23.pdf)

An automated resource analysis technique is introduced, targeting a Call-By-Push-Value abstract machine, with memory prediction as a practical goal. The machine has a polymorphic and linear type system enhanced with a first-order logical fragment, which encodes both low-level operational semantics of resource manipulations and high-level synthesis of algorithmic complexity. Resource analysis must involve a diversity of static analysis, for escape, aliasing, algorithmic invariants, and more. Knowing this, we implement the *Automated Amortized Resource Analysis* framework (AARA) from scratch in our generic system. In this setting, access to resources is a state-passing effect which produces a compile-time approximation of runtime resource usage. We implemented type inference constraint generation for our calculus, accompanied with an elaboration of bounds for iterators on algebraic datatypes, for minimal ML-style programming languages with Call-by-Value and Call-By-Push-Value semantics. The closed-formed bounds are derived as multivariate polynomials over the integers. This now serves as a base for the development of an experimental toolkit for automated memory analysis of functional languages.

## Autobill

<https://gitlab.lip6.fr/suzanneh/autobill>

The end-goal of the PhD is do develop and validate theorically the language described above. The implementation I am currently building is called *Autobill*: it is *auto*-matic, computes the cost of programs (their *bill*), and is based on *Intuitionistic Linear Logic*.

## CV/Resume

Download my resume [🇺🇸 here](cv.pdf). Mon CV en français est disponible [🇫🇷 ici](cv_fr.pdf).

Briefly:

- 2021-Today: PhD at LIP6 on memory usage analysis through static typing for functional-imperative programming .
- 2020-2021: Master's in mathematics *Logique, Mathématiques, et Fondements de l'Informatique* at *Université Paris Cité*
- 2018-2020: Master's in computer science *Sciences et Techniques do Logiciel* at *Sorbonne Université*
- 2016-2017: Licence in Computer Science at *ENS Paris-Saclay*
- 2014-2016: "Prépa" MPSI-MP* at *Lycée Descartes de Tours*

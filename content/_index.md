+++
title = "Hector Suzanne"
+++

I am a computer scientist working in software verification, currently via model-checking, at the [Laboratoire Méthodes Formelles (LMF)](https://lmf.cnrs.fr) of Université Paris-Saclay. I did my thesis on typing-based resource analysis at [LIP6](https://lip6.fr), the computer science lab of Sorbonne Université.


## Current Work

### Testing properties for model coverage via mutation techniques 

Will update this once I learn more about it...

## Research

### Transactional aspects of infinite-space model-checking 

Designing systems that gracefully scale to arbitrarily many nodes requires
thinking across interdependent scales: what code will a given node run ? how do
related nodes interact ? does the system at large maintain a viable state ? Those
scenarios overlap and (mis)interact. Model checkers, such as
[Cubicle](https://cubicle.lri.fr), allow designers to ensure that systems
maintain safety conditions. They represent systems as a set of arrays indexed by
node and a collection of transitions that describe the atomic test-and-update
rules the system evolves by.

This rule-based encoding erases control-flow information. It smears the original
intents together to faithfully represent real-life concurrency, but does come at
a cost: systems are often designed in terms of those desired narratives: "Some
process asks for write permission, which causes a manager node to invalidate
access for other nodes, at which point the original process is sent an ACK."

My postdoc work with Sylvain Conchon at LMF is `TxCubicle`, an extension of
Cubicle where those intents are *transactions*: finite chains of transitions
over a chosen slice of the system, which can branch and loop, and either commit
as a whole or roll back and have no effect.

Building a transactional model, then progressively dissolving its transactions by
changing the code or the model semantics, lets the emergent behavior of the
distributed system appear gradually. Designers can start modeling from the
happy paths and get more pessimistic as failure modes become relevant. Knowing
the designers' intent for their system is also useful in the search for
inductive invariants: candidate invariants can be guessed from the simpler
transactional system and tested against the smeared one, speeding up the search.

### Reusable resource analyses for high-level languages
Emergent behavior in programs make it impossible —in theory— to know in
advance how much work a computation will expend. We know how to enforce hard
budget caps in some situations (such as embedded and system programming), but
more generally, can we build languages that expose the possible cost of code ?
Preferably while doing our algorithmics homework for us, of course:

> "*This will allocate `8*n*log(n) + 5*n + 60` words of RAM after `n` requests*"

This was the overall topic of my PhD. Scientifically, it focused on compile-time
prediction of memory usage for programs written in functional-imperative style,
following, amongst others, the techniques of [Automated Amortized Resource
Analysis (AARA)](https://doi.org/10.1017/S0960129521000487), adapting them to
mainstream functional-programming implementation techniques. This ending up
taking us (me + Emmanuel Chailloux, my advisor) onto a journey spanning proof
theory, type theory, constraint solvers, and integer optimization.

The result was `Autobill`, a proof-of-concept analyser, that acted as a deconstruction and progressive dissolution of AARA into mainstream programming-language-theory techniques:

- It was the first AARA implementation supporting *Call-by-Push-Value* semantics, which lets functional programmers finely control the runtime operation of their programs, implement their own notions of iterators, and build effect systems.
- It was the first public implementation the *ILL* calculus/abstract machine. This let us separate reasoning on operation ordering, high-order computations, and flow of resources within programs.
- It simplified the implementation of resource-aware type systems by fusing reasoning on the nested scope data held in the stack and the structured arborescent data held on the heap.
- It re-interpreted AARA as a *constraint solving* problem. Starting from the type-level data inferred from programs, we were able to extract the algorithmic logic that underlie the budget constraint. This allowed different SMT solvers and optimizers to be used depending on algorithms a given program implements.
- The core of AARA was rephrased as a family of metrics on data structures. Those provide a *combinatorial grading** within each data-type that behave nicely under runtime operations and reduce search for asymtotically optimal resource bounds into optimization in `R^n`. 

## Pre-prints

### Transaction-Guided Parameterized Model Checking in TxCubicle
_with Sylvain Conchon, at ICFEM'26_ {% <link href="articles/icfem26.pdf"> %}PDF{% </link> %} {% <sep> %}{% </sep> %} {% <expand id="icfem26"> %}
Designing concurrent and distributed protocols is inherently difficult. Designers typically start from simple, high-level descriptions and progressively refine them into more detailed models that expose additional concurrency, communication patterns, and failure scenarios. For parameterized systems, whose correctness must hold for an arbitrary number of processes, this refinement process can quickly lead to models whose complexity overwhelms automated verification techniques.

This paper introduces TxCubicle, an extension of the Cubicle model checker with transactions that supports this progressive refinement process. Transactions are finite, possibly branching pieces of control flow involving a chosen slice of the system. Each resulting transaction path either completes as a whole or is rolled back and has no effect. These transactions can be composed, refined, split, and branched, allowing users to gradually introduce implementation details and concurrency while maintaining a manageable verification effort.

We have implemented TxCubicle by integrating transactions with Cubicle's existing verification infrastructure. Transactions can reduce the effective state space explored during verification and guide invariant generation by exposing higher-level behavioral patterns. Our implementation preserves compatibility with Cubicle's highly optimized symbolic algorithms and SMT-based reasoning without introducing significant overhead. Experimental results show that transactions provide a more natural and efficient alternative to ad hoc control-flow encodings, substantially accelerating invariant generation and improving verification performance even when the underlying reachable state space remains unchanged.
{% </expand> %}

### Reusable resource analyses for high-level languages
_my PhD thesis, under Emmanuel Chailloux_ {% <link href="articles/thesis.pdf"> %}Manuscript{% </link> %}
  
### A reusable machine-calculus for automated resource analyses
_with Emmanuel Chailloux, at LOPSTR'23_ {% <link href="articles/lopstr23.pdf"> %}PDF{% </link> %} {% <sep> %}{% </sep> %} {% <expand id="lopstr23"> %}
An automated resource analysis technique is introduced, targeting a Call-By-Push-Value abstract machine, with memory prediction as a practical goal. The machine has a polymorphic and linear type system enhanced with a first-order logical fragment, which encodes both low-level operational semantics of resource manipulations and high-level synthesis of algorithmic complexity. Resource analysis must involve a diversity of static analyses, for escape, aliasing, algorithmic invariants, and more. Knowing this, we implement the *Automated Amortized Resource Analysis* framework (AARA) from scratch in our generic system. In this setting, access to resources is a state-passing effect which produces a compile-time approximation of runtime resource usage. We implemented type inference constraint generation for our calculus, accompanied with an elaboration of bounds for iterators on algebraic datatypes, for minimal ML-style programming languages with Call-by-Value and Call-By-Push-Value semantics. The closed-form bounds are derived as multivariate polynomials over the integers. This now serves as a base for the development of an experimental toolkit for automated memory analysis of functional languages.
{% </expand> %}

## Software

### TxCubicle {% <link href="https://github.com/Polybulle/cubicle"> %}Github{% </link> %} {% <sep> %}{% </sep> %} {% <link href="https://cubicle.lri.fr"> %}Homepage{% </link> %}

A model-checker for infinite-space array transition system, including a tightly optimized SMT solver, that supports control-flow, invariant generation, and universal guards. 

### Autobill {% <link href="https://github.com/Polybulle/Autobill"> %}Github{% </link> %}

A type-checker and interpreter for a suite of ML-style languages with call-by-value and call-by-push-value semantics, including its intuintionistic-linear type system, resource-aware types, and polynomial-bound generation using AARA

## Resume

🇺🇸 Download my resume [here](SUZANNE_Hector_resume.pdf).

🇫🇷 Mon CV en français est disponible [ici](SUZANNE_Hector_CV.pdf).

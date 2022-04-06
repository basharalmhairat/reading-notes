## Purely functional programming

***Difference between pure and impure functional programming***

 Your function is pure if it does not contain any external code. Otherwise, it is impure if it includes one or more side effects
 
 ![image](https://user-images.githubusercontent.com/97823170/161921532-81957c88-a8f0-4143-9dbe-ec1a283e0dcd.png)

***Properties of purely functional programming***

In computer programming, a pure function is a function that has the following properties:
the function return values are identical for identical arguments (no variation with local static variables,
non-local variables, mutable reference arguments or input streams),
andthe function application has no side effects (no mutation of local static variables, non-local variables, mutable reference arguments or input/output streams).
Strict versus non-strict evaluation
Main article: Evaluation strategy
Each evaluation strategy which ends on a purely functional program returns the same result. In particular,
it ensures that the programmer does not have to consider in which order programs are evaluated, since eager evaluation will return the same result as lazy evaluation.
However, it is still possible that an eager evaluation may not terminate while the lazy evaluation of the same program halts. An advantage of this is that lazy evaluation can be implemented much more easily; as all expressions will return the same result at any moment
(regardless of program state), their evaluation can be delayed as much as necessary.

***Data structures***
Data structure is a storage that is used to store and organize data. It is a way of arranging data on a computer so that it can be accessed and updated efficiently.
Depending on your requirement and project, it is important to choose the right data structure for your project.

![image](https://user-images.githubusercontent.com/97823170/161922100-5a9058eb-5f4e-47de-b048-e6b9a602b534.png)

Types of Data Structure
Basically, data structures are divided into two categories:

Linear data structure
Non-linear data structure

***Purely functional language***
Functional programming languages are informally classified into pure and impure languages.
The precise meaning of this distinction has been a matter of controversy.
We therefore investigate a formal definition of purity. We begin by showing that some proposed definitions which rely on confluence
, soundness of the beta axiom, preservation of pure observational equivalences and independence of the order of evaluation,
do not withstand close scrutiny. We propose instead a definition based on parameter-passing independence. Intuitively,
the definition implies that functions are pure mappings from arguments to results; the operational decision of how to pass the arguments is irrelevant.
In the context of Haskell, our definition is consistent with the fact that the traditional call-by-name denotational semantics coincides with the
traditional call-by-need implementation. Furthermore, our definition is compatible with the stream-based,
continuation-based and monad-based integration of computational effects in Haskell. Finally,
we observe that call-by-name reasoning principles are unsound in compilers for monadic Haskell.

![image](https://user-images.githubusercontent.com/97823170/161923079-97bc65f9-cf9d-4cb2-9f19-fac9bb93b76c.png)


A function is a relation between terms. Every input term has exactly one output term. That's as simple as it gets.

No alt provided
In type theory, it's described in notation like this:

f : A → B
![image](https://user-images.githubusercontent.com/97823170/161923690-ed414d7d-2867-49c0-b9c6-5e071e767407.png)

Inputs to f are the terms in type A, and outputs from f are the terms in type B. The type might be Integer and the terms might be all integers .., -2, -1, 0, 1, 2, ...

The type might be Character and the terms might be Homer, Marge, SideShowBob, FrankGrimes, InanimateCarbonRod, etc.

This is the core of functional programming, and without type theory, it's hard to even talk formally about the meaning of functional programs.


Functional programming isn't
![image](https://user-images.githubusercontent.com/97823170/161923646-b350580f-c1d9-4e40-b091-8f11c20d1df2.png)

Functional programming as used generally by us as an industry tends to mean using first-class functions, closures that capture their environment properly,
immutable data structures, trying to write code that doesn't have side-effects, and things like that.

That's perfectly reasonable, but it's distinct from pure functional programming. It's called "pure functional", 
because it has only functions as defined in the previous section. But why aren't there proper functions in the popular meaning of functional programming?

No alt provided
It's something of a misnomer that many popular languages use this term function.
If you read the language specification for Scheme, you may notice that it uses the term procedure.
Some procedures may implement functions like cosine, but not all procedures are functions, in fact most aren't. Any procedure can do cheeky arbitrary effects.
But for the rest of popular languages, it's a misnomer we accept.

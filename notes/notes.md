---
author: Wouter Swierstra
title: "*Logic for Computer Science*"
book: true
titlepage: true
titlepage-rule-color: "6687C3"
toc-own-page: true
titlepage-text-color: 000000
classoption: [oneside]
sansfont: Open Sans
monofont: Ubuntu Mono
logo: uulogo.png
logo-width: 200
toc: true
---

# About these notes

These notes offer some supplementary material.

Follows after *Modelling Computing Systems* – but any one with a
background in logic should be able to understand them.

Thanks for Eisvogel template, pandoc, students for their helpful
feedback.

Wouter Swierstra

February 2020



# Inference rules

BNF notation for inductively defined sets.

Defin functions by induction on the structure of the data.

But how can we define relations inductively?

How now?

## Recap

So far, we have encountered propositional logic in several lectures:

* The first lecture defined the syntax of propositional logic informally

* Later, we saw how to define this syntax formally as an inductively defined set

* We have studied the semantics of propositional logic using truth tables.

* We have seen the semantics of propositional logic informally using proof strategies

Can we not give a more precise definition of proof?

And relate it to the 'truth table semantics' we saw in the first lecture?



## What is a proof?

Given a formula in propositional logic $p$, we can check when $p$
holds for all possible values of its atomic propositional variables --
this is what we do when we write a truth table.

We can also give a 'proof sketch' using proof strategies -- but we
haven't made precise what these strategies are, relying on an informal
diagrammatic description.

Can we define a set of all proofs of some propositional logic
formula?

After all, we managed to define the syntax of propositionial logic as
inductively defined set -- can we do the same for its semantics?



## Syntax and semantics

We can define the *syntax* of propositional logic using BNF as follows:

 $p,q$  ::=  true | false | $P$ | $¬p$ | $p ∧ q$ | $p ∨ q$ | $p ⇒ q$ | $p ⇔ q$ 

Can we define a *semantics*, describing the set of valid proofs for an
arbitrary propositional formula?



## Inductively defined relations

So far, we have seen the BNF notation for inductively defined sets.

But what notation should we use for inductively defined *relations*?

For example, we defined the $≤$ *relation* between Peano natural
numbers using the following rules:

* for all $n ∈ ℕ, \, 0 ≤ n$;
* if $n ≤ m$, then $s(n) ≤ s(m)$

Isn't there a better notation?



## Notation for inductively defined relations

Inductively defined relations are often given by means of *inference rules*:

\begin{prooftree}
\AxiomC{ }
\RightLabel{Base}
\UnaryInfC{$0 ≤ n$}
\end{prooftree}

\begin{prooftree}
\AxiomC{$n ≤ m$}
\RightLabel{Step}
\UnaryInfC{$s(n) ≤ s(m)$}
\end{prooftree}

Here we have two inference rules, named Base and Step; these rules
together define a relation $(\leq) \; \subseteq \; \mathbb{N} \times \mathbb{N}$.

The statements above the horizontal line are the *premises* - the
assumptions that you must establish in order to use this rule; the
statement under the horizontal line is the *conclusion* that you can
draw from these assumptions.



## Notation for inductively defined relations

These rules state that there are two ways to prove that $n ≤ m$:

\begin{prooftree}
\AxiomC{ }
\RightLabel{≤-Base}
\UnaryInfC{$0 ≤ n$}
\end{prooftree}

\begin{prooftree}
\AxiomC{$n ≤ m$}
\RightLabel{≤-Step}
\UnaryInfC{$s(n) ≤ s(m)$}
\end{prooftree}


* if $n=0$ the ≤-Base rule tells us that $0 \leq n$ -- for *any* n;

* if we can show $n \leq m$, we can use the ≤-Step rule to prove $s(n) \leq s(m)$.

A rule without premises is called an *axiom*.



## Writing proofs

By repeatedly applying these rules, we can write larger proofs.

For example, to give a formal proof that $2 \leq 5$ we write:

\begin{prooftree}
\AxiomC{ }
\RightLabel{≤-Base}
\UnaryInfC{$0 ≤ s(s(s(0)))$}
\RightLabel{≤-Step}
\UnaryInfC{$s(0) ≤ s(s(s(s(0))))$}
\RightLabel{≤-Step}
\UnaryInfC{$s(s(0)) ≤ s(s(s(s(s(0)))))$}
\end{prooftree}

We can read these rules top-to-bottom or bottom-to-top.

Such a proof is sometimes referred to a as *derivation*.

Each of the inference rules gives a different 'lego piece' that we can
use to write bigger proofs.



## Example: even numbers

We can use this inference rule notation to write all kinds of relations.

For example, we may want to define the unary relation isEven -- that
proves that a given number is even.


\begin{prooftree}
\AxiomC{ }
\RightLabel{isEven-Base}
\UnaryInfC{isEven(0)}
\end{prooftree}

\begin{prooftree}
\AxiomC{isEven(n)}
\RightLabel{isEven-Step}
\UnaryInfC{isEven(s(s(n))}
\end{prooftree}

#### {Question} \vspace{2mm}

Give a derivation that s(s(s(s(0)))) is even.




## Example: isSorted

Similarly, we can define inference rules that make precise when a list of numbers is sorted:

\begin{prooftree}
\AxiomC{ }
\RightLabel{isSorted-empty}
\UnaryInfC{isSorted($[ \, ]$)}
\end{prooftree}

\begin{prooftree}
\AxiomC{ }
\RightLabel{isSorted-Single}
\UnaryInfC{isSorted($n : [ \, ]$)}
\end{prooftree}

\begin{prooftree}
\AxiomC{$n ≤ m$}
\AxiomC{isSorted($m : w$)}
\RightLabel{isSorted-Step}
\BinaryInfC{isSorted($n : m : w$)}
\end{prooftree}

Note that we can require more than one hypothesis -- as in the isSorted-Step rule.

#### {Question}\vspace{2mm}

Prove that the list $1 : 3 : 5 : [ \, ]$ is indeed sorted.




## Exercise

A word over an alphabet Σ is called a **palindrome** if it reads the same backward as forward.

Examples include: 'racecar', 'radar', or 'madam'.

#### {Question}\vspace{2mm}

Give a inference rules that characterise a unary relation on words,
capturing the fact that they are a palindrome.

. . . 

\begin{prooftree}
\AxiomC{ }
\RightLabel{isPalindrome-empty}
\UnaryInfC{isPalindrome($ ε $)}
\end{prooftree}

\begin{prooftree}
\AxiomC{$a ∈ Σ$ }
\RightLabel{isPalindrome-Single}
\UnaryInfC{isPalindrome($a$)}
\end{prooftree}

\begin{prooftree}
\AxiomC{$a ∈ Σ$}
\AxiomC{isPalindrome($w$)}
\RightLabel{isPalindrome-Step}
\BinaryInfC{isPalindrome($a \, w \, a$)}
\end{prooftree}



## Challenge

Given the following set of propositional logical formulas over a set of atomic variables $P$:

 $p,q$  ::=  true | false | $P$ | $¬p$ | $p ∧ q$ | $p ∨ q$ | $p ⇒ q$ | $p ⇔ q$ 

Can we give inference rules that capture precisely the tautologies?

. . . 

Yes!

These inference rules, sometimes called *natural deduction*, formalize
the proof strategies that we have seen previously.



## Natural deduction

Most logical textbooks do not introduce an explicit name for the
relation capturing 'truthfulness' of a given propositional logical
formula, writing:

\begin{prooftree}
\AxiomC{$P$}
\AxiomC{$Q$}
\RightLabel{$\wedge$-I}
\BinaryInfC{$P \wedge Q$}
\end{prooftree}

Rather than the more explicit:

\begin{prooftree}
\AxiomC{isTrue($P$)}
\AxiomC{isTrue($Q$)}
\RightLabel{$\wedge$-I}
\BinaryInfC{isTrue($P \wedge Q$)}
\end{prooftree}



## Proof strategies vs natural deduction

Compare the proof strategy for conjunction introduction:

\begin{center}
\begin{tcolorbox}[width=6cm]
\begin{tcolorbox}
Proof of $P$
\end{tcolorbox}
\vspace{2mm}
\begin{tcolorbox}
Proof of $Q$
\end{tcolorbox}
\vspace{2mm}
Therefore we conclude $P ∧ Q$.
\end{tcolorbox} 
\end{center}

And the inference rule for conjunction introduction:

\begin{prooftree}
\AxiomC{$P$}
\AxiomC{$Q$}
\RightLabel{$\wedge$-I}
\BinaryInfC{$P \wedge Q$}
\end{prooftree}



## Conjuction elimination

\begin{center}
\begin{tcolorbox}[width=6cm]
\begin{tcolorbox}[width=4cm]
⋮
Proof of $P ∧ Q$\\
⋮
\end{tcolorbox}
\vspace{2mm}
Therefore, $P$ holds.
\end{tcolorbox}
\end{center}

#### {Question}\vspace{2mm}

What is the corresponding elimination rule for conjunction?


. . .

\begin{prooftree}
\AxiomC{$P \wedge Q$}
\RightLabel{$\wedge$-E$_l$}
\UnaryInfC{$P$}
\end{prooftree}



## Assumptions

Most textbooks in logic define natural deduction as a *unary* relation
on propositional formulas.

\begin{prooftree}
\AxiomC{$P \wedge Q$}
\RightLabel{$\wedge$-E$_l$}
\UnaryInfC{$P$}
\end{prooftree}

This rule states that from the assumption $P \wedge Q$, you can deduce $P$.

Once you have completed a derivation, we can read off all the
assumptions from the 'leaves' of our proof tree.



## Example derivation

Combining the rules we have seen so far, we can prove that if $P \wedge Q$ holds, so does $Q \wedge P$.

\begin{prooftree}
\AxiomC{$P \wedge Q$}
\RightLabel{$\wedge$-E$_r$}
\UnaryInfC{$Q$}
\AxiomC{$P \wedge Q$}
\RightLabel{$\wedge$-E$_l$}
\UnaryInfC{$P$}
\RightLabel{$\wedge$-I}
\BinaryInfC{$Q \wedge P$}
\end{prooftree}


But how can we manage these assumptions?

Wouldn't it be nicer to show that $(P \wedge Q) \Rightarrow (Q \wedge P)$ (without making any further assumptions)?

To prove this, we need the *implication introduction* rule.



## Implication introduction -- proof strategy


\begin{center}
\begin{tcolorbox}[width=8cm]
Assume $P$.\\
\begin{tcolorbox}[width=5cm]
⋮
Proof of $Q$.\\
⋮
\end{tcolorbox}
Therefore, we can conclude $P \Rightarrow Q \quad \square$
\end{tcolorbox}
\end{center}

In the implication introduction rule, we are allowed to *assume* that
$P$ holds to give a proof of $Q$, and then conclude $P \Rightarrow Q$
holds.

How can keep track of the assumptions in natural deduction proofs?



## Assumptions

\begin{prooftree}
\AxiomC{$P \wedge Q$}
\RightLabel{$\wedge$-E2}
\UnaryInfC{$Q$}
\AxiomC{$P \wedge Q$}
\RightLabel{$\wedge$-E1}
\UnaryInfC{$P$}
\RightLabel{$\wedge$-I}
\BinaryInfC{$Q \wedge P$}
\end{prooftree}

In the proof tree above, we have $P \wedge Q$ as \emph{axioms} --
propositions that we assume must hold.



## Implication introduction -- inference rule

\begin{prooftree}
\AxiomC{ }
\UnaryInfC{$P^1$}
\UnaryInfC{$\vdots$}
\UnaryInfC{$Q$}
\RightLabel{$\Rightarrow$-I 1}
\UnaryInfC{$P \Rightarrow Q$}
\end{prooftree}

The *implication introduction* rule takes a proof of $Q$ that is built
using $P$ as assumptions.

To conclude $P \Rightarrow Q$, we *discharge* all the occurrences of
$P$ as axioms *in the current subtree*.

We number each usage of the implication introduction rule; the
assumptions discharged are also numbered -- indicating which rule
discharged them.



## Example: $P \Rightarrow P$


\begin{prooftree}
\AxiomC{ }
\UnaryInfC{$P^1$}
\RightLabel{$\Rightarrow$-I 1}
\UnaryInfC{$P \Rightarrow P$}
\end{prooftree}

This proof is *closed* -- meaning there are no open assumptions that
it is making.

**Note:** when using the implication elimination rule more than once,
you'll need to assign a unique number to each application of this
inference rule.



## Example: $(P \wedge Q) \Rightarrow (Q \wedge P)$

#### {Question}\vspace{2mm}

Give a closed natural deduction proof of $(P \wedge Q) \Rightarrow (Q \wedge P)$.

. . .

\begin{prooftree}
\AxiomC{ }
\UnaryInfC{$(P \wedge Q)^1$}
\RightLabel{$\wedge$-E2}
\UnaryInfC{$Q$}
\AxiomC{ }
\UnaryInfC{$(P \wedge Q)^1$}
\RightLabel{$\wedge$-E1}
\UnaryInfC{$P$}
\RightLabel{$\wedge$-I}
\BinaryInfC{$Q \wedge P$}
\RightLabel{$\Rightarrow-I$ 1}
\UnaryInfC{$(P \wedge Q) \Rightarrow (Q \wedge P)$}
\end{prooftree}




## Wrong proofs

The statement $(P ⇒ P) ⇒ P$ is not true in general.

We previously saw how we 'abused' proof strategies to come up with an incorrect proof.

What kind of mistakes can we make when we writing a proof using natural deduction?

. . . 

\begin{prooftree}
\AxiomC{ }
\UnaryInfC{$P^1$}
\RightLabel{$\Rightarrow-I$ 1}
\UnaryInfC{$(P \Rightarrow P) \Rightarrow P$}
\end{prooftree}

Here we can make the previous mistake more explicit: we are
discharging the assumption $P$, whereas we should be discharging $P
\Rightarrow P$.



## Implication elimination

\begin{center}
\begin{tcolorbox}[width=8cm]
\begin{tcolorbox}[width=5cm]
Proof of $P \Rightarrow Q$.
\end{tcolorbox}
\vspace{5mm}
\begin{tcolorbox}[width=5cm]
Proof of $P$.
\end{tcolorbox}
Therefore, we can conclude $Q \quad \square$.
\end{tcolorbox}
\end{center}

#### {Question}\vspace{2mm}

What is the rule for implication elimination?

. . .

\begin{prooftree}
\AxiomC{$P$ }
\AxiomC{$P \Rightarrow Q$}
\RightLabel{$\Rightarrow-E$}
\BinaryInfC{$Q$}
\end{prooftree}



## Natural deduction

We'll go through the rules for natural deduction for propositional
logic.

Many of these rules closely mirror the proof strategies that we have
seen previously -- which is no coincidence of course.

They should be fairly familiar.

Once we've seen the rules for natural deduction proofs -- we can try
to relate them to the *truth table semantics* from our first lecture.



## Truth and falsity

Most logic textbooks use $\top$ for **T** (truth) and $\bot$ for **F**
(falsity).

The introduction rule for truth is trivial:

\begin{prooftree}
\AxiomC{$$}
\RightLabel{$\top$-I}
\UnaryInfC{$\top$}
\end{prooftree}

There is no introduction rule for falsity.



## Falsity elimination

\begin{center}
\begin{tcolorbox}[width=8cm]
\begin{tcolorbox}
Proof of a contradiction
\end{tcolorbox}
\vspace{2mm}
Therefore we conclude $P$.
\end{tcolorbox}
\end{center}

Or written as an inference rule:

\begin{prooftree}
\AxiomC{$\bot$}
\RightLabel{$\bot$-E}
\UnaryInfC{$P$}
\end{prooftree}



## Negation rules

Recall that $\neg P$ behaves just like $P \Rightarrow \bot$.


\begin{prooftree}
\AxiomC{$\neg P$}
\AxiomC{$P$}
\RightLabel{$\neg$-E}
\BinaryInfC{$\bot$}
\end{prooftree}

\begin{prooftree}
\AxiomC{ }
\UnaryInfC{$P^1$}
\UnaryInfC{$\vdots$}
\UnaryInfC{$\bot$}
\RightLabel{$\neg$-I 1}
\UnaryInfC{$\neg P$}
\end{prooftree}

**Note:** the negation introduction rule also discharges assumptions!
Remember: keep the numbering of such rules unique throughout the
entire proof tree to avoid confusion.

That is -- don't use rule number 1 for both introduction introduction
and negation introduction rules.


-

## Equivalence rules

Similarly, $P \Leftrightarrow Q$ behaves the same as $P \Rightarrow Q
\wedge P \Rightarrow P$.


\begin{prooftree}
\AxiomC{$P \Rightarrow Q$}
\AxiomC{$P \Rightarrow Q$}
\RightLabel{$\Leftrightarrow$-I}
\BinaryInfC{$P \Leftrightarrow Q$}
\end{prooftree}

\begin{prooftree}
\AxiomC{$P \Leftrightarrow Q$}
\RightLabel{$\Leftrightarrow$-$E_l$}
\UnaryInfC{$P \Rightarrow Q$}
\end{prooftree}

\begin{prooftree}
\AxiomC{$P \Leftrightarrow Q$}
\RightLabel{$\Leftrightarrow$-$E_r$}
\UnaryInfC{$Q \Rightarrow P$}
\end{prooftree}




## Exercise

#### {Question}\vspace{2mm}

Prove that $P \Rightarrow (Q \Rightarrow (Q \wedge P))$

. . . 

\begin{prooftree}
\AxiomC{}
\UnaryInfC{$Q^2$}
\AxiomC{}
\UnaryInfC{$P^1$}
\BinaryInfC{$Q \wedge P$}
\RightLabel{$\Rightarrow$-I 2}
\UnaryInfC{$Q \Rightarrow (Q \wedge P)$}
\RightLabel{$\Rightarrow$-I 1}
\UnaryInfC{$P \Rightarrow (Q \Rightarrow (Q \wedge P))$}
\end{prooftree}



## Discharging more than once

Consider the following proof that $P \Rightarrow (P \wedge P)$

\begin{prooftree}
\AxiomC{}
\UnaryInfC{$P^1$}
\AxiomC{}
\UnaryInfC{$P^1$}
\BinaryInfC{$P \wedge P$}
\RightLabel{$\Rightarrow$-I 1}
\UnaryInfC{$P \Rightarrow (P \wedge P)$}
\end{prooftree}

This example shows how we need to discharge **all** the occurrences of
the assumption $P$ in the current proof subtree.

-

## Exercise

#### {Question}\vspace{2mm}

Prove that $P \wedge \top \Leftrightarrow P$.

. . . 

\begin{prooftree}
\AxiomC{ }
\UnaryInfC{$P^1$}
\AxiomC{ }
\RightLabel{$\top$-I}
\UnaryInfC{$\top$}
\RightLabel{$\wedge$-I}
\BinaryInfC{$P \wedge \top$}
\RightLabel{$\Rightarrow$-I 1}
\UnaryInfC{$P \Rightarrow (P \wedge \top)$}
\AxiomC{}
\UnaryInfC{$(P \wedge \top)^2$}
\RightLabel{$\wedge$-E$_l$}
\UnaryInfC{$P$}
\RightLabel{$\Rightarrow$-I 2}
\UnaryInfC{$(P \wedge \top) \Rightarrow P$}
\RightLabel{$\Leftrightarrow$-I}
\BinaryInfC{$P \wedge \top \Leftrightarrow P$}
\end{prooftree}



## What's missing?

The only thing remaining are the rules for disjunction.

The *introduction* rules are easy:

. . . 


\begin{prooftree}
\AxiomC{$P$}
\RightLabel{$\vee$-$I_l$}
\UnaryInfC{$P \vee Q$}
\end{prooftree}

\begin{prooftree}
\AxiomC{$Q$}
\RightLabel{$\vee$-$I_r$}
\UnaryInfC{$P \vee Q$}
\end{prooftree}



## Disjuction elimination: proof strategy

\begin{center}
\begin{tcolorbox}[width=9cm]
\begin{tcolorbox}[width=6cm]
Proof of $P ∨ Q$
\end{tcolorbox}
Assume that $P$ is true.\vspace{2mm}
\begin{tcolorbox}[width=6cm]
Proof of $R$
\end{tcolorbox}
\vspace{2mm}
Next, assume $Q$ is true.
\vspace{2mm}
\begin{tcolorbox}[width=6cm]
Proof of $R$
\end{tcolorbox}
\vspace{2mm}
Therefore, $R$ is true, regardless of which of $P$ or $Q$ is true.
\end{tcolorbox}
\end{center}



## Disjuction elimination

\begin{prooftree}
\AxiomC{$P \vee Q$}
\AxiomC{ }
\UnaryInfC{$P^1$}
\UnaryInfC{$\vdots$}
\UnaryInfC{$R$}

\AxiomC{ }
\UnaryInfC{$Q^1$}
\UnaryInfC{$\vdots$}
\UnaryInfC{$R$}

\RightLabel{$\vee$-E 1}
\TrinaryInfC{$R$}
\end{prooftree}

If we know $P \vee Q$ holds...

... and we know that $R$ holds whenever $P$ does;

... and we know that $R$ holds whenever $Q$ does;

... we can conclude that $R$ must always hold.



## Exercise

#### {Question}\vspace{2mm}

Give a proof that $(P \vee \bot) \Rightarrow P$.

. . .

\begin{prooftree}
\AxiomC{ }
\UnaryInfC{$(P \vee \bot)^1$}

\AxiomC{ }
\UnaryInfC{$P^2$}

\AxiomC{ }
\UnaryInfC{$\bot^2$}
\UnaryInfC{$P$}

\RightLabel{$\vee$-E 2}
\TrinaryInfC{$P$}
\RightLabel{$\Rightarrow$-I 1}
\UnaryInfC{$P \vee \bot \Rightarrow P$}
\end{prooftree}



## Final rules

We need one final rule:

\begin{prooftree}
\AxiomC{ }
\UnaryInfC{$\neg P^1$}
\UnaryInfC{$\vdots$}
\RightLabel{$\wedge$-E1}
\UnaryInfC{$\bot$}
\RightLabel{RAA}
\UnaryInfC{$P$}
\end{prooftree}

This rule, sometimes called *reductio ad absurdum*, states that if
$\neg P$ leads to a contradiction, $P$ must hold.

(Notice how it is the only rule that is not an
introduction-elimination rule for a logical operator?)




## Beyond propositional logic...

I've presented the rules for propositional logic -- but we can extend
these rules to handle *predicate* logic.

Rather than introduce a more complicated system for natural deduction
for handling quantifiers, I'd rather relate the natural deduction
rules to truth tables...

But before I can do that, let's revisit what 'proof-by-truth-table'
really means...



## Semantics of propositional logic

When we fill out a truth table for some propositional formula $p$, we
show how each choice of atomic propositional variables of $p$ results
in a true/false value.

| `p`     | `q`    | `¬` | `(p` | `∨` | `q)` | `⇒`    | `(¬p` | `∧` | `¬q)` |
|:-:|::|::|:-:|::|:-:|::|:--:|::|:--:|
|  F      |  F     |  T  |   F  |  F  |  F   |  **T** |   T   |  T  |   T   |
|  F      |  T     |  F  |   F  |  T  |  T   |  **T** |   T   |  F  |   F   |
|  T      |  F     |  F  |   T  |  T  |  F   |  **T** |   F   |  F  |   T   |
|  T      |  T     |  F  |   T  |  T  |  T   |  **T** |   F   |  F  |   F   |

For each value of `p` and `q`, we can check the corresponding row to
see the value of the entire proposotional formula.

Can we make this more precise?



## Semantics of propositional logic

We call a function $v : P$ → **Bool** a *truth assignment*.

Such a function chooses the values of associated with each atomic propositional variables.

**Claim** Given any truth assignment $v$ and propositional logic
formula $p$, we can calculate the truth value of a $p$.



## Semantics of propositional logic

**Claim** Given any truth assignment $v$ and propositional logic
formula $p$, we can calculate the truth value of a $p$.

We can do this by induction on $p$. Recall that the propositional
logic formulas are given by the following BNF:

 $p,q$  ::=  true | false | $P$ | $¬p$ | $p ∧ q$ | $p ∨ q$ | $p ⇒ q$ | $p ⇔ q$ 

. . .

* if $p$ is true, we return **T**;
* if $p$ is false, we return **F**;
* if $p$ is of the form $\neg q$, we can compute the value associated
  with $q$. If this is **T**, we return **F**; if it is **F**, we
  return **T**.





## Semantics of propositional logic

**Claim** Given any truth assignment $v$ and propositional logic
formula $p$, we can calculate the truth value of a $p$.

We can do this by induction on $p$. Recall that the propositional
logic formulas are given by the following BNF:

 $p,q$  ::=  true | false | $P$ | $¬p$ | $p ∧ q$ | $p ∨ q$ | $p ⇒ q$ | $p ⇔ q$ 

. . .

* if $p$ is of the form $q_1 \wedge q_2$, we can compute the value
  associated with $q_1$ and $q_2$. If this both are **T**, we return
  **T**; otherwise we return **F**.
* if $p$ is of the form $q_1 \vee q_2$, we can compute the value
  associated with $q_1$ and $q_2$. If this both are **F**, we return
  **F**; otherwise we return **T**.
* similar cases exist for implication and logical equivalence.
. . . 

* but what about variables?



## Semantics of propositional logic

**Claim** Given any truth assignment $v$ and propositional logic
formula $p$, we can calculate the truth value of a $p$.

We can do this by induction on $p$. Recall that the propositional
logic formulas are given by the following BNF:

 $p,q$  ::=  true | false | $P$ | $¬p$ | $p ∧ q$ | $p ∨ q$ | $p ⇒ q$ | $p ⇔ q$ 

* if $p$ is an atomic propositional variable $P$, we return $v(P)$.

Our truth assignment tells us exactly how to treat atomic propositions.



## Semantics of propositional logic

**Claim** Given any truth assignment $v$ and propositional logic
formula $p$, we can calculate the truth value of a $p$.

This defines the semantics of all propositional logic formulas,
usually written $〚 p 〛$.

  $〚 p 〛: (P → \Bool) → \Bool$

That is, we have defined a function that maps each propositional logic
formula $p$ into a function that, given a truth assignment for all
atomic propositional variables, computes the truth value of the entire
propositional logic formula $p$.

. . . 

But what does this have to do with truth tables?



## Finite functions

If you think back to the lectures on functions and induction, we saw
how to *define* a function on a *finite* domain by listing all it
output value for every possible input value.

Suppose I'm teaching a class with 5 students 

S = \{Alice, Bob, Carroll, David, Eve \}.

I can define a functions `marks` mapping $S \to \{1..10\}$ by giving
each student their mark:

 marks(Alice)     = 8

 marks(Bob)       = 6

 marks(Carroll)   = 7

 ...
 


## Finite functions and truth tables

When filling out a truth table for some propositional logic formula
$p$, you are essentially computing the truth value of $p$ *for all
possible choice of value for the atomic variables in p*.

For any formula $p$, there are $2^{\mid fv(p)\mid}$ possible truth
assignments for the free variables in $p$.

Hence, you can give the semantics for $p$, that is the function:

  $〚 p 〛: (P → \Bool) → \Bool$

as a truth table with $2^{\mid fv(p)\mid}$ rows.

**Truth tables are simply the tabulation of this semantics.**



## Natural deduction vs semantics

Given any propositional logic formula $p$, we can assign it semantics:

  $〚 p 〛: (P → \Bool) → \Bool$

But how is this semantics related to our natural deduction rules?

Our inference rules for natural deduction all seem perfectly 'logical'.

But can we be sure that any propositional formula proven using this
inference rules always holds?

And can we be sure that we haven't left out any inference rules?



## Notation

Given a set of propositional logic formulas, $\Gamma$, we will write
$\Gamma \vdash p$ whenever we can find a natural deduction proof of
the formula $p$ using the assumptions from $\Gamma$.

When we do not need any assumptions to show $p$, we write $\vdash p$.

. . . 

Given an truth assignment $v$ we write $v \models p$ if $\llbracket p
\rrbracket v = \mathbf{T}$.

If for all truth assignments $v$, we have $v \models p$ we say that $\models
p$ (and $p$ is a tautotology).



## Soundness and completeness

It turns out that natural deduction inference rules above satisfy two
important properties:

**Soundness** If $\vdash p$ then $\models p$. In other words, if we can find a proof
of $p$ using the inference rules of natural deduction, then the truth
table of $p$ consists of only **T**.

**Completeness** If $\models p$ then $\vdash p$. In other words, if the truth table of
$p$ consists of only **T**, there is *some* derivation of $p$ using
the inference rules of natural deduction.



## Proofs?

The proofs of soundness and completeness are a subject of a more
advanced course on formal logic...

...but in principle you have the reasoning techniques to understand
them.

. . . 

* Soundness is relatively easy to show: given a derivation of some
  formula $p$, we can do induction on this derivation. If we can show
  each of our inference rules is safe to use, we can trust each proof
  built using them.
  
* Completeness is harder: we don't have a derivation to do induction
  on; instead we need to create a derivation for some arbitrary
  formula $p$... The proof of completeness is usually much harder; the
  lecture notes from last year give one proof, going via a
  Hilbert-style proof system.



## Soundness and completeness

These results show just how clean and simple propositional logic is...

But they break down as soon as you study richer predicate logics...




# Natural deducton

Now that we know how to define inductive relations, we can study *proofs* formally.

Given a propositional formula, can we define the *proofs* of this formula?

This turns out to formalize the proof strategies we have seen previously.

## Soundness and completeness

## Exercises

# Reasoning about programs

We have already seen the syntax of a (toy) programming language, While
-- but what is its semantics?

## Operational semantics



 $e$  ::=  $n$ | $x$ | $e + e$ | $e × e$ | …

 $b$  ::=  true | false | $b₁$ || $b₂$ | $b₁$ && $b₂$ | $e₁$ < $e₂$ | …

**Idea** We can write a pair of inductively defined functions that
take *syntax*, evaluate it to a number or boolean.

But – this doesn't quite work: what is the value of `x + 3`?

. . .

This depends on the last value we assigned to the variable `x` -- we
need to keep track of the computer's memory.

## Memory

We can mode the contents of the computer's memory as a function $V \to
\Int$  this function tells us for each variable in $V$ what its
current value is.

We can use this function to write a pair of inductively defined functions
that take *syntax*, evaluate it to a number or boolean.

   $〚 e 〛: (V \to \Int) \to \Int$
   $〚 b 〛: (V \to \Int) \to \Bool$

Just as we saw for the semantics of propositional logic, we use this
function to associate meaning with variables.



## Example

Previously we didn't know the meaning of `x + 3` – but what if we are
given the current memory $σ : V → \Int$ and we know that $σ(x) = 7$:

  $〚 x + 3  〛_\sigma = 〚 x 〛_\sigma+〚 3 〛_\sigma= σ(x) + 3 = 7 + 3 = 10$

We can compute the integer associated with expressions and the boolean
value associated with boolean expressions provided we know the current
*state* of the computer's memory.



## Semantics for statements

 $p$  ::=  $x := e$ 

   | $p₁;p₂$ 

   | if $b$ then $p₁$ else $p₂$ 

   | while $b$ do $p$

How should I define a semantics?

A statement such as:

   $x := 17$

doesn't return any interesting result -- but rather *modifies the state of our program*

. . .

Any semantics for our language should carefully describe how the state changes...




## Example execution

\begin{tabular}{p{10mm}l}
 & \texttt{x := 3;}  \\
 &\texttt{p := 0;}  \\
 &\texttt{i := 1;}  \\
 &\texttt{while (i <= x)}  \\
 &\texttt{\{}  \\
 &\quad\quad \texttt{p := p+i;}  \\
 &\quad\quad \texttt{i := i+1;}  \\
 &\texttt{\}}  \\
\end{tabular}

We start execution from some begin state -- let's assume that the
variables `x`, `p` and `i` all start as 0,1,2 respectively.
That is initially we're in a state $\sigma$ which satisfies:

 $σ(\mathtt{x}) = 0$
 $σ(\mathtt{p}) = 1$
 $σ(\mathtt{i}) = 2$

Now let's run this program step by step...


## Hoare logic

## Making this more precise...

This gives some idea of how a program is executed.

But this example raises some interesting questions:

* What would have happened if we would have used a different initial
  state? Would the results have been the same?
  
* Does every program terminate in a finite number of steps?

* Can our program 'go wrong' somehow -- dividing by zero or accessing
  unallocated memory?
  
My goal isn't to answer all these questions -- but just to highlight
the kind of issues you need to address when making the semantics of
programming languages precise.

Let's try to give a mathematical account of program execution.



## Modelling state

We model the current state of our computer's memory (storing the value
of all our variables) as function:

  $σ : V \to \Int$

If we want to know the value of a given variable $x$, we can simply
look it up $σ(x)$;

We will sometimes also need to *update* the current memory.

We write $σ[x ↦ n]$ for the memory that is the same as σ for all
variables in $V$ **except** $x$, where it stores the value $n$.

In other words, this updates the current memory at one location,
setting the value for $x$ to $n$.



## The meaning of our programs

Using the *inference rule notation* from the previous lecture, we can
formalize the semantics of our language.

The key idea is that we define a relation on (While × State) × (While
× State) – that is given the current state of the computer's memory
and the program that we're executing, this relation determines the
next state and remaining program to execute...

This formalizes the example we had a few slides ago, where we 'stepped
through' the execution of a program studying how the state changed at
every step.



## Notation

We will write use the following notation:

  ⟨ p , σ ⟩ → ⟨ p' , σ' ⟩

To mean that the program $p$ running with the current state σ can
perform a single step of execution, yielding a new state σ' and
remaining program to execute $p'$.

If running $p$ for one step causes our program to terminate we write:


  ⟨ p , σ ⟩ → σ' 

To mean the program $p$ running in the state σ terminates in one step,
producing the final state σ'.

This relation gives an **operational semantics** for our programs,
describing how to execute a program step by step.



## Operational semantics

 $p$  ::=  $x := e$  |   $p₁;p₂$  |  if $b$ then $p₁$ else $p₂$ fi   |   while $b$ do $p$ end

We have four language constructs -- we'll only need very few rules to
describe their behaviour (in contrast to, say, natural deduction rules
for propositional logic).

* Assignments -- $x := e$

* Sequential composition -- $p₁;p₂$

* Conditionals -- if $b$ then $p₁$ else $p₂$ fi

* Loops -- while $b$ do $p$ end



## Assignment

\begin{prooftree}
\RightLabel{Assignment}
\AxiomC{$\llbracket e \rrbracket_\sigma = n$}
\UnaryInfC{$\langle x := e , \sigma \rangle \; \to \; \sigma[x \mapsto n]$}
\end{prooftree}

There is one rule for handling assignment.

The assignment statement always terminates in one step.

Starting in the state σ, executing $x := e$ produces a new state, σ[x
↦ n], that updates the memory location for $x$ to store the value of $e$.

For example, given a state σ satisfying $σ(y) = 3$, we can execute the
command $x := y + 2$ by:

\begin{prooftree}
\AxiomC{$\llbracket y + 2 \rrbracket_\sigma = 5$}
\UnaryInfC{$\langle x := y + 2 , \sigma \rangle \; \to \; \sigma[x \mapsto 5]$}
\end{prooftree}



## Conditionals


\begin{prooftree}
\RightLabel{If-true}
\AxiomC{$\llbracket b \rrbracket_\sigma = true $}
\UnaryInfC{⟨ if $b$ then $p_1$ else $p_2$ fi  , σ ⟩ → ⟨ $p_1$ , σ ⟩}
\end{prooftree}

\begin{prooftree}
\RightLabel{If-false}
\AxiomC{$\llbracket b \rrbracket_\sigma = false $}
\UnaryInfC{⟨ if $b$ then $p_1$ else $p_2$ fi  , σ ⟩ → ⟨ $p_2$ , σ ⟩}
\end{prooftree}

There are two rules for evaluating if-then-else statements:

* if the guard $b$ is true, we continue evaluating the then branch, leaving the state unchanged;

* if the guard $b$ is false, we continue evaluating the else branch, leaving the state unchanged;




## Example


Suppose we start from a state σ satisfying σ(x) = 3 and σ(y) = 10

We can execute the following program:

```c
if x < y then r := x else r := y
```

Using the previous derivation rules:


\begin{prooftree}
\RightLabel{If-true}
\AxiomC{$\llbracket x < y \rrbracket_\sigma = true $}
\UnaryInfC{⟨ if $x < y$ then $r := x$ else $r := y$ fi  , σ ⟩ → ⟨ $r := x$ , σ ⟩}
\end{prooftree}


\begin{prooftree}
\RightLabel{Assignment}
\AxiomC{$\llbracket x < y \rrbracket_\sigma = true $}
\UnaryInfC{⟨ $r := x$  , σ ⟩ → σ[r ↦ 3]}
\end{prooftree}




## Notation

It's often clear enough which rule is being applied.

For reasons of space, I may sometimes write:

⟨ if $x < y$ then $r := x$ else $r := y$ fi  , σ ⟩ → ⟨ $r := x$ , σ ⟩ → σ[r ↦ 3]

In other words, our original progam halts in the state where r has become 3.




## Sequential composition

\begin{prooftree}
\RightLabel{seq-a}
\AxiomC{⟨ $p_1$ , σ ⟩ → $σ'$}
\UnaryInfC{⟨ $(p_1 ; p_2)$ , σ ⟩ → ⟨ $p_2$ , $σ'$ ⟩}
\end{prooftree}

\begin{prooftree}
\RightLabel{seq-b}
\AxiomC{⟨ $p_1$ , σ ⟩ → ⟨ $p_1'$, $σ'$ ⟩}
\UnaryInfC{⟨ $(p_1 ; p_2)$ , σ ⟩ → ⟨ $(p_1' ; p_2$) , $σ'$ ⟩}
\end{prooftree}

There are two rules for sequential composition:

* if the first program, $p_1$, stops after one step in the state $σ'$,
  we continue executing the second program $p_2$ from $σ'$;
* otherwise, we continue evaluating the remaining program $p_1'$ until
  it is done.




## Sequential composition

\begin{prooftree}
\RightLabel{seq-a}
\AxiomC{⟨ $p_1$ , σ ⟩ → $σ'$}
\UnaryInfC{⟨ $(p_1 ; p_2)$ , σ ⟩ → ⟨ $p_2$ , $σ'$ ⟩}
\end{prooftree}

\begin{prooftree}
\RightLabel{seq-b}
\AxiomC{⟨ $p_1$ , σ ⟩ → ⟨ $p_1'$, $σ'$ ⟩}
\UnaryInfC{⟨ $(p_1 ; p_2)$ , σ ⟩ → ⟨ $(p_1' ; p_2$) , $σ'$ ⟩}
\end{prooftree}

There are two rules for sequential composition:

* if $p_1$ is done in one step (like an assignment) -- we'll generally use the first rule;
* if $p_1$ needs more steps, like the if-then-else rules or loops,
  we'll use the second rule.




## Loops

\begin{prooftree}
\RightLabel{While-false}
\AxiomC{$\llbracket b \rrbracket_\sigma = false $}
\UnaryInfC{⟨ while $b$ do $p$ od  , σ ⟩ → σ}
\end{prooftree}

\begin{prooftree}
\RightLabel{While-true}
\AxiomC{$\llbracket b \rrbracket_\sigma = true $}
\UnaryInfC{⟨ while $b$ do $p$ od  , σ ⟩ → ⟨ $p$ ; while $b$ do $p$ od , σ ⟩}
\end{prooftree}

Just as we saw for conditionals, we need two rules to handle loops:

* if the guard $b$ is false, we do not enter the loop body or change
  the state -- but rather halt in the current state σ;
* if the guard $b$ is true, we execute the loop body $p$, and then
  continue executing the main while loop.



## Operational semantics

These seven rules determine precisely how a program is executed.

Given any initial state σ and program $p$, we can repeatedly apply
these rules to determine if the program terminates or not.

This formalizes the process I went through with large example I did at
the beginning of the lecture: showing how to evaluate an example
program from some initial state.

Let's extend our operational semantics to handle many execution steps



## More than one step

We say a given program $p$ and starting state σ **terminates** in τ
precisely if:

* ⟨ $p$ , σ ⟩ → $\tau$
* or ⟨ $p$ , σ ⟩ → ⟨ $p'$ , $σ'$ ⟩ and ⟨ $p'$ , $σ'$ ⟩ terminates in τ;

Our initial example showed how the following program terminates

```
x := 3; p:= 0; i := 1;
while (i <= x) {
  p:=p+i; i:=i+1; }
```
 in the state

 $σ(\mathtt{x}) = 3$
 $σ(\mathtt{p}) = 6$
 $σ(\mathtt{i}) = 4$

by repeatedly applying the rules from our operational semantics.




## Labelled transition systems

This semantics forms a **labelled transition system**:

* the set of states are the current program $p$ and memory σ;
* our operational semantics determine the transition relation between
  our states;
* if we extend our language with other effects, such as opening a
  window or writing to stdout -- we can add further *actions* to our
  system to observe these effects.



## From operational semantics to logic

These operational semantics determine how a program is executed from a given initial state σ.

But consider the following mini-program:

```c
if x < y then r := x else r := y
```

Can we prove that after execution `r` will store the minimal value of `x` and `y`?

This requires reasoning about *all* possible states -- rather than *one* initial state.

To perform this kind of reasoning, we need a logic to reason about **all possible** executions.

. . .

This motivates the shift from *operational semantics* to *program logic*.



## Specifications

A **formal specification** is a mathematical description of what a program should do.

Such a specification ignores many important details, such as the
*non-functional* requirements about how fast the program is, the
language used for its implementation, the development cost, etc.

Instead, we use a formal specification to answer one question:

**Is this program doing what it should?**



## Specificiations

We will give specifications in the form of a pre- and post-condition
that are predicates on our states.

Intuitively, the precondition captures the assumptions the program
makes about the initial state;

The postcondition expresses the properties that are guaranteed to hold
after the program has finished executing.



## Notation

To define our logic for reasoning about programs, we introduce the following notation:

\begin{center}
\begin{tabular}{ccc}
\large{$\{\ P \ \}$} & \large{$p$} & \large{$\{\ Q \ \}$}\\
&&\\
pre-condition & programme & post-condition
\end{tabular}
\end{center}

For each state σ that satisfies the precondition $P$, 

if executing $⟨ p , σ ⟩$ terminates in some final state τ, then τ must satisfy $Q$.

We'll define this -- once again -- using inference rules. But's let
look at some examples first.



## Examples

* \{ x = 3\}  `x := x + 1`  \{ x = 4\}

Unsurprising: if x = 3, after executing `x := x + 1`, we know x = 4.

* \{ x = A ∧ y = B\}  z:= x; x := y; y := z  \{ x = B ∧ y = A\}

This is more interesting: it works for *any* values of A and B -- this
describes many possible executions, starting from some state for which
the precondition holds.

* \{ true \} while true do p := 0 od  \{p = 500 \}

Note that the postcondition only makes a statement about the final
state. If the program never terminates, it trivially satisfies any
postcondition!



## Examples

\{ true \} 
```c
  x := 3;
  p := 0;
  i := 1;
  while i <= x do
        p := p + i;
        i := i+1
  od
```
\{ p = 6 \}

How can we write a derivation proving this? What are the *inference rules* that we can use?



## Hoare logic

We'll give a handful of inference rules for proving statements of the
form $\{ P \} \; p \; \{ Q \}$.

Together these define a logic known as *Hoare logic* -- named after
Tony Hoare, a British computer scientist who pioneered the approach
together with Edsger Dijkstra, Robert Floyd, and others.



## Hoare logic -- assignment

What rule should we use for assignment? We've seen one example:

\{ x = 3\}  `x := x + 1`  \{ x = 4\}

We could generalise this:

\{ x = N\}  `x := x + 1`  \{ x = N + 1\}

. . .

But what if we want to assign another expression than `x + 1`?

Or what if the pre- and postcoditions are not a simple equality?

. . .

What's the most general rule?



## Hoare logic -- assignment


\begin{prooftree}
\AxiomC{}
\RightLabel{Assign}
\UnaryInfC{\{ $Q[x \backslash e]$ \}  x := e  \{ $Q$ \}}
\end{prooftree}

* We write $Q[x \backslash e]$ for the result of replacing all the
  occurrences of $x$ with $e$ in $Q$.

* This rule seems backwards! It helps to read it back to front: in
  order for $Q$ to hold after the assignment x := e, the precondition
  $Q[x \backslash e]$ should already hold.
  
Let's look at some examples...



## Hoare logic -- assignment


\begin{prooftree}
\AxiomC{}
\RightLabel{Assign}
\UnaryInfC{\{ $Q[x \backslash e]$ \}  x := e  \{ $Q$ \}}
\end{prooftree}

Here are three different examples of this rule in action:

\begin{prooftree}
\AxiomC{}
\RightLabel{Assign}
\UnaryInfC{\{ y = 3 \} x := 3 \{ y = x \}}
\end{prooftree}


\begin{prooftree}
\AxiomC{}
\RightLabel{Assign}
\UnaryInfC{\{ x = N + 1 \} x := x - 1 \{ x = N \}}
\end{prooftree}


\begin{prooftree}
\AxiomC{}
\RightLabel{Assign}
\UnaryInfC{\{ x + y = V \} z := x + y \{ z = V \}}
\end{prooftree}







## Hoare logic -- conditional


\begin{prooftree}
\AxiomC{????}
\AxiomC{????}
\RightLabel{If}
\BinaryInfC{\{ $P$ \} \quad if $b$ then $p_1$ else $p_2$ \quad \{ $Q$ \}}
\end{prooftree}

What happens when we execute an if statement?

We will continue executing either the 'then-branch' or the
'else-branch'; if both branches manage to end in a state satisfying
$Q$, the entire if-statement will.



## Hoare logic -- conditional


\begin{prooftree}
\AxiomC{\{ $P \wedge b$ \} \; $p_1$ \; \{$Q$\}}
\AxiomC{\{ $P \wedge \neg b$ \} \; $p_2$ \; \{$Q$\}}
\RightLabel{If}
\BinaryInfC{\{ $P$ \} \quad if $b$ then $p_1$ else $p_2$ \quad \{ $Q$ \}}
\end{prooftree}


By checking whether the guard $b$ holds or not, we learn something. As
a result, the precondition changes in both branches of the if-statement.

. . . 

## Question

Use the two rules we have seen so far to show that:

  \{ 0 ≤ x ≤ 5 \}  if x < 5 then x := x+1 else x := 0 fi  \{ 0 ≤ x ≤ 5 \}



## Hoare logic -- composition

\begin{prooftree}
\AxiomC{\{ $P$ \} \; $p_1$ \; \{$R$\}}
\AxiomC{\{ $R$ \} \; $p_2$ \; \{$Q$\}}
\RightLabel{Seq}
\BinaryInfC{\{ $P$ \} \quad $p_1 ; p_2$ \quad \{ $Q$ \}}
\end{prooftree}

The rule for composition of programs is beautiful – it may remind you
of function composition.

If we know that $P$ holds of our initial state, we can run $p_1$ to
reach a state satisfying $R$;

But now we can run $p_2$ on this state, to produce a state satisfying $Q$.



## Hoare logic -- bookkeeping

\begin{prooftree}
\AxiomC{\{ $P$ \} \; $p_1$ \; \{$R$\}}
\AxiomC{\{ $R$ \} \; $p_2$ \; \{$Q$\}}
\RightLabel{Seq}
\BinaryInfC{\{ $P$ \} \quad $p_1 ; p_2$ \quad \{ $Q$ \}}
\end{prooftree}

If you look at this rule though, you may need to be very lucky to be
able to use it: the postcondition of $p_1$ and precondition of $p_2$
must match **exactly**...

This rarely happens in larger derivations.

To still be able to use such rules, we need an additional
'bookkeeping' rule.



## Hoare logic -- consequence

\begin{prooftree}
\AxiomC{$P' \Rightarrow P$}
\AxiomC{\{ $P$ \} \; $p$ \; \{$Q$\}}
\AxiomC{$Q \Rightarrow Q'$}
\RightLabel{Consequence}
\TrinaryInfC{\{ $P'$ \} \quad $p$ \quad \{ $Q'$ \}}
\end{prooftree}


The **rule of consequence** states that we can change the pre- and postcondition provided:

* the **precondition** is **stronger** -- that is, $P' \Rightarrow P$;
* the **postcondition** is **weaker** -- that is, $Q \Rightarrow Q'$;

We can justify this rule by thinking back to what a statement of the
form $\{ P \} \; p \; \{ Q \}$ means:


For each state σ that satisfies the precondition $P$, 

if executing $⟨ p , σ ⟩$ terminates in some final state τ, then τ must satisfy $Q$.




## Hoare logic -- while

\begin{prooftree}
\AxiomC{\{ $??? \wedge b$ \} \; $p$ \; \{$???$\}}
\RightLabel{While}
\UnaryInfC{\{ $P$ \} \quad while $b$ do $p$ od \quad \{ $??? \wedge \neg b$ \}}
\end{prooftree}

The general structure of the rule for loops should be along these lines:

* some precondition $P$ should hold initially;
* the loop body may assume that the guard $b$ is true;
* after completion, we know that the guard $b$ is no longer true.

But how should we fill in the question marks?



## Hoare logic -- while

\begin{prooftree}
\AxiomC{\{ ${P} \wedge b$ \} \; $p$ \; \{$???$\}}
\RightLabel{While}
\UnaryInfC{\{ $P$ \} \quad while $b$ do $p$ od \quad \{ $??? \wedge \neg b$ \}}
\end{prooftree}

When we first enter the loop body, we know that $P$ still holds.



## Hoare logic -- while

\begin{prooftree}
\AxiomC{\{ $P \wedge b$ \} \; $p$ \; \{${P}$\}}
\RightLabel{While}
\UnaryInfC{\{ $P$ \} \quad while $b$ do $p$ od \quad \{ $??? \wedge \neg b$ \}}
\end{prooftree}

After completing the loop body, we may need to execute the loop body
again (and again and again and again).

The precondition of $p$ should *continue to hold during execution*.





## Hoare logic -- while

\begin{prooftree}
\AxiomC{\{ $P \wedge b$ \} \; $p$ \; \{$P$\}}
\RightLabel{While}
\UnaryInfC{\{ $P$ \} \quad while $b$ do $p$ od \quad \{ ${P} \wedge \neg b$ \}}
\end{prooftree}

After running the loop body over and over again, the postcondition of
the entire while statement says that both $P$ and $\neg b$ hold.

. . .

We call $P$ the **loop invariant** -- it continues to hold throughout
the execution of the while loop.



## Example

#### {Question}\vspace{2mm}

Give a derivation of the following statement:

\{ x ≥ 5 \}  `while x > 5 do x := x - 1 od`  \{ x ≥ 5 ∧ x ≤ 5\}

. . .

\begin{prooftree}
\RightLabel{Assignment}
\AxiomC{ \{ x - 1 ≥ 5 \}  x := x -1   \{ x ≥ 5 \}}    
\RightLabel{Consq}
\UnaryInfC{ \{ x ≥ 5 ∧ x > 5 \}  x := x -1   \{ x ≥ 5 \}}
\RightLabel{While}
\UnaryInfC{\{ x ≥ 5 \}  while x > 5 do x := x - 1 od  \{ x ≥ 5 ∧ x ≤ 5\}}
\end{prooftree}





## Hoare logic -- soundness and completeness

How can we be sure that we chose the right set of inference rules?

Once again, we can show that these rules are **sound** and
**complete** with respect to our operational semantics.


**Soundness** If we can prove $\{ P \} \; p \; \{ Q \}$ then for all
states σ such that $P(σ)$, if ⟨ p , σ ⟩ → τ then $Q(τ)$

**Completeness** For all states σ and τ and programs $p$,
such that ⟨ p , σ ⟩ → τ. Then for all preconditions $P$ and
postconditions $Q$ for which $P(σ) ⇒ Q(τ)$, there exists a
derivation showing $\{ P \} \; p \; \{ Q \}$.

**We can reason about all possible program behaviours
using the rules of Hoare logic.**

. . . 

Put differently, we never need to *execute* code to prove its correctness.



## From While to C\#

We still need to consider a bucketload of missing features to turn our
simple imperative language into a more realistic programming language:

* Classes, objects, inheritance, abstract classes, virtual methods, ...
* Strings, arrays, and other richer types
* Exceptions;
* Concurrency;
* Recursion;
* Shared memory;
* Standard libraries;
* Compiler primitives;
* Foreign function interfaces;
* ...




## Program calculation

#### Problem\vspace{2mm}

Given a precondition $P$ and postcondition $Q$, find a program $p$
such that $\{ P \} \; p \; \{ Q \}$ holds.

There is a rich field of research on **program calculation** that tries to solve this problem.

Approaches include the refinement calculus, pioneered by people such
as Edsger Dijkstra, Tony Hoare, and many others.





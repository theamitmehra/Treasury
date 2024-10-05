# The Foundations : Logic and Proofs 
## Propositional Logic

A **proposition** is a declarative sentence (that is, a sentence that declares a fact) that is either true or false, but not both.
We use letters to denote **propositional variables** (or sentential variables), that is, variables
that represent propositions, just as letters are used to denote numerical variables. 
The conventional letters used for propositional variables are p, q, r, s, $\ldots$.

The truth value of a proposition is true, denoted by T, if it is a true proposition, and the truth value of a proposition is false, denoted by F, if it is a false proposition. Propositions that cannot be expressed in terms of simpler propositions are called **atomic propositions**.
The area of logic that deals with propositions is called the **propositional calculus or propositional logic**. 
#### Logical Operators
* **Negation ($\lnot$p)** :
	Let p be a proposition. The negation of p, denoted by $\lnot$p (also denoted by p), is the statement "It is not the case that p." The proposition $\lnot$p is read "not p." The truth value of the negation of p, $\lnot$p, is the opposite of the truth value of p.
	
* **Conjunction (p $\land$ q)** :
	Let p and q be propositions. The conjunction of p and q, denoted by p $\land$ q, is the proposition "p and q." The conjunction p $\land$ q is true when both p and q are true and is false otherwise.
	
* **Disjunction (p $\lor$ q)** :
	Let p and q be propositions. The disjunction of p and q, denoted by p $\lor$ q, is the proposition "p or q." The disjunction p $\lor$ q is false when both p and q are false and is true otherwise.
	
* **XOR (p $\oplus$ q)** :
	Let p and q be propositions. The exclusive or of p and q, denoted by p $\oplus$ q (or p XOR q), is the proposition that is true when exactly one of p and q is true and is false otherwise.

* **NAND & NOR (p ∣ q & p $\downarrow$ q)** :
	The proposition p NOR q is true when both p and q are false, and it is false otherwise. The propositions p NAND q and p NOR q are denoted by p ∣ q and p $\downarrow$ q, respectively. (The operators **|** and **$\downarrow$** are called **The Sheffer Stroke** and **The Peirce Arrow**.)

#### Conditional Statements
*  **Implication (p $\rightarrow$ q)** :
	  Let p and q be propositions. The conditional statement p $\rightarrow$ q is the proposition "if p, then q." The conditional statement p $\rightarrow$ q is false when p is true and q is false, and true otherwise. 
	  In the conditional statement p $\rightarrow$ q, p is called **the hypothesis (or antecedent or premise)** and q is called **the conclusion (or consequence)**.
	  
* **Biconditional (p $\leftrightarrow$ q)** :
	  Let p and q be propositions. The bi-conditional statement p $\leftrightarrow$ q is the proposition "p if and only if q". The bi-conditional statement p $\leftrightarrow$ q is true when p and q have the same truth values, and is false otherwise. 
	  Biconditional statements are also called bi-implications.

#### Truth Tables

| p   | q   | $\lnot$p | $\lnot$q | p $\land$ q | p $\lor$ q | p $\oplus$ q | p $\rightarrow$ q | p $\leftrightarrow$ q |
| --- | --- | -------- | -------- | ----------- | ---------- | ------------ | ----------------- | --------------------- |
| T   | T   | F        | F        | T           | T          | F            | T                 | T                     |
| T   | F   | F        | T        | F           | T          | T            | F                 | F                     |
| F   | T   | T        | F        | F           | T          | T            | T                 | F                     |
| F   | F   | T        | T        | F           | F          | F            | T                 | T                     |
#### Converse, Contrapositive, AND Inverse
The proposition q $\rightarrow$ p is called the converse of p $\rightarrow$ q. 
The contrapositive of p $\rightarrow$ q is the proposition $\lnot$q $\rightarrow$ $\lnot$p. 
The proposition $\lnot$p $\rightarrow$ $\lnot$q is called the inverse of p $\rightarrow$ q.

| p   | q   | $\lnot$p  | $\lnot$q  | p $\rightarrow$ q | $\lnot$q $\rightarrow$ $\lnot$p | q $\rightarrow$ p | $\lnot$p $\rightarrow$ $\lnot$q |
| --- | --- | --- | --- | ----- | ------- | ----- | ------- |
| T   | T   | F   | F   | T     | T       | T     | T       |
| T   | F   | F   | T   | F     | F       | T     | T       |
| F   | T   | T   | F   | T     | T       | F     | F       |
| F   | F   | T   | T   | T     | T       | T     | T       |
So *p $\rightarrow$ q* is equivalent to its contrapositive *$\lnot$q $\rightarrow$ $\lnot$p* and *q $\rightarrow$ p* is equivalent to its contrapositive *$\lnot$p $\rightarrow$ $\lnot$q*.


## Propositional Equivalences

* A compound proposition that is always true, no matter what the truth values of the propositional variables that occur in it, is called a **tautology**. 
* A compound proposition that is always false is called a **contradiction**. 
* A compound proposition that is neither a tautology nor a contradiction is called a **contingency**.

The compound propositions p and q are called logically equivalent if p $\leftrightarrow$ q is a tautology.
The notation p $\equiv$ q denotes that p and q are logically equivalent.

**De Morgan’s Laws** :
$\lnot$(p $\land$ q) $\equiv$ $\lnot$p $\lor$ $\lnot$q
$\lnot$(p $\lor$ q) $\equiv$ $\lnot$p $\land$ $\lnot$q

#### Logical Equivalences
| Name                | Equivalences                                                       |
| ------------------- | ------------------------------------------------------------------ |
| Identity Laws       | p $\land$ T $\equiv$ p<br>p $\lor$ F $\equiv$ p                                             |
| Domination Laws     | p $\lor$ T $\equiv$ T<br>p $\land$ F $\equiv$ F                                             |
| Idempotent Laws     | p $\lor$ p $\equiv$ p<br>p $\land$ p $\equiv$ p                                             |
| Double Negation Law | $\lnot$($\lnot$p) $\equiv$ p                                                          |
| Commutative laws    | p $\lor$ q $\equiv$ q $\lor$ p<br>p $\land$ q $\equiv$ q $\land$ p                                     |
| Associative laws    | (p $\lor$ q) $\lor$ r $\equiv$ p $\lor$ (q $\lor$ r)<br>(p $\land$ q) $\land$ r $\equiv$ p $\land$ (q $\land$ r)             |
| Distributive laws   | p $\lor$ (q $\land$ r) $\equiv$ (p $\lor$ q) $\land$ (p $\lor$ r)<br>p $\land$ (q $\lor$ r) $\equiv$ (p $\land$ q) $\lor$ (p $\land$ r) |
| De Morgan’s laws    | $\lnot$(p $\land$ q) $\equiv$ $\lnot$p $\lor$ $\lnot$q<br>$\lnot$(p $\lor$ q) $\equiv$ $\lnot$p $\land$ $\lnot$q                           |
| Absorption laws     | p $\lor$ (p $\land$ q) $\equiv$ p<br>p $\land$ (p $\lor$ q) $\equiv$ p                                 |
| Negation laws       | p $\lor$ $\lnot$p $\equiv$ T<br>p $\land$ $\lnot$p $\equiv$ F                                           |

#### Logical Equivalences Involving Biconditional Statements.
* p $\leftrightarrow$ q $\equiv$ (p $\rightarrow$ q) $\land$ (q $\rightarrow$ p)
* p $\leftrightarrow$ q $\equiv$ $\lnot$p $\leftrightarrow$ $\lnot$q
* p $\leftrightarrow$ q $\equiv$ (p $\land$ q) $\lor$ ($\lnot$p $\land$ $\lnot$q)
* $\lnot$(p $\leftrightarrow$ q) $\equiv$ p $\leftrightarrow$ $\lnot$q
* (p $\rightarrow$ q) $\equiv$ ($\lnot$p $\lor$ q) (**The Conditional-Disjunction Equivalence**)

We will sometimes use the notation :
$\bigvee$$_{j=1}^n$ p$_j$ for p$_1$ $\lor$ p$_2$ $\lor$ $\ldots$ $\lor$ p$_n$ and $\bigwedge$$_{j=1}^n$ p$_j$ for p$_1$ $\land$ p$_2$ $\land$ $\ldots$ $\land$ p$_n$. Using this notation, the extended version of De Morgan’s laws can be written concisely as : $\lnot$($\bigvee$$_{j=1}^n$ p$_j$) $\equiv$ $\bigwedge$$_{j=1}^n$ $\lnot$p$_j$.

## Predicates and Quantifiers

#### Predicates
The statement **"x is greater than 3"** has two parts. The first part, **the variable x**, is the subject of the statement. The second part—**the predicate, "is greater than 3"**—refers to a property that the subject of the statement can have. We can denote the statement "x is greater than 3" by P(x), where P denotes the predicate "is greater than 3" and x is the variable. The statement P(x) is also said to be the value of the propositional function P at x. Once a value has been assigned to the variable x, the statement P(x) becomes a proposition and has a truth value.

In general, a statement involving the n variables x$_1$, x$_2$, $\ldots$, x$_n$ can be denoted by
P(x$_1$, x$_2$, $\ldots$, x$_n$). A statement of the form P(x$_1$, x$_2$, $\ldots$, x$_n$) is the value of the propositional function P at the n-tuple (x$_1$, x$_2$, $\ldots$, x$_n$), and P is also called an **n-place predicate** or an **n-ary predicate**.

###### Preconditions AND Postconditions
The statements that describe valid input are known as **preconditions** and the conditions that the output should satisfy when the program has run are known as **postconditions**.

#### Quantifiers
###### The Universal Quantification
The universal quantification of P(x) is the statement "P(x) for all values of x in the domain."
The notation **$\forall$xP(x)** denotes the universal quantification of P(x). **Here $\forall$ is called the universal quantifier**. We read **$\forall$xP(x) as "for all xP(x)"**. An element for which P(x) is false is called a **counterexample** to $\forall$xP(x).

###### The Existential Quantification
The existential quantification of P(x) is the proposition :
"There exists an element x in the domain such that P(x)." We use the notation **$\exists$xP(x)** for the existential quantification of P(x). **Here $\exists$ is called the existential quantifier.**

###### The Uniqueness Quantifier
The uniqueness quantifier is denoted by The notation **$\exists!$xP(x)** stating **"There exists a unique x such that P(x) is true"**.

#### Quantifiers over finite domain
When the domain of a quantifier is finite, that is, when all its elements can be listed, quantified statements can be expressed using propositional logic. 
In particular, when the elements of the domain are x$_1$, x$_2$, $\ldots$, x$_n$, the universal quantification $\forall$xP(x) is the same as the conjunction P(x$_1$) $\land$ P(x$_2$) $\land$ $\ldots$ $\land$ P(x$_n$), because this conjunction is true if and only if P(x$_1$), P(x$_2$), $\ldots$ , P(x$_n$) are all true.

#### Binding Variables
Statements involving predicates and quantifiers are logically equivalent if and only if they have the same truth value no matter which predicates are substituted into these statements
and which domain of discourse is used for the variables in these propositional functions.
We use the notation S $\equiv$ T to indicate that two statements S and T involving predicates and
quantifiers are logically equivalent.

* **$\forall$x(P(x) $\land$ Q(x)) $\equiv$ $\forall$xP(x) $\land$ $\forall$xQ(x).**
* **$\exists$x(P(x) $\lor$ Q(x))** $\equiv$ **$\exists$xP(x) $\lor$ $\exists$xQ(x)**
* **$\lnot$$\forall$xP(x) $\equiv$ $\exists$x $\lnot$P(x)**
* **$\lnot$$\exists$xQ(x) $\equiv$ $\forall$x $\lnot$Q(x)**

A statement is in **Prenex Normal Form (PNF)** if and only if it is of the form :
Q$_1$x$_1$Q$_2$x$_2$$\ldots$ P(x$_1$, x$_2$, $\ldots$, x$_k$), where each Q$_i$, i $=$ 1, 2, $\ldots$ , k, is either the existential quantifier or the universal quantifier, and P(x$_1$, x$_2$, $\ldots$, x$_k$) is a predicate involving no quantifiers. 
For example, $\exists$x$\forall$y(P(x, y) $\land$ Q(y)) is in prenex normal form, whereas $\exists$xP(x) $\lor$ $\forall$xQ(x) is not (because the quantifiers do not all occur first). 
Every statement formed from propositional variables, predicates, T, and F using logical connectives and quantifiers is equivalent to a statement in prenex normal form.

## Rules of Inference

Everything within the scope of a quantifier can be thought of as a propositional function.
For example, **$\forall$x$\exists$y(x + y $=$ 0) is the same thing as $\forall$xQ(x), where Q(x) is $\exists$yP(x, y), where P(x, y) is x + y $=$ 0**.

By an **argument**, we mean a sequence of statements that end with a conclusion. 
By valid, we mean that the **conclusion**, or final statement of the argument, must follow from the truth of the preceding statements, or **premises**, of the argument.

#### Valid Arguments in Propositional Logic
An argument in propositional logic is a sequence of propositions. 
All but the final proposition in the argument are called *premises* and the final proposition is called the *conclusion*. An argument is valid if the truth of all its premises implies that the conclusion is true. 
An *argument form* in propositional logic is a sequence of compound propositions involving propositional variables. An argument form is *valid* if no matter which particular propositions are substituted for the propositional variables in its premises, the conclusion is true if the premises are all true.

For large number of propositional variables, we do not have to resort to truth tables. Instead, we can first establish the validity of some relatively simple argument forms, called **rules of inference**. These rules of inference can be used as building blocks to construct more complicated valid argument forms.
*We will now introduce the most important rules of inference in propositional logic*.
The tautology **(p $\land$ (p $\rightarrow$ q)) $\rightarrow$ q** is the basis of the rule of inference called ***Modus ponens***,
or the **law of detachment**. (***Modus ponens*** is Latin for *mode that affirms*.) 

#### Rules of Inference

| Name                   | Tautology                                                                           | Rule of Inference                                                            |
| ---------------------- | ----------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| Modus Ponens           | (p $\land$ (p $\rightarrow$ q)) $\rightarrow$ q                                     | p<br>p $\rightarrow$ q<br>- - - - - -<br>$\therefore$ q                                 |
| Modus Tollens          | ($\lnot$q $\land$ (p $\rightarrow$ q)) $\rightarrow$ $\lnot$p                       | $\lnot$q<br>p $\rightarrow$ q<br>- - - - - -<br>$\therefore$ $\lnot$p                   |
| Hypothetical Syllogism | ((p $\rightarrow$ q) $\land$ (q $\rightarrow$ r)) $\rightarrow$ (p $\rightarrow$ r) | p $\rightarrow$ q<br>q $\rightarrow$ r<br>- - - - - -<br>$\therefore$ p $\rightarrow$ r |
| Disjunctive Syllogism  | ((p $\lor$ q) $\land$ $\lnot$p) $\rightarrow$ q                                     | p $\lor$ q<br>$\lnot$p<br>- - - - - -<br>$\therefore$ q                                 |
| Addition               | p $\rightarrow$ (p $\lor$ q)                                                        | p<br>- - - - - -<br>$\therefore$ p $\lor$ q                                             |
| Simplification         | (p $\land$ q) $\rightarrow$ p                                                       | p $\land$ q<br>- - - - - -<br>$\therefore$ p                                            |
| Conjunction            | ((p) $\land$ (q)) $\rightarrow$ (p $\land$ q)                                       | p<br>q<br>- - - - - -<br>$\therefore$ p $\land$ q                                       |
| Resolution             | ((p $\lor$ q) $\land$ ($\lnot$p $\lor$ r)) $\rightarrow$ (q $\lor$ r)               | p $\lor$ q<br>$\lnot$p $\lor$ r<br>- - - - - -<br>$\therefore$ q $\lor$ r               |
#### Resolution
Computer programs have been developed to automate the task of reasoning and proving theorems. Many of these programs make use of a rule of inference known as resolution. This rule of inference is based on the tautology **((p $\lor$ q) $\land$ ($\lnot$p $\lor$ r)) $\rightarrow$ (q $\lor$ r)**.

#### Fallacies

The proposition **((p $\rightarrow$ q) $\land$ q) $\rightarrow$ p** is not a tautology, because it is false when p is false and
q is true. However, there are many incorrect arguments that treat this as a tautology. 
In other words, they treat the argument with premises p $\rightarrow$ q and q and conclusion p as a valid argument form, which it is not. This type of incorrect reasoning is called **the fallacy of affirming the conclusion**.

The proposition **((p $\rightarrow$ q) $\land$ $\lnot$p) $\rightarrow$ $\lnot$q** is not a tautology, because it is false when p is false and q is true. Many incorrect arguments use this incorrectly as a rule of inference. 
This type of incorrect reasoning is called **the fallacy of denying the hypothesis**.

#### Rules of Inference for Quantified Statements
**Universal instantiation** is the rule of inference used to conclude that P(c) is true, where c is a particular member of the domain, given the premise $\forall$xP(x). 
Universal instantiation is used when we conclude from the statement "All women are wise" that "Lisa is wise," where Lisa is a member of the domain of all women.

**Universal generalization** is the rule of inference that states that $\forall$xP(x) is true, given the
premise that P(c) is true for all elements c in the domain. Universal generalization is used when we show that $\forall$xP(x) is true by taking an arbitrary element c from the domain and showing that P(c) is true. The element c that we select must be an arbitrary, and not a specific, element of the domain. That is, when we assert from $\forall$xP(x) the existence of an element c in the domain, we have no control over c and cannot make any other assumptions about c other than it comes from the domain. 
Universal generalization is used implicitly in many proofs in mathematics and is seldom mentioned explicitly. However, the error of adding unwarranted assumptions about the arbitrary element c when universal generalization is used is all too common in incorrect reasoning.

**Existential instantiation** is the rule that allows us to conclude that there is an element c in
the domain for which P(c) is true if we know that $\exists$xP(x) is true. We cannot select an  arbitrary value of c here, but rather it must be a c for which P(c) is true. Usually we have no knowledge of what c is, only that it exists. Because it exists, we may give it a name (c) and continue our argument.

**Existential generalization** is the rule of inference that is used to conclude that $\exists$xP(x) is true when a particular element c with P(c) true is known. That is, if we know one element c in the domain for which P(c) is true, then we know that $\exists$xP(x) is true.

| Name                       | Rule Of Inference                                                                                                                                                |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Universal instantiation    | $\forall$xP(x)<br>- - - - - - - - - - - - - - - - - - -<br>$\therefore$ P(c)                                                                                                        |
| Universal generalization   | P(c) for an arbitrary c<br>- - - - - - - - - - - - - - - - - - -<br>$\therefore$ $\forall$xP(x)                                                                                     |
| Existential instantiation  | $\exists$xP(x)<br>- - - - - - - - - - - - - - - - - - -<br>$\therefore$ P(c) for some element c                                                                                     |
| Existential generalization | P(c) for some element c<br>- - - - - - - - - - - - - - - - - - -<br>$\therefore$ $\exists$xP(x)                                                                                     |
| Universal Modus Ponens     | $\forall$x(P(x) $\rightarrow$ Q(x))<br>P(a), where a is a particular element in the domain<br>- - - - - - - - - - - - - - - - - - -- - - - - - - - - - - - - - - - - - -<br>$\therefore$ Q(a)   |
| Universal Modus Tollens    | $\forall$x(P(x) $\rightarrow$ Q(x))<br>$\lnot$Q(a), where a is a particular element in the domain<br>- - - - - - - - - - - - - - - - - - -- - - - - - - - - - - - - - - - - - -<br>$\therefore$ $\lnot$P(a) |

## Introduction to Proofs
Formally, a **theorem** is a statement that can be shown to be true. 
In mathematical writing, the term theorem is usually reserved for a statement that is considered at least somewhat important.
Less important theorems sometimes are called **propositions**. (Theorems can also be referred to as facts or results.) A theorem may be the universal quantification of a conditional statement with one or more premises and a conclusion.
A **proof** is a valid argument that establishes the truth of a theorem.
The statements used in a proof can include **axioms (or postulates)**, which are statements we assume to be true. Axioms may be stated using primitive terms that do not require definition, but all other terms used in theorems and their proofs must be defined. 
Rules of inference, together with definitions of terms, are used to draw conclusions from other assertions, tying together the steps of a proof. In practice, the final step of a proof is usually just the conclusion of the theorem.

A less important theorem that is helpful in the proof of other results is called a **lemma
(plural lemmas)**. Complicated proofs are usually easier to understand when they are
proved using a series of lemmas, where each lemma is proved individually. 
A **corollary** is a theorem that can be established directly from a theorem that has been proved. A **conjecture** is a statement that is being proposed to be a true statement, usually on the basis of some partial evidence, a heuristic argument, or the intuition of an expert. When a proof of a conjecture is found, the conjecture becomes a theorem. Many times conjectures are shown to be false, so they are not theorems.

A **direct proof** of a conditional statement p $\rightarrow$ q is constructed when the first step is the assumption that p is true; subsequent steps are constructed using rules of inference, with the final step showing that q must also be true. A direct proof shows that a conditional statement p $\rightarrow$ q is true by showing that if p is true, then q must also be true, so that the combination p true and q false never occurs. 
In a direct proof, we assume that p is true and use axioms, definitions, and previously proven theorems, together with rules of inference, to show that q must also be true.

We need other methods of proving theorems of the form $\forall$x(P(x) $\rightarrow$ Q(x)). 
Proofs of theorems of this type that are not direct proofs, that is, that do not start with the premises and end with the conclusion, are called **indirect proofs**.
An extremely useful type of indirect proof is known as proof by **contraposition**. 
Proofs by contraposition make use of the fact that the conditional statement p $\rightarrow$ q is equivalent to its contrapositive, $\lnot$q $\rightarrow$ $\lnot$p. This means that the conditional statement p $\rightarrow$ q can be proved by showing that its contrapositive, $\lnot$q $\rightarrow$ $\lnot$p, is true. 
In a proof by contraposition of p $\rightarrow$ q, we take $\lnot$q as premise, and using axioms, definitions, and previously proven theorems, together with rules of inference, we show that $\lnot$p must follow.

Suppose we want to prove that a statement p is true. Furthermore, suppose that we can find a contradiction q such that $\lnot$p $\rightarrow$ q is true. Because q is false, but $\lnot$p $\rightarrow$ q is true, we can conclude that $\lnot$p is false, which means that p is true.
Because the statement r $\land$ $\lnot$r is a contradiction whenever r is a proposition, we can prove that p is true if we can show that $\lnot$p $\rightarrow$ (r $\land$ $\lnot$r) is true for some proposition r. 
Proofs of this type are called proofs by **contradiction**. Because a proof by contradiction does not prove a result directly, it is another type of **indirect proof**.


## Proof Methods and Strategy
#### Exhaustive Proof and Proof by Cases
To prove a conditional statement of the form **(p$_1$ $\lor$ p$_2$ $\lor$ $\ldots$ $\lor$ p$_n$) $\rightarrow$ q** 
the tautology **\[(p$_1$ $\lor$ p$_2$ $\lor$ $\ldots$ $\lor$ p$_n$) $\rightarrow$ q\] $\leftrightarrow$ \[(p$_1$ $\rightarrow$ q) $\land$ (p$_2$ $\rightarrow$ q) $\land$ $\ldots$ $\land$ (p$_n$ $\rightarrow$ q)\]** can be used as a rule of inference. This shows that the original conditional statement with a hypothesis made up of a disjunction of the propositions p$_1$ $\lor$ p$_2$ $\lor$ $\ldots$ $\lor$ p$_n$ can be proved by proving each of the n conditional statements p$_i$ $\rightarrow$ q, i $=$ 1, 2, $\ldots$ , n, individually. Such an argument is called a **proof by cases**. Sometimes to prove that a conditional statement p $\rightarrow$ q is true, it is convenient to use a disjunction p$_1$ $\lor$ p$_2$ $\lor$ $\ldots$ $\lor$ p$_n$ instead of p as the hypothesis of the conditional statement, where p and p$_1$ $\lor$ p$_2$ $\lor$ $\ldots$ $\lor$ p$_n$ are equivalent.

In general, when the phrase "**without loss of generality**" is used in a proof (often abbreviated as WLOG), we assert that by proving one case of a theorem, no additional argument is required to prove other specified cases. That is, other cases follow by making straightforward changes to the argument, or by filling in some straightforward initial step. Proofs by cases can often be made much more efficient when the notion of without loss of generality is employed.
Incorrect use of this principle, however, can lead to unfortunate errors. Sometimes assumptions are made that lead to a loss in generality. Such assumptions can be made that do not take into account that one case may be substantially different from others. This can lead to an incomplete, and possibly unsalvageable, proof. In fact, many incorrect proofs of famous theorems turned out to rely on arguments that used the idea of "without loss of generality" to establish cases that could not be quickly proved from simpler cases.

#### Existence Proofs
Many theorems are assertions that objects of a particular type exist. A theorem of this type is a proposition of the form $\exists$xP(x), where P is a predicate. A proof of a proposition of the form $\exists$xP(x) is called an **existence proof**. There are several ways to prove a theorem of this type. Sometimes an existence proof of $\exists$xP(x) can be given by finding an element a, called a witness, such that P(a) is true. This type of existence proof is called **constructive**. It is also possible to give an existence proof that is **nonconstructive**; that is, we do not find an element a such that P(a) is true, but rather prove that $\exists$xP(x) is true in some other way. 
One common method of giving a nonconstructive existence proof is to use proof by contradiction and show that the negation of the existential quantification implies a contradiction.

Some theorems assert the existence of a unique element with a particular property. In other
words, these theorems assert that there is exactly one element with this property. To prove a statement of this type we need to show that an element with this property exists and that no other element has this property. The two parts of a **uniqueness** proof are:
*Existence*: We show that an element x with the desired property exists.
*Uniqueness*: We show that if x and y both have the desired property, then x $=$ y.

Showing that there is a unique element x such that P(x) is the same as proving the statement **$\exists$x(P(x) $\land$ $\forall$y(y $\ne$ x $\rightarrow$ $\lnot$P(y)))**.
# Topic 4: Logic-Based Representation: Propositional Logic

## Overview
This topic covers propositional logic as a method for knowledge representation, including syntax, semantics, logical connectives, truth tables, and its limitations for KBS.

---

## Learning Outcome Questions

### 1. Remember: Basic Symbols and Connectives
**Question:** Define the basic symbols and connectives used in Propositional Logic.

**Your Response:**

Propositional Logic uses atomic propositions (simple true/false statements like "P", "Q") and logical connectives: (1) Negation (¬) meaning "NOT", (2) Conjunction (∧) meaning "AND", (3) Disjunction (∨) meaning "OR", (4) Implication (→) meaning "IF-THEN", and (5) Biconditional (↔) meaning "IF AND ONLY IF". Compound formulas combine these with proper syntax and operator precedence (negation highest, then conjunction, disjunction, implication, biconditional lowest).

---

### 2. Understand: Truth Values
**Question:** Explain how truth values are assigned to propositions and compound statements.

**Your Response:**

Each atomic proposition receives a truth value: true (T) or false (F). For compound propositions, truth values are assigned using truth tables based on these rules: Negation (¬P) flips the truth value. Conjunction (P ∧ Q) is true only when both are true. Disjunction (P ∨ Q) is true when at least one is true. Implication (P → Q) is false only when P is true and Q is false. Biconditional (P ↔ Q) is true when both have same truth value. The truth value of any formula depends compositionally on the truth values of its atomic components and the connectives used.

---

### 3. Apply: Construct Truth Tables
**Question:** Construct truth tables for given propositional logic expressions.

**Your Response:**

For formula (P ∧ Q) → ¬R:

| P | Q | R | P∧Q | ¬R | (P∧Q)→¬R |
|---|---|---|-----|----|----|
| T | T | T | T | F | F |
| T | T | F | T | T | T |
| T | F | T | F | F | T |
| T | F | F | F | T | T |
| F | T | T | F | F | T |
| F | T | F | F | T | T |
| F | F | T | F | F | T |
| F | F | F | F | T | T |

Process: Create row for each 2^n combination of n propositions. Evaluate subexpressions left-to-right, innermost parentheses first. Truth value of implication depends on antecedent and consequent truth values according to the implication truth table rule.

---

### 4. Analyze: Break Down Statements
**Question:** Break down complex statements into propositional logic formulas.

**Your Response:**

Natural Language: "If the alarm goes off AND the building is not empty, THEN either call security OR evacuate"
- P: "Alarm goes off"
- Q: "Building is empty"
- R: "Call security"
- S: "Evacuate"

Formula: (P ∧ ¬Q) → (R ∨ S)

Natural Language: "You get a refund if and only if you have a receipt and the item is unused"
- P: "Get refund"
- Q: "Have receipt"
- R: "Item is unused"

Formula: P ↔ (Q ∧ R)

Key translation rules: "and/but" = ∧, "or" = ∨, "not" = ¬, "if-then" = →, "if and only if" = ↔. Use parentheses to disambiguate compound statements.

---

### 5. Evaluate: Expressiveness and Limitations
**Question:** Assess the expressiveness and limitations of Propositional Logic for knowledge representation.

**Your Response:**

**Strengths**: Propositional logic is simple, decidable, computationally tractable for reasonable problem sizes, has clear semantics, and supports sound/complete inference rules. It's suitable for Boolean reasoning and simple decision problems.

**Limitations**: Cannot express objects/properties ("Socrates is mortal" requires separate propositions for each individual), cannot express relationships between objects, cannot use quantifiers (universal "all" or existential "some"), causes knowledge base explosion with multiple instances of similar facts, cannot represent variables or patterns, and has limited reasoning power without explicit rules. Example: Knowing "All humans are mortal", "All mortals die", and "Socrates is human" cannot derive "Socrates dies" using only propositional logic because relationships must be explicit in advance.

First-Order Logic overcomes these limitations by adding predicates, variables, and quantifiers.

---

### 6. Create: Real-World Scenarios
**Question:** Formulate simple real-world scenarios using propositional logic.

**Your Response:**

**Home Security System**:
Variables: P="Motion detected", Q="Nighttime", R="Door forced", S="Smoke detected", D="System disabled", A="Alarm triggers"
Formula: A ↔ (¬D ∧ ((P ∧ Q) ∨ R ∨ S))
Scenario: If system enabled and (motion+nighttime) OR forced door OR smoke detected, then trigger alarm

**Loan Approval**:
Variables: C="Credit ≥700", I="Income ≥$50k", B="Collateral ≥$100k", C2="Credit ≥650", K="Bankrupt", A="Approved"
Formula: A ↔ (¬K ∧ ((C ∧ I) ∨ (B ∧ C2)))
Scenario: Approve if not bankrupt AND (good-credit-and-income OR good-collateral-and-decent-credit)

**Restaurant Table Assignment**:
Variables: S="Small party", SM="Smoking", O="Outdoor available", W="Wheelchair needed", OT="Open", C="Can assign"
Formula: C ↔ (OT ∧ CL), TA ↔ (C ∧ S)
Scenario: Can assign table if open and before closing time

---

## Capstone Assignment

### Task: Solve a set of logical puzzles by representing the given information in propositional logic and using truth tables to find the solutions.

**Your Submission:**

**LOGIC PUZZLE 1: Knight and Knave**

Setup: Two islanders, each either Knight (always truth) or Knave (always lies). Islander A says "We are both Knights." Determine what each is.

Variables: A_K="A is Knight", B_K="B is Knight"

Analysis:
- If A is Knight: Statement is true, so both must be Knights ✓
- If A is Knave: Statement must be false, so both are NOT Knights, meaning both are Knaves ✓
- But if A is Knave and says "both are Knights" (false), then B must be Knight for logical consistency

**Answer: A is Knight, B is Knight** (if we assume A's statement is made)

**LOGIC PUZZLE 2: Farm Animals**

Clues:
1. C → Co (If chickens, then cows)
2. ¬(H ∧ Co) (Not both horses and cows)
3. C ∨ H (Chickens or horses)
4. H → ¬C (If horses, then not chickens)

Truth table analysis shows only two valid solutions:
- Chickens=T, Cows=T, Horses=F
- Chickens=F, Cows=F, Horses=T

**Answer: Either (has chickens and cows) OR (has horses only)**

**LOGIC PUZZLE 3: Crime Investigation**

Clues:
1. A ∨ B ∨ C (At least one guilty)
2. ¬(A ∧ B) (Not both A and B)
3. B → ¬C (If B guilty, C innocent)
4. A ∨ C (A or C guilty)

Valid solutions:
- Alice and Carol guilty, Bob innocent
- Alice guilty, others innocent
- Carol guilty, others innocent

**Answer: Multiple scenarios; additional evidence needed**

---

## References (APA 7)

Ahenda, J. (2026). APT3020VA: Knowledge-based systems course outline. United States International University–Africa.

Hurley, P. J. (2015). *A concise introduction to logic* (12th ed.). Cengage Learning.

Wikipedia contributors. (2026). Propositional calculus. In *Wikipedia, the free encyclopedia.* Retrieved March 18, 2026, from https://en.wikipedia.org/wiki/Propositional_calculus

---

**Status:** Complete
**Date Completed:** March 18, 2026

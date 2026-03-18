# Topic 5: Logic-Based Representation: First-Order Logic

## Overview
This topic extends propositional logic to first-order logic, covering objects, predicates, variables, quantifiers, and representing facts and rules in a more expressive knowledge representation scheme.

---

## Learning Outcome Questions

### 1. Remember: Key Components
**Question:** Identify the key components of First-Order Logic.

**Your Response:**

First-Order Logic (FOL), also called Predicate Logic or First-Order Predicate Calculus, extends Propositional Logic by introducing additional components that enable more expressive knowledge representation. The key components of FOL are:

**1. Constants**: Fixed, named objects or entities in the domain (e.g., "John", "Alice", "Kenya", 2025). Constants represent specific individuals or things.

**2. Variables**: Symbols representing arbitrary objects from a domain (e.g., x, y, z, P, Q). Variables can be replaced with constants through instantiation, allowing general statements about multiple objects.

**3. Predicates (Relations)**: Symbols that express properties or relationships between objects. Predicates have arity (number of arguments):
   - Unary predicates: `Doctor(x)` - "x is a doctor"
   - Binary predicates: `Parent(x, y)` - "x is a parent of y"
   - N-ary predicates: `Located(city, country, continent)` - "city is in country in continent"

**4. Quantifiers**: Operators that specify the scope of variables:
   - Universal quantifier (∀): "for all" - `∀x Doctor(x) → Competent(x)` means "all doctors are competent"
   - Existential quantifier (∃): "there exists" - `∃x Doctor(x) ∧ Specialist(x)` means "there exists at least one doctor who is a specialist"

**5. Functions**: Mappings that produce values from arguments (e.g., `Father(John)` returns John's father, `Plus(2, 3)` returns 5). Functions allow complex term construction.

**6. Terms**: Expressions representing objects. Terms can be:
   - Constants: `John`, `2025`
   - Variables: `x`, `y`
   - Functional terms: `Father(John)`, `Plus(x, 2)`

**7. Formulas (Well-Formed Expressions)**:
   - Atomic formulas: `Doctor(John)`, `Parent(Mary, John)` - single predicate with arguments
   - Compound formulas: Built using logical connectives (¬, ∧, ∨, →, ↔) and quantifiers

**8. Logical Connectives**: The same as in Propositional Logic:
   - Negation (¬)
   - Conjunction (∧)
   - Disjunction (∨)
   - Implication (→)
   - Biconditional (↔)

---

### 2. Understand: Quantifiers
**Question:** Explain the meaning and usage of quantifiers in FOL.

**Your Response:**

Quantifiers are fundamental to FOL as they enable expressing generalizations about domains of objects. They specify how many objects satisfy a particular condition and are essential for representing real-world knowledge effectively.

**Universal Quantifier (∀ - "for all")**

The universal quantifier asserts that a statement applies to ALL objects in a domain.

Syntax: `∀x P(x)` - "for all x, P(x) is true"

Meaning: A statement is true for every possible instantiation of the variable.

Examples:
- `∀x Doctor(x) → Ethical(x)` - "All doctors are ethical"
- `∀x ∀y Parent(x, y) → Older(x, y)` - "For all x and y, if x is parent of y, then x is older than y"
- `∀x Student(x) ∧ AttendClass(x) → Learn(x)` - "All students who attend class learn"

**Existential Quantifier (∃ - "there exists")**

The existential quantifier asserts that a statement applies to AT LEAST ONE object in a domain.

Syntax: `∃x P(x)` - "there exists x such that P(x) is true"

Meaning: A statement is true for at least one instantiation of the variable.

Examples:
- `∃x Doctor(x) ∧ Specialist(x)` - "There exists at least one doctor who is a specialist"
- `∃x Student(x) ∧ Score(x, 100)` - "At least one student scored 100"
- `∃y Farmer(y) ∧ Successful(y) ∧ Location(y, Kenya)` - "There exists a successful farmer in Kenya"

**Scope and Binding**

The scope of a quantifier determines which variables it governs:
- In `∀x P(x) ∨ Q(x)`, the universal quantifier typically applies to the entire expression (scope includes both P(x) and Q(x))
- In `∀x P(x) ∨ Q(y)`, the quantifier only binds x in P(x); y is unbound (a free variable)

Bound variables: Variables within the scope of a quantifier - their values are determined by the quantifier
Free variables: Variables not bound by any quantifier - they remain unspecified

**Combining Quantifiers**

Multiple quantifiers can be combined, and order matters:
- `∀x ∃y Parent(x, y)` - "Everyone has a parent" (each person has at least one parent)
- `∃x ∀y Parent(x, y)` - "Someone is the parent of everyone" (one person parents all)

**Negation with Quantifiers**

De Morgan's Laws apply to quantifiers:
- `¬∀x P(x)` ≡ `∃x ¬P(x)` - "It is not the case that all x have property P" means "there exists x without property P"
- `¬∃x P(x)` ≡ `∀x ¬P(x)` - "There does not exist x with property P" means "no x has property P"

---

### 3. Apply: Translate Natural Language
**Question:** Translate simple natural language sentences into FOL.

**Your Response:**

Translating natural language to FOL requires careful analysis of grammatical structure to identify objects, properties, relationships, and quantification. Below are detailed examples demonstrating the translation process:

**Example 1: Simple Properties**

Natural Language: "John is a doctor"
FOL: `Doctor(John)`

Natural Language: "All doctors are competent"
FOL: `∀x Doctor(x) → Competent(x)`

**Example 2: Binary Relations**

Natural Language: "Mary is the parent of John"
FOL: `Parent(Mary, John)`

Natural Language: "Someone is taller than everyone else"
FOL: `∃x ∀y Taller(x, y)`

**Example 3: Multiple Quantifiers and Conjunctions**

Natural Language: "All students who study hard will pass the exam"
FOL: `∀x (Student(x) ∧ StudiesHard(x)) → PassExam(x)`

Natural Language: "Every farmer in Kenya uses modern techniques"
FOL: `∀x (Farmer(x) ∧ Location(x, Kenya)) → UsesTechniques(x, modern)`

**Example 4: Existential and Negation**

Natural Language: "There exists a teacher who is not strict"
FOL: `∃x (Teacher(x) ∧ ¬Strict(x))`

Natural Language: "No student failed the course"
FOL: `¬∃x (Student(x) ∧ Failed(x, Course))` or equivalently `∀x (Student(x) → ¬Failed(x, Course))`

**Example 5: Complex Nested Structures**

Natural Language: "If anyone studies, they will understand the material"
FOL: `∀x (Studies(x) → Understands(x, Material))`

Natural Language: "All parents who care about education encourage their children to read"
FOL: `∀x (Parent(x) ∧ CareAbout(x, Education) → ∀y (ChildOf(y, x) → Encourage(x, y, Read)))`

**Example 6: Functional Terms**

Natural Language: "The father of John is older than John"
FOL: `Older(Father(John), John)`

Natural Language: "Everyone has a mother, and every mother is a woman"
FOL: `∀x ∃y Mother(y, x) ∧ ∀y (∃x Mother(y, x)) → Woman(y)`

---

### 4. Analyze: Compare Logics
**Question:** Compare and contrast Propositional Logic and First-Order Logic.

**Your Response:**

While both Propositional Logic (PL) and First-Order Logic (FOL) are fundamental logical systems for knowledge representation, they differ significantly in expressiveness, complexity, and applicability. Below is a detailed comparison:

| **Aspect** | **Propositional Logic** | **First-Order Logic** |
|---|---|---|
| **Basic Units** | Propositions (atomic sentences) | Predicates, objects, variables, quantifiers |
| **Expressiveness** | Limited; cannot express relationships between objects or general properties | Highly expressive; can represent objects, relationships, and generalizations |
| **Quantification** | Not supported | Universal (∀) and existential (∃) quantifiers enable general statements |
| **Example Statement** | "Rain → Wet" (if it rains, ground is wet) | "∀x (Rain(x) → Wet(x))" (for all objects, if it rains on x, then x is wet) |
| **Complexity (Decidability)** | Decidable - truth value of any formula can be algorithmically determined in finite time | Undecidable - no algorithm exists to determine truth of all FOL formulas |
| **Complexity (Computational)** | CoNP-complete (easier to compute) | Semi-decidable; sound inference exists but completeness not guaranteed for all cases |
| **Inference Rules** | Modus ponens, resolution | Forward chaining, backward chaining, resolution with unification |
| **Domain Representation** | Each atomic proposition must be separately stated | General rules apply to entire domain through quantification |
| **Scalability** | Poorly scalable; knowledge base grows linearly with number of facts | More scalable; fewer rules needed to represent larger domains |
| **Real-World Applications** | Simple decision systems, basic rule-based logic | Expert systems, medical diagnosis, natural language processing, database queries |

**Key Differences Explained:**

**1. Expressiveness Gap**

PL Example: "John is a doctor", "Mary is a doctor", "Alice is a doctor" - requires three separate propositions

FOL Equivalent: `∀x Doctor(x)` - single statement expressing the same information for all objects

This demonstrates FOL's superior ability to capture generalizations and patterns.

**2. Quantification Capability**

PL cannot express: "All X have property Y" or "There exists at least one X with property Y"

FOL can express these through quantifiers, making it suitable for representing domain knowledge with multiple entities.

**3. Decidability and Complexity**

PL is decidable - there exists a complete decision procedure (e.g., truth tables) to determine if a statement is valid.

FOL is semi-decidable - we can prove true statements but cannot always prove false ones. Church's Theorem (1936) proved that first-order logic is undecidable.

**4. Inference Complexity**

PL inference: Relatively simple, can use resolution with complete algorithms

FOL inference: Requires unification and more sophisticated algorithms; can be computationally expensive but more powerful

**5. Knowledge Base Size**

PL: To represent "All doctors are competent," requires stating this for each doctor individually if the domain has 1000 doctors

FOL: Single rule `∀x Doctor(x) → Competent(x)` applies to all doctors regardless of domain size

**Limitations of Each Approach:**

Propositional Logic Limitations:
- Cannot represent properties of objects
- Cannot express relationships between multiple entities
- Not suitable for domains with multiple similar entities
- Requires explosive growth of statements with domain size

First-Order Logic Limitations:
- Undecidable - cannot create a complete proof procedure
- Computationally more expensive than PL
- Still cannot express second-order properties (properties of properties)
- May be overly complex for simple domains

---

### 5. Evaluate: Expressiveness
**Question:** Discuss the increased expressiveness of FOL for knowledge representation.

**Your Response:**

First-Order Logic's expressiveness far exceeds Propositional Logic, enabling representation of complex real-world knowledge. This section evaluates the practical and theoretical implications of FOL's expressive power for knowledge-based systems.

**Strengths of FOL Expressiveness:**

**1. Object-Level Reasoning**

FOL enables reasoning about objects and their properties, not just abstract propositions:
- Can represent: "John is a doctor" and derive consequences specific to John
- Can generalize: "All doctors must complete continuing education"
- Can instantiate rules: Derive that "John must complete continuing education"

This object-level reasoning is essential for expert systems in domains like medical diagnosis, legal reasoning, and engineering.

**2. Relationship Representation**

FOL captures complex relationships between multiple entities:
- Binary: `Parent(Mary, John)` - Mary is John's parent
- Ternary: `Teaches(Professor, Subject, Student)` - A professor teaches a subject to a student
- N-ary: Complex domain relationships requiring multiple arguments

Without FOL, representing relationships requires separate propositional statements, leading to exponential growth in knowledge base size.

**3. Universal and Existential Knowledge**

FOL naturally captures:
- General principles: `∀x Patient(x) → RequiresMedicalEvaluation(x)` - All patients require evaluation
- Specific existential claims: `∃x Symptom(x) ∧ Indicates(x, Disease)` - Some symptom indicates the disease
- Conditional expertise: `∀x (Patient(x) ∧ Age(x, >65)) → RiskCategory(x, high)` - Elderly patients are high-risk

**4. Function and Composition**

FOL includes functions enabling:
- Compositional descriptions: `Father(Mary)` returns Mary's father object
- Recursive definitions: `Ancestor(x, y) ← Parent(x, y) ∨ (Parent(x, z) ∧ Ancestor(z, y))`
- Complex term construction: `Salary(Department(Employee))` - get the salary of the department of an employee

**5. Inference Capability Enhancement**

FOL's increased expressiveness enables more sophisticated inference:
- Pattern matching across instances
- Unification: Finding variable instantiations that satisfy constraints
- Backward chaining: Goal-driven reasoning through rule implications
- Forward chaining: Data-driven reasoning applying rules to facts

**Practical Benefits for Knowledge Representation:**

**Scalability Across Domain Size:**
- PL: Adding 100 new patients to a medical system requires 100+ new propositions
- FOL: Adding 100 patients requires only fact additions; rules remain unchanged

**Knowledge Reusability:**
- FOL rules apply across the entire domain
- Single rule captures expertise applicable to unlimited instances
- Reduces knowledge engineering effort and maintenance

**Semantic Clarity:**
- FOL statements closer match natural language expressions
- Easier for domain experts to validate knowledge
- Clearer documentation of domain logic

**Limitations and Trade-offs:**

**Computational Complexity:**
- Inference in FOL is computationally expensive compared to PL
- NP-hard reasoning problems become common
- Scalability of inference engine depends on optimization strategies

**Undecidability:**
- Unlike PL, FOL cannot guarantee algorithmic proof of all valid statements
- Some queries may not terminate
- Requires intelligent search strategies (depth-first, breadth-first, heuristic-guided)

**Knowledge Engineering Burden:**
- Requires careful domain analysis to identify predicates, functions, and relationships
- Potential for ambiguous or incorrect predicate definitions
- More complex knowledge acquisition process

**Real-World Knowledge Representation Examples:**

**Medical Diagnosis System:**
```
∀x (Patient(x) ∧ HasSymptom(x, fever) ∧ HasSymptom(x, cough)) → ConsiderDiagnosis(x, influenza)
∀x (Patient(x) ∧ Age(x, <5)) → RiskGroup(x, complications)
∀x Patient(x) → RequiresMedicalHistory(x)
```

**Agricultural Knowledge System:**
```
∀x (Crop(x) ∧ Season(currentSeason) ∧ Suitable(x, currentSeason)) → Recommend(x)
∀x (Farmer(x) ∧ Location(x, region) ∧ Climate(region, tropical)) → Recommend(x, tropicalCrops)
∃y (CropDisease(y) ∧ AffectsCrop(y, maize)) → RequiresTreatment(maize, treatmentType(y))
```

**E-Commerce Recommendation:**
```
∀x (Customer(x) ∧ PurchasedCategory(x, category)) → RecommendCategory(x, category)
∀x ∀y (Customer(x) ∧ Customer(y) ∧ SimilarPreferences(x, y)) → ShareRecommendations(x, y)
```

**Conclusion on Expressiveness:**

FOL's increased expressiveness makes it indispensable for representing complex, real-world knowledge in knowledge-based systems. The ability to express objects, relationships, and generalizations through quantification dramatically improves knowledge representation efficiency, maintainability, and scalability compared to Propositional Logic. However, this power comes with increased computational complexity and the need for careful knowledge engineering. The choice between PL and FOL depends on domain complexity: simple domains may benefit from PL's simplicity, while complex domains with multiple entities and relationships require FOL's expressiveness.

---

### 6. Create: Complex Scenarios
**Question:** Represent a more complex scenario using first-order logic.

**Your Response:**

**Scenario: University Course Enrollment and Grade Management System**

This complex system involves students, courses, instructors, prerequisites, and grading logic. Below is a comprehensive FOL representation:

**Domain Objects and Predicates:**

```
Constants: course101, course201, course301, alice, bob, charlie, dr_smith, dr_johnson, 2026

Predicates:
- Student(x): x is a student
- Course(x): x is a course
- Instructor(x): x is an instructor
- Enrolled(x, y): student x is enrolled in course y
- Teaches(x, y): instructor x teaches course y
- Prerequisite(x, y): course x is a prerequisite for course y
- Completed(x, y, g): student x completed course y with grade g
- Grade(g): g is a valid grade (A, B, C, D, F)
- PassingGrade(g): g is a passing grade (A, B, C)
- GPA(x, v): student x has GPA value v
- Major(x, discipline): student x's major is discipline
- CanEnroll(x, y): student x can enroll in course y
- Competent(x, y): student x is competent to take course y
```

**Facts (Knowledge Base):**

```
% Students
Student(alice)
Student(bob)
Student(charlie)

% Courses
Course(course101)
Course(course201)
Course(course301)

% Instructors
Instructor(dr_smith)
Instructor(dr_johnson)

% Teaching assignments
Teaches(dr_smith, course101)
Teaches(dr_johnson, course201)
Teaches(dr_smith, course301)

% Prerequisites
Prerequisite(course101, course201)
Prerequisite(course201, course301)

% Past completions
Completed(alice, course101, A)
Completed(alice, course201, B)
Completed(bob, course101, C)
Completed(charlie, course101, A)
Completed(charlie, course201, A)

% Current enrollments
Enrolled(alice, course301)
Enrolled(bob, course201)
Enrolled(charlie, course301)

% Grade information
Grade(A)
Grade(B)
Grade(C)
Grade(D)
Grade(F)
PassingGrade(A)
PassingGrade(B)
PassingGrade(C)
```

**Rules (Inference Logic):**

```
% Rule 1: Can enroll in a course if all prerequisites are completed
∀x ∀y (CanEnroll(x, y) ← ¬∃z (Prerequisite(z, y) ∧ ¬(∃g Completed(x, z, g) ∧ PassingGrade(g))))

% Rule 2: A student is competent to take a course if prerequisites are satisfied
∀x ∀y (Competent(x, y) ← ∀z (Prerequisite(z, y) → ∃g (Completed(x, z, g) ∧ PassingGrade(g))))

% Rule 3: Can enroll only if competent
∀x ∀y (Enrolled(x, y) ∧ ¬Competent(x, y)) → ViolatesPolicy(x, y)

% Rule 4: Students who pass all courses have good standing
∀x (GoodStanding(x) ← ∀y (Completed(x, y, g) → PassingGrade(g)))

% Rule 5: Instructors can only teach one course per semester (not explicitly stated but inferable)
∀x ∀y ∀z (Teaches(x, y) ∧ Teaches(x, z) ∧ y ≠ z) → CanTeach(x)

% Rule 6: Two students have similar academic paths if they completed the same prerequisites
∀x ∀y ∀z (SimilarPath(x, y) ← (Completed(x, z, g1) ∧ Completed(y, z, g2) ∧ PassingGrade(g1) ∧ PassingGrade(g2)))

% Rule 7: A course is advanced if it has prerequisites
∀x (Advanced(x) ← ∃y Prerequisite(y, x))
```

**Query Examples and Inference:**

```
Query 1: Which students are eligible to enroll in course301?
Answer: Competent(alice, course301) ∧ Competent(charlie, course301)
Reasoning: Both alice and charlie completed course201 with passing grades (A and A respectively)

Query 2: Is bob competent to take course201?
Answer: Yes
Reasoning: bob completed course101 with grade C (passing grade)

Query 3: Which students are not competent for their current enrollments?
Answer: None violate the policy based on current facts
Reasoning: All enrolled students meet prerequisite requirements

Query 4: List all students who have completed prerequisites for advanced courses
Answer: alice, charlie
Reasoning: Advanced(course201) and Advanced(course301) have prerequisites
          Both alice and charlie completed course101

Query 5: Can a student take course201 if they failed course101?
Answer: ¬∃x (Enrolled(x, course201) ∧ ∃g (Completed(x, course101, g) ∧ ¬PassingGrade(g)))
Meaning: No student can be enrolled in course201 if they failed the prerequisite course101

Query 6: What is the relationship between students who took the same prerequisites?
Answer: SimilarPath(alice, charlie) (both completed course101 with passing grades)
        SimilarPath(bob, alice)
        SimilarPath(bob, charlie)
Reasoning: All three completed course101, establishing similarity
```

**Complex Logical Deduction Scenario:**

```
Scenario: Determining if Alice can graduate

Required knowledge:
∀x (CanGraduate(x) ← Major(x, discipline) ∧
                      ∀y (RequiredForMajor(y, discipline) → ∃g (Completed(x, y, g) ∧ PassingGrade(g))))

Assume: Major(alice, ComputerScience)
        RequiredForMajor(course101, ComputerScience)
        RequiredForMajor(course201, ComputerScience)
        RequiredForMajor(course301, ComputerScience)

Facts showing:
        Completed(alice, course101, A) - PassingGrade(A) ✓
        Completed(alice, course201, B) - PassingGrade(B) ✓
        Enrolled(alice, course301) - assuming future passing grade

Conclusion: If alice passes course301, then CanGraduate(alice) = true
```

**Second-Order Properties and Constraints:**

```
% Constraint: No student can be enrolled in more than 4 courses simultaneously
∀x (Student(x) → ¬∃y1 ∃y2 ∃y3 ∃y4 ∃y5
    (Enrolled(x, y1) ∧ Enrolled(x, y2) ∧ Enrolled(x, y3) ∧ Enrolled(x, y4) ∧ Enrolled(x, y5) ∧
     y1 ≠ y2 ≠ y3 ≠ y4 ≠ y5))

% Constraint: Every course must have at least one instructor
∀x (Course(x) → ∃y (Instructor(y) ∧ Teaches(y, x)))

% Constraint: A student cannot enroll in a course they already completed
∀x ∀y (¬(∃g Completed(x, y, g) ∧ Enrolled(x, y)))
```

**Summary:**

This comprehensive university system demonstrates FOL's ability to represent:
- Complex domain objects with multiple types (students, courses, instructors)
- Binary, ternary, and n-ary relationships (prerequisites, teaching assignments, enrollment)
- Conditional logic and dependencies (prerequisites enable enrollment)
- Quantified reasoning across multiple entities (all students who passed, any course with prerequisites)
- Constraint representation and violation detection
- Realistic inference patterns (eligibility determination, policy compliance checking)
- Scalability (can add thousands of students, courses, and relationships without changing the rule structure)

---

## Capstone Assignment

### Task: Translate a given set of natural language rules and facts about a family relationship into First-Order Logic.

**Your Submission:**

**Family Relationship System - Complete FOL Representation**

This capstone translates natural language family relationships into a complete, executable FOL system with predicates, facts, rules, and query answering mechanisms.

**Domain Specification:**

The domain consists of individuals in a family tree with relationships based on biological and marital connections. This system enables inference of derived relationships (e.g., "grandparent," "sibling," "cousin") from basic facts (e.g., "parent," "spouse").

**Step 1: Define Core Predicates**

```
% Basic relationships
Parent(x, y): x is the parent of y
Male(x): x is male
Female(x): x is female
Spouse(x, y): x is married to y

% Derived predicates (to be inferred)
Father(x, y): x is the father of y
Mother(x, y): x is the mother of y
Child(x, y): x is a child of y
Son(x, y): x is the son of y
Daughter(x, y): x is the daughter of y
Sibling(x, y): x and y share at least one parent
Brother(x, y): x is the brother of y
Sister(x, y): x is the sister of y
Grandparent(x, y): x is a grandparent of y
Grandfather(x, y): x is the grandfather of y
Grandmother(x, y): x is the grandmother of y
Grandchild(x, y): x is a grandchild of y
Aunt(x, y): x is the aunt of y
Uncle(x, y): x is the uncle of y
Niece(x, y): x is the niece of y
Nephew(x, y): x is the nephew of y
Ancestor(x, y): x is an ancestor of y
Descendant(x, y): x is a descendant of y
Cousin(x, y): x and y share at least one grandparent through sibling parents
```

**Step 2: Base Facts (Family Database)**

```
% Males
Male(john)
Male(james)
Male(michael)
Male(david)
Male(robert)

% Females
Female(mary)
Female(susan)
Female(patricia)
Female(jane)
Female(elizabeth)

% Parent-child relationships
Parent(john, james)
Parent(john, susan)
Parent(mary, james)
Parent(mary, susan)

Parent(james, michael)
Parent(james, patricia)
Parent(susan, david)
Parent(susan, robert)

Parent(michael, jane)
Parent(patricia, elizabeth)

% Spouse relationships
Spouse(john, mary)
Spouse(james, margaret)
Spouse(susan, william)
```

**Step 3: Inference Rules**

```
% Rule 1: Father relationship
∀x ∀y (Father(x, y) ← Parent(x, y) ∧ Male(x))

% Rule 2: Mother relationship
∀x ∀y (Mother(x, y) ← Parent(x, y) ∧ Female(x))

% Rule 3: Child relationship (converse of parent)
∀x ∀y (Child(x, y) ← Parent(y, x))

% Rule 4: Son relationship
∀x ∀y (Son(x, y) ← Parent(y, x) ∧ Male(x))

% Rule 5: Daughter relationship
∀x ∀y (Daughter(x, y) ← Parent(y, x) ∧ Female(x))

% Rule 6: Sibling relationship (same parent)
∀x ∀y (Sibling(x, y) ← ∃z (Parent(z, x) ∧ Parent(z, y) ∧ x ≠ y))

% Rule 7: Brother relationship
∀x ∀y (Brother(x, y) ← Sibling(x, y) ∧ Male(x))

% Rule 8: Sister relationship
∀x ∀y (Sister(x, y) ← Sibling(x, y) ∧ Female(x))

% Rule 9: Grandparent relationship
∀x ∀y (Grandparent(x, y) ← ∃z (Parent(x, z) ∧ Parent(z, y)))

% Rule 10: Grandfather relationship
∀x ∀y (Grandfather(x, y) ← Grandparent(x, y) ∧ Male(x))

% Rule 11: Grandmother relationship
∀x ∀y (Grandmother(x, y) ← Grandparent(x, y) ∧ Female(x))

% Rule 12: Grandchild relationship (converse of grandparent)
∀x ∀y (Grandchild(x, y) ← Grandparent(y, x))

% Rule 13: Aunt relationship (parent's sister)
∀x ∀y (Aunt(x, y) ← ∃z (Parent(z, y) ∧ Sister(x, z)))

% Rule 14: Uncle relationship (parent's brother)
∀x ∀y (Uncle(x, y) ← ∃z (Parent(z, y) ∧ Brother(x, z)))

% Rule 15: Niece relationship (sibling's daughter)
∀x ∀y (Niece(x, y) ← ∃z (Sibling(z, y) ∧ Parent(z, x) ∧ Female(x)))

% Rule 16: Nephew relationship (sibling's son)
∀x ∀y (Nephew(x, y) ← ∃z (Sibling(z, y) ∧ Parent(z, x) ∧ Male(x)))

% Rule 17: Ancestor relationship (transitive)
∀x ∀y (Ancestor(x, y) ← Parent(x, y))
∀x ∀y ∀z (Ancestor(x, y) ← Parent(x, z) ∧ Ancestor(z, y))

% Rule 18: Descendant relationship (converse of ancestor)
∀x ∀y (Descendant(x, y) ← Ancestor(y, x))

% Rule 19: Cousin relationship (parents are siblings)
∀x ∀y (Cousin(x, y) ← ∃z ∃w (Parent(z, x) ∧ Parent(w, y) ∧ Sibling(z, w)))
```

**Step 4: Answering Queries**

Query 1: "Is James the father of Michael?"
```
Query: Father(james, michael)
Known facts: Parent(james, michael) and Male(james)
Apply Rule 1: Father(x, y) ← Parent(x, y) ∧ Male(x)
Answer: YES, Father(james, michael) is true
```

Query 2: "Who are the siblings of James?"
```
Query: Sibling(x, james)
Known facts: Parent(john, james) and Parent(mary, james)
           Parent(john, susan) and Parent(mary, susan)
Apply Rule 6: Sibling(x, y) ← ∃z (Parent(z, x) ∧ Parent(z, y))
Answer: Sibling(susan, james) - Susan is James's sibling
```

Query 3: "Who are the grandchildren of John?"
```
Query: Grandchild(x, john)
Known facts: Parent(john, james) and Parent(james, michael)
Apply Rule 12: Grandchild(x, y) ← Grandparent(y, x)
Apply Rule 9: Grandparent(x, y) ← ∃z (Parent(x, z) ∧ Parent(z, y))
With z = james: Parent(john, james) ∧ Parent(james, michael)
Answer: Grandchild(michael, john) - Michael is John's grandchild
        Grandchild(patricia, john) - Patricia is John's grandchild
```

Query 4: "Who is the aunt of David?"
```
Query: Aunt(x, david)
Known facts: Parent(susan, david) and Sibling(susan, james)
Apply Rule 13: Aunt(x, y) ← ∃z (Parent(z, y) ∧ Sister(x, z))
With z = susan: Parent(susan, david) and Sister(x, susan)
Answer: Sister(patricia, susan) - Patricia is Susan's sister
        Therefore: Aunt(patricia, david) - Patricia is David's aunt
```

Query 5: "Are Michael and David cousins?"
```
Query: Cousin(michael, david)
Known facts: Parent(james, michael) and Sibling(james, susan) and Parent(susan, david)
Apply Rule 19: Cousin(x, y) ← ∃z ∃w (Parent(z, x) ∧ Parent(w, y) ∧ Sibling(z, w))
With z = james, w = susan:
Parent(james, michael) and Parent(susan, david) and Sibling(james, susan)
Answer: YES, Cousin(michael, david) is true
```

Query 6: "List all ancestors of Jane"
```
Query: Ancestor(x, jane)
Known facts: Parent(michael, jane)
Apply Rule 17a: Ancestor(x, jane) ← Parent(x, jane)
Answer: Ancestor(michael, jane)

Apply Rule 17b: Ancestor(x, jane) ← Parent(x, z) ∧ Ancestor(z, jane)
With z = michael: Parent(james, michael) and Ancestor(michael, jane)
Answer: Ancestor(james, jane)

Continue transitively:
Ancestor(john, jane) and Ancestor(mary, jane)
Complete list: michael, james, john, mary (all of Jane's ancestors)
```

**Step 5: Constraint Validation**

```
% Constraint 1: No one can be their own ancestor
∀x ¬Ancestor(x, x)

% Constraint 2: Parent-child relationship is asymmetric
∀x ∀y (Parent(x, y) → ¬Parent(y, x))

% Constraint 3: A person has exactly two biological parents (assuming no single parents)
∀x (∃y1 ∃y2 (Parent(y1, x) ∧ Parent(y2, x) ∧ y1 ≠ y2))

% Constraint 4: Spouse relationship is symmetric
∀x ∀y (Spouse(x, y) → Spouse(y, x))

% Constraint 5: No one can be their own sibling
∀x ¬Sibling(x, x)
```

**Summary of Capabilities:**

This FOL family system demonstrates:
1. **Complete knowledge representation** of family relationships using basic predicates
2. **Recursive rule definition** for transitive relationships (ancestors, descendants)
3. **Multi-step inference** combining multiple rules (e.g., finding cousins requires sibling and parent relationships)
4. **Constraint modeling** for domain integrity
5. **Scalability** to large family trees without rule modification
6. **Query answering** through logical inference and unification
7. **Extensibility** to add new relationships (in-laws, half-siblings) by adding rules without changing existing structure

---

## References (APA 7)

Genesereth, M. R., & Nilsson, N. J. (1987). *Logical foundations of artificial intelligence*. Morgan Kaufmann Publishers.

Luger, G. F. (2008). *Artificial intelligence: structures and strategies for complex problem solving* (5th ed.). Addison-Wesley.

Nilsson, N. J. (1998). *Artificial intelligence: a new synthesis*. Morgan Kaufmann Publishers.

Russell, S. J., & Norvig, P. (2020). *Artificial intelligence: a modern approach* (4th ed.). Pearson.

Shapiro, S. C. (1992). Artificial intelligence. In S. C. Shapiro (Ed.), *Encyclopedia of artificial intelligence* (2nd ed., pp. 54-67). John Wiley & Sons.

van Dalen, D. (2004). *Logic and structure* (4th ed.). Springer-Verlag.

---

**Status:** Complete
**Date Completed:** 2026-03-18

# Topic 12: Reasoning and Inference in KBS

## Overview
This topic covers reasoning and inference mechanisms in KBS including rule-based reasoning, case-based reasoning, and handling uncertainty through Bayesian reasoning and fuzzy logic.

---

## Learning Outcome Questions

### 1. Remember: Reasoning Mechanisms
**Question:** List different types of reasoning mechanisms used in KBS.

**Your Response:**

**Eight Major Reasoning Mechanisms in KBS:**

**1. Forward Chaining (Data-Driven)**
- Start with known facts, apply rules to derive new conclusions
- Suitable for: Diagnostic systems, monitoring, planning
- Example: From symptoms → diagnose disease

**2. Backward Chaining (Goal-Driven)**
- Start with desired goal, work backward to find supporting facts
- Suitable for: Question answering, problem solving, planning
- Example: To prove hypothesis → what evidence needed?

**3. Rule-Based Reasoning**
- Apply IF-THEN rules to knowledge base
- Uses symbolic manipulation: modus ponens, modus tollens
- Strengths: Transparent, explainable, predictable
- Limitations: Brittle with incomplete/uncertain data

**4. Case-Based Reasoning (CBR)**
- Solve new problem by retrieving and adapting similar past cases
- Process: Retrieve → Reuse → Revise → Retain
- Suitable for: Legal reasoning, medical diagnosis, design
- Strengths: Leverages experience, learns from cases
- Limitations: Requires library of cases, similarity metrics difficult

**5. Bayesian Reasoning**
- Probabilistic reasoning using conditional probability
- Formula: P(A|B) = P(B|A) × P(A) / P(B)
- Suitable for: Diagnosis with uncertain data, risk assessment
- Strengths: Theoretically sound, handles uncertainty
- Limitations: Requires probability estimates, computationally intensive

**6. Fuzzy Logic**
- Deals with approximate/vague concepts (not crisp true/false)
- Uses membership degrees (0.0 to 1.0) instead of binary
- Suitable for: Control systems, imprecise domains
- Example: Temperature "hot" is fuzzy (75°F partially hot)

**7. Abductive Reasoning**
- Inference to best explanation: given effects, infer likely causes
- Process: Observe result → hypothesize cause
- Suitable for: Diagnosis (disease from symptoms), fault detection
- Differs from deduction/induction: creative but non-monotonic

**8. Analogical Reasoning**
- Apply knowledge from similar domain to current problem
- Suitable for: Creative problem solving, transfer learning
- Example: Solar system analogy for atomic structure

---

### 2. Understand: Forward and Backward Chaining
**Question:** Explain the step-by-step process of forward and backward chaining.

**Your Response:**

**Forward Chaining: Data-Driven Inference Process**

**Algorithm Steps:**

1. **Initialize**: Load all known facts into working memory
2. **Iterate**:
   - Match rule antecedents (IF parts) against working memory
   - Fire rules whose conditions are satisfied
   - Add derived facts to working memory
3. **Repeat**: Continue until no new facts derived (fixed point) or goal found
4. **Terminate**: Return all derived facts or goal proof

**Example: Agricultural Pest Management**

```
Knowledge Base:
  Fact: Plant has_pest Aphid
  Fact: Weather temperature > 25°C
  Rule R1: If plant has_pest X then apply_treatment Y
  Rule R2: If temperature > 25°C AND has_pest then increase_monitoring

Working Memory (Initial): [Plant has_pest Aphid, temperature = 28°C]

Forward Chaining Execution:
  Iteration 1:
    - Check R1: plant has_pest Aphid? YES → Fire R1
    - Derive: apply_treatment for_aphid
    - Check R2: temp > 25°C? YES, has_pest? YES → Fire R2
    - Derive: increase_monitoring
    - Working Memory: [Plant has_pest Aphid, temp=28°C, apply_treatment, increase_monitoring]

  Iteration 2:
    - No new rules match
    - Algorithm terminates

  Result: Conclude apply_treatment and increase_monitoring
```

**Characteristics**:
- Breadth-first exploration of solution space
- Generates all possible conclusions
- Efficient when goal likely derivable early
- All inference paths explored (may be wasteful)

---

**Backward Chaining: Goal-Driven Inference Process**

**Algorithm Steps:**

1. **Initialize**: Set goal to prove
2. **Match**: Find rules that conclude the goal
3. **Subgoal**: Set rule antecedents as new subgoals
4. **Recurse**: Recursively prove each subgoal
5. **Backtrack**: If subgoal fails, try alternative rules
6. **Succeed**: Goal proven if chain reaches base facts

**Example: Medical Diagnosis**

```
Knowledge Base:
  Fact: Patient has_symptom Fever
  Fact: Patient has_symptom Cough
  Rule R1: If has_symptom Fever AND has_symptom Cough then Diagnosis = Influenza
  Rule R2: If has_symptom Fever then Diagnosis = Common_Cold

Goal: Prove Diagnosis = Influenza

Backward Chaining Execution:
  Goal: Diagnosis = Influenza
  ├─ Find rules concluding Influenza → R1 applies
  ├─ Subgoals: [has_symptom Fever, has_symptom Cough]
  │
  ├─ Subgoal 1: has_symptom Fever?
  │  └─ Check facts: YES (base fact matches)
  │
  └─ Subgoal 2: has_symptom Cough?
     └─ Check facts: YES (base fact matches)

  Result: All subgoals proven → Diagnosis = Influenza PROVEN
```

**Characteristics**:
- Depth-first exploration focusing on goal
- Only explores relevant solution paths
- More efficient when goal unlikely but specific
- Stops at first proof (may miss alternatives)

---

**Comparison Table**:

| Aspect | Forward Chaining | Backward Chaining |
|--------|------------------|-------------------|
| **Direction** | Facts → Conclusions | Goal ← Supporting Facts |
| **Focus** | All possibilities | Specific goal only |
| **Efficiency** | All paths explored | Focused relevant paths |
| **When to Use** | Many facts, few rules | Clear goal, many possible derivations |
| **Memory** | Grows with derived facts | Grows with recursion depth |
| **Completeness** | Finds all conclusions | Finds first proof or none |
| **Example Domain** | Monitoring, monitoring systems | Diagnosis, question answering |

**Hybrid Bidirectional Chaining**:
- Combine both directions for efficiency
- Forward from facts until subset of goal space reached
- Backward from goal until matches forward results
- Meets in middle to minimize exploration

---

### 3. Apply: Choose Appropriate Chaining
**Question:** Determine whether forward or backward chaining is more suitable for a given problem.

**Your Response:**

**Selection Framework: Choosing Chaining Method**

**Decision Criteria**:

| Criterion | Favors Forward | Favors Backward |
|-----------|---|---|
| **Input Data Volume** | Large amount | Small amount |
| **Goal Specificity** | Multiple vague goals | Single clear goal |
| **Output Requirements** | All possible conclusions | Proof of specific goal |
| **Rule Structure** | Few rules, many facts | Many rules, few facts |
| **Interaction Pattern** | System-initiated | User-query-initiated |
| **Performance Priority** | Batch processing | Real-time response |

---

**Problem Scenario 1: Manufacturing Quality Control**

**Description**: Automated system monitoring production line. Thousands of sensor readings per minute. Goal: Detect any anomalies and recommend corrective actions.

**Analysis**:
- Input: Continuous high-volume sensor data
- Output: All detected anomalies and corrective actions
- Reasoning: Need to check all data against all rules
- User interaction: None (autonomous system)

**Recommendation**: **FORWARD CHAINING**

**Justification**:
- Facts (sensor readings) continuously accumulating
- Multiple possible anomalies may occur simultaneously
- Need to generate all applicable conclusions
- System operates independently without user queries
- Batch processing of data appropriate

**Rules Example**:
```
If Temperature > 95°C then Alert_Overheating
If Vibration > 5.0Hz then Alert_Imbalance
If Speed < 80RPM then Alert_Slowdown
```

---

**Problem Scenario 2: Customer Service Chatbot**

**Description**: Online support system answers customer questions about eligibility for loan programs.

**Analysis**:
- Input: Customer query (eligibility for specific loan)
- Output: YES/NO answer with justification
- Reasoning: Trace backward from goal to supporting facts
- User interaction: Direct queries requiring specific answers

**Recommendation**: **BACKWARD CHAINING**

**Justification**:
- User provides clear goal (eligibility for Loan X)
- Specific question requiring specific answer
- Rules form tree with many branches, facts are base nodes
- Real-time interaction—user awaits quick answer
- Backward chaining explores only relevant paths

**Rules Example**:
```
If age >= 25 AND income >= $50k AND credit_score >= 650
  then Eligible_for_Standard_Loan
If employed >= 2years AND income >= $30k AND credit_score >= 600
  then Eligible_for_Starter_Loan
```

---

**Problem Scenario 3: Network Intrusion Detection**

**Description**: Security system analyzing network traffic for suspicious patterns.

**Analysis**:
- Input: Continuous network packets/logs
- Output: Detection of any anomalies/intrusions
- Pattern: Multiple patterns may match simultaneously
- Requirement: Detect all attacks, not just one

**Recommendation**: **FORWARD CHAINING**

**Justification**:
- Continuous streaming input data
- Multiple attack patterns possible simultaneously
- System needs to detect ALL threats (not just first match)
- No single clear goal; all patterns important
- Autonomous monitoring operation

---

**Problem Scenario 4: Debugging Software System**

**Description**: Developer debugger helps identify root cause of crash.

**Analysis**:
- Input: Symptom described by user ("Program crashes on login")
- Output: Root cause diagnosis
- Reasoning: Work backward from symptom to cause
- User interaction: User provides symptom, expects diagnosis

**Recommendation**: **BACKWARD CHAINING**

**Justification**:
- Clear specific goal: identify crash cause
- Forward would explore all possible system behaviors (too broad)
- Backward naturally traces effect → cause reasoning
- Real-time: developer awaits answer
- Interactive: user guides exploration with information

**Example Logic**:
```
Goal: Program_Crashes
  ← Try rules concluding crash
  ← Rule: If Memory_Corrupted then Program_Crashes
    ├─ Subgoal: Memory_Corrupted?
    │  ├─ Check buffer overflow? password field has 256 chars max, input 500
    │  └─ YES: Buffer overflow causes memory corruption
```

---

**Problem Scenario 5: Supply Chain Optimization**

**Description**: Identify all opportunities to reduce costs in supply chain.

**Analysis**:
- Input: Cost data for all suppliers, logistics, materials
- Output: All cost reduction opportunities
- Completeness: Must find all opportunities
- Pattern: Exhaustive search of possibility space

**Recommendation**: **FORWARD CHAINING**

**Justification**:
- Comprehensive data available (all cost factors)
- Goal is discovery of all opportunities (not specific goal)
- Batch processing (plan for next quarter)
- Need all options for decision-making
- Not user-query-initiated

---

**Decision Tree**:

```
┌─ Is there a single, specific goal to prove?
│  ├─ YES → BACKWARD CHAINING
│  │  └ Focus on that goal; ignore irrelevant paths
│  │
│  └─ NO → FORWARD CHAINING
│     └ Need all conclusions; explore all facts
│
└─ Is data continuously arriving?
   ├─ YES → FORWARD CHAINING
   │  └ Process new facts immediately
   │
   └─ NO → DEPENDS on other factors above
```

---

**Hybrid Approach**:

**Problem Scenario 6: Hospital Admission Triage**

Combination forward + backward:
- **Forward**: Process vital signs, symptoms → narrow to relevant conditions
- **Backward**: From suspected conditions → verify required tests/protocols

This hybrid approach filters irrelevant paths while still exploring specific goals.

---

### 4. Analyze: Rule-Based vs. Case-Based
**Question:** Compare and contrast rule-based and case-based reasoning.

**Your Response:**

**Rule-Based Reasoning (RBR)**

**Core Concept**: Capture domain knowledge as IF-THEN rules; apply rules to derive conclusions.

**Process**:
1. Encode expert knowledge as rules: "If symptoms then diagnosis"
2. Match current facts against rule conditions
3. Fire matching rules; derive new conclusions
4. Repeat until goal reached or no more rules apply

**Example**:
```
Rule 1: If fever > 101°F AND headache then Influenza_suspected
Rule 2: If nausea AND diarrhea then Gastroenteritis_suspected
Rule 3: If rash AND fever then Measles_suspected
```

**Strengths**:
- **Explainability**: Clear chain of if-then logic easy to follow
- **Modularity**: Rules are independent; new rules added easily
- **Domain Expertise**: Captures expert knowledge explicitly
- **Deterministic**: Same facts always produce same conclusions
- **Validation**: Can verify rules with domain experts
- **Scalability**: Works well with many rules

**Weaknesses**:
- **Knowledge Acquisition**: Extracting rules from experts time-consuming and difficult
- **Brittleness**: Fails on cases outside rule coverage
- **Uncertainty**: Difficult to represent probabilistic or fuzzy knowledge
- **Combinatorial Explosion**: Many rules can create complex interactions
- **Maintenance**: Rule conflicts and redundancies difficult to manage
- **Context Sensitivity**: Rules may need exception handling

---

**Case-Based Reasoning (CBR)**

**Core Concept**: Solve new problem by retrieving similar past problems (cases) and adapting their solutions.

**Process** (4 R's):
1. **Retrieve**: Find cases in case base most similar to current problem
2. **Reuse**: Adapt solution from retrieved case to current problem
3. **Revise**: Test adapted solution; modify if needed based on outcome
4. **Retain**: Store new problem+solution as case in case base (learning)

**Example**:
```
Current Problem: Patient with fever (101°F), cough, body aches
Similar Case Retrieved: Case #2847 - Patient with fever (102°F), cough, body aches
  → Diagnosed as Influenza, treated with antivirals
Reuse: Apply similar diagnosis/treatment to current patient
Revise: Monitor response; adjust if needed
Retain: Add current patient to case base for future reference
```

**Strengths**:
- **Learning**: System improves by accumulating cases
- **Complexity Handling**: Handles cases requiring complex reasoning
- **Intuitive**: Mirrors human reasoning (people use past experience)
- **Partial Knowledge**: Works even if domain rules unknown
- **Novelty**: Can handle unprecedented cases through adaptation
- **Natural for Subjective Domains**: Legal, design decisions

**Weaknesses**:
- **Case Library Dependency**: Requires comprehensive case collection
- **Similarity Metrics**: Determining "similar" is problem-dependent and difficult
- **Consistency**: May produce inconsistent results (different solutions to similar problems)
- **Adaptation Difficulty**: Adapting solutions requires judgment
- **First-Problem**: System helpless on completely novel problems
- **Overhead**: Case retrieval and matching computationally expensive
- **Explanation**: Justifying "because similar case solved it this way" less rigorous

---

**Detailed Comparison Table**:

| Aspect | Rule-Based | Case-Based |
|--------|-----------|-----------|
| **Knowledge Source** | Expert rules | Historical cases |
| **Knowledge Form** | Symbolic rules | Concrete examples |
| **Problem Solving** | Logical deduction | Analogical reasoning |
| **Learning** | Static (manual) | Dynamic (case accumulation) |
| **Explanation** | "Because rule X fired" | "Similar case solved this way" |
| **Completeness** | All cases must match rule | Partial matching acceptable |
| **Scalability** | Rules scale well | Case base grows unwieldy |
| **Development** | Requires expert knowledge elicitation | Requires case collection |
| **Performance** | Consistent; predictable | Variable; depends on cases |
| **Suitability** | Domains with clear rules | Domains based on experience |
| **Maintenance** | Rule conflicts, redundancy | Case organization, indexing |

---

**Selection: When to Use RBR vs. CBR**

**Choose Rule-Based When**:
- Domain knowledge well-understood (clear rules exist)
- Solutions deterministic (same input → same output required)
- Domain relatively stable (rules don't change frequently)
- Explanation critical (must justify decisions)
- Performance must be consistent
- Example domains: Diagnosis with clear symptoms, financial rules, configuration

**Choose Case-Based When**:
- Domain knowledge tacit (captured in examples, not rules)
- Solutions judgment-based/subjective (multiple valid solutions)
- Domain evolving (need to learn from experience)
- Rare/novel cases must be handled
- Partial matching acceptable
- Example domains: Legal reasoning, architectural design, medical complex cases

**Choose Hybrid When**:
- Part of domain rule-based, part case-based
- Initial rules guide case retrieval
- Cases provide exception handling to rules

---

**Hybrid Approach Example: Medical Diagnosis**

**Rule-Based Component**:
- Clear rules: "High fever + red spots = measles"
- Eliminates common cases quickly
- Provides baseline diagnosis

**Case-Based Component**:
- Complex/atypical presentations handled via cases
- Previous unusual diagnoses inform current unusual case
- Adaptation handles presentation variations

**Process**:
1. Apply rules first for straightforward cases
2. If rule diagnosis uncertain, retrieve similar cases
3. Expert reviews case-based suggestions
4. New unusual case adds to case base

---

**Implementation Technologies**:

**Rule-Based**:
- CLIPS, Jess (rule engines)
- OWL/SWRL (semantic web)
- Business rule engines

**Case-Based**:
- Specialized CBR systems (ReMind, ESTEEM)
- Custom implementations in Python/Java
- Often integrated with databases for case storage

---

**Effectiveness Across Domains**:

| Domain | RBR | CBR | Best Choice |
|--------|-----|-----|-------------|
| Tax regulation | High | Low | RBR |
| Patent examination | Medium | High | CBR |
| Equipment diagnosis | High | Medium | RBR |
| Product design | Low | High | CBR |
| Credit approval | High | Medium | RBR |
| Legal argumentation | Medium | High | CBR |

---

### 5. Evaluate: Reasoning with Uncertainty
**Question:** Discuss the challenges of reasoning with uncertain information.

**Your Response:**

**Sources of Uncertainty in KBS**

1. **Incomplete Information**: Not all data available (unknown patient history)
2. **Imprecise Data**: Measurement errors, sensor noise (blood pressure reading ±2 mmHg)
3. **Vague Concepts**: Fuzzy boundaries (high fever, young person, expensive item)
4. **Probabilistic Events**: Outcomes uncertain even with all data (drug effectiveness 85%)
5. **Missing Rules**: Domain knowledge incomplete (unexpected disease manifestations)
6. **Conflicting Evidence**: Multiple sources suggest different conclusions

---

**Challenge 1: Combining Evidence**

**Problem**: How to combine multiple pieces of uncertain evidence?

Example: Patient has symptom A (suggests disease X 60%), symptom B (suggests disease X 70%), symptom C (suggests disease Y 50%)

**Traditional Logic Fails**:
- If we use AND: 0.60 × 0.70 × ... = very small probability (incorrect)
- If we use OR: takes maximum (loses information about certainty)

**Bayesian Approach**:
```
P(Disease|Symptoms) = P(Symptoms|Disease) × P(Disease) / P(Symptoms)

With multiple symptoms:
P(Disease|S1,S2,S3) uses Bayesian update iteratively
```

**Challenges**:
- Requires knowing P(Symptom|Disease) for all combinations
- Independence assumptions often violated
- Probability estimates difficult to obtain

---

**Challenge 2: Handling Non-Binary Truth Values**

**Problem**: Real-world concepts not strictly true or false

Example: Is temperature "warm"?
- 60°F: Clearly not warm
- 80°F: Clearly warm
- 72°F: Somewhat warm? (classical logic says YES or NO, not MAYBE)

**Classical Approach**: Binary (true/false)
```
warm(temperature) ← temperature > 75
```
Issue: 74°F is "not warm" but 75°F is "warm" (unrealistic jump)

**Fuzzy Logic Approach**: Degree of membership (0.0 to 1.0)
```
warm(75°F) = 0.8 (very warm)
warm(72°F) = 0.5 (somewhat warm)
warm(60°F) = 0.1 (slightly warm)
```

---

**Challenge 3: Computational Complexity**

**Problem**: Reasoning with uncertainty computationally expensive

**Bayesian Networks Example**:
- 10 variables with 2 values each: 2^10 = 1,024 states
- 20 variables: 2^20 = 1,048,576 states
- Full probability calculation becomes intractable

**Solutions**:
- Approximate inference (sampling)
- Belief propagation
- Causal structure exploitation (Bayesian Networks)

---

**Challenge 4: Knowledge Elicitation**

**Problem**: Obtaining uncertainty parameters from experts difficult

**Bayesian Case**:
- Expert says "Patient with fever has 60% chance of influenza"
- What does 60% mean? Frequency? Subjective belief?
- Different experts give different estimates
- Estimates may be systematically biased

**Fuzzy Logic Case**:
- Define membership function for "high fever"
- How exactly to shape the function?
- Expert judgment necessary but variable

**Solutions**:
- Multiple expert consensus
- Calibration against historical data
- Sensitivity analysis (results change if probability ±5%?)

---

**Challenge 5: Updating Beliefs**

**Problem**: How to incorporate new evidence into existing beliefs?

**Forward Reasoning**:
- Start with prior beliefs P(Disease)
- Get symptom evidence
- Update to posterior P(Disease|Symptom)

**Issue**: Different scenarios give different posteriors
```
Patient A: Prior probability of disease = 1% (low-risk population)
           Test positive: P(Disease|Test+) = ?

Patient B: Prior probability of disease = 30% (high-risk population)
           Same test positive: P(Disease|Test+) = ?

Same test, different disease probability based on prior
```

**Solution**: Proper Bayesian update
```
P(Disease|Test+) = P(Test+|Disease) × P(Disease) / P(Test+)

But requires accurate prior and likelihood estimates
```

---

**Challenge 6: Handling Conflicting Rules**

**Problem**: Different rules may suggest different conclusions with confidence

```
Rule 1: Fever → Influenza (confidence 0.7)
Rule 2: Cough → Bronchitis (confidence 0.8)
Rule 3: Fever ∧ Cough → Pneumonia (confidence 0.6)

Patient has fever and cough: Which diagnosis?
```

**Issues**:
- No clear way to combine conflicting confidence
- Rule priority unclear
- Multiple conclusions possible with varying confidence

**Solutions**:
- Dempster-Shafer theory
- Certainty factors (MYCIN approach)
- Fuzzy aggregation operators

---

**Challenge 7: Information vs. Uncertainty**

**Problem**: Distinguishing lack of information from actual uncertainty

```
Case A: "Disease X probability unknown" (no information)
Case B: "Disease X probability 50%" (maximum uncertainty)
Case C: "Disease X probability 95%" (high certainty)
```

**Default Assumptions Matter**:
- Closed World: Unknowns assumed false (databases)
- Open World: Unknowns may be true or false (semantic web)

**For KBS**:
- Open world assumption appropriate (missing data doesn't mean false)
- But this increases reasoning complexity

---

**Bayesian Networks: Structured Uncertainty**

**Solution Approach**: Represent uncertainty as directed acyclic graph

```
        [Genetic_Predisposition]
              ↓
        [Disease_Risk] → [Symptom_1]
              ↓
        [Symptom_2]
```

**Advantages**:
- Decomposes complex probability into simpler local relationships
- Computationally tractable for many problems
- Captures causal structure

**Challenges**:
- Building correct network structure difficult
- Still requires probability estimates
- Limited to discrete or parameterized continuous variables

---

**Fuzzy Logic: Continuous Uncertainty**

**Solution Approach**: Allow continuous membership values

```
Membership in "hot":
     1.0 |      ___
         |    /     \
    0.5 |___/       \___
         |_______________
          50°C  70°C  90°C

hot(65°C) = 0.5 (temperature is partially hot)
hot(80°C) = 0.9 (temperature is mostly hot)
```

**Advantages**:
- Intuitive for vague concepts
- No probability estimates needed
- Works with incomplete information

**Challenges**:
- Lack of formal probabilistic semantics
- Parameter selection (where to place membership curves?)
- Interaction between fuzzy variables unclear

---

**Summary: Uncertainty Challenges**

| Challenge | Bayesian | Fuzzy | Hybrid |
|-----------|----------|-------|--------|
| **Combining Evidence** | Well-founded | Heuristic | Structured |
| **Vague Concepts** | Awkward | Natural | Good |
| **Parameter Learning** | Possible from data | Limited | Moderate |
| **Computational Cost** | O(2^n) | Linear | Moderate |
| **Explainability** | Mathematical | Intuitive | Moderate |
| **Uncertain Uncertainty** | Addressed | Unclear | Depends |

**Best Practice**: Choose method based on domain characteristics and available knowledge about uncertainty.

---

### 6. Create: Rule-Based System
**Question:** Design a simple rule-based system for a specific task.

**Your Response:**

**Rule-Based System: Student Scholarship Eligibility Determination**

**System Overview**:
Purpose: Automatically determine scholarship eligibility for university applicants based on academic, financial, and demographic criteria.

**Domain**: Student financial aid and admissions

---

**Facts (Input Data)**:

```prolog
% Student Profile Facts
student(john_smith).
student(maria_garcia).
student(david_lee).

% Academic Performance
gpa(john_smith, 3.85).
gpa(maria_garcia, 3.45).
gpa(david_lee, 2.95).

test_score(john_smith, 1450).        % SAT out of 1600
test_score(maria_garcia, 1380).
test_score(david_lee, 1200).

major(john_smith, computer_science).
major(maria_garcia, business).
major(david_lee, general_studies).

% Demographic Information
family_income(john_smith, 35000).    % Annual household income
family_income(maria_garcia, 125000).
family_income(david_lee, 55000).

first_generation(maria_garcia).      % First in family to attend college

% Achievement Records
awards(john_smith, [national_science_fair, state_math_olympiad]).
awards(maria_garcia, [community_service_award]).
awards(david_lee, []).

% Need Assessment
financial_need(Student) :-
    family_income(Student, Income),
    Income < 100000.

% Geographic Criteria
state(john_smith, california).
state(maria_garcia, texas).
state(david_lee, new_york).

underrepresented_state(texas).
underrepresented_state(wyoming).
```

---

**Rules**:

```prolog
%% RULE 1: Merit Scholarship (Academic Excellence)
merit_scholarship(Student, 5000) :-
    student(Student),
    gpa(Student, GPA),
    GPA >= 3.8,
    test_score(Student, Score),
    Score >= 1400,
    \+ already_scholarship(Student, merit_scholarship).

/* Explanation: Award $5000 merit scholarship to students with:
   - GPA of 3.8 or higher AND
   - SAT score of 1400 or higher AND
   - Not already receiving merit scholarship */

%% RULE 2: Need-Based Scholarship
need_based_scholarship(Student, Amount) :-
    student(Student),
    financial_need(Student),
    gpa(Student, GPA),
    GPA >= 3.0,
    calculate_need_amount(Student, Amount).

calculate_need_amount(Student, 3000) :-
    family_income(Student, Income),
    Income < 50000.

calculate_need_amount(Student, 2000) :-
    family_income(Student, Income),
    Income >= 50000,
    Income < 100000.

/* Explanation: Award need-based aid to students with:
   - Annual family income < $100,000 AND
   - GPA >= 3.0
   - Award amount depends on income level */

%% RULE 3: First-Generation Scholarship
first_generation_scholarship(Student, 2500) :-
    student(Student),
    first_generation(Student),
    gpa(Student, GPA),
    GPA >= 3.2,
    financial_need(Student).

/* Explanation: Award $2,500 to first-generation students with:
   - Demonstrated financial need AND
   - GPA >= 3.2 */

%% RULE 4: STEM Excellence Scholarship
stem_scholarship(Student, 4000) :-
    student(Student),
    major(Student, Major),
    stem_major(Major),
    gpa(Student, GPA),
    GPA >= 3.6,
    test_score(Student, Score),
    Score >= 1350.

stem_major(computer_science).
stem_major(engineering).
stem_major(mathematics).
stem_major(physics).
stem_major(chemistry).
stem_major(biology).

/* Explanation: Award $4,000 to STEM majors with:
   - GPA >= 3.6 AND
   - SAT >= 1350 */

%% RULE 5: Diversity Scholarship
diversity_scholarship(Student, 3000) :-
    student(Student),
    state(Student, State),
    underrepresented_state(State),
    gpa(Student, GPA),
    GPA >= 3.0,
    test_score(Student, Score),
    Score >= 1200.

/* Explanation: Award $3,000 to students from underrepresented states:
   - With GPA >= 3.0 AND
   - SAT >= 1200 */

%% RULE 6: Achievement Scholarship
achievement_scholarship(Student, 1500) :-
    student(Student),
    awards(Student, AwardList),
    length(AwardList, NumAwards),
    NumAwards >= 2,
    gpa(Student, GPA),
    GPA >= 3.3.

/* Explanation: Award $1,500 to students with:
   - 2+ significant awards AND
   - GPA >= 3.3 */

%% RULE 7: Ineligibility Rules
ineligible(Student, gpa_too_low) :-
    student(Student),
    gpa(Student, GPA),
    GPA < 2.5.

ineligible(Student, test_score_too_low) :-
    student(Student),
    test_score(Student, Score),
    Score < 1000.

/* Explanation: Students with GPA < 2.5 or SAT < 1000 are ineligible */

%% RULE 8: Full Scholarship (Exceptional Candidates)
full_scholarship(Student, 15000) :-
    student(Student),
    gpa(Student, GPA),
    GPA >= 3.9,
    test_score(Student, Score),
    Score >= 1500,
    financial_need(Student),
    \+ ineligible(Student, _).

/* Explanation: Full scholarship ($15,000) for exceptional candidates:
   - GPA >= 3.9 AND
   - SAT >= 1500 AND
   - Demonstrated financial need AND
   - No ineligibility factors */

%% RULE 9: Aggregate Scholarships (Total Award)
total_scholarship(Student, Total) :-
    findall(Amount,
            (merit_scholarship(Student, Amount) ;
             need_based_scholarship(Student, Amount) ;
             first_generation_scholarship(Student, Amount) ;
             stem_scholarship(Student, Amount) ;
             diversity_scholarship(Student, Amount) ;
             achievement_scholarship(Student, Amount) ;
             full_scholarship(Student, Amount)),
            Amounts),
    sum_list(Amounts, Total),
    Total > 0.

/* Explanation: Calculate total scholarship by summing all eligible awards */

%% RULE 10: Eligibility Status
eligibility_status(Student, eligible) :-
    student(Student),
    gpa(Student, GPA),
    GPA >= 2.5,
    \+ ineligible(Student, _).

eligibility_status(Student, ineligible(Reason)) :-
    student(Student),
    ineligible(Student, Reason).
```

---

**Query Examples and Expected Results**:

**Query 1**: Who is eligible for merit scholarship?
```prolog
?- merit_scholarship(Student, Amount).

Results:
merit_scholarship(john_smith, 5000).  % GPA 3.85, SAT 1450
```

**Query 2**: What is the total scholarship for each student?
```prolog
?- student(S), total_scholarship(S, Total).

Results:
total_scholarship(john_smith, 9500).   % Merit (5000) + Achievement (1500) + Diversity (3000)
total_scholarship(maria_garcia, 5500). % Need-based (2000) + First-generation (2500) + Diversity (1000)
total_scholarship(david_lee, 0).       % No scholarships (GPA < 3.0, below thresholds)
```

**Query 3**: Why is david_lee ineligible for certain scholarships?
```prolog
?- ineligible(david_lee, Reason).

Results:
ineligible(david_lee, gpa_too_low).  % GPA 2.95 < 3.0 minimum for most scholarships
```

---

**Execution Trace (Forward Chaining for john_smith)**:

```
Initial Facts:
  student(john_smith), gpa(john_smith, 3.85), test_score(john_smith, 1450)
  major(john_smith, computer_science), family_income(john_smith, 35000)
  state(john_smith, california), awards(john_smith, [national_science_fair, state_math_olympiad])

Iteration 1:
  → Check merit_scholarship rule:
     GPA 3.85 >= 3.8? YES, SAT 1450 >= 1400? YES
     → FIRE: merit_scholarship(john_smith, 5000) ✓

  → Check need_based_scholarship:
     Income $35,000 < $100,000? YES, GPA >= 3.0? YES
     → FIRE: need_based_scholarship(john_smith, 3000) ✓

  → Check STEM scholarship:
     Major = computer_science (is STEM)? YES, GPA 3.85 >= 3.6? YES, SAT >= 1350? YES
     → FIRE: stem_scholarship(john_smith, 4000) ✓

  → Check achievement_scholarship:
     NumAwards = 2 >= 2? YES, GPA >= 3.3? YES
     → FIRE: achievement_scholarship(john_smith, 1500) ✓

  → Check diversity_scholarship:
     State = california (not underrepresented)? NO
     → FAIL

  → Check full_scholarship:
     GPA 3.85 >= 3.9? NO
     → FAIL

Derived Facts:
  merit_scholarship(john_smith, 5000)
  need_based_scholarship(john_smith, 3000)
  stem_scholarship(john_smith, 4000)
  achievement_scholarship(john_smith, 1500)

Final Query: total_scholarship(john_smith, Total)
  → Sum: 5000 + 3000 + 4000 + 1500 = 13,500
  → Result: total_scholarship(john_smith, 13500) ✓
```

---

**System Characteristics**:

- **Type**: Forward chaining (all eligible scholarships derived)
- **Size**: 10 rules, 6 basic fact types
- **Scalability**: Easily extended with new scholarship types
- **Explainability**: Each rule transparent; can trace why award given
- **Maintenance**: Rules independent; changes don't affect others
- **Limitations**: No uncertainty (rules binary); no adaptive learning

---

## Capstone Assignment

### Task: Given a set of rules and facts, trace the execution of forward or backward chaining to reach a conclusion.

**Your Submission:**

**Complete Inference Trace: Automotive Fault Diagnosis System**

**Knowledge Base**:

**Facts**:
```
engine_status(running)
battery_voltage(11.5)              % Volts (normal is 12-14V)
starter_sound(cranking)
fuel_smell(detected)
dash_warning(check_engine_light)
gas_level(empty)
```

**Rules**:
```
R1: If gas_level(empty) Then engine_will_not_start
R2: If battery_voltage(V), V < 12 Then weak_battery
R3: If weak_battery Then starter_sound(slow_or_silent)
R4: If battery_voltage(V), V < 10 Then dead_battery
R5: If engine_status(not_running) AND starter_sound(cranking) Then engine_cranks_but_not_starts
R6: If engine_cranks_but_not_starts AND fuel_smell(detected) Then flooded_engine
R7: If engine_cranks_but_not_starts AND fuel_smell(not_detected) Then no_fuel_ignition
R8: If no_fuel_ignition AND gas_level(empty) Then out_of_gas
R9: If gas_level(empty) Then refill_gas
R10: If flooded_engine Then clear_flooded_engine_procedures
R11: If dead_battery Then replace_battery
R12: If weak_battery Then recharge_battery
```

**Query**:
```
GOAL: What should the mechanic do to fix the car?
```

---

**APPROACH 1: BACKWARD CHAINING (Goal-Driven)**

**Strategy**: Start with goal "Fix the car" and work backward through rules

```
GOAL: What should be done?

Step 1: What could cause the problem?
  → Look for rules that conclude repair actions
  → R9: refill_gas ← gas_level(empty)
  → R10: clear_flooded_engine ← flooded_engine
  → R11: replace_battery ← dead_battery
  → R12: recharge_battery ← weak_battery

Step 2: Check which conditions are met
  SUBGOAL: Is gas_level(empty)?
    → Check facts: YES! gas_level(empty) is a fact
    → SUCCEED: refill_gas is recommended

  SUBGOAL: Is dead_battery?
    → Need: battery_voltage(V) AND V < 10
    → Fact: battery_voltage(11.5)
    → 11.5 < 10? NO
    → FAIL: Not dead_battery

  SUBGOAL: Is weak_battery?
    → Need: battery_voltage(V) AND V < 12
    → Fact: battery_voltage(11.5)
    → 11.5 < 12? YES
    → SUCCEED: recharge_battery is recommended

  SUBGOAL: Is flooded_engine?
    → Need: engine_cranks_but_not_starts AND fuel_smell(detected)
    → Need: engine_cranks_but_not_starts
      → Need: engine_status(not_running) AND starter_sound(cranking)
      → Fact: engine_status(running) - Does NOT match engine_status(not_running)
      → FAIL: Not flooded_engine

CONCLUSIONS (Backward Chaining):
  ✓ refill_gas (because gas_level(empty) is true)
  ✓ recharge_battery (because battery_voltage(11.5) < 12)
  ✗ replace_battery (because battery > 10V)
  ✗ clear_flooded_engine (because engine_status is running, not not_running)

BACKWARD CHAINING SUMMARY:
  Total rules examined: 6 out of 12
  Path efficiency: 50% (focused on goal-relevant rules)
  Execution time: Fast (stops when goals found)
```

---

**APPROACH 2: FORWARD CHAINING (Data-Driven)**

**Strategy**: Start with all facts and apply all rules until no new conclusions

```
ITERATION 1:
  Working Memory: [engine_status(running), battery_voltage(11.5),
                   starter_sound(cranking), fuel_smell(detected),
                   dash_warning(check_engine_light), gas_level(empty)]

  Apply R1: If gas_level(empty) Then engine_will_not_start
    Condition: gas_level(empty)? YES
    → Derive: engine_will_not_start ✓
    Working Memory += engine_will_not_start

  Apply R2: If battery_voltage(V), V < 12 Then weak_battery
    Condition: battery_voltage(11.5) < 12? YES
    → Derive: weak_battery ✓
    Working Memory += weak_battery

  Apply R3: If weak_battery Then starter_sound(slow_or_silent)
    Condition: weak_battery? YES (just derived)
    → Derive: starter_sound(slow_or_silent) ✓
    Working Memory += starter_sound(slow_or_silent)

  Apply R4: If battery_voltage(V), V < 10 Then dead_battery
    Condition: 11.5 < 10? NO
    → FAIL: No derivation

  Apply R5: If engine_status(not_running) AND starter_sound(cranking) Then ...
    Condition: engine_status(not_running)? NO (is 'running')
    → FAIL: No derivation

  Apply R6-R8: Similar, conditions not met
    → FAIL for all

  Apply R9: If gas_level(empty) Then refill_gas
    Condition: gas_level(empty)? YES
    → Derive: refill_gas ✓
    Working Memory += refill_gas

  Apply R10: If flooded_engine Then clear_flooded_engine_procedures
    Condition: flooded_engine? NO (not derived yet)
    → FAIL

  Apply R11: If dead_battery Then replace_battery
    Condition: dead_battery? NO (not derived)
    → FAIL

  Apply R12: If weak_battery Then recharge_battery
    Condition: weak_battery? YES (derived in this iteration)
    → Derive: recharge_battery ✓
    Working Memory += recharge_battery

ITERATION 2:
  New facts to check: engine_will_not_start, weak_battery,
                      starter_sound(slow_or_silent), refill_gas, recharge_battery

  Re-apply all rules:
  R1-R12: All conditions already checked or still not satisfied
  → No new derivations

  FIXED POINT REACHED: Stop

FORWARD CHAINING RESULTS:
  Derived Facts:
    ✓ engine_will_not_start
    ✓ weak_battery
    ✓ starter_sound(slow_or_silent) [conflicting with fact starter_sound(cranking)]
    ✓ refill_gas
    ✓ recharge_battery

FORWARD CHAINING SUMMARY:
  Total rules examined: All 12 (explores all possibilities)
  Facts derived: 5 new facts
  Path efficiency: 100% coverage (but explores unnecessary paths)
  Execution time: Moderate (processes all rules regardless of goal)
```

---

**COMPARISON & ANALYSIS**

**Results Comparison**:

| Aspect | Backward | Forward |
|--------|----------|---------|
| **Recommendations** | refill_gas, recharge_battery | refill_gas, recharge_battery |
| **Conclusions Match** | YES | YES (same actions recommended) |
| **Rules Examined** | 6/12 (50%) | 12/12 (100%) |
| **Time Efficiency** | Fast | Moderate |
| **Complete Results** | Goal-focused | All implications |

**Efficiency Analysis**:

**Backward Chaining**:
- Advantages:
  - Focused on goal (doesn't derive irrelevant facts)
  - Faster execution (50% fewer rules examined)
  - Natural for answering specific questions
- Disadvantages:
  - Missed the "conflicting starter_sound states" issue
  - Doesn't reveal all system state implications

**Forward Chaining**:
- Advantages:
  - Complete inference: derives ALL consequences
  - Discovered contradiction: starter_sound is both cranking AND slow_or_silent
  - Full picture of system state
- Disadvantages:
  - More computation (all rules checked)
  - May derive irrelevant conclusions
  - Slower than focused backward chaining

---

**Identified Issues**:

Forward chaining revealed a **contradiction**:
```
Fact: starter_sound(cranking)
Derived: starter_sound(slow_or_silent)  [from weak battery]
```

This inconsistency not detected by backward chaining!

**Resolution**:
- Weak battery typically causes slow cranking, not full silent failure
- OR: Rules need refinement: "If weak_battery THEN modify_starter_sound"
- OR: Priority ordering: newer derivations override older ones

---

**Recommended Mechanic Actions** (from both methods):

1. **PRIMARY**: Refill gas (immediate, low cost)
2. **SECONDARY**: Recharge battery (weak at 11.5V, should be 12-14V)
3. **Monitor**: After refilling gas and recharging battery, see if car starts
4. **If still fails**: Re-examine other systems (ignition, fuel pump, spark plugs)

---

**Which Method Better?**

For automotive diagnosis:
- **Backward Chaining**: Quick answer to "What to fix?" (cost-effective)
- **Forward Chaining**: Complete diagnosis revealing all system issues (thorough)

**Hybrid Recommendation**:
1. **Forward chaining** phase 1: Derive all implications (find contradictions)
2. **Backward chaining** phase 2: Answer specific questions (what to fix)
3. **Conflict resolution**: Reconcile contradictions before presenting to mechanic

---

## References (APA 7)

Aamodt, A., & Plaza, E. (1994). Case-based reasoning: Foundational issues, methodological variations, and system approaches. *AI Communications*, 7(1), 39-59.

Pearl, J. (1988). *Probabilistic reasoning in intelligent systems: Networks of plausible inference*. Morgan Kaufmann Publishers.

Russell, S. J., & Norvig, P. (2020). *Artificial intelligence: A modern approach* (4th ed.). Pearson Education.

Zadeh, L. A. (1965). Fuzzy sets. *Information and Control*, 8(3), 338-353.

Jackson, P. (1999). *Introduction to expert systems* (3rd ed.). Addison-Wesley.

Duda, R. O., Hart, P. E., & Nilsson, N. J. (1976). Subjective Bayesian methods for rule-based inference systems. *AFIPS Conference Proceedings*, 45, 1075-1082.

---

**Status:** Complete
**Date Completed:** 2026-03-18

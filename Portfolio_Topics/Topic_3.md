# Topic 3: Knowledge Representation: Introduction

## Overview
This topic introduces knowledge representation in AI systems, exploring why it's important, desirable properties, and different approaches to representing knowledge effectively in KBS.

---

## Learning Outcome Questions

### 1. Remember: Define Knowledge Representation
**Question:** Define "Knowledge Representation" in the context of AI.

**Your Response:**

Knowledge Representation (KR) in AI is the methodology and formalism used to encode information about the world in a form that a computer system can use to solve complex tasks. It involves translating human knowledge and understanding into explicit symbolic structures—such as logical formulas, semantic networks, frames, rules, or ontologies—that computer systems can process, reason with, and manipulate. Knowledge representation bridges the gap between how humans think about the world (implicit, intuitive understanding) and how computers need information structured (explicit, formal, processable). It is the "language" that KBS use to store and communicate knowledge internally.

---

### 2. Understand: Importance
**Question:** Explain why effective knowledge representation is crucial for KBS.

**Your Response:**

Effective knowledge representation is crucial for KBS for several fundamental reasons:

**1. Enables Reasoning**: Knowledge must be represented in a form that inference engines can process. The representation scheme directly determines what kind of reasoning the system can perform. Poor representation can make certain valid reasoning impossible or inefficient.

**2. Determines System Capability**: The representational scheme fundamentally limits what the system can know and reason about. Logic-based representations excel at symbolic reasoning but struggle with uncertainty. Semantic networks excel at hierarchical relationships but are weaker at numerical reasoning. The choice of representation determines the system's strengths and weaknesses.

**3. Affects Knowledge Acquisition**: How we represent knowledge influences how difficult it is to acquire that knowledge from experts. If the representation requires experts to formalize their knowledge in ways that are unnatural to them, knowledge acquisition becomes painfully slow and error-prone.

**4. Influences Maintenance and Evolution**: As systems must be updated and knowledge must be refined, the representation scheme determines how easy or difficult it is to modify, extend, and debug the knowledge base. Poorly chosen representations can lead to brittle systems where changes have unexpected side effects.

**5. Impacts Computational Efficiency**: Different representations have different computational costs. Some representations can execute inference very quickly, while others require extensive computation. For real-time systems, this can be critical.

**6. Facilitates Knowledge Sharing**: Standardized, well-defined knowledge representations allow knowledge to be shared between different systems and organizations. This is why ontologies and semantic web technologies are important.

**7. Enables Explainability**: The representation scheme affects whether the system can explain its reasoning to users. Symbolic representations (logic, rules) are naturally explainable, while distributed representations (neural networks) are not.

---

### 3. Apply: Key Properties
**Question:** Identify the key properties that a good knowledge representation scheme should possess.

**Your Response:**

A good knowledge representation scheme should possess the following desirable properties:

**1. Representational Adequacy**: The scheme must be capable of expressing all types of knowledge needed in the domain. It should not have inherent limitations that prevent expressing important concepts or relationships.

**2. Inferential Adequacy**: The representation must support the kinds of inferences and reasoning required by the application. The inference mechanisms available to the system must be able to operate effectively on the representation.

**3. Inferential Efficiency**: While inferential adequacy is important, the inferences must be computationally efficient. A representation that requires exponential time to derive conclusions is impractical for real systems.

**4. Acquisitional Efficiency**: Knowledge in the representation should be relatively easy for domain experts and knowledge engineers to acquire and input into the system. The representation should be close to how experts naturally think about the domain.

**5. Explicit Representation of Knowledge**: Important knowledge should be explicitly represented rather than implicit in the structure. This makes the knowledge visible, debuggable, and modifiable.

**6. Modularity**: Knowledge should be representable in relatively independent modules that can be modified or removed without cascading effects throughout the entire knowledge base. This facilitates maintenance and testing.

**7. Clarity and Unambiguity**: The representation should be unambiguous and clear. Given a piece of represented knowledge, its meaning should be singular and precisely defined. Ambiguity leads to logical inconsistencies.

**8. Tractability**: The representation should allow for tractable reasoning—that is, problems should be solvable in reasonable time. Some representations can be expressive but computationally intractable.

**9. Naturalness**: The representation should match the way domain experts naturally think about and discuss the domain. Representations that are too formal or counterintuitive hinder knowledge acquisition.

**10. Standardization**: Ideally, representations should follow standards or conventions so that knowledge can be shared across systems and understood by multiple stakeholders.

---

### 4. Analyze: Different Approaches
**Question:** Categorize different knowledge representation approaches based on their underlying principles.

**Your Response:**

Knowledge representation approaches can be categorized into several families based on their underlying principles:

**Logic-Based Representations**:
- **Propositional Logic**: Represents knowledge as propositions (true/false statements) connected by logical operators (AND, OR, NOT)
- **First-Order Logic**: Extends propositional logic with predicates, variables, and quantifiers, allowing representation of objects and relationships
- **Non-monotonic Logic**: Handles default reasoning where conclusions can be revised when new information arrives
- **Principle**: Based on formal mathematical logic and symbolic reasoning

**Network-Based Representations**:
- **Semantic Networks**: Knowledge represented as nodes (concepts) connected by labeled edges (relationships) forming a graph
- **Conceptual Graphs**: Similar to semantic networks but with more formal structure and semantics
- **Principle**: Based on graph theory; relationships between concepts are explicit; good for hierarchical knowledge

**Structured Representations**:
- **Frames**: Represent stereotypical knowledge about objects or situations, with slots for properties and procedures
- **Scripts**: Similar to frames but for sequences of events or standard scenarios
- **Principle**: Based on data structures with attributes and procedural attachments; good for representing stereotypical situations

**Knowledge Organization Structures**:
- **Ontologies**: Formal specifications of conceptualizations, defining concepts, relationships, and axioms in a domain
- **Taxonomies**: Hierarchical classification schemes
- **Thesauri**: Vocabulary with relationships between terms
- **Principle**: Based on shared conceptualization; facilitates knowledge sharing and interoperability

**Production Rules**:
- **IF-THEN Rules**: Conditional statements of the form "IF condition THEN action"
- **Constraint-Based Rules**: Rules expressing constraints that must be satisfied
- **Principle**: Based on condition-action pairs; intuitive for many domains; supports forward and backward chaining

**Hybrid Approaches**:
- **Blackboard Architecture**: Combines multiple representation schemes for different knowledge sources
- **Multi-Representation Systems**: Use different representations for different knowledge types
- **Principle**: Recognizes that single representation is often inadequate; different knowledge types benefit from different representations

**Categorical Classification**:
- **Declarative vs. Procedural**: Declarative represents "what" (facts, relationships), procedural represents "how" (processes, procedures)
- **Symbolic vs. Distributed**: Symbolic uses discrete symbols and discrete representations; distributed (like neural networks) uses continuous values and learned representations
- **Explicit vs. Implicit**: Explicit makes knowledge visible and accessible; implicit embeds knowledge in system structure

---

### 5. Evaluate: Trade-offs
**Question:** Discuss the trade-offs involved in choosing a particular knowledge representation method.

**Your Response:**

Choosing a knowledge representation involves accepting trade-offs across multiple dimensions:

**Expressiveness vs. Tractability**:
- More expressive representations (like first-order logic) can represent complex relationships but may be computationally intractable
- Less expressive representations (like propositional logic) are more tractable but may not capture important nuances
- Trade-off: You gain expressive power at the cost of computational efficiency

**Explainability vs. Learning Capacity**:
- Symbolic representations (logic, rules, semantic networks) are explainable but don't learn from data automatically
- Learned representations (neural networks, statistical models) learn from data but lack explainability
- Trade-off: You gain learning capacity at the cost of interpretability, or gain explainability at the cost of learning

**Generality vs. Domain Specificity**:
- General representations work across many domains but may not capture domain-specific nuances efficiently
- Highly specialized representations excel in their domain but don't transfer to other domains
- Trade-off: You gain domain-specific efficiency at the cost of generality and reusability

**Knowledge Acquisition Burden vs. System Completeness**:
- More complete knowledge bases produce better system performance but require enormous knowledge acquisition effort
- Simpler knowledge bases are quicker to build but produce less capable systems
- Trade-off: You gain completeness at the cost of development time and expense

**Formality vs. Naturalness**:
- Formal representations (first-order logic) are unambiguous and have clear semantics but are often unnatural to domain experts
- Natural representations (frames, scripts) are easier for experts to work with but may be ambiguous
- Trade-off: You gain clarity and rigor at the cost of accessibility, or gain usability at the cost of precision

**Modularity vs. Efficiency**:
- Modular representations (where knowledge is independent) are easier to maintain and test but may require more inference steps
- Integrated representations are computationally efficient but difficult to modify without side effects
- Trade-off: You gain maintainability at the cost of efficiency, or efficiency at the cost of flexibility

**Universality vs. Specificity**:
- Universal representations try to apply everywhere but often perform mediocrely in any specific context
- Specific representations optimized for particular problem types perform better but don't generalize
- Trade-off: You gain flexibility at the cost of performance in any specific domain

**Practical Implication**: There is no perfect knowledge representation. The choice must be tailored to the specific application's priorities and constraints.

---

### 6. Create: Strategy for New Domain
**Question:** Outline a strategy for representing knowledge in a new, simple domain.

**Your Response:**

**Domain: Plant Disease Diagnosis for Smallholder Farmers (Simple Version)**

**Step 1: Domain Analysis and Knowledge Inventory**
- Meet with 3-5 experienced farmers and agricultural extension officers
- Document all disease types they commonly encounter (e.g., maize leaf blight, bean rust, tomato powdery mildew)
- Identify observable symptoms (leaf spots, discoloration, wilting patterns)
- Identify environmental conditions that favor each disease (humidity, temperature, season)
- Document recommended management practices (resistant varieties, fungicides, cultural practices)

**Step 2: Identify Knowledge Types**
- **Factual Knowledge**: Disease names, symptoms, conditions, treatments
- **Procedural Knowledge**: Steps to diagnose (observation sequence), steps to manage
- **Heuristic Knowledge**: "High humidity + leaf spots = likely fungal disease"
- **Causal Knowledge**: "Poor drainage causes soil-borne diseases"

**Step 3: Select Representation Scheme**
**Choose: Production Rules (IF-THEN) with semantic network support**

**Rationale**:
- Production rules are intuitive for experts ("IF the farmer sees yellow spots AND the spots have a ring pattern THEN suspect bacterial blight")
- Easy to acquire from experts who think in "if-then" patterns
- Compatible with inference engines (forward/backward chaining)
- Can be updated as new diseases emerge
- Can include confidence factors for uncertain conditions

**Step 4: Design the Knowledge Representation Structure**

```
KNOWLEDGE BASE STRUCTURE:

FACTS (Base Knowledge):
- Disease(maize_blight): causative_agent(fungus), season(rainy)
- Symptom(yellow_spots): color(yellow), shape(circular), location(leaf_margin)
- Environment(high_humidity): threshold(>75%)

RULES (Diagnostic Rules):
IF: observed_symptom(leaf_spots) AND
    spot_color(yellow) AND
    spot_pattern(concentric_rings) AND
    season(rainy) AND
    crop(corn)
THEN: disease(corn_leaf_blight) [confidence: 0.85]

Management Rules:
IF: confirmed_disease(corn_leaf_blight)
THEN: recommend_action(apply_fungicide)
AND:  recommend_action(plant_resistant_variety_next_season)
AND:  recommend_action(practice_crop_rotation)

SEMANTIC NETWORK (Hierarchical relationships):
  Disease
    └─ Fungal Disease
         ├─ Corn Leaf Blight
         └─ Bean Rust
    └─ Bacterial Disease
         └─ Bacterial Wilt

Environmental Conditions:
  ├─ Temperature: [optimal_range: 20-25°C]
  ├─ Humidity: [high: >75%]
  └─ Rainfall: [heavy: >50mm/week]
```

**Step 5: Implementation Details**

**Representation Format** (Pseudo-code):
```
Rule format:
  IF (condition1) AND (condition2) AND ...
  THEN (action1), (action2)
  [confidence: X.XX]

Fact format:
  Property(entity, value)

Query format (Backward chaining):
  "What disease causes yellow concentric spots on corn leaves?"
```

**Step 6: Knowledge Acquisition Strategy**

1. **Phase 1**: Interview 3 expert farmers individually
   - Document disease names, symptoms, and conditions in natural language
   - Create symptom-disease matrix

2. **Phase 2**: Formalize knowledge into rules
   - Convert expert descriptions into IF-THEN structure
   - Assign confidence scores based on expert agreement

3. **Phase 3**: Validation with group of experts
   - Present rules back to experts
   - Refine based on feedback
   - Test with historical disease cases

4. **Phase 4**: Field testing
   - Have extension officers test recommendations on actual farmer cases
   - Record successes and failures
   - Iteratively improve rules

**Step 7: System Interaction Example**

```
Farmer Input: "My corn has brown spots with rings. It's been raining a lot."

System Reasoning:
1. Match facts: brown_spots(confirmed), rings_pattern(confirmed),
   high_rainfall(confirmed), season(rainy)
2. Query rules: Which diseases cause brown spots with rings?
3. Apply inference: Disease-A matches 2/3 conditions (confidence 0.6)
                   Disease-B matches 3/3 conditions (confidence 0.85)
4. Recommend Disease-B as most likely
5. Provide explanation: "Based on the ring pattern and wet conditions favoring
   the fungus, I suspect Disease-B"

System Output:
Likely diagnosis: Disease-B (85% confidence)
Recommended actions:
  1. Plant resistant variety
  2. Improve drainage
  3. Use recommended fungicide
Explanation: "Ring-patterned spots in rainy season indicate fungal disease B"
```

**Step 8: Maintenance Strategy**

- **Monthly**: Collect feedback from extension officers about system recommendations
- **Quarterly**: Add new disease patterns if farmers encounter unfamiliar symptoms
- **Seasonally**: Update environmental thresholds based on current season conditions
- **Annually**: Full expert review and rule refinement

**Advantages of This Strategy**:
- Uses intuitive IF-THEN rules that match expert thinking
- Easily extended as new diseases emerge
- Explainable (farmers understand why diagnosis was made)
- Maintainable (rules can be updated without affecting others)
- Confidence factors handle uncertainty

**Limitations**:
- Cannot automatically discover new disease patterns
- Requires expert knowledge to formalize
- May struggle with multi-disease situations
- Doesn't improve with data without manual rule updates

---

## Capstone Assignment

### Task: Prepare a presentation explaining the significance of knowledge representation and outlining the various approaches available.

**Your Submission:**

**KNOWLEDGE REPRESENTATION IN AI SYSTEMS: SIGNIFICANCE AND APPROACHES**

**I. SIGNIFICANCE AND IMPORTANCE**

Knowledge representation is the cornerstone of artificial intelligence and knowledge-based systems. Without effective knowledge representation, no intelligent reasoning is possible. The significance of KR can be understood through multiple lenses:

**Philosophical Significance**: Knowledge representation embodies how we choose to encode our understanding of reality. Different representations reflect different assumptions about what aspects of reality are important and how they relate.

**Practical Significance**: Effective KR is the difference between a system that can reason intelligently about a domain and one that merely executes pre-programmed procedures. It determines whether the system can:
- Adapt to novel situations
- Explain its reasoning
- Learn and evolve
- Interact naturally with humans
- Scale to complex problems

**Economic Significance**: The choice of representation scheme directly impacts development time, maintenance costs, and system longevity. Poor representation choices lead to expensive rework and maintenance problems.

**Cognitive Significance**: KR is about bridging human understanding with machine computation. It's the interface between human experts' implicit knowledge and computer systems' formal requirements.

---

**II. DESIRABLE PROPERTIES OF KNOWLEDGE REPRESENTATIONS**

Research has identified key properties that distinguish good KR schemes from poor ones:

1. **Representational Adequacy**: Can it express what needs to be expressed?
2. **Inferential Adequacy**: Can the system derive the conclusions it needs?
3. **Inferential Efficiency**: Can it do so in reasonable time?
4. **Acquisitional Efficiency**: Can knowledge be acquired and added without excessive effort?
5. **Clarity and Unambiguity**: Is the meaning precise and single?
6. **Modularity**: Can knowledge be modified independently?
7. **Tractability**: Are computations feasible?
8. **Naturalness**: Does it match how experts think?
9. **Standardization**: Can knowledge be shared across systems?
10. **Explainability**: Can the system explain its reasoning?

No single representation excels on all these properties. The challenge is selecting one that best balances these properties for a particular application.

---

**III. MAJOR REPRESENTATION APPROACHES**

**A. LOGIC-BASED REPRESENTATIONS**

*Propositional Logic*:
- Knowledge: P ∧ Q → R (if P and Q, then R)
- Strengths: Simple, clear semantics, mechanizable reasoning
- Weaknesses: Limited expressiveness, cannot represent objects/relationships
- Use: Boolean reasoning, hardware design

*First-Order Logic*:
- Knowledge: ∀x (Parent(x,y) ∧ Parent(y,z) → Grandparent(x,z))
- Strengths: Highly expressive, formal semantics, powerful reasoning
- Weaknesses: Computationally expensive, unnatural for many domains
- Use: Complex relationship representation, scientific domains

*Advantages of Logic*:
✓ Formal semantics and clear meaning
✓ Automated theorem proving available
✓ Sound and complete inference procedures exist
✓ Highly explainable

*Disadvantages of Logic*:
✗ Open-world assumption (unknown = false, which is wrong for incomplete knowledge)
✗ Computational complexity
✗ Difficult knowledge acquisition
✗ Struggle with defaults and exceptions

---

**B. NETWORK-BASED REPRESENTATIONS**

*Semantic Networks*:
```
         has_color
    Tomato ────────→ Red
     │     is_a
     │
   plant ←─────────
     │
     └──→ Requires(water)
          Requires(sunlight)
```
- Knowledge represented as nodes (concepts) and edges (relationships)
- Strengths: Intuitive visualization, hierarchical organization, easy to understand
- Weaknesses: Ambiguous relationship semantics, no standard formal semantics
- Use: Taxonomies, conceptual organization

*Advantages of Networks*:
✓ Intuitive and visual
✓ Captures hierarchical knowledge naturally
✓ Facilitates similarity-based reasoning
✓ Good for organizing large knowledge bases

*Disadvantages of Networks*:
✗ Ambiguous semantics
✗ No standard formal reasoning procedures
✗ Difficult to handle constraints
✗ Can become unwieldy for complex domains

---

**C. STRUCTURED REPRESENTATIONS**

*Frames*:
```
Frame: Tomato
├── color: [red, green, yellow]
├── size: [small, medium, large]
├── maturity: [unripe, ripe, overripe]
├── growing_requirements:
│   ├── water: 25-30mm/week
│   ├── temperature: 20-25°C
│   └── sunlight: 6-8 hours/day
└── procedures:
    ├── ripen(): if_color=green then wait 2_weeks
    └── is_edible(): if_maturity=ripe then true
```

- Strengths: Intuitive representation of objects, procedural attachments, defaults
- Weaknesses: Less formal, specialized reasoning mechanisms needed
- Use: Object-oriented representation, prototypical knowledge

*Advantages of Frames*:
✓ Intuitive for objects and scenarios
✓ Efficient retrieval of organized knowledge
✓ Support for defaults and exceptions
✓ Integrates data and procedures

*Disadvantages of Frames*:
✗ Less formal semantics
✗ Specialized reasoners needed for each frame type
✗ Difficult to do complex logical reasoning
✗ Knowledge acquisition still challenging

---

**D. ONTOLOGY-BASED REPRESENTATIONS**

*Formal Ontologies*:
- Explicit, machine-processable representation of concepts and relationships
- Include formal axioms defining relationships
- Example: Open Biomedical Ontologies (OBO) for life sciences

*Advantages of Ontologies*:
✓ Facilitate knowledge sharing and reuse
✓ Enable semantic interoperability
✓ Formal definitions reduce ambiguity
✓ Support integration of multiple knowledge sources

*Disadvantages of Ontologies*:
✗ Expensive to develop (require significant expertise)
✗ Difficult to maintain consistency at scale
✗ Knowledge acquisition burden
✗ May over-constrain domains with high variation

---

**IV. COMPARATIVE ANALYSIS**

| Approach | Expressiveness | Tractability | Learnability | Explainability | Domains |
|---|---|---|---|---|---|
| Propositional Logic | Low | High | Medium | Excellent | Boolean, Hardware |
| First-Order Logic | High | Low | Low | Excellent | Complex relationships |
| Semantic Networks | Medium | High | Medium | Good | Taxonomies, Concepts |
| Frames | Medium-High | Medium | Medium | Good | Objects, Scenarios |
| Ontologies | Very High | Low | Low | Excellent | Knowledge Sharing |
| Production Rules | Medium | High | Medium | Excellent | Expert Systems |
| Neural Networks | Very High | High | High | Poor | Pattern Recognition |

---

**V. SELECTION CRITERIA FOR REPRESENTATION METHODS**

Choose based on:

1. **Domain Requirements**:
   - Complex relationships → First-Order Logic
   - Hierarchical concepts → Semantic Networks, Ontologies
   - Object-based → Frames
   - Pattern-based → Neural Networks

2. **Reasoning Requirements**:
   - Logical inference → Logic-based
   - Similarity matching → Case-based, Networks
   - Optimization → Genetic Algorithms
   - Pattern recognition → Neural Networks

3. **Knowledge Acquisition Context**:
   - Expert availability → Rules, Ontologies
   - Historical data available → Machine Learning approaches
   - Mixed sources → Hybrid approaches

4. **System Constraints**:
   - Real-time performance → Efficient representations
   - Explainability critical → Symbolic representations
   - Large datasets → Learning-based representations
   - Maintenance burden → Modular approaches

5. **Integration Needs**:
   - Need to integrate multiple KBs → Ontologies
   - Standalone system → Any approach
   - Web-based sharing → Semantic web technologies

---

**VI. PRACTICAL EXAMPLES IN DIFFERENT DOMAINS**

**Healthcare**:
- Uses: Ontologies (SNOMED CT, ICD), Medical knowledge bases (First-Order Logic), Neural Networks (diagnostic support)
- Why: Complex hierarchies of diseases, need for standardization, large data for learning

**Legal**:
- Uses: Production rules (legal precedents), Semantic networks (legal concepts), Ontologies (legal terminology)
- Why: Explicit rules and precedents, complex hierarchical relationships, knowledge sharing across jurisdictions

**E-commerce**:
- Uses: Semantic networks (product taxonomies), Neural networks (recommendations), Frames (product descriptions)
- Why: Need hierarchical product organization, massive data for learning, object-based product representation

**Manufacturing**:
- Uses: Production rules (process control), Ontologies (parts and processes), Frames (equipment specifications)
- Why: Well-defined processes, need for standardization, complex equipment descriptions

**Agriculture**:
- Uses: Production rules (crop management), Semantic networks (crop relationships), Data mining (pattern discovery)
- Why: Expert knowledge in rules, hierarchical crop classification, benefit from discovering local patterns

---

**VII. FUTURE DIRECTIONS IN KNOWLEDGE REPRESENTATION**

1. **Hybrid Representations**: Combining symbolic and neural approaches (neuro-symbolic AI)
2. **Knowledge Graphs**: Large-scale, interconnected knowledge representations (Google Knowledge Graph, DBpedia)
3. **Semantic Web Standards**: RDF, OWL enabling machine-readable web
4. **Commonsense Knowledge**: Representing everyday reasoning (ConceptNet, YAGO)
5. **Temporal and Uncertainty**: Better handling of time-dependent and uncertain knowledge
6. **Transfer Learning**: Representations that transfer across domains

---

**VIII. CONCLUSION**

Knowledge representation is not a solved problem. Choosing the right representation requires understanding the trade-offs between expressiveness, tractability, learnability, and explainability. Most modern intelligent systems use hybrid approaches, combining multiple representation schemes optimized for different knowledge types. The future of AI likely involves better integration of symbolic (interpretable) and neural (learnable) approaches.

The key insight is that **how you represent knowledge is how you think about problems**. Better representations lead to better reasoning, easier knowledge acquisition, and more maintainable systems.

---

## References (APA 7)

Ahenda, J. (2026). APT3020VA: Knowledge-based systems course outline. United States International University–Africa.

Davis, R., Shrobe, H., & Szolovits, P. (1993). What is a knowledge representation? *AI Magazine*, 14(1), 17-33.

Guarino, N., & Poli, R. (2010). Ontologies and knowledge bases. In *Handbook on ontologies* (pp. 3-22). Springer Berlin Heidelberg.

Newell, A. (1982). The knowledge level. *Artificial Intelligence*, 18(1), 87-127.

Sowa, J. F. (2000). *Knowledge representation: Logical, philosophical, and computational foundations.* Brooks/Cole.

Wikipedia contributors. (2026). Knowledge representation. In *Wikipedia, the free encyclopedia.* Retrieved March 18, 2026, from https://en.wikipedia.org/wiki/Knowledge_representation

---

**Status:** Complete
**Date Completed:** March 18, 2026

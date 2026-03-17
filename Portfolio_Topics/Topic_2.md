# Topic 2: Types of Knowledge-Based Systems

## Overview
This topic explores the different categories of Knowledge-Based Systems including Expert Systems, Case-Based Reasoning, Neural Networks, Genetic Algorithms, Intelligent Agents, and Data Mining systems, examining their fundamental principles and applications.

---

## Learning Outcome Questions

### 1. Remember: List Different Types
**Question:** List the different types of Knowledge-Based Systems.

**Your Response:**

The main types of Knowledge-Based Systems include:

1. **Expert Systems (ES)** - Rule-based systems that capture domain expertise using if-then rules and an inference engine to provide expert-level decision support.

2. **Case-Based Reasoning (CBR) Systems** - Systems that solve new problems by retrieving, reusing, and adapting solutions from previously solved cases stored in a case library.

3. **Neural Networks (NNs)** - Computational models inspired by biological neural networks that learn patterns and representations from data through interconnected nodes.

4. **Genetic Algorithms (GAs)** - Evolutionary computation techniques that use selection, crossover, and mutation operations to evolve solutions toward optimal results.

5. **Intelligent Agents** - Autonomous entities that perceive their environment, reason about situations, and take actions to achieve goals, often combining multiple KBS approaches.

6. **Data Mining Systems** - Systems designed to discover hidden patterns, relationships, and actionable knowledge from large datasets through analytical and statistical techniques.

7. **Blackboard Systems** - Cooperative architecture-based systems where multiple independent knowledge sources contribute to problem-solving through a shared workspace.

8. **Intelligent Tutoring Systems (ITS)** - Educational systems that provide personalized instruction by combining domain knowledge, student modeling, and pedagogical strategies.

---

### 2. Understand: Fundamental Principles
**Question:** Describe the fundamental principles of each type of KBS.

**Your Response:**

**Expert Systems** operate on the principle of capturing domain expertise as IF-THEN rules. When provided with facts about a specific problem, the inference engine applies these rules systematically using forward chaining (data-driven) or backward chaining (goal-driven) to derive conclusions. The system mimics how a human expert would reason through the problem step-by-step.

**Case-Based Reasoning Systems** operate on the principle that similar problems have similar solutions. The CBR cycle includes: (1) Retrieve - find the most similar past cases, (2) Reuse - adapt the solution from the retrieved case, (3) Revise - modify the solution based on the current problem, and (4) Retain - store the new problem-solution pair for future use. Learning happens through accumulation of solved cases.

**Neural Networks** learn patterns from data without explicit programming. They use layers of interconnected artificial neurons with weighted connections. During training, these weights are adjusted iteratively to minimize prediction errors. The network learns to recognize complex patterns and can generalize to new, unseen inputs. Knowledge is distributed across the network structure.

**Genetic Algorithms** use evolutionary principles to solve optimization problems. A population of candidate solutions "evolves" over generations through selection (fittest solutions survive), crossover (combining solution properties), and mutation (introducing variation). The population gradually converges toward better solutions through this evolutionary process.

**Intelligent Agents** operate on the principle of sense-decide-act: they perceive environmental information through sensors, make decisions based on their knowledge and goals, and execute actions to influence their environment. Multi-agent systems allow cooperation and competition between multiple agents pursuing different or shared goals.

**Data Mining Systems** operate on the principle of discovering patterns hidden in large datasets. They use statistical, machine learning, and data analysis techniques to find associations, clusters, anomalies, and predictive patterns that might not be obvious through manual inspection.

**Blackboard Systems** operate on a shared workspace principle where multiple knowledge sources (each with different expertise) contribute solutions simultaneously. A control mechanism coordinates these contributions, evaluating partial solutions and deciding which knowledge sources to activate next.

**Intelligent Tutoring Systems** operate on the principle of personalized instruction based on continuous assessment. They model student knowledge, identify learning gaps, select appropriate learning content and strategies, and adapt instruction based on student responses and progress.

---

### 3. Apply: Classify a Scenario
**Question:** Classify a given scenario into one of the KBS types.

**Your Response:**

**Scenario**: A telecommunications company wants to build a system to diagnose network faults. The system receives alerts about network anomalies, customer complaints, and performance metrics. It must identify the root cause of the problem, recommend maintenance actions, and predict potential future failures.

**Classification and Justification**: This scenario would be best served by a **Hybrid approach combining Expert System (primary) with Data Mining elements**.

**Expert System Component (primary)**:
- Use case: The immediate fault diagnosis and recommendation phase
- Reasoning: Network faults follow patterns that can be captured as expert rules (e.g., "If packet loss > 5% AND latency > 100ms, then likely backbone congestion")
- Advantage: Provides immediate, explainable recommendations that network engineers can understand and trust
- Rules can be captured from experienced network engineers and vendor documentation

**Data Mining Component (secondary)**:
- Use case: Pattern discovery from historical fault data to identify emerging issues
- Reasoning: Allows identification of complex correlations between network parameters that human experts might not have explicitly formulated (e.g., "Monday 9 AM shows 40% higher congestion correlated with specific web services")
- Advantage: Continuously improves system by discovering new fault patterns from accumulated historical data

**Why not other types?**:
- **Neural Networks alone**: Would work for prediction but lacks explainability (engineers won't trust a black-box recommendation)
- **Case-Based Reasoning alone**: Would require storing thousands of detailed fault cases with variations
- **Genetic Algorithms**: Overkill for this problem; not an optimization problem but a classification/diagnosis problem
- **Intelligent Agents**: Could work but adds unnecessary complexity for a relatively straightforward diagnostic problem

**Conclusion**: The Expert System provides the core diagnostic capability with explainability, while Data Mining adds learning and pattern discovery. This hybrid approach combines the strengths of both paradigms.

---

### 4. Analyze: Compare and Contrast
**Question:** Compare and contrast the strengths and weaknesses of different KBS types.

**Your Response:**

| Characteristic | Expert Systems | Case-Based Reasoning | Neural Networks | Genetic Algorithms |
|---|---|---|---|---|
| **Knowledge Source** | Domain expertise from experts | Past cases and experiences | Training data patterns | Problem domain heuristics |
| **Learning Method** | Manual knowledge engineering | Incremental learning from new cases | Machine learning from training data | Evolutionary optimization |
| **Speed** | Fast (simple rule application) | Fast retrieval and adaptation | Very fast inference (learned patterns) | Slow (requires many generations) |
| **Accuracy** | High in domain of knowledge | Depends on case library quality | High after proper training | Depends on fitness function |
| **Explainability** | Excellent (can trace reasoning) | Good (can show similar cases) | Poor (black box) | Poor (encoding in genes) |
| **Data Requirements** | Low (requires expert input) | Requires comprehensive case library | High (needs large training set) | Low to Medium |
| **Adaptability** | Requires expert updates | Improves naturally with new cases | Can retrain with new data | Can evolve to new environments |
| **Maintenance Burden** | High (knowledge brittleness) | Low (just add new cases) | Medium (data quality issues) | Medium (fitness function tuning) |
| **Uncertainty Handling** | Can use confidence factors | Similarity measures handle variations | Natural through probabilistic outputs | Can be encoded in algorithm |
| **Scaling** | Degrades with very large rule sets | Degrades with massive case bases | Scales well | Scales with population size |
| **Suitable Problems** | Diagnostic, classification | Recommendation, design | Pattern recognition, prediction | Optimization, scheduling |

**Key Contrasts**:

**Explainability vs. Accuracy Trade-off**: Expert Systems excel at explainability but may lack accuracy outside their knowledge domain. Neural Networks provide superior accuracy on complex pattern problems but sacrifice explainability. Case-Based Reasoning offers a middle ground.

**Knowledge Representation**: Expert Systems require explicit knowledge formulation (challenging). Neural Networks extract implicit patterns from data (requires large datasets). Case-Based Reasoning stores actual problem-solution pairs (intuitive but storage-intensive).

**Maintenance Philosophy**: Expert Systems require periodic expert-driven updates when knowledge changes. Case-Based Reasoning improves continuously through new case additions. Neural Networks require periodic retraining. Genetic Algorithms once evolved, require re-evolution for new domains.

**Domain Transferability**: Expert Systems are typically not transferable between domains (rules are domain-specific). Neural Networks can sometimes transfer learned representations. Case-Based Reasoning can work across domains if case representation is domain-independent.

**Robustness**: Expert Systems can be brittle when facing situations beyond their knowledge. Neural Networks gracefully degrade with slightly different inputs. Case-Based Reasoning depends heavily on case library coverage.

---

### 5. Evaluate: Most Suitable Type
**Question:** Determine the most suitable KBS type for a given problem.

**Your Response:**

**Problem Statement**: A Kenyan agricultural extension service wants to optimize crop yields for smallholder farmers across different regions. The system needs to: (1) consider multiple crop varieties, soil types, weather patterns, pest pressures, and market prices; (2) generate farm-specific recommendations; (3) improve over time as new data is collected; (4) work with limited historical data initially; (5) help farmers make decisions even in novel situations.

**Analysis of Options**:

**Expert System**: Would work moderately well, capturing agricultural expert knowledge as rules. However, optimizing across multiple variables (crop choice, planting date, fertilizer type, irrigation timing, pest control) becomes complex. Many interdependent rules needed. Problem: Brittleness—if weather patterns shift or new pests emerge, rules become invalid.

**Case-Based Reasoning**: Could be effective once sufficient case library is built (e.g., "In region X with soil type Y and rainfall pattern Z, crop variety W produced yield R"). However, initially the system would be weak with limited cases. Problem: Requires comprehensive historical data not readily available in developing regions.

**Neural Networks**: Could excel at learning complex patterns from weather, soil, and yield data. Once trained, could generate predictions and recommendations quickly. However, would require large labeled dataset of historical yields with corresponding conditions. Problem: Poor explainability—farmers wouldn't understand why the system recommends one crop over another.

**Genetic Algorithms**: Could optimize crop and input selection given fitness function of maximizing yield while minimizing input costs. Would help identify locally-optimal farming practices. However, requires defining complete search space upfront. Problem: Slow convergence, requires multiple iterations.

**Data Mining + Intelligent Agents**: Data mining could discover patterns in available data (e.g., which combinations of practices work). Intelligent Agents could represent individual farmers' constraints and goals, with agents adapting recommendations to local contexts.

**Recommended Best Fit**: **Hybrid: Expert System (core) + Data Mining (supporting)**

**Justification**:
1. **Expert System as Core**: Agricultural researchers can provide foundational expert knowledge about crop requirements, soil management, and pest control. This knowledge base is relatively stable and well-documented.

2. **Data Mining for Enhancement**: As the system accumulates data from farmers' experiences and yields, data mining components continuously discover new patterns and regional variations not in the original expert knowledge.

3. **Why this hybrid works**:
   - Starts functional immediately (with expert knowledge) even with limited farmer data
   - Improves over time (data mining discovers patterns)
   - Remains explainable (expert rules are transparent)
   - Combines stability (expert knowledge) with learning (data mining)
   - Can handle variations across regions better than either alone

4. **Why other types were rejected**:
   - Pure NN: Lacks explainability; insufficient data
   - Pure CBR: Insufficient initial cases; farmers need immediate recommendations
   - GA alone: No explainability; not focused on interpretable recommendations

**Expected Performance**: System provides good recommendations immediately (via expert rules), then continuously improves as farmers provide feedback and outcome data, discovering regional patterns and new techniques through data mining.

---

### 6. Create: High-Level Architecture
**Question:** Design a high-level architecture for a specific type of KBS.

**Your Response:**

**E-Commerce Product Recommendation System using Case-Based Reasoning**

This architecture demonstrates a Case-Based Reasoning system for recommending products to e-commerce customers.

```
┌─────────────────────────────────────────────────────────┐
│              USER INTERFACE LAYER                        │
│  - Customer browsing history display                     │
│  - Product recommendations                              │
│  - "Why this recommendation?" explanation               │
└────────────────────┬────────────────────────────────────┘
                     │
┌────────────────────▼────────────────────────────────────┐
│          CBR CYCLE CONTROLLER                           │
│  Coordinates: Retrieve → Reuse → Revise → Retain       │
└────────────────────┬────────────────────────────────────┘
                     │
        ┌────────────┼────────────┬───────────────┐
        │            │            │               │
┌───────▼─────┐  ┌──▼────────┐ ┌─▼──────────┐ ┌─▼──────────┐
│  RETRIEVAL  │  │   REUSE   │ │   REVISE   │ │   RETAIN   │
│   MODULE    │  │  MODULE   │ │  MODULE    │ │  MODULE    │
├─────────────┤  ├───────────┤ ├────────────┤ ├────────────┤
│ - Similarity│  │ - Adapt   │ │ - Adjust   │ │ - Store    │
│   matching  │  │   solution│ │   ranking  │ │   new case │
│ - Indexing  │  │ - Weight  │ │ - Get user │ │ - Update   │
│ - K-NN algo │  │   features│ │   feedback │ │   indices  │
│ - Feature   │  │           │ │           │ │           │
│   extraction│  │           │ │           │ │           │
└─────────────┘  └───────────┘ └────────────┘ └────────────┘
        │              │             │              │
        └──────────────┴─────────────┴──────────────┘
                      │
        ┌─────────────▼─────────────┐
        │   CASE BASE MANAGEMENT    │
        ├───────────────────────────┤
        │ - Customer Profile Cases  │
        │   * Demographics          │
        │   * Purchase history      │
        │   * Product preferences   │
        │   * Browse patterns       │
        │                           │
        │ - Product Cases          │
        │   * Features             │
        │   * Category             │
        │   * Price range          │
        │   * Customer reviews     │
        │                           │
        │ - Purchase Case Records  │
        │   * What was bought      │
        │   * When                 │
        │   * By whom              │
        │   * Outcome ratings      │
        └───────────────────────────┘
                      │
        ┌─────────────▼─────────────┐
        │  KNOWLEDGE SOURCES        │
        ├───────────────────────────┤
        │ - Product Database        │
        │ - Customer Database       │
        │ - Transaction Logs        │
        │ - External Reviews (API)  │
        │ - Trending Products       │
        │ - Inventory Status        │
        └───────────────────────────┘
```

**Component Descriptions**:

**1. Retrieval Module**: When a customer arrives or searches, this module:
   - Extracts features from the customer (demographics, recent purchases, browsing patterns)
   - Finds similar customers in the case base using similarity metrics (e.g., cosine similarity, Euclidean distance)
   - Retrieves the top K most similar customer cases and their associated product purchases

**2. Reuse Module**: Takes retrieved cases and:
   - Identifies products that similar customers purchased
   - Weights the recommendations based on similarity scores
   - Filters out products already known to the current customer
   - Creates initial recommendation list

**3. Revise Module**: Refines recommendations by:
   - Checking inventory availability
   - Applying business logic (e.g., margin considerations, promotional priorities)
   - Adjusting for recent trend changes (trending products boost)
   - Getting implicit feedback (how long customer looks at recommendation, whether they click)

**4. Retain Module**: Learns from outcomes by:
   - Recording whether customer purchases recommended products
   - Storing successful recommendation cases with outcomes
   - Recording failure cases to learn what doesn't work
   - Updating similarity metrics based on accuracy

**5. Case Base**: Stores three types of cases:
   - **Customer profile cases**: Describes customers with their characteristics and purchase patterns
   - **Product cases**: Describes products and their attributes
   - **Transaction cases**: Documents specific purchases with context and outcomes

**System Flow Example**:
1. New customer logs in → System extracts features
2. Retrieval: Find 5 customers most similar to this customer
3. Reuse: Products purchased by those 5 customers → initial recommendations
4. Revise: Filter/adjust based on availability, trends, margins
5. Present: Show top 3-5 recommendations with "Because customers like you bought..."
6. Retain: Record whether customer clicked, purchased, or ignored recommendations

**Advantages of This CBR Architecture**:
- Explainable: Can show similar customers and their purchases
- Adapts naturally: Every successful recommendation becomes a case for future use
- Handles diversity: Works across diverse product categories
- Personalized: Leverages actual customer behavior patterns

**Limitations**:
- Initial cold start: Few cases means weak recommendations at first
- Case base scaling: Thousands of customers can slow similarity matching
- Temporal issues: Old cases may not reflect current preferences

---

## Capstone Assignment

### Task: Develop a comparative table summarizing the key features, advantages, and disadvantages of at least three different types of Knowledge-Based Systems.

**Your Submission:**

**COMPREHENSIVE COMPARISON TABLE: KNOWLEDGE-BASED SYSTEM TYPES**

| Aspect | Expert Systems | Case-Based Reasoning | Neural Networks |
|--------|---|---|---|
| **Key Features** | - If-then production rules<br>- Inference engine (forward/backward chaining)<br>- Explicit knowledge representation<br>- Confidence factors<br>- Explanation trace capabilities | - Case library of solved problems<br>- Similarity-based retrieval<br>- 4R Cycle: Retrieve-Reuse-Revise-Retain<br>- Adaptation mechanisms<br>- Incremental learning | - Interconnected artificial neurons<br>- Weighted connections/layers<br>- Parallel processing capability<br>- Non-linear decision boundaries<br>- Learned implicit representations |
| **Advantages** | ✓ Highly explainable and transparent<br>✓ Fast decision making<br>✓ Requires low data volume<br>✓ Can handle symbolic reasoning<br>✓ Easy to verify correctness<br>✓ Suitable for rule-based domains | ✓ Learns continuously from experience<br>✓ Intuitive for users (human-like)<br>✓ Handles novel situations through adaptation<br>✓ Requires less explicit knowledge engineering<br>✓ Gracefully degrades<br>✓ Good for domains with repetitive problems | ✓ Excellent at pattern recognition<br>✓ Handles non-linear relationships<br>✓ Scales well with large data<br>✓ Fast inference after training<br>✓ Natural generalization capability<br>✓ Handles noisy/incomplete data |
| **Disadvantages** | ✗ Knowledge acquisition bottleneck<br>✗ Brittle outside knowledge domain<br>✗ Maintenance burden grows with rule base size<br>✗ Struggles with uncertainty<br>✗ Cannot learn from data<br>✗ Poor at novel situation handling | ✗ Requires comprehensive case library<br>✗ Slow retrieval with large case bases<br>✗ Cold start problem (limited cases)<br>✗ Storage intensive<br>✗ Similarity measure design is critical<br>✗ Can be biased toward old solutions | ✗ Black-box nature (no explainability)<br>✗ Requires large training datasets<br>✗ Long training time<br>✗ Prone to overfitting<br>✗ Difficult to debug failures<br>✗ Cannot incorporate domain constraints |
| **Real-World Applications** | - Medical diagnosis (MYCIN)<br>- Legal case analysis<br>- Configuration systems<br>- Equipment diagnostics<br>- Fraud detection rules<br>- Credit scoring | - Customer support recommendations<br>- Legal case precedent finding<br>- Movie/product recommendations<br>- Architectural design<br>- Troubleshooting help<br>- Personnel recruitment | - Image and speech recognition<br>- Stock price prediction<br>- Credit risk assessment<br>- Email spam filtering<br>- Autonomous vehicles<br>- Biological protein folding |
| **Suitable Problem Domains** | - Diagnostic problems<br>- Rule-intensive domains<br>- Static knowledge domains<br>- High transparency requirement<br>- Limited data availability<br>- Symbolic reasoning required | - Repetitive problem types<br>- Design-oriented tasks<br>- Domains with experience value<br>- Recommendation scenarios<br>- Few-shot learning needed<br>- Adaptation important | - Pattern recognition<br>- Prediction tasks<br>- Large data availability<br>- Non-linear relationships<br>- High-dimensional data<br>- Approximate solutions acceptable |
| **Data Requirements** | Minimal (expert knowledge) | Medium (case library) | Extensive (training datasets) |
| **Explainability** | Excellent | Good | Poor (black-box) |
| **Learning Capability** | None (static) | Incremental | Batch training |
| **Implementation Time** | Medium-High (knowledge engineering) | Low-Medium | High (model development) |
| **Cost** | High (expertise capture) | Medium | Medium-High (data/compute) |

---

**ANALYSIS: WHEN TO USE EACH TYPE**

**Expert Systems** are most appropriate when:
- Domain knowledge is well-established and relatively stable (medicine, law, engineering rules)
- Transparency and explainability are critical (regulated industries, high-stakes decisions)
- User adoption depends on understanding the "why" behind recommendations
- Limited training data is available but domain experts are accessible
- The problem involves clear if-then logical reasoning

Examples: Medical diagnosis systems, equipment troubleshooting, legal opinion systems, tax advising systems.

Expert Systems should be avoided when: The domain is rapidly evolving, expertise is poorly understood, or massive non-linear pattern recognition is required.

**Case-Based Reasoning** is most appropriate when:
- Problems follow recurring patterns with variations (customer support, design problems)
- Experience accumulation is valuable (system improves with more solved cases)
- Rapid response is needed using past solutions (troubleshooting, recommendations)
- Users can relate to and understand "similar past situations"
- The domain has sufficient historical cases available or can be built quickly

Examples: Customer support chatbots, product recommendations, design assistance, legal precedent research, personnel recruitment.

Case-Based Reasoning should be avoided when: The problem domain is entirely novel, critical decisions require absolute explainability, or storage and retrieval of massive case bases becomes impractical.

**Neural Networks** are most appropriate when:
- Large volumes of training data are available
- Problem involves complex non-linear relationships (pattern recognition, prediction)
- Exact interpretability is less important than accuracy
- The system benefits from learning and improvement over time
- Scalability to high-dimensional data is important

Examples: Image recognition, speech understanding, credit scoring, fraud detection, recommender systems (deep learning), autonomous systems.

Neural Networks should be avoided when: Explainability is critical, training data is limited, or the domain requires symbolic reasoning and rule enforcement.

**Practical Recommendation**: Most modern organizations use **hybrid systems** combining these approaches—for example, using Expert Systems for interpretable primary decisions, with Neural Networks for complex pattern components, and Case-Based Reasoning for learning and adaptation.

---

## References (APA 7)

Ahenda, J. (2026). APT3020VA: Knowledge-based systems course outline. United States International University–Africa.

Kolodner, J. L. (1993). *Case-based reasoning.* Morgan Kaufmann Publishers.

KMS Learning Hub. (n.d.). *What is knowledge-based system? Types & advantages.* Retrieved January 12, 2026, from https://kmslh.com/glossary/knowledge-based-system/

Goodfellow, I., Bengio, Y., & Courville, A. (2016). *Deep learning.* MIT Press.

Koza, J. R. (1992). *Genetic programming: On the programming of computers by means of natural selection.* MIT Press.

Wikipedia contributors. (2026). Case-based reasoning. In *Wikipedia, the free encyclopedia.* Retrieved January 12, 2026, from https://en.wikipedia.org/wiki/Case-based_reasoning

Wikipedia contributors. (2026). Neural network. In *Wikipedia, the free encyclopedia.* Retrieved January 12, 2026, from https://en.wikipedia.org/wiki/Neural_network

---

**Status:** Complete
**Date Completed:** March 17, 2026

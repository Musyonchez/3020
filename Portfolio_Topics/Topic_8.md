# Topic 8: Frames

## Overview
This topic covers frame-based knowledge representation, including frame structure, slots, facets, inheritance mechanisms, and default values for representing stereotypical objects and concepts.

---

## Learning Outcome Questions

### 1. Remember: Frame Components
**Question:** Identify the main components of a frame in knowledge representation.

**Your Response:**

Frames are a knowledge representation technique that encapsulates stereotypical information about objects, concepts, or situations in a structured, hierarchical manner. They combine aspects of semantic networks (relationships) with object-oriented structures (attributes and methods).

**Main Components of a Frame:**

**1. Frame Name**

The name identifies the frame and represents the concept it models.

Examples:
```
PERSON
RESTAURANT
VEHICLE
MEDICAL-DISEASE
AGRICULTURAL-CROP
```

**2. Slots (Attributes)**

Slots represent properties or attributes of the frame. Each slot can hold a value or a range of values.

```
Frame: PERSON
├─ Slot: NAME
├─ Slot: AGE
├─ Slot: OCCUPATION
├─ Slot: ADDRESS
├─ Slot: EDUCATION
└─ Slot: RELATIONSHIP
```

**3. Facets (Slot Modifiers)**

Facets provide additional information about how slots should be used or interpreted. Each slot can have multiple facets.

Common facets include:

**Value Facet:**
- **Default:** Standard value if not specified
- **Type:** Data type of the slot (integer, string, object reference, etc.)
- **Range:** Acceptable values or value restrictions
- **Instance:** Current value for a specific instance

```
Example:
Slot: AGE
├─ Default: Unknown
├─ Type: Integer
├─ Range: 0-150
└─ Instance: 25
```

**Constraint Facets:**
- **If-needed:** Procedure to compute value if not present
- **If-added:** Procedure to execute when value is added
- **If-modified:** Procedure when value changes
- **If-removed:** Procedure when value is deleted

**4. Parent-Child Relationships**

Frames organize in hierarchies, allowing inheritance and specialization.

```
Frame Hierarchy:
        LIVING-THING
           ▲
           │ parent-of
           │
        ANIMAL
           ▲
           │ parent-of
           │
        DOG
           ▲
           │ parent-of
           │
      SPECIFIC-DOG
```

**5. Inheritance Mechanism**

Frames support inheritance of slots and facets from parent frames.

```
ANIMAL (parent frame)
├─ Slot: LEGS
│  └─ Default: 4
├─ Slot: BREATHING
│  └─ Default: Lungs
└─ Slot: REPRODUCTION
   └─ Default: Live birth

DOG (child frame, inherits from ANIMAL)
├─ Inherited Slots: LEGS, BREATHING, REPRODUCTION
├─ New Slot: BREED
│  └─ Default: Unknown
├─ New Slot: BARK-SOUND
│  └─ Default: Loud
└─ Override: LEGS = 4 (inherited, may override if needed)
```

**6. Default Values**

Default values represent typical or expected values for slots when no specific value is known.

```
Frame: RESTAURANT
├─ Slot: TYPE
│  └─ Default: Full-Service
├─ Slot: HOURS
│  └─ Default: 9AM-11PM
├─ Slot: CUISINE
│  └─ Default: American
├─ Slot: SEATING
│  └─ Default: 50 customers
└─ Slot: PRICE-RANGE
   └─ Default: Moderate
```

**7. Procedures and Methods**

Frames can include procedures associated with slots or the frame overall.

```
Frame: CROP
├─ Slot: WATERING
│  └─ If-needed: Call CALCULATE-WATER-NEEDS()
├─ Slot: DISEASE-CHECK
│  └─ If-added: Call MONITOR-DISEASE()
└─ Frame-method: HARVEST()
   └─ Executes harvesting procedure
```

**8. Instance vs. Class Frames**

Frames exist at two levels:

**Class Frame (Prototype):**
```
Frame: CAR (Class)
├─ Slot: NUMBER-OF-WHEELS
│  └─ Type: Integer
│  └─ Default: 4
├─ Slot: ENGINE-TYPE
│  └─ Type: String
│  └─ Default: Internal Combustion
└─ Slot: FUEL-TYPE
   └─ Type: String
   └─ Default: Gasoline
```

**Instance Frame (Specific Example):**
```
Frame: MY-CAR (Instance of CAR)
├─ Parent: CAR
├─ Slot: NUMBER-OF-WHEELS
│  └─ Instance: 4
├─ Slot: ENGINE-TYPE
│  └─ Instance: V8 Diesel
├─ Slot: FUEL-TYPE
│  └─ Instance: Diesel
└─ Slot: LICENSE-PLATE
   └─ Instance: ABC-1234
```

**9. Attached Knowledge**

Frames can include various types of attached knowledge:

- **Triggers:** Rules that activate based on slot values
- **Conditions:** Constraints on slot values
- **Relationships:** Links to other frames
- **Examples:** Specific instances
- **Exceptions:** Non-standard cases

**10. Slot Value Types**

Slots can hold different types of values:

```
ATOMIC VALUES:
- Numbers: 42, 3.14
- Strings: "John", "Red"
- Booleans: True, False

STRUCTURED VALUES:
- Lists: [1, 2, 3, 4]
- Ranges: 0-100
- Enumerated: {Red, Green, Blue}

COMPLEX VALUES:
- Frame references: → PERSON frame
- Procedures: CALCULATE-AGE()
- Constraints: AGE > 18 AND AGE < 65
```

**Complete Frame Example:**

```
Frame: STUDENT
├─ Slots:
│  ├─ NAME
│  │  ├─ Type: String
│  │  ├─ Value: Unknown
│  │  └─ Required: Yes
│  │
│  ├─ STUDENT-ID
│  │  ├─ Type: Integer
│  │  ├─ Value: Unknown
│  │  ├─ Range: 100000-999999
│  │  └─ Required: Yes
│  │
│  ├─ AGE
│  │  ├─ Type: Integer
│  │  ├─ Default: Unknown
│  │  ├─ Range: 16-80
│  │  └─ If-added: VALIDATE-AGE()
│  │
│  ├─ MAJOR
│  │  ├─ Type: Frame reference → DISCIPLINE
│  │  ├─ Default: Undeclared
│  │  └─ If-modified: UPDATE-MAJOR-REQUIREMENTS()
│  │
│  ├─ GPA
│  │  ├─ Type: Float
│  │  ├─ Default: 0.0
│  │  ├─ Range: 0.0-4.0
│  │  ├─ If-added: CALCULATE-STANDING()
│  │  └─ If-needed: COMPUTE-CURRENT-GPA()
│  │
│  ├─ COURSES-TAKEN
│  │  ├─ Type: List of Frame references → COURSE
│  │  ├─ Default: Empty list
│  │  └─ If-added: UPDATE-TRANSCRIPT()
│  │
│  └─ STANDING
│     ├─ Type: Enumerated {Good, Warning, Probation}
│     ├─ Default: Good
│     ├─ If-needed: EVALUATE-STANDING()
│     └─ If-modified: NOTIFY-ADVISOR()
│
├─ Parent Frame: PERSON
│  └─ Inherited Slots: NAME, ADDRESS, PHONE, EMAIL
│
├─ Associated Frames:
│  ├─ MAJOR → DISCIPLINE frame
│  ├─ ADVISOR → FACULTY frame
│  └─ COURSES-TAKEN → COURSE frames
│
└─ Methods:
   ├─ REGISTER-FOR-COURSE(course)
   ├─ DROP-COURSE(course)
   ├─ VIEW-TRANSCRIPT()
   └─ REQUEST-GRADE-APPEAL()
```

Frame structure provides a rich, organized way to represent knowledge about stereotypical objects and situations, combining the efficiency of defaults with the flexibility to represent exceptions and dynamic behaviors.

---

### 2. Understand: Inheritance in Frames
**Question:** Explain how inheritance works in frame-based systems.

**Your Response:**

Inheritance in frame-based systems is a fundamental mechanism that allows child frames to acquire slots and default values from parent frames, reducing redundancy and enabling efficient knowledge organization.

**Basic Inheritance Mechanism**

**Simple Inheritance:**

```
PLANT (Parent)
├─ Slot: HEIGHT (Default: 1 meter)
├─ Slot: REQUIRES-WATER (Default: Yes)
├─ Slot: REQUIRES-SUNLIGHT (Default: Yes)
└─ Slot: COLOR (Default: Green)
    │
    │ (Child inherits all slots)
    ▼
TREE (Child of PLANT)
├─ Inherited: HEIGHT (can override: 20 meters)
├─ Inherited: REQUIRES-WATER
├─ Inherited: REQUIRES-SUNLIGHT
├─ Inherited: COLOR
├─ New Slot: BARK-TYPE (Default: Rough)
├─ New Slot: LEAF-TYPE (Default: Deciduous)
└─ Override: HEIGHT = 20 meters (different from parent default)
```

**Inheritance Rules:**

```
1. Slot Inheritance Rule:
   If Slot S exists in Parent Frame P
   And Child Frame C is-a P
   Then C inherits Slot S

2. Default Value Inheritance:
   If Slot S has Default D in Parent P
   And Child C inherits Slot S
   Then C inherits Default D (unless overridden)

3. Facet Inheritance:
   If Slot S has Facet F in Parent P
   And Child C inherits Slot S
   Then C inherits Facet F (unless overridden)

4. Override Rule:
   If Child C explicitly defines Slot S
   Then C's definition of S takes precedence
   over Parent P's definition of S
```

**Multiple Inheritance:**

Frames support multiple inheritance, where a child frame inherits from multiple parents.

```
VEHICLE (Parent 1)
├─ Slot: WHEELS
│  └─ Default: 4
├─ Slot: ENGINE
│  └─ Default: Internal Combustion
└─ Slot: FUEL-TYPE
   └─ Default: Gasoline

WATER-TRANSPORTATION (Parent 2)
├─ Slot: HULL-TYPE
│  └─ Default: Fiberglass
├─ Slot: PROPULSION
│  └─ Default: Sail
└─ Slot: MAXIMUM-DEPTH
   └─ Default: 100 meters

AMPHIBIOUS-VEHICLE (Child of VEHICLE and WATER-TRANSPORTATION)
├─ Inherited from VEHICLE:
│  ├─ WHEELS (4)
│  ├─ ENGINE
│  └─ FUEL-TYPE
│
├─ Inherited from WATER-TRANSPORTATION:
│  ├─ HULL-TYPE
│  ├─ PROPULSION
│  └─ MAXIMUM-DEPTH
│
└─ New Slots:
   ├─ CONVERSION-TIME (switching from land to water)
   └─ AMPHIBIOUS-MODE (Land/Water/Both)
```

**Inheritance Chains:**

```
LIVING-THING (Level 0)
├─ Slots: NAME, AGE, WEIGHT, ENERGY-LEVEL
    │
    │ inherited-by
    ▼
ANIMAL (Level 1)
├─ Inherited: NAME, AGE, WEIGHT, ENERGY-LEVEL
├─ New: DIET, HABITAT, REPRODUCTION-TYPE, LEGS
    │
    │ inherited-by
    ▼
MAMMAL (Level 2)
├─ Inherited: All from ANIMAL and LIVING-THING
├─ New: FUR-TYPE, MAMMARY-GLANDS, THERMOREGULATION
    │
    │ inherited-by
    ▼
DOG (Level 3)
├─ Inherited: All from MAMMAL, ANIMAL, LIVING-THING
├─ New: BREED, BARK-SOUND, PACK-BEHAVIOR
    │
    │ inherited-by
    ▼
GERMAN-SHEPHERD (Level 4 - Instance)
├─ Inherited: All slots from all ancestors
├─ Instance values:
│  ├─ NAME: "Rex"
│  ├─ AGE: 5
│  ├─ BREED: "German Shepherd"
│  ├─ FUR-TYPE: "Double coat"
│  └─ TRAINING-LEVEL: "Highly trained"
```

**Property Inheritance Example:**

```
Slot: HEIGHT
├─ In PLANT: Default = 1 meter
├─ In TREE (inherits): Default = 20 meters (override)
├─ In OAK (inherits from TREE): Default = 30 meters (override)
└─ In MY-OAK (instance): Value = 32 meters (specific instance)

Resolution: MY-OAK's HEIGHT
1. Check instance value: 32 meters (use this)
2. If not found, check MY-OAK class default: 30 meters
3. If not found, check OAK default: 30 meters
4. If not found, check TREE default: 20 meters
5. If not found, check PLANT default: 1 meter
```

**Override and Specialization:**

```
TRANSPORTATION (Parent)
├─ Slot: MAX-SPEED (Default: 100 km/h)
├─ Slot: FUEL-EFFICIENCY (Default: Unknown)
└─ Slot: PASSENGER-CAPACITY (Default: 1)
    │
    │ specialized
    ▼
CAR (Child - specializes TRANSPORTATION)
├─ Inherited: MAX-SPEED (override: 200 km/h)
├─ Inherited: FUEL-EFFICIENCY (override: 8L/100km)
├─ Inherited: PASSENGER-CAPACITY (override: 5)
└─ New: TRUNK-VOLUME (Default: 400 liters)
    │
    │ specialized
    ▼
SPORTS-CAR (Child of CAR)
├─ Inherited: MAX-SPEED (override: 300 km/h)
├─ Inherited: FUEL-EFFICIENCY (override: 12L/100km)
├─ Inherited: PASSENGER-CAPACITY (inherit: 5)
├─ Inherited: TRUNK-VOLUME (override: 200 liters)
└─ New: ACCELERATION-0-100 (Default: 4 seconds)
```

**Inheritance with Facets:**

```
Slot: PRICE
├─ In PRODUCT:
│  ├─ Type: Currency
│  ├─ Default: Unknown
│  ├─ Range: 0-unlimited
│  └─ If-added: CALCULATE-TAX()
│
├─ Inherited in FOOD:
│  ├─ Type: Currency (inherited)
│  ├─ Default: $5 (override)
│  ├─ Range: $0-50 (override)
│  └─ If-added: CHECK-EXPIRATION() (override procedure)
│
└─ Inherited in PRODUCE:
   ├─ Type: Currency (inherited)
   ├─ Default: $1 (override)
   ├─ Range: $0-10 (override)
   └─ If-added: CHECK-FRESHNESS() (override procedure)
```

**Inheritance Resolution (Shadowing):**

When multiple parent frames define the same slot, inheritance resolution rules determine which value is used.

```
EMPLOYEE (Parent 1)
├─ Slot: WORK-LOCATION (Default: Office)
├─ Slot: SALARY (Default: $40,000)

CONSULTANT (Parent 2)
├─ Slot: WORK-LOCATION (Default: Client Site)
├─ Slot: HOURLY-RATE (Default: $75/hour)

EMPLOYEE-CONSULTANT (Multiple Inheritance)
├─ Inheritance order: EMPLOYEE, CONSULTANT
├─ WORK-LOCATION: Uses EMPLOYEE's default (Office)
│  (first parent's definition takes precedence)
├─ SALARY: Uses EMPLOYEE's default ($40,000)
└─ HOURLY-RATE: Uses CONSULTANT's default ($75/hour)
```

**Non-Monotonic Inheritance (Exceptions):**

Real-world knowledge often includes exceptions to inherited properties.

```
BIRD (Parent)
├─ Slot: CAN-FLY (Default: Yes)
└─ Slot: WINGS (Default: Yes)
    │
    ├─ Normal inheritance
    │       ▼
    │   ROBIN (inherited: CAN-FLY = Yes)
    │
    └─ Exception handling
            ▼
        PENGUIN
        ├─ Inherited: WINGS = Yes (normal)
        ├─ Override: CAN-FLY = No (exception!)
        └─ New: SWIMS = Yes (adapted for exception)
```

**Inheritance Benefits:**

```
1. Code/Knowledge Reuse:
   Define properties once in parent
   All children automatically have them

2. Reduced Redundancy:
   DEFAULT-BEHAVIOR defined in VEHICLE
   CAR, TRUCK, MOTORCYCLE inherit it
   No need to repeat for each subclass

3. Efficient Updates:
   Change property in parent
   All children reflect the change
   Except for explicit overrides

4. Hierarchical Organization:
   Knowledge organized by generality
   Reflects natural conceptual structure

5. Specialization Support:
   Create specific knowledge types
   by inheriting and overriding
   defaults from general types
```

**Inheritance Implementation:**

```
Algorithm: GET-VALUE(frame, slot)
1. Check if frame instance has explicit value for slot
   If yes: return value
2. Check if frame class defines default for slot
   If yes: return default
3. Check if parent frame defines slot
   If yes: recursively GET-VALUE(parent, slot)
4. If multiple parents, use priority order
5. If no value found in hierarchy: return Unknown

Algorithm: SET-VALUE(frame, slot, value)
1. Validate value against slot constraints
2. Execute If-added procedures
3. Store value in frame instance
4. Execute If-modified triggers
```

Frame inheritance provides a powerful mechanism for organizing knowledge hierarchically, enabling defaults while allowing flexibility for exceptions and specializations.

---

### 3. Apply: Create Frame Structure
**Question:** Represent a stereotypical object or event using a frame structure.

**Your Response:**

**Restaurant Dining Event Frame Structure**

```
Frame: RESTAURANT-VISIT (Stereotypical Dining Event)

Slots and Facets:

Slot: RESTAURANT
├─ Type: Frame reference → RESTAURANT
├─ Default: Unknown
├─ Required: Yes
└─ Constraints: Must be operational

Slot: DINER
├─ Type: Frame reference → PERSON
├─ Default: Unknown
├─ Required: Yes
└─ Cardinality: 1 or more

Slot: ARRIVAL-TIME
├─ Type: Time
├─ Default: Current time
├─ Range: Restaurant operating hours
└─ If-added: NOTIFY-MAÎTRE-D()

Slot: SEATING
├─ Type: Enumerated {Indoor, Outdoor, Bar}
├─ Default: Indoor
└─ If-modified: ADJUST-NOISE-LEVEL()

Slot: PARTY-SIZE
├─ Type: Integer
├─ Default: 1
├─ Range: 1-20
└─ If-added: CHECK-TABLE-AVAILABILITY()

Slot: DINING-TIME-ESTIMATE
├─ Type: Duration
├─ Default: 60 minutes
├─ If-needed: ESTIMATE-DURATION(RESTAURANT, MEAL-TYPE)
└─ If-modified: UPDATE-NEXT-SEATING()

Slot: MENU-ITEM
├─ Type: List of Frame references → DISH
├─ Default: House recommendations
├─ If-added: CALCULATE-TOTAL-PRICE()
└─ If-added: CHECK-DIETARY-RESTRICTIONS()

Slot: BEVERAGES
├─ Type: List of Frame references → DRINK
├─ Default: Water
└─ If-added: SUGGEST-WINE-PAIRING()

Slot: SPECIAL-REQUESTS
├─ Type: String
├─ Default: None
└─ If-added: NOTIFY-KITCHEN()

Slot: BILL-TOTAL
├─ Type: Currency
├─ Default: Unknown
├─ If-needed: CALCULATE-TOTAL()
└─ Constraints: Must be positive

Slot: PAYMENT-METHOD
├─ Type: Enumerated {Cash, Credit, Debit}
├─ Default: Credit
└─ If-added: PROCESS-PAYMENT()

Slot: TIP-AMOUNT
├─ Type: Currency
├─ Default: 18% of BILL-TOTAL
├─ If-added: ACKNOWLEDGE-GRATUITY()
└─ Range: 0-50% of BILL-TOTAL

Slot: EXPERIENCE-RATING
├─ Type: Integer
├─ Range: 1-5 stars
├─ Default: Unknown
└─ If-added: STORE-REVIEW(), EMAIL-SATISFACTION()

Slot: DURATION-ACTUAL
├─ Type: Duration
├─ If-needed: CALCULATE(DEPARTURE-TIME - ARRIVAL-TIME)
└─ Constraints: > 15 min, < 4 hours

Parent Frame: EVENT
├─ Inherited: DURATION, LOCATION, PARTICIPANTS
└─ Inherited: DATE, TIME

Associated Frames:
├─ RESTAURANT (where event occurs)
├─ PERSON (participants)
├─ DISH (items consumed)
└─ PAYMENT-TRANSACTION (financial aspect)

Methods:
├─ MAKE-RESERVATION()
├─ UPDATE-RESERVATION()
├─ CANCEL-RESERVATION()
├─ REQUEST-TABLE()
├─ ORDER-FOOD()
├─ REQUEST-BILL()
├─ LEAVE-REVIEW()
└─ SUGGEST-NEARBY-RESTAURANT()
```

**Related Frame: RESTAURANT**

```
Frame: RESTAURANT

Slot: NAME
├─ Type: String
├─ Required: Yes
└─ Constraints: Non-empty, unique

Slot: CUISINE-TYPE
├─ Type: List of Enumerated values
├─ Default: [American]
└─ Options: Italian, French, Asian, Mexican, etc.

Slot: LOCATION
├─ Type: Address
├─ Required: Yes
└─ If-modified: UPDATE-DIRECTIONS()

Slot: PHONE
├─ Type: String
├─ Format: (XXX) XXX-XXXX
└─ If-added: ENABLE-RESERVATIONS()

Slot: OPERATING-HOURS
├─ Type: Schedule
├─ Default: 11AM-11PM daily
└─ Exceptions: CLOSED-DAYS list

Slot: PRICE-RANGE
├─ Type: Enumerated {Budget, Moderate, Expensive, Luxury}
├─ Default: Moderate
└─ If-needed: ESTIMATE-COST-PER-PERSON()

Slot: SEATING-CAPACITY
├─ Type: Integer
├─ Default: 50
└─ Range: 10-500

Slot: AVAILABLE-TABLES
├─ Type: List of Table objects
├─ Default: All tables
└─ If-modified: UPDATE-RESERVATION-SYSTEM()

Slot: PARKING
├─ Type: Enumerated {Valet, Lot, Street, None}
├─ Default: Street
└─ Cost: Currency

Slot: DRESS-CODE
├─ Type: Enumerated {Casual, Smart Casual, Business, Formal}
├─ Default: Casual
└─ If-added: NOTIFY-DINER()

Parent Frame: ESTABLISHMENT
├─ Inherited: REVIEWS, MANAGER, WEBSITE
└─ Inherited: RATING, PHONE, ADDRESS

Methods:
├─ ACCEPT-RESERVATION()
├─ CHECK-AVAILABILITY()
├─ UPDATE-MENU()
├─ GET-RECOMMENDATIONS()
└─ PROCESS-PAYMENT()
```

**Example Instance: "John's Dinner Tonight"**

```
Frame: JOHN-DINNER (Instance of RESTAURANT-VISIT)

Instance Values:
├─ RESTAURANT: → ITALIAN-BISTRO frame
├─ DINER: → JOHN frame
├─ ARRIVAL-TIME: 7:00 PM
├─ PARTY-SIZE: 2
├─ SEATING: Outdoor
├─ MENU-ITEM: [Pasta Carbonara, Risotto Milanese]
├─ BEVERAGES: [Chianti wine, Sparkling water]
├─ SPECIAL-REQUESTS: "No peanuts (allergy)"
├─ PAYMENT-METHOD: Credit card
├─ DINING-TIME-ESTIMATE: 90 minutes (computed)
├─ DURATION-ACTUAL: 95 minutes (after completion)
├─ BILL-TOTAL: $85.50
├─ TIP-AMOUNT: $15.35
├─ EXPERIENCE-RATING: 5 stars
└─ DEPARTURE-TIME: 8:35 PM
```

This frame effectively captures the stereotypical structure of a dining event, with reasonable defaults, flexible slots for specific instances, and procedures that trigger appropriate actions.

---

### 4. Analyze: Frames vs. Semantic Networks
**Question:** Compare and contrast frames with semantic networks.

**Your Response:**

| **Aspect** | **Frames** | **Semantic Networks** |
|---|---|---|
| **Structure** | Structured attributes in containers | Simple nodes and edges |
| **Organization** | Object-oriented with slots and facets | Graph-based with nodes and links |
| **Default Values** | Built-in, explicit defaults per slot | Implicit defaults through inheritance |
| **Inheritance** | Multiple inheritance with override | Parent-child class hierarchies |
| **Attribute Definition** | Detailed through facets (type, range, constraints) | Simple labeled edges |
| **Attached Procedures** | If-added, if-modified, if-needed procedures | No direct procedure attachment |
| **Type Specification** | Strong typing via Type facets | Loose or untyped |
| **Scalability** | Better for complex entity representation | Better for relationship visualization |
| **Reasoning Complexity** | Object-oriented reasoning paradigm | Network traversal and inheritance |
| **Knowledge Acquisition** | Easier to structure complex domains | Easier initial conceptualization |

**Key Differences:**

**1. Structural Formality**

**Frames:**
```
Frame: CAR
├─ Slot: WHEELS (Type: Integer, Default: 4, Range: 3-6)
├─ Slot: ENGINE (Type: Engine-type, Default: V6)
└─ Slot: COLOR (Type: String, Default: Black)
```

**Semantic Networks:**
```
    Car ──has──> Wheels
    Car ──has──> Engine
    Car ──has──> Color
(No type info or constraints visible)
```

**2. Procedure Attachment**

**Frames:**
```
Slot: PRICE
├─ If-added: CALCULATE-TAX()
├─ If-modified: UPDATE-INVENTORY()
└─ If-needed: ESTIMATE-MARKET-PRICE()
```

**Semantic Networks:**
- No standard way to attach procedures
- Requires external implementation

**3. Attribute Specification Detail**

**Frames:** Highly detailed facet definitions
**Semantic Networks:** Simple labeled relationships

**4. Computational Efficiency**

| Task | Frames | Semantic Networks |
|---|---|---|
| Finding entity properties | O(1) - direct slot access | O(n) - follow edges |
| Inheritance resolution | O(d) - depth of hierarchy | O(d) - path traversal |
| Type validation | O(1) - check facet constraints | Manual, not automated |
| Procedure execution | Built-in | External implementation |

**When Frames Excel:**

✓ Detailed object/entity representation
✓ Complex attribute specification
✓ Required type checking and constraints
✓ Need for attached procedures/methods
✓ Object-oriented design problems

**When Semantic Networks Excel:**

✓ Relationship-rich domains
✓ Visual knowledge representation
✓ Quick prototyping
✓ Emphasizing inheritance hierarchies
✓ Domains with varied relationship types

**Hybrid Approach:**

Modern knowledge systems often combine both:
- Use **frames** for entity representation
- Use **semantic networks** for relationship visualization
- Use **frame inheritance** for class hierarchies
- Use **network edges** for non-hierarchical associations

---

### 5. Evaluate: Suitability
**Question:** Discuss the suitability of frames for representing specific types of knowledge.

**Your Response:**

Frames are particularly suitable for specific knowledge domains and representation needs. Their effectiveness varies based on knowledge characteristics, domain structure, and application requirements.

**Highly Suitable Domains:**

**1. Stereotypical Objects (Excellent Match)**

Frames excel at representing objects with clear, defining characteristics:
- Medical records (standard patient attributes)
- Product descriptions (standardized properties)
- Vehicle specifications (model-dependent features)
- Personnel profiles (consistent employee attributes)

**2. Complex Entities with Multiple Attributes (Excellent)**

Frames handle complex attribute sets better than alternatives:
- Hospital patient: demographics, medical history, current medications, allergies, test results
- Scientific researcher: education, publications, grants, institutional affiliation
- Agricultural farm: location, soil type, water availability, crop history, equipment

**3. Hierarchical Knowledge (Excellent)**

Frame inheritance effectively captures specialization:
- Organizational hierarchies
- Product families (Car → Sedan → Honda Civic)
- Biological taxonomy
- Disease classification

**4. Default-Based Reasoning (Very Good)**

Frames' default mechanism matches real-world reasoning:
- "Typical dog has 4 legs" (default)
- "Most restaurants are open for lunch" (default)
- "Standard student takes 4-5 courses" (default)
- Exceptions explicitly override defaults

**5. Constrained Values (Very Good)**

Frames excel when attributes have specific constraints:
- Age: Integer, 0-120 range
- Grade: Enumerated {A, B, C, D, F}
- GPA: Float, 0.0-4.0 range
- Price: Currency, > 0

**Moderately Suitable Domains:**

**6. Procedural Knowledge (Moderate)**

Frames can include procedures, making them suitable for:
- Workflow representation
- Event-triggered actions
- System control

However, logic-based systems are often better for complex procedural knowledge.

**7. Relationship-Heavy Domains (Moderate)**

While frames handle relationships through slots, semantic networks may be better for:
- Social networks (emphasis on connections)
- Knowledge graphs (focus on relationships)
- Ontologies (relationship taxonomy)

**Less Suitable Domains:**

**8. Highly Dynamic Knowledge (Poor)**

Frames are less suitable when:
- Attributes change frequently
- Structure varies significantly per instance
- Little standardization exists

Example: Real-time sensor data, stock market information

**9. Complex Logical Reasoning (Poor)**

Frames lack formal logical semantics needed for:
- Mathematical proofs
- Constraint satisfaction
- Complex conditional logic

First-order logic is better suited for these.

**10. Unstructured Information (Poor)**

Frames are inappropriate for:
- Free-form text
- Natural language understanding
- Completely heterogeneous data

Domain-specific languages or NLP approaches are better.

**Comparative Suitability Matrix:**

| Domain Type | Frames | FOL | Semantic Networks | Rules |
|---|---|---|---|---|
| Stereotypical objects | ✓✓✓ | ✓✓ | ✓✓ | ✓ |
| Complex entities | ✓✓✓ | ✓✓ | ✓ | ✓ |
| Hierarchies | ✓✓✓ | ✓✓ | ✓✓✓ | ✓✓ |
| Default reasoning | ✓✓✓ | ✓ | ✓✓ | ✓✓✓ |
| Constrained values | ✓✓✓ | ✓✓✓ | ✗ | ✓✓ |
| Procedures | ✓✓ | ✓ | ✗ | ✓✓✓ |
| Relationships | ✓✓ | ✓✓✓ | ✓✓✓ | ✓✓ |
| Logical reasoning | ✗ | ✓✓✓ | ✗ | ✓✓ |
| Uncertainty | ✓ | ✓ | ✓✓ | ✓✓✓ |
| Performance | ✓✓✓ | ✓ | ✓✓ | ✓✓✓ |

**Real-World Application Assessment:**

**Ideal Frame Applications:**
- Medical diagnosis systems
- Student information systems
- Product catalogs
- Personnel management
- Building information systems

**Challenging Frame Applications:**
- Real-time recommendation engines
- Continuous sensor monitoring
- Complex constraint solving
- Theorem proving

---

### 6. Create: Interconnected Frames
**Question:** Design a set of interconnected frames to represent a common scenario.

**Your Response:**

**E-Commerce Shopping Scenario - Interconnected Frame System**

```
SHOPPING-TRANSACTION Frame
├─ Links to: CUSTOMER → PRODUCT → PAYMENT
├─ Slot: CUSTOMER
│  └─ Type: Frame reference → CUSTOMER frame
├─ Slot: ITEMS
│  └─ Type: List of Frame references → PRODUCT-ORDER frame
├─ Slot: TOTAL-PRICE
│  └─ If-needed: SUM(ITEMS.PRICE)
└─ Slot: DELIVERY-STATUS
   └─ Type: Enumerated {Pending, Shipped, Delivered}

CUSTOMER Frame
├─ Slot: NAME
├─ Slot: ADDRESS → SHIPPING-ADDRESS frame
├─ Slot: PAYMENT-METHOD → PAYMENT frame
├─ Slot: PURCHASE-HISTORY → List of SHOPPING-TRANSACTION
└─ Methods: UPDATE-ADDRESS(), VIEW-ORDERS()

PRODUCT Frame
├─ Slot: SKU
├─ Slot: CATEGORY → PRODUCT-CATEGORY frame
├─ Slot: PRICE (Type: Currency, If-added: CHECK-STOCK())
├─ Slot: INVENTORY → INVENTORY-LEVEL frame
└─ Methods: GET-RECOMMENDATIONS()

PRODUCT-ORDER Frame (Instance-specific)
├─ Parent: PRODUCT
├─ Slot: QUANTITY
├─ Slot: UNIT-PRICE
├─ Slot: DISCOUNT
└─ Methods: APPLY-COUPON()

Relationship Chain:
CUSTOMER --(purchases)--> SHOPPING-TRANSACTION
                                      │
                                     has
                                      │
                         PRODUCT-ORDER --(references)--> PRODUCT
                                      │
                                   includes
                                      │
                         PAYMENT --(processes)--> PAYMENT-TRANSACTION
```

This design demonstrates how frames interconnect through references, enabling complex system modeling through linked frame relationships.

---

## Capstone Assignment

### Task: Develop a frame-based representation for a "Student" entity, including relevant slots, facets, and default values.

**Your Submission:**

**STUDENT Frame-Based System**

```
Frame: PERSON (Parent Class)
├─ Slot: NAME
│  ├─ Type: String
│  ├─ Required: Yes
│  └─ Constraints: Non-empty
├─ Slot: DATE-OF-BIRTH
│  ├─ Type: Date
│  └─ If-added: CALCULATE-AGE()
├─ Slot: ADDRESS
│  ├─ Type: Address Structure
│  ├─ Default: Unknown
│  └─ If-modified: UPDATE-CONTACT-INFO()
└─ Slot: EMAIL
   ├─ Type: Email
   └─ If-added: SEND-WELCOME-EMAIL()


Frame: STUDENT (Inherits from PERSON)
├─ Inherited Slots: NAME, DATE-OF-BIRTH, ADDRESS, EMAIL
│
├─ NEW SLOTS:
│
├─ Slot: STUDENT-ID
│  ├─ Type: String
│  ├─ Format: S[0-9]{6}
│  ├─ Required: Yes
│  ├─ Default: Auto-generated
│  └─ Constraints: Unique
│
├─ Slot: ENROLLMENT-DATE
│  ├─ Type: Date
│  ├─ Default: Current date
│  └─ If-added: CREATE-ACADEMIC-RECORD()
│
├─ Slot: MAJOR
│  ├─ Type: Frame reference → DISCIPLINE
│  ├─ Default: Undeclared
│  ├─ If-added: UPDATE-MAJOR-REQUIREMENTS()
│  └─ If-modified: RESET-PROGRESS-TRACKER()
│
├─ Slot: MINOR
│  ├─ Type: Frame reference → DISCIPLINE
│  ├─ Default: None
│  └─ Optional: True
│
├─ Slot: ENROLLMENT-STATUS
│  ├─ Type: Enumerated {Full-time, Part-time, Suspended, Graduated}
│  ├─ Default: Full-time
│  └─ If-modified: UPDATE-TUITION-RATE()
│
├─ Slot: ACADEMIC-STANDING
│  ├─ Type: Enumerated {Good, Warning, Probation, Dismissed}
│  ├─ Default: Good
│  ├─ If-needed: EVALUATE-STANDING()
│  └─ If-modified: NOTIFY-ADVISOR(), SEND-ALERT()
│
├─ Slot: GPA
│  ├─ Type: Float
│  ├─ Range: 0.0 - 4.0
│  ├─ Default: 0.0
│  ├─ If-needed: CALCULATE-CUMULATIVE-GPA()
│  ├─ If-modified: UPDATE-STANDING()
│  └─ Precision: 2 decimal places
│
├─ Slot: CREDITS-EARNED
│  ├─ Type: Integer
│  ├─ Default: 0
│  ├─ Range: 0-150
│  ├─ If-needed: SUM(COURSES.CREDITS WHERE GRADE ≠ F)
│  └─ If-modified: CHECK-GRADUATION-ELIGIBILITY()
│
├─ Slot: CREDITS-REQUIRED
│  ├─ Type: Integer
│  ├─ Default: 120
│  ├─ If-needed: LOOKUP(MAJOR.REQUIREMENTS)
│  └─ Constraints: ≤ CREDITS-EARNED for graduation
│
├─ Slot: COURSES-TAKEN
│  ├─ Type: List of Frame references → COURSE-ENROLLMENT
│  ├─ Default: Empty list
│  ├─ Cardinality: 1 or more (after first semester)
│  └─ If-added: UPDATE-TRANSCRIPT()
│
├─ Slot: CURRENT-COURSES
│  ├─ Type: List of Frame references → COURSE
│  ├─ Default: Empty list
│  ├─ If-added: ENABLE-ATTENDANCE-TRACKING()
│  └─ Constraints: Max 5 courses per semester
│
├─ Slot: ADVISOR
│  ├─ Type: Frame reference → FACULTY
│  ├─ Default: Automatically assigned
│  ├─ If-added: NOTIFY-ADVISOR()
│  └─ If-modified: NOTIFY-OLD-AND-NEW-ADVISOR()
│
├─ Slot: FINANCIAL-AID
│  ├─ Type: Frame reference → FINANCIAL-AID-PACKAGE
│  ├─ Default: None
│  └─ If-modified: UPDATE-PAYMENT-SCHEDULE()
│
├─ Slot: TUITION-PAID
│  ├─ Type: Currency
│  ├─ Default: 0
│  ├─ If-needed: SUM(PAYMENTS)
│  └─ If-modified: UPDATE-ACCOUNT-BALANCE()
│
├─ Slot: DISCIPLINARY-RECORD
│  ├─ Type: List of Incident records
│  ├─ Default: Empty list
│  ├─ If-added: ASSESS-IMPACT(), NOTIFY-PARENT()
│  └─ Constraints: Confidential, restricted access
│
├─ Slot: SPECIAL-ACCOMMODATIONS
│  ├─ Type: String
│  ├─ Default: None
│  ├─ If-added: NOTIFY-FACULTY()
│  └─ Constraints: Requires documentation
│
├─ Parent Frame: PERSON
│  └─ Inherited: All PERSON slots and methods
│
├─ Sub-Frames/Associated Frames:
│  ├─ COURSE-ENROLLMENT → course instance, grade, semester
│  ├─ DISCIPLINE → major/minor requirements
│  ├─ FINANCIAL-AID-PACKAGE → loans, grants, scholarships
│  └─ FACULTY → advisor information
│
└─ Methods:
   ├─ REGISTER-FOR-COURSE(course)
   ├─ DROP-COURSE(course)
   ├─ ADD-COURSE(course)
   ├─ VIEW-TRANSCRIPT()
   ├─ REQUEST-GRADE-APPEAL()
   ├─ CHANGE-MAJOR(new-major)
   ├─ CHECK-GRADUATION-READINESS()
   └─ REQUEST-ACADEMIC-STANDING-REVIEW()


Frame: COURSE-ENROLLMENT (Student's course instance)
├─ Parent: COURSE
├─ Slot: STUDENT-ID
│  └─ Type: Frame reference → STUDENT
├─ Slot: SEMESTER
│  ├─ Type: Enumerated {Fall, Spring, Summer}
│  ├─ Format: "{Season}{Year}"
│  └─ Example: "Fall2025"
├─ Slot: GRADE
│  ├─ Type: Enumerated {A, B, C, D, F, W, I}
│  ├─ Default: In-Progress
│  ├─ If-added: UPDATE-GPA()
│  └─ If-modified: UPDATE-STANDING()
└─ Slot: COMPLETION-DATE
   ├─ Type: Date
   └─ If-needed: End of semester date


Frame: DISCIPLINE (Major/Minor framework)
├─ Slot: DISCIPLINE-CODE
│  ├─ Type: String
│  ├─ Format: "[A-Z]{2,3}[0-9]{3}"
│  └─ Example: "CS101" or "BIO"
├─ Slot: NAME
│  └─ Type: String
├─ Slot: REQUIRED-CREDITS
│  ├─ Type: Integer
│  ├─ Range: 20-60
│  └─ Default: 40
├─ Slot: CORE-COURSES
│  └─ Type: List of COURSE frames
└─ Slot: ELECTIVE-REQUIREMENTS
   ├─ Type: Structure
   └─ Contains: Credit count and course choices


EXAMPLE INSTANCE: "alice-student"

Frame: ALICE-STUDENT (Instance of STUDENT)
├─ Instance-of: STUDENT
│
├─ ACTUAL VALUES:
│  ├─ NAME: "Alice Johnson"
│  ├─ DATE-OF-BIRTH: 2005-03-15
│  ├─ EMAIL: "alice.johnson@university.edu"
│  ├─ ADDRESS: "123 Oak Street, City, State 12345"
│  ├─ STUDENT-ID: "S203567"
│  ├─ ENROLLMENT-DATE: 2023-09-01
│  ├─ MAJOR: → Computer Science DISCIPLINE frame
│  ├─ MINOR: → Mathematics DISCIPLINE frame
│  ├─ ENROLLMENT-STATUS: Full-time
│  ├─ ACADEMIC-STANDING: Good
│  ├─ GPA: 3.75
│  ├─ CREDITS-EARNED: 45
│  ├─ CREDITS-REQUIRED: 120
│  ├─ CURRENT-COURSES: [CS201, MATH301, PHYS101, ENG202]
│  ├─ ADVISOR: → Prof. Dr. Smith FACULTY frame
│  ├─ COURSES-TAKEN: [
│  │   → CS101 (Grade: A)
│  │   → MATH101 (Grade: A)
│  │   → ENG101 (Grade: B+)
│  │   → PHYS101 (Grade: A-)
│  │   → CS102 (Grade: A)
│  │   ... more courses ...
│  │ ]
│  ├─ FINANCIAL-AID: → Merit Scholarship frame
│  ├─ TUITION-PAID: 15000.00
│  ├─ DISCIPLINARY-RECORD: Empty
│  └─ SPECIAL-ACCOMMODATIONS: "Extended test-taking time (documented)"
│
└─ COMPUTED VALUES (If-needed procedures):
   ├─ ACADEMIC-STANDING: Computed from GPA
   ├─ GPA: Computed from COURSES-TAKEN grades
   └─ GRADUATION-ELIGIBLE: Computed from CREDITS-EARNED vs CREDITS-REQUIRED
```

**Frame Design Explanation:**

**1. Inheritance Structure:**
STUDENT inherits from PERSON, reusing personal information slots while adding academic-specific attributes.

**2. Complex Facet Usage:**
Slots use comprehensive facets (Type, Default, Range, If-added, If-modified, If-needed) to ensure data integrity and trigger appropriate actions.

**3. Multi-level References:**
Frame references enable linking to related frames (COURSE, DISCIPLINE, FACULTY) creating a cohesive knowledge system.

**4. Computed Values:**
If-needed procedures allow GPA, standing, and graduation eligibility to be computed on-demand rather than stored.

**5. Event Triggers:**
If-added and If-modified procedures ensure consistency (e.g., grade changes trigger GPA recalculation and standing re-evaluation).

**6. Instance Flexibility:**
Demonstrates how the frame template accommodates specific student instances with actual data while maintaining structure.

---

## References (APA 7)

Minsky, M. L. (1975). A framework for representing knowledge. In P. H. Winston (Ed.), *The psychology of computer vision* (pp. 211-277). McGraw-Hill.

Minsky, M. L. (1981). A framework for representing knowledge. *Mind Design*, 2, 95-128.

Brachman, R. J., & Schmolze, J. G. (1985). An overview of the KL-ONE knowledge representation system. *Journal of Cognitive Science*, 9(2), 171-216.

Rumelhart, D. E., & Norman, D. A. (1985). Representation of knowledge. In A. M. Aitkenhead & J. M. Slack (Eds.), *Issues in cognitive modeling* (pp. 15-78). Lawrence Erlbaum Associates.

Quillian, M. R., & Collins, A. M. (1969). Retrieval time from long-term memory. *Journal of Verbal Learning and Verbal Behavior*, 8(2), 240-247.

Bobrow, D. G., & Winograd, T. (1977). An overview of KRL, a knowledge representation language. *Cognitive Science*, 1(1), 3-46.

---

**Status:** Complete
**Date Completed:** 2026-03-18

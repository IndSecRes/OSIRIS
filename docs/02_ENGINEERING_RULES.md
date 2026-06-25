# OSIRIS Engineering Rules & Design Principles

Open Source Intelligence Research & Investigation System

Version 1.0

---

# 1. Purpose

This document defines the permanent engineering principles governing OSIRIS development.

The purpose is to ensure that future modules, agents, models, databases, and capabilities integrate into OSIRIS without damaging the intelligence architecture.

OSIRIS is not developed as a collection of features.

OSIRIS is developed as an intelligence operating system.

---

# 2. Core Engineering Philosophy

OSIRIS follows:

```text
Evidence
    ↓
Structured Intelligence Objects
    ↓
Knowledge Graph
    ↓
Reasoning
    ↓
Investigation Intelligence
```

Every engineering decision must strengthen this flow.

---

# 3. OSIRIS Is Not

OSIRIS is not:

- A chatbot
- A search engine
- A scraper
- A collection of AI models
- A single autonomous agent
- A workflow automation script

---

# 4. OSIRIS Is

OSIRIS is:

An Intelligence Runtime Environment.

Where:

- Models provide perception
- Entities represent reality
- Evidence supports claims
- Graphs preserve relationships
- Agents execute investigations
- Memory improves performance
- Humans make final decisions

---

# 5. Entity First Principle

## Highest Priority Rule

Entities are the foundation of OSIRIS intelligence.

Everything connects to entities.

Examples:

- People
- Organizations
- Locations
- Domains
- Devices
- Wallets
- Documents
- Events

### Rule

Text is not identity.

Incorrect:

```text
"John Smith"
```

Correct:

```text
Entity ID:
ENT-8F72A91

Display:
John Smith
```

---

# 6. Entity Identity Rule

All intelligence objects must use:

```text
entity_id
```

Never:

```text
entity.text
```

for identity matching.

Text is only:

- Display
- Search
- Human readability

---

# 7. Single Source of Truth Rule

Every major intelligence object must have one owner.

Examples:

```text
Entity      → core/entity.py
Graph       → graph/
Evidence    → evidence/
Case        → case/
```

No duplicated definitions.

---

# 8. No Duplicate Schema Rule

Never create temporary structures like:

```python
{
    "text": "",
    "label": "",
    "confidence": ""
}
```

inside random modules.

Use canonical objects:

- Entity()
- Observation()
- Case()
- Relationship()
- Evidence()

from the core schema layer.

---

# 9. Model Ownership Rule

Models do not own intelligence.

Models generate candidates.

```text
spaCy / GLiNER / Flair / DeBERTa
                ↓
        Entity Candidate
                ↓
      OSIRIS Resolution
                ↓
       Canonical Entity
```

OSIRIS owns identity.

---

# 10. LLM Governance Rule

LLMs cannot directly control OSIRIS decisions.

Correct:

```text
LLM
 ↓
Hypothesis
 ↓
OSIRIS Validation
 ↓
Decision
```

Incorrect:

```text
LLM
 ↓
Automatic Intelligence Output
```

---

# 11. Pipeline Rule

Pipeline files orchestrate.

They do not become intelligence engines.

### Pipeline Responsibilities

Allowed:

- Call modules
- Manage flow
- Coordinate execution

Not Allowed:

- Extract entities
- Calculate intelligence
- Store data
- Perform reasoning

---

# 12. Service Ownership Rule

Future architecture:

```text
core/
services/
processing/
graph/
evidence/
agents/
memory/
reports/
```

Each layer owns its responsibility.

---

# 13. Data Processing vs Intelligence Rule

Separate:

## Data Processing

Handles:

- Extraction
- Cleaning
- Normalization
- Storage

## Intelligence

Handles:

- Scoring
- Correlation
- Prioritization
- Reasoning

Never mix them.

---

# 14. Evidence First Rule

Every intelligence conclusion must trace back to evidence.

Incorrect:

```text
Assumption
 ↓
Decision
```

Correct:

```text
Evidence
 ↓
Entity
 ↓
Relationship
 ↓
Reasoning
 ↓
Conclusion
```

---

# 15. Provenance Rule

Every intelligence object should eventually contain:

```json
{
  "source": "",
  "created_by": "",
  "timestamp": "",
  "transformation": "",
  "confidence": ""
}
```

OSIRIS must always know:

- Where did this come from?
- How was it created?

---

# 16. Confidence Rule

Confidence is not a single number.

Future confidence should include:

- Source reliability
- Model confidence
- Entity agreement
- Evidence quality
- Temporal consistency
- Relationship strength

Confidence must be layered.

---

# 17. Agent Rule

Agents are workers.

They are not the intelligence system.

Agents:

- Execute tasks
- Call tools
- Gather evidence
- Create investigation traces

Agents do not replace:

- Graph
- Entity system
- Evidence system

---

# 18. Skill Rule

Capabilities should become reusable skills.

A skill contains:

- Purpose
- Procedure
- Tools
- Permissions
- Validation
- Examples
- Memory

Skills should be:

- Versioned
- Measurable
- Improvable

---

# 19. Memory Rule

OSIRIS memory is structured.

Types:

## Knowledge Memory

What is known?

## Graph Memory

How things connect?

## Case Memory

How investigations happened?

## Episodic Memory

What events occurred?

## Trajectory Memory

Which actions worked?

---

# 20. Database Rule

Storage should never define intelligence.

Database stores:

- Entities
- Evidence
- Relationships
- Events

Intelligence logic remains in OSIRIS engines.

---

# 21. Visualization Rule

UI is a view layer.

UI must not contain:

- Intelligence logic
- Entity decisions
- Scoring
- Investigation rules

Correct:

```text
Engine
 ↓
API / Service
 ↓
UI
```

---

# 22. Refactor Rule

Do not refactor because code looks imperfect.

Refactor when:

- Ownership is unclear
- Duplication appears
- Intelligence logic leaks
- Scaling is blocked

---

# 23. Development Order Rule

Preferred development order:

```text
Entity
 ↓
Evidence
 ↓
Graph
 ↓
Case Intelligence
 ↓
Timeline
 ↓
Reporting
 ↓
Agents
 ↓
Skills
 ↓
Memory
 ↓
Learning
```

---

# 24. AI Evolution Rule

Future AI additions must strengthen OSIRIS.

Not replace OSIRIS.

Correct:

```text
AI improves investigation capability
```

Incorrect:

```text
AI becomes the investigation system
```

---

# 25. Final Engineering Principle

The system must always move toward:

```text
Raw Information
 ↓
Evidence
 ↓
Knowledge
 ↓
Understanding
 ↓
Investigation
 ↓
Intelligence
```

OSIRIS is built as an intelligence ecosystem.

Not a software collection.

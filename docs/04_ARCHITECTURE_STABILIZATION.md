# OSIRIS Architecture Stabilization & Refactor Plan

Open Source Intelligence Research & Investigation System

Version 1.0

Architectural Governance Document

---

# 1. Purpose

This document defines the architectural stabilization strategy for OSIRIS.

OSIRIS has evolved from a prototype intelligence processing system into a modular intelligence platform.

The purpose of this document is to:

- Prevent architectural drift
- Maintain module ownership
- Avoid duplicated intelligence logic
- Preserve explainability
- Prepare OSIRIS for future scaling

The goal is not immediate rewriting.

The goal is controlled evolution.

---

# 2. Current Architectural State

Current Intelligence Flow:

```text
INPUT
    ↓
Observation Extraction
    ↓
Multi Model NER
(spaCy / GLiNER / Flair / DeBERTa)
    ↓
Entity Fusion
    ↓
Canonical Entities
    ↓
Case Engine
    ↓
Knowledge Graph
    ↓
Signal Engine
    ↓
Investigator View
    ↓
Reporting
```

Current system capability:

- Entity extraction
- Entity fusion
- Case intelligence
- Graph relationships
- Signal scoring
- Temporal foundations
- Investigation interface

The system works.

The current challenge is ownership.

---

# 3. Primary Architectural Principle

OSIRIS must separate:

## Data Processing

Responsible for:

- Extraction
- Normalization
- Storage
- Transformation

## Intelligence Processing

Responsible for:

- Scoring
- Reasoning
- Prioritization
- Relationship analysis
- Investigation decisions

These layers must not merge.

---

# 4. Entity Authority Layer

Priority: CRITICAL

Entity is the central intelligence object in OSIRIS.

Current flow:

```text
NER Models
    ↓
entity_fusion.py
    ↓
Case Entities
    ↓
Graph
```

Problem:

Multiple modules interpret entities differently.

Examples:

- Model confidence
- Fusion confidence
- Case confidence
- Graph importance

These are different intelligence signals.

### Future Authority Model

```text
EntityCandidate
    ↓
Entity Resolution Engine
    ↓
OSIRIS Entity
       ↙      ↘
    Case      Graph
```

Canonical Entity Ownership:

```text
core/entity.py
or
core/schemas.py
```

All modules use:

```text
Entity()
```

Never:

```python
{
    "text": "",
    "label": "",
    "confidence": ""
}
```

---

# 5. Graph Ownership Rule

Priority: HIGH

Current risk:

```text
graph/graph_engine.py

processing/graph_engine.py
```

Danger:

Two graph implementations create conflicting intelligence.

### Future Ownership

Only:

```text
graph/
├── engine.py
├── models.py
├── storage.py
└── relationship_engine.py
```

Graph responsibilities:

### YES

- Nodes
- Relationships
- Traversal
- Graph export

### NO

- Extraction
- Entity creation
- Reporting
- UI logic

---

# 6. Pipeline Responsibility

Current risk:

```text
core/pipeline.py
```

is becoming a God Object.

Current responsibilities:

- Extraction
- Case creation
- Persistence
- Graph updates
- Signals
- Output preparation

### Target Design

Pipeline becomes orchestrator only.

```text
OSIRIS Pipeline
      ↓
Observation Service
      ↓
Entity Service
      ↓
Case Service
      ↓
Graph Service
      ↓
Signal Service
      ↓
Reporting Service
```

Pipeline coordinates.

Services execute.

---

# 7. Extractor Refactor Plan

Current extractor responsibilities:

```text
processing/extractor.py
```

Handles:

- Model loading
- spaCy
- Flair
- DeBERTa
- GLiNER
- Telemetry
- Normalization
- Fusion
- Observation creation

Problem:

Too many responsibilities.

### Future Structure

```text
processing/

├── extractor.py

models/
├── spacy_engine.py
├── gliner_engine.py
├── flair_engine.py
└── deberta_engine.py

telemetry/
└── model_monitor.py

fusion/
└── entity_fusion.py
```

Extractor becomes:

Input:

```text
text
```

Output:

```text
Observation
```

---

# 8. Case Engine Isolation

Current problem:

```text
case_builder.py
```

imports extraction internals.

Problem:

Case system knows extraction details.

### Future

Create:

```text
core/entity_access.py
```

Example:

```python
def get_canonical_entities(observation):
    return observation.entities["fused"]
```

Flow:

```text
Extractor
    ↓
Observation
    ↓
Case Builder
    ↓
Case
```

No extractor dependency.

---

# 9. Confidence Engine

Current situation:

Confidence exists in multiple locations.

Examples:

- Model confidence
- Fusion confidence
- Case confidence
- Signal score

### Future

Create:

```text
intelligence/
└── confidence.py
```

Unified object:

```python
ConfidenceScore(
    entity_confidence,
    source_reliability,
    agreement_score,
    temporal_confidence,
    relationship_confidence
)
```

---

# 10. Model Governance

Models must not control intelligence.

Correct:

```text
MODEL
    ↓
Suggestion
    ↓
OSIRIS Validation
    ↓
Decision
```

Incorrect:

```text
LLM
    ↓
OSIRIS Decision
```

Models provide signals.

OSIRIS owns decisions.

---

# 11. Persistence Evolution

Current:

```text
SQLite + JSON
```

Acceptable.

Future:

Separate intelligence objects:

- Cases
- Entities
- Aliases
- Observations
- Relationships
- Events
- Evidence
- Provenance

Migration path:

```text
SQLite
    ↓
PostgreSQL
    ↓
Neo4j / Graph Database
```

---

# 12. Refactor Priority Order

Do not refactor everything.

### Phase 1 — Foundation Stabilization

1. Remove duplicate graph ownership
2. Complete Entity Authority Layer
3. Centralize schemas
4. Remove extractor dependency from case layer

### Phase 2 — Intelligence Separation

Create:

```text
intelligence/
├── entity_resolution.py
├── confidence.py
└── relationship_engine.py
```

### Phase 3 — Scaling

Create:

```text
storage/
├── graph_store.py
└── entity_store.py
```

### Phase 4 — AI Layer

Create:

```text
reasoning/
├── llm_assistant.py
└── hypothesis_engine.py
```

---

# 13. Architectural Rules

## Rule 1

Entity identity always uses:

```text
entity_id
```

Text is display only.

## Rule 2

Agents do not replace intelligence engines.

Agents orchestrate.

## Rule 3

Models are replaceable.

OSIRIS owns:

- Evidence
- Graph
- Reasoning Flow
- Memory

## Rule 4

Every intelligence object requires:

- Source
- Timestamp
- Confidence
- Provenance

---

# 14. Final Architectural Objective

OSIRIS should evolve into:

An Intelligence Runtime Environment

where:

- Models perceive
- Entities represent reality
- Graphs remember
- Evidence validates
- Agents investigate
- Skills provide expertise
- Memory improves
- Humans decide

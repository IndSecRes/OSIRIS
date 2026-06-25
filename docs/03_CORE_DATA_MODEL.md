# OSIRIS Core Data & Intelligence Model Specification

Open Source Intelligence Research & Investigation System

Version 1.0

Canonical Intelligence Object Definitions

---

# 1. Purpose

This document defines the canonical data structures used by OSIRIS.

The purpose is to establish a single source of truth for intelligence objects.

OSIRIS operates on structured intelligence objects rather than raw text.

The transformation model is:

```text
Raw Information
    ↓
Observation
    ↓
Entity Resolution
    ↓
Evidence
    ↓
Relationships
    ↓
Knowledge Graph
    ↓
Investigation Intelligence
```

---

# 2. Core Design Principles

## Principle 1 — One Object, One Owner

Every intelligence object has one canonical definition.

No module should recreate schemas.

## Principle 2 — Identity First

OSIRIS uses stable identity.

Incorrect:

```text
John Smith
```

Correct:

```text
entity_id: ENT-XXXXXXXX
```

Text is display.

Identity is intelligence.

## Principle 3 — Provenance Required

Every intelligence object should preserve:

- Source
- Timestamp
- Creator
- Transformation History

## Principle 4 — Confidence Is Layered

OSIRIS separates:

```text
Model Confidence
    ↓
Fusion Confidence
    ↓
Entity Confidence
    ↓
Relationship Confidence
    ↓
Investigation Confidence
```

Confidence values should not be mixed.

---

# 3. Entity Object

## Purpose

Represents a real-world object.

Examples:

- Person
- Organization
- Location
- Tool
- Domain
- Device
- Event

## Canonical Entity Schema

```text
Entity
{
    entity_id,

    canonical_name,

    entity_type,

    aliases,

    confidence,

    sources,

    evidence,

    first_seen,

    last_seen,

    metadata,

    lifecycle
}
```

### Key Fields

#### entity_id

Permanent unique identity.

Example:

```text
ENT-982731
```

Never changes.

#### canonical_name

Primary display name.

Example:

```text
Bellingcat
```

#### entity_type

Examples:

```text
PERSON
ORG
LOCATION
TOOL
DOMAIN
EVENT
```

#### aliases

Alternative references.

Example:

```text
GitHub
github.com
GH
```

All resolve to one entity.

---

# 4. Entity Candidate Object

Models do not create entities.

Models create candidates.

Flow:

```text
NER Model
    ↓
Entity Candidate
    ↓
Entity Resolution
    ↓
Canonical Entity
```

Schema:

```text
EntityCandidate
{
    text,

    predicted_type,

    confidence,

    source_model,

    timestamp,

    metadata
}
```

Example:

```text
spaCy:
John Smith
PERSON
0.70

GLiNER:
John Smith
PERSON
0.91
```

Fusion determines identity.

---

# 5. Observation Object

## Purpose

Represents raw intelligence input.

An observation is not yet intelligence.

It is an analyzed input event.

Schema:

```text
Observation
{
    id,

    text,

    source,

    timestamp,

    entities,

    claims,

    metadata
}
```

Contains:

- Raw text
- Extraction results
- Claims
- Model outputs
- Metadata

---

# 6. Evidence Object

## Purpose

Represents validated information.

Evidence is stronger than raw observation.

Schema:

```text
Evidence
{
    evidence_id,

    source,

    content,

    evidence_type,

    timestamp,

    entities,

    claims,

    confidence,

    provenance
}
```

Evidence Types:

- Document
- Image
- Video
- Website
- Dataset
- Screenshot

---

# 7. Claim Object

## Purpose

Represents statements requiring evaluation.

Schema:

```text
Claim
{
    claim_id,

    statement,

    source,

    supporting_evidence,

    confidence,

    status
}
```

Possible status:

- unverified
- supported
- contradicted
- confirmed

---

# 8. Relationship Object

## Purpose

Represents connections between entities.

Schema:

```text
Relationship
{
    relationship_id,

    source_entity,

    target_entity,

    relationship_type,

    confidence,

    evidence,

    timestamp,

    provenance
}
```

Examples:

```text
Person
    owns
Company

Domain
    associated_with
Organization
```

---

# 9. Case Object

## Purpose

Represents an investigation container.

Schema:

```text
Case
{
    case_id,

    title,

    objective,

    entities,

    observations,

    evidence,

    relationships,

    timeline,

    signal,

    status,

    created_at
}
```

A case contains:

- Investigation objective
- Relevant entities
- Evidence
- Findings

---

# 10. Signal Object

## Purpose

Represents investigation priority.

Schema:

```text
Signal
{
    score,

    classification,

    components,

    confidence,

    timestamp
}
```

Example:

```text
Score: 85
Classification: HIGH
```

Components may include:

- Entity Score
- Graph Score
- Observation Score
- Confidence Score

---

# 11. Timeline Event Object

## Purpose

Represents temporal intelligence.

Schema:

```text
Event
{
    event_id,

    timestamp,

    description,

    entities,

    evidence,

    location
}
```

Used for:

- Event reconstruction
- Activity ordering
- Investigation timelines

---

# 12. Contradiction Object

## Purpose

Represents conflicting intelligence.

Schema:

```text
Contradiction
{
    id,

    claim_a,

    claim_b,

    evidence,

    confidence,

    status
}
```

Example:

```text
Claim A:
Person was in Delhi

Claim B:
Person was abroad
```

---

# 13. Agent Task Object

## Purpose

Defines controlled agent execution.

Schema:

```text
AgentTask
{
    task_id,

    objective,

    inputs,

    required_capabilities,

    permissions,

    expected_output,

    validation_rules
}
```

---

# 14. Skill Object

## Purpose

Represents operational expertise.

Schema:

```text
Skill
{
    skill_id,

    name,

    purpose,

    procedure,

    tools,

    permissions,

    validation,

    examples,

    version
}
```

---

# 15. Capability Object

## Purpose

Represents available resources.

Schema:

```text
Capability
{
    capability_id,

    type,

    description,

    interface,

    requirements,

    status
}
```

Examples:

- API
- Tool
- Model
- Agent
- Dataset

---

# 16. Provenance Object

## Purpose

Maintains audit history.

Schema:

```text
Provenance
{
    created_by,

    created_at,

    source,

    transformation,

    parent_objects
}
```

Every intelligence transformation should be traceable.

---

# 17. Object Relationship Model

```text
Observation
    ↓
Entity Candidates
    ↓
Entity Resolution
    ↓
Entities
    ↓
Relationships
    ↓
Knowledge Graph
    ↓
Case
    ↓
Signal
    ↓
Report
```

---

# 18. Storage Evolution

Current:

```text
SQLite + JSON
```

Future:

### Relational Storage

- entities
- aliases
- relationships
- evidence
- observations
- events

### Graph Storage

- Neo4j or equivalent

### Vector Storage

- Semantic retrieval

---

# 19. Non-Negotiable Rules

1. Never use text as identity.

2. Never duplicate entity schemas.

3. Never allow models to directly modify intelligence truth.

4. Never remove provenance.

5. Never store conclusions without evidence.

---

# 20. Final Objective

The OSIRIS intelligence model exists to create a reliable bridge:

```text
Information
    ↓
Structured Objects
    ↓
Knowledge Representation
    ↓
Explainable Intelligence
```

This model forms the foundation upon which:

- Graph Intelligence
- Agents
- Memory
- Reporting
- Reasoning
- Learning Systems

will operate.

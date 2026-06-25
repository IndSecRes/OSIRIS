# OSIRIS Documentation Index

**Open Source Intelligence Research & Investigation System**

Version: 1.0

---

## Purpose

This document serves as the master index for all OSIRIS architecture, engineering, and development documentation.

OSIRIS is developed as an Intelligence Runtime Environment designed to transform raw information into structured, evidence-based intelligence.

The documentation is organized to separate:

* Vision
* Architecture
* Engineering Rules
* Data Models
* Development State
* Future Evolution

---

# Documentation Structure

## 01. Master Architecture & Vision

**File:**

`01_MASTER_ARCHITECTURE.md`

Defines:

* What OSIRIS is
* What OSIRIS is not
* Intelligence philosophy
* Investigation philosophy
* System vision
* Long-term objectives
* Major architectural components

Read this first to understand the purpose and direction of the system.

---

## 02. Engineering Rules & Design Principles

**File:**

`02_ENGINEERING_RULES.md`

Defines:

* Core engineering philosophy
* Entity-first design
* Ownership rules
* Evidence-first architecture
* Memory principles
* Agent governance
* Development order
* Refactoring rules

These principles govern all future development.

---

## 03. Core Data & Intelligence Model

**File:**

`03_CORE_DATA_MODEL.md`

Defines the canonical intelligence objects used by OSIRIS.

Includes:

* Entity
* EntityCandidate
* Observation
* Evidence
* Claim
* Relationship
* Case
* Signal
* Event
* Contradiction
* AgentTask
* Skill
* Capability
* Provenance

This document acts as the system's data model specification.

---

## 04. Architecture Stabilization & Refactor Plan

**File:**

`04_ARCHITECTURE_STABILIZATION.md`

Defines:

* Current architectural risks
* Refactor priorities
* Ownership boundaries
* Pipeline responsibilities
* Entity authority layer
* Graph ownership
* Confidence architecture
* Scaling strategy

This document guides architectural evolution.

---

## 05. Current System Snapshot

**File:**

`05_CURRENT_SYSTEM_SNAPSHOT.md`

Records the current implementation state.

Includes:

* Current pipeline
* Completed components
* Folder structure
* Known issues
* Development priorities
* Completion estimates

Unlike the architecture documents, this file changes frequently.

---

# OSIRIS Intelligence Flow

Information

↓

Observation

↓

Entity Candidates

↓

Entity Resolution

↓

Canonical Entities

↓

Evidence

↓

Relationships

↓

Knowledge Graph

↓

Reasoning

↓

Investigation Intelligence

↓

Decision Support

---

# Development Philosophy

OSIRIS is developed as an intelligence ecosystem.

Not as:

* A chatbot
* A search engine
* A workflow automation tool
* A collection of AI models

OSIRIS is an Intelligence Runtime Environment where:

* Models perceive
* Entities represent reality
* Evidence validates
* Graphs preserve relationships
* Memory improves investigations
* Agents execute tasks
* Skills provide expertise
* Humans make decisions

---

# Current Development Focus

Current priority:

1. Entity Authority Layer
2. Graph Ownership Stabilization
3. Alias Intelligence
4. Ontology Expansion
5. Evidence Engine
6. Timeline Intelligence
7. Reporting Layer
8. Agent Runtime
9. Memory Expansion

---

# Future Documentation

Planned architecture documents:

* Knowledge Graph Architecture Specification
* Evidence Intelligence Architecture
* Timeline Intelligence Architecture
* Memory Architecture Specification
* Agent Runtime Architecture
* Skill Intelligence Framework
* Capability Discovery Framework
* Governance Architecture
* Reporting Architecture

---

# Repository Navigation

```text
docs/
├── 00_PROJECT_INDEX.md
├── 01_MASTER_ARCHITECTURE.md
├── 02_ENGINEERING_RULES.md
├── 03_CORE_DATA_MODEL.md
├── 04_ARCHITECTURE_STABILIZATION.md
└── 05_CURRENT_SYSTEM_SNAPSHOT.md
```

---

## Recommended Reading Order

1. Master Architecture & Vision
2. Engineering Rules & Design Principles
3. Core Data & Intelligence Model
4. Architecture Stabilization & Refactor Plan
5. Current System Snapshot

This order moves from vision to implementation.

---

**OSIRIS Objective**

Transform information into explainable, evidence-based intelligence while preserving transparency, traceability, and human decision authority.

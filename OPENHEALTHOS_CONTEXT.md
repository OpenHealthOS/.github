# OpenHealthOS — Ecosystem Context

**Document:** OPENHEALTHOS_CONTEXT.md  
**Scope:** OpenHealthOS Organization  
**Version:** 1.1  
**Status:** Active  
**Last Updated:** 2026-08-07

---

# 1. PURPOSE

This document is the authoritative high-level context for the entire
OpenHealthOS ecosystem.

It defines:

- project vision
- mission
- ecosystem architecture
- repository responsibilities
- technology strategy
- AI strategy
- healthcare interoperability strategy
- open-source philosophy
- cross-repository dependencies
- organization-wide roadmap
- architectural principles

It does NOT replace repository-specific documentation.

---

# 2. SOURCE OF TRUTH MODEL

OpenHealthOS uses a layered documentation model.

## Organization-level source of truth

Repository:

    OpenHealthOS/.github

Primary document:

    OPENHEALTHOS_CONTEXT.md

Purpose:

    Defines the overall OpenHealthOS ecosystem.

---

## Repository-level source of truth

Each repository maintains:

    OPENHEALTHOS_CONTEXT.md

Purpose:

    Defines the implementation and current state of that repository.

Examples:

    platform/OPENHEALTHOS_CONTEXT.md
    web/OPENHEALTHOS_CONTEXT.md
    sdk-python/OPENHEALTHOS_CONTEXT.md

---

## Detailed engineering documentation

Repository-specific documentation lives under:

    docs/

Examples:

    platform/docs/architecture/
    web/docs/
    sdk-python/docs/

---

## Architecture decisions

Architectural decisions should be recorded as ADRs.

Repository-specific ADRs belong to the relevant repository.

Organization-wide architectural decisions belong in the organization
documentation.

---

# 3. DOCUMENTATION HIERARCHY

The hierarchy is:

    Organization Context
            ↓
    Repository Context
            ↓
    Architecture Documentation
            ↓
    ADRs
            ↓
    Source Code
            ↓
    Tests

The more specific layer takes precedence for implementation details.

The organization context defines direction.

Repository context defines implementation.

Source code defines actual behavior.

---

# 4. PROJECT VISION

OpenHealthOS is an open-source healthcare technology platform designed to
provide reusable infrastructure for:

- healthcare interoperability
- FHIR
- EHR/EMR data processing
- clinical data management
- healthcare AI/ML
- clinical decision support
- clinical research
- early disease detection
- clinical trial intelligence
- healthcare analytics
- healthcare data quality
- extensible healthcare applications

The long-term objective is to create a reusable platform rather than a
single healthcare application.

---

# 5. PROJECT MISSION

Make healthcare technology development more accessible by providing an
open-source, interoperable, cloud-native platform that developers,
researchers, and organizations can extend.

---

# 6. CORE PRINCIPLES

OpenHealthOS follows these principles:

1. Open Source
2. Community First
3. Documentation First
4. API First
5. Cloud Native
6. Security by Default
7. FHIR Interoperability
8. AI Ready
9. Modular Architecture
10. Contributor Friendly
11. Vendor Neutral Where Practical
12. Evidence-Based Engineering

---

# 7. ECOSYSTEM ARCHITECTURE

High-level:

                    OpenHealthOS
                         |
              +----------+----------+
              |                     |
             Web              External Clients
              |                     |
              +----------+----------+
                         |
                    API Gateway
                         |
       +-----------------+------------------+
       |                 |                  |
    Identity           FHIR              Clinical
       |                 |                 Data
       +-----------------+------------------+
                         |
                    Event Platform
                         |
              +----------+----------+
              |                     |
        AI / ML Runtime        Data Services
              |
        +-----+------+
        |            |
     External      Native
     Frameworks     OpenHealthOS AI

---

# 8. TECHNOLOGY STRATEGY

## Backend

- C#
- .NET 10
- ASP.NET Core
- Minimal APIs
- Microservices

## Frontend

- Angular

## AI / ML

- Python
- healthcare AI/ML ecosystem
- clinical NLP
- model providers
- machine learning frameworks

## Database

- Azure Cosmos DB

## Messaging

- Azure Service Bus
- event-driven architecture

## Infrastructure

- Docker
- Docker Hub
- GitHub Actions

## Development

- VS Code
- GitHub Copilot

---

# 9. POLYGLOT STRATEGY

OpenHealthOS intentionally uses multiple programming languages.

## C#

Primary language for:

- platform services
- APIs
- gateway
- identity
- FHIR services
- infrastructure services

## Python

Primary language for:

- AI
- machine learning
- clinical NLP
- research
- model experimentation
- AI SDK capabilities

This is a deliberate architectural decision.

The goal is not to force every workload into one language.

---

# 10. HEALTHCARE INTEROPERABILITY

FHIR is a core OpenHealthOS interoperability strategy.

FHIR should be used where appropriate for:

- Patient
- Observation
- Encounter
- Condition
- Medication
- DiagnosticReport
- Procedure
- ClinicalDocument
- other healthcare resources

The platform should prioritize interoperability over proprietary data
formats.

---

# 11. AI STRATEGY

AI is a major component of OpenHealthOS but should remain modular.

Potential capabilities:

- clinical NLP
- EHR/EMR analysis
- risk stratification
- clinical decision support
- early disease detection
- clinical research
- clinical trial intelligence
- predictive analytics
- data quality
- clinical summarization

AI components should be independently deployable where practical.

---

# 12. PYHEALTH STRATEGY

PyHealth:

    https://pyhealth.dev/

is an important project in the healthcare AI ecosystem.

OpenHealthOS may learn from, integrate with, or adapt compatible concepts
from PyHealth.

However:

OpenHealthOS should not become permanently dependent on PyHealth.

Long-term:

    Learn
      ↓
    Integrate where useful
      ↓
    Validate
      ↓
    Develop native capabilities
      ↓
    Maintain independent architecture

Licensing and attribution must always be respected.

---

# 13. AI ECOSYSTEM INSPIRATION

Healthcare AI projects such as PyHealth and Keiji.ai can be evaluated for:

- useful workflows
- clinical AI concepts
- interoperability ideas
- user experience
- model integration
- research opportunities

Ideas may inspire OpenHealthOS features but should not be copied without
appropriate licensing and attribution.

---

# 14. REPOSITORY ECOSYSTEM

The organization currently targets:

    OpenHealthOS/
    |
    +-- .github
    +-- platform
    +-- web
    +-- docs
    +-- sdk-dotnet
    +-- sdk-python
    +-- plugins
    +-- labs
    +-- samples
    +-- awesome-openhealthos

---

# 15. REPOSITORY RESPONSIBILITIES

## platform

The core cloud-native healthcare platform.

Primary technologies:

- .NET 10
- C#
- ASP.NET Core
- Cosmos DB
- YARP
- Docker

Responsibilities:

- APIs
- Gateway
- identity
- FHIR services
- clinical services
- infrastructure
- security
- events
- observability

---

## web

The primary OpenHealthOS web application.

Technology:

- Angular

Responsibilities:

- user interface
- authentication UI
- healthcare data visualization
- FHIR exploration
- clinical workflows
- AI insights
- administration

---

## docs

Public documentation and educational resources.

Responsibilities:

- getting started
- architecture
- API documentation
- developer documentation
- healthcare concepts
- contributor guides
- deployment guides

---

## sdk-dotnet

.NET developer SDK.

Purpose:

Make OpenHealthOS APIs easier to consume from .NET applications.

---

## sdk-python

Python developer and AI SDK.

Purpose:

Enable:

- AI applications
- research
- data science
- machine learning
- healthcare analytics

to interact with OpenHealthOS.

---

## plugins

OpenHealthOS extensibility ecosystem.

Potential plugins:

- FHIR connectors
- EHR connectors
- AI models
- NLP processors
- analytics
- notifications
- external services

---

## labs

Experimental and research environment.

Potential areas:

- clinical NLP
- healthcare AI
- new models
- algorithms
- datasets
- experimental integrations

Labs work does not automatically become production code.

---

## samples

Developer examples.

Examples:

- basic API client
- FHIR application
- AI inference
- plugin
- SDK usage
- healthcare workflow

---

## awesome-openhealthos

Curated healthcare technology and open-source resources.

Potential categories:

- FHIR
- healthcare AI
- clinical NLP
- datasets
- interoperability
- standards
- tools
- research

---

# 16. REPOSITORY MATURITY

Not every repository needs to be fully implemented immediately.

Priority:

1. platform
2. web
3. docs
4. samples
5. sdk-dotnet
6. sdk-python
7. plugins
8. labs
9. awesome-openhealthos

This ordering can change based on actual project requirements.

---

# 17. CROSS-REPOSITORY RULES

Repositories should remain independently maintainable.

Avoid unnecessary direct source-code dependencies.

Communication should happen through:

- public APIs
- contracts
- events
- SDKs
- documented interfaces

The following dependency direction is preferred:

    web
      ↓
    SDK / APIs
      ↓
    platform
      ↓
    infrastructure

AI:

    AI Runtime
       ↓
    APIs / Events
       ↓
    platform

---

# 18. CONTRIBUTOR MODEL

OpenHealthOS is designed for external contributors.

Contributors should be able to:

- understand architecture
- run projects locally
- create features
- write tests
- submit PRs
- create plugins
- contribute AI experiments
- propose architectural changes

Documentation is therefore considered part of the product.

---

# 19. QUALITY PRINCIPLES

Every repository should prioritize:

- tests
- documentation
- CI
- security
- maintainability
- reproducibility

Every major feature should have:

- implementation
- tests
- documentation
- appropriate ADR if architectural

---

# 20. SECURITY

Healthcare systems require strong security practices.

OpenHealthOS should consider:

- authentication
- authorization
- encryption
- audit logging
- secrets management
- least privilege
- secure APIs
- data minimization
- privacy
- healthcare compliance requirements

OpenHealthOS should not claim regulatory compliance unless formally
evaluated.

---

# 21. PROJECT ROADMAP

Completed:

- Epic 0 — Organization
- Epic 1 — Repository Foundation
- Epic 2 — Documentation
- Architecture Sprint
- Epic 3 — Platform Foundation
- Epic 4 — Cloud-Native Gateway

Planned:

- Epic 5 — Identity
- Epic 6 — FHIR Foundation
- Epic 7 — Clinical Data
- Epic 8 — Event Platform
- Epic 9 — AI Runtime
- Epic 10 — AI Framework Integration
- Epic 11 — Healthcare AI
- Epic 12 — Plugin Platform
- Epic 13 — SDKs
- Epic 14 — Web Platform
- Epic 15 — Community Ecosystem

Roadmap order may evolve.

---

# 22. CURRENT STATUS

Current project maturity:

    Early platform / pre-alpha

Completed major work:

    Organization foundation
    Architecture
    Platform foundation
    Cloud-native gateway

Current implementation focus:

    platform

Next major focus:

    Identity

---

# 23. PROFESSIONAL IMPACT STRATEGY

OpenHealthOS is intended to create genuine technical and community impact
in healthcare technology.

Potential measurable outcomes include:

- contributors
- GitHub stars
- forks
- downloads
- releases
- Docker pulls
- external integrations
- academic usage
- research collaborations
- publications
- citations
- conference presentations
- healthcare technology adoption

The project should prioritize real impact rather than creating evidence
solely for immigration purposes.

---

# 24. DOCUMENTATION GOVERNANCE

The organization context should be updated when:

- project vision changes
- ecosystem architecture changes
- repository responsibilities change
- major cross-repository decisions occur
- major roadmap changes occur

Repository contexts should be updated when:

- an Epic completes
- architecture changes
- technology changes
- repository responsibilities change
- major implementation milestones complete

---

# 25. CONTEXT RECOVERY

When using an AI assistant for OpenHealthOS:

For ecosystem-level work:

    Upload:
    OpenHealthOS/.github/OPENHEALTHOS_CONTEXT.md

For repository-specific work:

    Upload:
    OpenHealthOS/.github/OPENHEALTHOS_CONTEXT.md
    +
    <repository>/OPENHEALTHOS_CONTEXT.md

For detailed work:

    Also provide:
    relevant architecture documentation
    ADRs
    issue/PR
    source code where necessary

---

# 26. AUTHORITY RULE

When information conflicts:

1. Actual source code defines current behavior.
2. Repository documentation defines intended implementation.
3. Repository context defines repository-level project state.
4. Organization context defines ecosystem-level direction.
5. AI-generated suggestions are proposals, not facts.

An AI assistant must not assume that planned functionality is implemented.

---

# END

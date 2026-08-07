# OpenHealthOS — Project Context

**Document:** OPENHEALTHOS_CONTEXT.md
**Version:** 1.0
**Status:** Active
**Project:** OpenHealthOS
**Founder / Lead Maintainer:** Ponchanon Datta Rone

---

# 1. PURPOSE OF THIS DOCUMENT

This document is the persistent project context for OpenHealthOS.

It exists to preserve:

- project vision
- architecture
- repositories
- technology decisions
- AI strategy
- development roadmap
- completed work
- architectural decisions
- deferred ideas
- contributor strategy
- current implementation status
- future plans

This document should be treated as the primary high-level context when
continuing OpenHealthOS development in a new AI/ChatGPT session.

The actual GitHub repositories, source code, ADRs, and architecture
documents remain the ultimate technical source of truth.

---

# 2. PROJECT VISION

OpenHealthOS is an open-source, cloud-native healthcare technology
platform designed to provide reusable infrastructure for:

- healthcare interoperability
- clinical data management
- FHIR
- EHR/EMR data processing
- healthcare AI/ML
- clinical decision support
- clinical research
- early disease detection
- clinical trial intelligence
- healthcare data quality
- extensible healthcare applications

The project should be:

- open source
- contributor friendly
- modular
- cloud native
- secure by default
- interoperable
- AI-ready
- vendor neutral where practical
- suitable for research and production-oriented use

---

# 3. LONG-TERM OBJECTIVE

OpenHealthOS should become a reusable healthcare technology platform rather
than a single healthcare application.

The platform should allow developers and researchers to build healthcare
applications without repeatedly implementing:

- identity
- healthcare interoperability
- FHIR infrastructure
- clinical data processing
- event infrastructure
- observability
- AI integration
- model execution
- plugin infrastructure
- common healthcare APIs

---

# 4. DEVELOPMENT PHILOSOPHY

OpenHealthOS follows these principles:

1. Community First
2. Documentation First
3. API First
4. Cloud Native
5. Security by Default
6. AI is Optional
7. FHIR is a Core Interoperability Language
8. Plugin Everything Where Appropriate
9. Test Everything
10. Production Quality

Additional engineering principles:

- Architecture before implementation
- Small, reviewable pull requests
- Every PR should produce a working build
- Avoid speculative abstractions
- Prefer incremental evolution
- No AI-generated code should be merged without human review
- Contributors should be able to understand architectural decisions
- Services should communicate through APIs/events rather than direct
  service-to-service implementation dependencies

---

# 5. PRIMARY TECHNOLOGY STACK

## Backend / Platform

- C#
- .NET 10
- ASP.NET Core
- Minimal APIs
- YARP
- Microservices

## Frontend

- Angular

## AI / Machine Learning

- Python
- Python-based AI runtime
- Provider/model abstraction
- Healthcare NLP
- ML/AI inference

## Database

- Azure Cosmos DB

## Messaging / Events

Planned:

- Azure Service Bus
- Event-driven communication
- Integration events

## Caching

- Redis

## Local development infrastructure

- Docker
- Docker Compose
- Azurite
- Redis
- Seq

## CI/CD

- GitHub Actions

## Container distribution

- Docker Hub

## Development environment

- VS Code
- GitHub Copilot

---

# 6. ARCHITECTURE

OpenHealthOS uses a cloud-native microservice architecture.

High-level architecture:

                    OpenHealthOS
                         |
              +----------+----------+
              |                     |
          Angular Web          External Clients
              |                     |
              +----------+----------+
                         |
                    API Gateway
                        YARP
                         |
       +-----------------+------------------+
       |                 |                  |
    Identity          FHIR              Patient
       |                 |                  |
       +-----------------+------------------+
                         |
                    Event System
                         |
                 Azure Service Bus
                         |
              +----------+----------+
              |                     |
          AI Runtime           Data Services
              |
           Python
              |
       +------+------+
       |             |
    PyHealth      Native AI
    (initial)     (long-term)

---

# 7. ARCHITECTURAL STYLE

OpenHealthOS follows:

- Microservices
- Cloud-native architecture
- Event-driven architecture
- API-first design
- Minimal APIs
- Vertical Slice Architecture
- Modular design
- Plugin-oriented extensibility
- FHIR interoperability
- Provider-independent AI architecture

Services must not directly reference other services' implementation projects.

Inter-service communication should occur through:

- HTTP APIs
- events
- messaging
- shared contracts

---

# 8. BUILDING BLOCKS

The platform contains reusable internal building blocks.

Current / planned:

BuildingBlocks/

    OpenHealthOS.SharedKernel

    OpenHealthOS.Contracts

    OpenHealthOS.Infrastructure

    OpenHealthOS.Security

    OpenHealthOS.Observability

    OpenHealthOS.ServiceDefaults

    OpenHealthOS.Hosting

---

# 9. SHARED KERNEL

OpenHealthOS.SharedKernel contains reusable domain primitives.

Examples:

- Entity
- AggregateRoot
- ValueObject
- Result
- DomainEvent
- Guard

The SharedKernel must remain independent of:

- ASP.NET
- Cosmos DB
- Azure
- HTTP
- infrastructure implementations

---

# 10. CONTRACTS

OpenHealthOS.Contracts contains shared communication contracts.

Potential contents:

- Integration Events
- DTOs
- Commands
- Queries
- API contracts
- event abstractions

Contracts should describe communication and should not contain business
implementation.

---

# 11. INFRASTRUCTURE

OpenHealthOS.Infrastructure is responsible for reusable infrastructure
implementations.

Planned areas:

- Cosmos DB
- Redis
- messaging
- Azure Storage
- persistence
- external service adapters

Infrastructure must not leak into domain logic.

---

# 12. SECURITY

OpenHealthOS.Security will eventually provide reusable security
capabilities.

Planned:

- authentication
- authorization
- JWT
- permissions
- service-to-service authentication
- API keys
- OpenID Connect readiness
- SMART on FHIR compatibility

---

# 13. OBSERVABILITY

OpenHealthOS.Observability will provide:

- structured logging
- metrics
- distributed tracing
- correlation IDs
- telemetry conventions
- health checks

Planned technologies include:

- OpenTelemetry
- Serilog
- Seq for local development
- Azure Monitor in Azure deployments
- future Prometheus/Grafana compatibility

---

# 14. OPENHEALTHOS.SERVICEDEFAULTS

OpenHealthOS.ServiceDefaults is inspired by the service-default approach
used by modern .NET cloud-native applications.

Its purpose is to provide consistent capabilities across every service.

Expected responsibilities:

- Health checks
- readiness checks
- liveness checks
- OpenTelemetry
- structured logging
- correlation IDs
- Problem Details
- exception handling
- HTTP client defaults
- API conventions
- JSON conventions
- API versioning

Target usage:

    builder.Services.AddOpenHealthServiceDefaults();

and:

    app.UseOpenHealthPipeline();

Every OpenHealthOS service should eventually inherit the same operational
conventions.

---

# 15. OPENHEALTHOS.HOSTING

OpenHealthOS.Hosting provides common application bootstrap and hosting
configuration.

Target usage:

    var builder = OpenHealthHost.CreateBuilder(args);

Responsibilities:

- configuration loading
- environment configuration
- dependency injection bootstrap
- hosting defaults
- common application configuration

The public API should remain intentionally small.

---

# 16. GATEWAY

The Gateway is the front door of OpenHealthOS.

Technology:

- ASP.NET Core
- Minimal APIs
- YARP
- OpenAPI
- Scalar
- API versioning
- Problem Details
- OpenTelemetry
- Serilog

Gateway responsibilities:

- API routing
- service discovery/routing
- request handling
- health endpoints
- observability
- future rate limiting
- future authentication/authorization integration

The Gateway should remain thin.

Business logic belongs in services.

---

# 17. GATEWAY PIPELINE

Target middleware order:

Exception Handler
        ↓
Correlation ID
        ↓
Request Logging
        ↓
Problem Details
        ↓
Authentication
        ↓
Authorization
        ↓
Rate Limiting (future)
        ↓
YARP
        ↓
Endpoints

---

# 18. API CONVENTIONS

OpenHealthOS APIs should use:

- Minimal APIs
- OpenAPI
- API versioning
- RFC 9457 Problem Details
- consistent JSON conventions
- health endpoints

Standard operational endpoints:

    /health
    /ready
    /live

---

# 19. FRONTEND REPOSITORY

Repository:

    OpenHealthOS/web

Technology:

- Angular

Purpose:

The web repository is the primary user-facing application for OpenHealthOS.

Planned responsibilities:

- healthcare application UI
- authentication UI
- FHIR data exploration
- patient views
- clinical data visualization
- AI/clinical insights UI
- administration
- platform management
- plugin management

The web application should consume OpenHealthOS APIs rather than directly
accessing Cosmos DB or other backend infrastructure.

---

# 20. AI REPOSITORY / AI ARCHITECTURE

AI is intentionally separated from the .NET platform.

The primary AI/model runtime should use:

- Python
- Python ML ecosystem
- healthcare NLP libraries
- model providers
- specialized healthcare AI frameworks

Reason:

Python provides stronger ecosystem support for:

- machine learning
- deep learning
- NLP
- clinical NLP
- model experimentation
- scientific computing

C# remains the primary platform/backend language.

Python is the primary AI/model language.

This is a deliberate polyglot architecture.

---

# 21. AI RUNTIME

The long-term AI architecture should support:

- EHR/EMR analysis
- clinical NLP
- clinical decision support
- risk stratification
- early disease detection
- clinical research
- clinical trial intelligence
- healthcare data quality
- predictive analytics

AI should be exposed through well-defined platform interfaces.

The .NET platform should not become tightly coupled to individual ML
frameworks.

---

# 22. PYHEALTH STRATEGY

PyHealth was identified as a valuable healthcare AI/ML project.

Reference:

    https://pyhealth.dev/

OpenHealthOS should learn from PyHealth and potentially use compatible
components during early development.

However:

OpenHealthOS should NOT become permanently dependent on PyHealth.

Long-term strategy:

    Learn from PyHealth
           ↓
    Adapter / integration
           ↓
    Validate use cases
           ↓
    Build native OpenHealthOS capabilities
           ↓
    Reduce external dependency where appropriate

PyHealth should be treated as an ecosystem/reference/integration opportunity,
not the permanent core of OpenHealthOS.

---

# 23. KEIJI.AI STRATEGY

Reference discussed:

    https://keiji.ai/

Keiji.ai was reviewed as a potential source of ideas for healthcare AI
features and workflows.

Relevant concepts should be considered as inspiration rather than copied
implementation.

Any useful capability should be evaluated against:

- OpenHealthOS architecture
- open-source licensing
- healthcare interoperability
- extensibility
- clinical usefulness
- contributor value

---

# 24. REPOSITORY ECOSYSTEM

The OpenHealthOS organization is intended to contain multiple repositories.

Target ecosystem:

    OpenHealthOS/
    |
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

# 25. REPOSITORY RESPONSIBILITIES

## platform

Primary backend/platform.

Technology:

- .NET 10
- C#
- ASP.NET Core
- microservices
- Cosmos DB
- messaging
- security
- observability
- Gateway

This is currently the primary implementation repository.

---

## web

Primary frontend.

Technology:

- Angular

Purpose:

- web application
- platform UI
- healthcare data visualization
- AI insights
- administration

---

## docs

Project documentation.

Contains:

- architecture
- developer guides
- API documentation
- contributor guides
- ADRs
- healthcare concepts
- deployment documentation

---

## sdk-dotnet

Future .NET SDK.

Purpose:

Allow .NET developers to interact with OpenHealthOS APIs easily.

Should not be built aggressively until APIs stabilize.

---

## sdk-python

Future Python SDK.

Purpose:

Provide convenient access to OpenHealthOS from:

- AI projects
- research projects
- data science
- clinical research workflows

Particularly important for the AI ecosystem.

---

## plugins

Future OpenHealthOS plugin ecosystem.

Potential plugins:

- healthcare data connectors
- FHIR connectors
- EHR integrations
- AI models
- NLP processors
- analytics
- notifications
- external services

Plugins should have a clear contract and security model.

---

## labs

Experimental/research repository.

Purpose:

- AI experiments
- clinical NLP experiments
- new algorithms
- prototypes
- research ideas
- experimental integrations

Labs code does not automatically become production code.

---

## samples

Examples for contributors and developers.

Examples could include:

- Hello OpenHealthOS
- FHIR example
- patient example
- AI inference example
- SDK example
- plugin example

---

## awesome-openhealthos

Curated healthcare/open-source ecosystem.

Potential contents:

- FHIR resources
- datasets
- healthcare AI projects
- clinical NLP resources
- standards
- tools
- research
- community projects

This should become useful to the broader community rather than being
purely promotional.

---

# 26. REPOSITORY MATURITY STRATEGY

We should NOT attempt to fully implement all repositories simultaneously.

Initial priority:

1. platform
2. web
3. docs
4. samples

Later:

5. sdk-dotnet
6. sdk-python
7. plugins
8. labs
9. awesome-openhealthos

Repositories should become active when their APIs or community purpose
justify them.

---

# 27. DATABASE STRATEGY

Primary database:

    Azure Cosmos DB

Reasons:

- cloud-native
- scalable
- flexible document model
- suitable for distributed systems
- Azure integration
- useful for healthcare data workloads

However, healthcare interoperability should be represented using standards
rather than proprietary application-specific models where appropriate.

FHIR resources should be treated as first-class healthcare interoperability
objects.

---

# 28. EVENT-DRIVEN ARCHITECTURE

OpenHealthOS should use asynchronous events where appropriate.

Potential infrastructure:

    Azure Service Bus

Examples:

    PatientCreated
    PatientUpdated
    ObservationCreated
    ClinicalDocumentReceived
    AIAnalysisCompleted

Services should not rely on synchronous calls for every workflow.

Events should be versioned and documented.

---

# 29. DOCKER STRATEGY

OpenHealthOS uses Docker for local development and deployment.

Local development infrastructure currently includes:

- Redis
- Azurite
- Seq

Cosmos DB emulator is intentionally deferred until persistence implementation
requires it.

Container images should eventually be published to Docker Hub.

---

# 30. CI/CD

GitHub Actions should provide:

- restore
- build
- test
- quality checks
- container build
- future container publishing
- future release automation

Every PR should pass CI before merging.

---

# 31. CONTRIBUTOR MODEL

OpenHealthOS is intended to remain open for external contributors.

Contributor experience is a major architectural requirement.

Documentation should explain:

- how to build
- how to run
- how to test
- architecture
- coding standards
- PR process
- issue process
- service creation
- plugin creation
- AI contribution

---

# 32. AI-GENERATED CODE POLICY

GitHub Copilot and ChatGPT can be used to accelerate development.

However:

AI-generated code must be reviewed and understood by the maintainer before
being merged.

The project should prioritize:

- correctness
- security
- maintainability
- tests
- documentation

over simply generating code quickly.

---

# 33. NIW-RELEVANT PROJECT STRATEGY

OpenHealthOS is also being developed as a long-term professional and
open-source contribution demonstrating work in healthcare technology,
AI, interoperability, and clinical innovation.

The project should therefore prioritize measurable technical impact.

Potential evidence over time:

- GitHub contributions
- commits
- pull requests
- releases
- contributors
- stars/forks
- downloads
- Docker image pulls
- external adoption
- documentation usage
- integrations
- research collaborations
- publications
- conference presentations
- citations
- independent users
- healthcare/academic collaborations

The project should NOT be engineered merely to create immigration evidence.

Real technical/community impact is the priority.

---

# 34. ROADMAP

## Epic 0 — Organization

STATUS: COMPLETED

Established OpenHealthOS organization/project foundation.

---

## Epic 1 — Repository Foundation

STATUS: COMPLETED

Established repository structure and foundational standards.

---

## Epic 2 — Documentation

STATUS: COMPLETED

Established project documentation and engineering documentation.

---

## Architecture Sprint

STATUS: COMPLETED

Defined:

- service boundaries
- database strategy
- API approach
- events
- plugin architecture
- AI runtime
- authentication
- deployment model

Architecture documentation is maintained in:

    platform/docs/architecture/

---

# Epic 3 — Platform Bootstrap

STATUS: COMPLETED

Completed:

- .NET 10 solution
- BuildingBlocks
- global configuration
- Docker infrastructure
- GitHub Actions
- code quality
- project structure
- documentation

BuildingBlocks include:

- SharedKernel
- Contracts
- Infrastructure
- Security
- Observability
- ServiceDefaults
- Hosting

---

# Epic 4 — Cloud-Native Gateway

STATUS: COMPLETED

Epic 4 established the reusable service/platform foundation.

Major areas:

1. OpenHealthOS.Hosting
2. OpenHealthOS.ServiceDefaults
3. Observability
4. API Platform
5. Gateway Foundation
6. YARP

Target capabilities established:

- configuration
- hosting conventions
- health checks
- readiness/liveness
- Problem Details
- structured logging
- OpenTelemetry
- correlation IDs
- OpenAPI
- Scalar
- API versioning
- Minimal APIs
- YARP

The Gateway is intended to be the reference implementation for future
services.

---

# 35. NEXT MAJOR EPICS

The exact sequence can evolve as implementation progresses.

Likely sequence:

## Epic 5 — Identity

Potential capabilities:

- authentication
- JWT
- refresh tokens
- RBAC
- permissions
- service-to-service authentication
- OpenID Connect
- SMART on FHIR readiness

---

## Epic 6 — FHIR Foundation

Potential capabilities:

- FHIR resource model
- FHIR APIs
- resource validation
- terminology
- FHIR search
- interoperability foundation

---

## Epic 7 — Patient / Clinical Data

Potential capabilities:

- Patient
- Observation
- Encounter
- Condition
- Medication
- clinical documents
- data ingestion

---

## Epic 8 — Event Platform

Potential capabilities:

- Service Bus
- integration events
- event contracts
- event versioning
- reliable messaging
- event processing

---

## Epic 9 — AI Runtime

Potential capabilities:

- Python AI runtime
- model provider abstraction
- clinical NLP
- EHR/EMR analysis
- inference APIs
- model registry
- model metadata
- AI auditability

---

## Epic 10 — PyHealth Integration

Evaluate and implement appropriate adapters/integration.

The goal is interoperability and learning rather than permanent dependency.

---

## Epic 11 — Healthcare AI

Potential capabilities:

- risk stratification
- clinical decision support
- early disease detection
- clinical research
- clinical trial intelligence
- predictive analytics

AI features must include appropriate safety, auditability, and transparency.

---

## Epic 12 — Plugin Platform

Create:

- plugin contracts
- plugin lifecycle
- plugin discovery
- plugin security
- plugin configuration
- plugin marketplace/ecosystem foundations

---

## Epic 13 — SDKs

Develop:

- sdk-dotnet
- sdk-python

after core APIs have stabilized.

---

## Epic 14 — Web Platform

Continue building the Angular web platform around stable backend APIs.

Potential UI:

- FHIR explorer
- patient view
- clinical data
- AI insights
- administration
- platform configuration
- plugin management

---

## Epic 15 — Community / Ecosystem

Grow:

- samples
- labs
- awesome-openhealthos
- contributor documentation
- community plugins
- integrations
- external contributors

---

# 36. DEFERRED IDEAS

These should not be implemented prematurely:

- excessive abstraction
- full plugin marketplace
- complex AI orchestration
- premature SDK generation
- unnecessary service proliferation
- unnecessary databases
- premature Kubernetes complexity
- unnecessary event infrastructure before real use cases
- excessive BuildingBlock code without consumers

Architecture should evolve with real requirements.

---

# 37. CURRENT STATE

As of the current project checkpoint:

COMPLETED:

- Epic 0
- Epic 1
- Epic 2
- Architecture Sprint
- Epic 3
- Epic 4

Current state:

    Platform foundation complete
    Cloud-native Gateway foundation complete
    ServiceDefaults established
    Hosting established
    Observability established
    API platform established
    YARP established

NEXT:

    Epic 5 — Identity

---

# 38. SOURCE OF TRUTH

Primary source:

    GitHub OpenHealthOS organization

Platform:

    https://github.com/OpenHealthOS/platform

Architecture:

    https://github.com/OpenHealthOS/platform/tree/main/docs/architecture

Other repositories are authoritative for their respective implementation
areas.

This context file is a high-level recovery document and should not replace
actual repository documentation.

---

# 39. CHATGPT / AI WORKING INSTRUCTIONS

When assisting with OpenHealthOS:

1. Treat this document as project context.
2. Check current repository state before proposing major changes.
3. Respect existing architecture and ADRs.
4. Do not reverse an architectural decision without discussing it.
5. Prefer incremental PRs.
6. Give exact implementation instructions.
7. Include tests.
8. Include documentation updates.
9. Explain why architectural decisions are being made.
10. Avoid speculative abstractions.
11. Avoid unnecessary dependencies.
12. Keep services independently deployable.
13. Keep AI runtime modular.
14. Preserve FHIR interoperability.
15. Preserve contributor friendliness.
16. Treat security and healthcare data protection as first-class concerns.
17. Do not claim that an implementation is complete without verification.
18. Distinguish planned work from completed work.
19. Distinguish external integrations from native OpenHealthOS capabilities.
20. When uncertain about current code, inspect the repository rather than
    assuming.

---

# 40. CONTEXT RECOVERY PROCEDURE

When starting a new OpenHealthOS conversation:

Upload:

    OPENHEALTHOS_CONTEXT.md

Then provide:

    "Use this as the OpenHealthOS project context and source of truth.
     We are continuing from the current state documented here."

For detailed implementation tasks, also provide or reference the relevant:

- architecture documents
- ADR
- repository README
- current issue/PR
- source code

The context file should be updated whenever a major Epic or architectural
decision is completed.

---

# 41. CONTEXT VERSIONING

Version this file.

Example:

    1.0 — Epic 4 completed
    1.1 — Epic 5 completed
    1.2 — FHIR architecture updated
    2.0 — Major architecture revision

Never silently rewrite major architectural history.

Update the document with:

- date
- change
- reason
- affected areas

---

# 42. CURRENT IMMEDIATE NEXT STEP

Before beginning Epic 5:

1. Update project context.
2. Review Epic 4 implementation.
3. Verify CI.
4. Verify Docker environment.
5. Verify Gateway health endpoints.
6. Verify OpenAPI/Scalar.
7. Verify observability.
8. Verify YARP.
9. Document any deviations from the planned architecture.
10. Then begin Epic 5.

---

# END OF OPENHEALTHOS_CONTEXT.md

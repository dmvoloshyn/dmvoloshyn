# DmV Software Architecture Mapping

## Purpose

This document defines the relationship between the engineering patterns layer and the commercial software products developed under DmV Software.

The purpose of this layer is to demonstrate how reusable engineering solutions are transformed into practical software systems.

DmV Software represents the implementation stage where system concepts become real user-oriented applications.

---

# Architecture Flow

The overall development flow:

Engineering Patterns  
↓  
Computational Logic  
↓  
Product Implementation  
↓  
Commercial Software Application

---

# Product Mapping

## Concrete Works Cost Estimator Pro

Concrete Works Cost Estimator Pro is a specialized engineering calculation system focused on construction cost estimation workflows.

The application transforms domain-specific engineering requirements into a structured calculation environment.

### Related Engineering Patterns

## Expression Processing Pattern

Purpose:

Transforms user-defined inputs and calculation parameters into structured computational operations.

Application:

- estimation formulas
- parameter processing
- calculation workflow execution
- result generation


## Safe String Transformation Pattern

Purpose:

Provides controlled processing of complex text expressions where multiple symbols, units, and tokens may overlap.

Application:

- unit handling
- input normalization
- safe preprocessing of calculation expressions


## Reactive User Interface Pattern

Purpose:

Creates direct interaction between user actions, interface state, and calculation processes.

Application:

- dynamic controls
- automatic updates
- interactive calculation workflow

---

# DmV Calculator PRO

DmV Calculator PRO is a general engineering calculation environment based on expression-driven computation.

The system focuses on flexible mathematical and engineering calculations through a compact user interaction model.

### Related Engineering Patterns

## Expression Parser Logic

Purpose:

Converts human-readable mathematical expressions into executable computational structures.

Application:

- formula evaluation
- operator processing
- calculation execution


## Unicode Arrow Conversion DSL Pattern

Purpose:

Creates a lightweight domain-specific language for unit conversion using readable text expressions.

Example:

5km→mi

Application:

- engineering conversions
- compact user commands
- human-readable calculation syntax


## Text-Based Structured Data Pattern

Purpose:

Uses formatted calculation history as an interactive structured environment.

Application:

- action logs
- calculation history navigation
- user workflow tracking

---

# Marine Data Lab

Marine Data Lab extends the architecture from deterministic engineering computation into scientific data integration and analysis.

---

## Related Engineering Patterns

---

## Native Library Integration Through JNI

Application:

- Java application architecture
- native C++ scientific libraries
- JNI integration boundary
- structured result processing

## Structured Spatial Data Integration

Application:

- JSON data processing
- GeoJSON spatial information
- structured geographic datasets
- spatial analysis workflows

## Dual-Mode Scientific Analysis Architecture

Application:

- individual measurement analysis
- spatial-temporal dataset analysis
- shared scientific data model
- persistent research context
- automated assessment and manual validation

## Persistent Research Data Reuse

Application:

- History Journal
- research record search
- reusable datasets
- intelligent autofill
- selection of records for further analysis

---

# NASA Enterprise Mission Control Agent

NASA Enterprise Mission Control Agent extends the architecture into Agentic AI and distributed external-service orchestration.

---

## Related Engineering Patterns

---

## Agentic Tool Orchestration

Application:

- Java
- LangChain4j
- LLM reasoning
- task decomposition
- deterministic tools
- multi-step tool chaining

## Resilient API and Model Fallback

Application:

- multiple NASA APIs
- API failure handling
- model fallback
- credential/key rotation
- controlled degradation
- alternative execution paths

## Live-Data Grounding

Application:

- live NASA API retrieval
- structured external data
- factual grounding
- reduced hallucination risk
- traceable data-to-response flow

## Deterministic Agent Evaluation

Application:

- expected tool selection
- actual tool selection
- execution outcomes
- workflow validation
- failure localization
- system-level agent evaluation

## Extended Architecture Flow

The portfolio architecture therefore expands from deterministic engineering computation into scientific integration and Agentic AI:

```text
        System Architecture
                 ↓
        Engineering Patterns
                 ↓
Scientific & AI Integration Patterns
                 ↓
   Product / Agent Implementation
                 ↓
       Execution & Validation
                 ↓
    Commercial or Research Output
```

---

# Shared Architectural Principles

Both DmV Software products are based on the same engineering principles.

## Lightweight Architecture

The systems avoid unnecessary complexity and maintain direct control over computational behavior.

The architecture focuses on:

- clear logic
- reusable solutions
- efficient implementation

## User-Oriented Computation

The user interface is treated as an active part of the computational process.

Interaction, input, calculation, and output are combined into a single workflow.

## Reusable Engineering Logic

Engineering solutions created for one product can be adapted and transferred into other software systems.

This creates a scalable foundation for future applications.

---

# Relationship Between Layers

DmV Software connects multiple architectural levels:

``` text
System Architecture

         ↓

Engineering Patterns

         ↓

DmV Software Products

         ↓

Commercial Distribution
```

---

# Architecture Diagram

<img width="2502" height="1684" alt="Diagram3_1" src="https://github.com/user-attachments/assets/d13572b5-dbb2-443f-a1bb-23ce47ed6027" />

This diagram represents the relationship between:

- System Architecture
- Engineering Patterns
- DmV Software Products
- Commercial Applications

---

# Summary

DmV Software products are practical implementations of the engineering concepts defined in the system architecture.

The architecture connects reusable computational patterns with real-world software solutions.

This creates a scalable product foundation where engineering logic can evolve into multiple commercial applications.

## Navigation

[Back to System Overview](./00_system/System-Overview.md)
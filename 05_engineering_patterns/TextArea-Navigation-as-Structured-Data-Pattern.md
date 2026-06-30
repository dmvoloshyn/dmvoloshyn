# TextArea Navigation as Structured Data Pattern

## Overview

This article describes a non-standard approach to implementing structured navigation over unstructured UI text in a JavaFX application.

Instead of using a dedicated data model (tree, list, or AST), the system treats a plain `TextArea` as a structured data source.

Navigation, filtering, and semantic interpretation are performed using regex-based classification and cursor movement logic.

---

## Problem

Traditional solutions for action logs or history systems use:

- structured data models (List, Tree, Map)
- separate UI representations
- explicit parsing layers

However, in lightweight engineering tools, maintaining a parallel data structure introduces unnecessary complexity and synchronization overhead.

The goal was to:

- keep a single source of truth (TextArea)
- enable structured navigation (up/down movement)
- differentiate semantic line types

---

## Solution Concept

The core idea is:

    Treat formatted text as implicit structured data


Instead of parsing text into objects, the system:

1. keeps everything in a single TextArea
2. classifies lines using regex
3. navigates using cursor-based logic

Two logical line types are defined:

- header lines (contain ":")
- result lines (contain "=")
- special numeric patterns (including negative results)

---

## Original Implementation Fragment

Navigation logic is implemented via word-based and regex-based scanning:

    String[] sp1 = y1.split(
        "snh|csh|tnh|asn|acs|atn|sin|cos|tan|lg|ln|abs|\\u221B|[V%^*/+\\-]"
    );


This split separates mathematical tokens from expression content.

---

## Navigation Logic Concept

The Action Log behaves as a hybrid structure:

- visually a text document
- logically a structured dataset

Navigation is implemented by scanning text sequentially and applying classification rules.

Key behavior:

- ↑ / ↓ navigation moves through logical entries, not raw lines
- Home / End jump between semantic boundaries
- selection is based on pattern recognition, not indexing

---

## Structural Interpretation Rules

Each line is interpreted dynamically:

- if line contains ":" → treated as category/header
- if line contains "=" → treated as computed result
- if line contains "-=" → treated as negative result variant

This allows the system to reconstruct structure without storing explicit objects.

---

## Engineering Reasoning

A classical architecture would require:

- ActionLogEntry objects
- a List or Tree structure
- synchronization between model and UI

Instead, this design chooses:

- zero duplication of state
- UI as data source
- regex as structural inference layer

This reduces architectural overhead significantly.

---

## Pattern Definition

The pattern can be described as:

    Unstructured Text
            ↓
    Regex Classification Layer
            ↓
    Navigation Logic
            ↓
    Structured Behavior (without structure)

---

## Applications

This pattern is useful in:

- lightweight logging systems
- calculator history views
- DSL-based editors
- debugging consoles
- embedded UI tools with minimal architecture

---

## Engineering Insight

The key idea is not storing structure explicitly.

Instead, structure is inferred at runtime from formatted text.

This shifts system design from:

    data-driven architecture

to:

    perception-driven architecture over text

This approach is particularly effective in compact engineering tools where minimizing abstraction layers is critical.
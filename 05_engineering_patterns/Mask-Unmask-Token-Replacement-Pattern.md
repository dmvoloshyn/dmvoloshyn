# Safe Multi-Pattern String Substitution: The Mask-Unmask Technique for Overlapping Tokens

## Overview

This article describes a string-processing pattern developed for a Java-based engineering calculation system.

The technique solves a common problem in expression parsers: handling overlapping tokens where a short identifier is also part of a longer unit name.

Examples:

- m — meter
- mm — millimeter
- mmHg — millimeters of mercury
- mph — miles per hour
- mps — meters per second

The challenge is to modify expressions without destroying valid measurement units.

---

## Problem

Direct replacement operations create collisions.

For example:

    25mmHg

contains the token:

    m

but also contains:

    mmHg


A simple replacement:

    replace("m", "")

would transform the expression into:

    25Hg


The original meaning is lost.

The system therefore requires a controlled transformation process where complex tokens are protected before simpler operations are executed.

---

## Solution Concept

The implemented approach follows the principle:

    Protect → Transform → Restore


The processing sequence:

1. Detect multi-character tokens.
2. Temporarily replace them with protected aliases.
3. Apply required transformations.
4. Restore the original tokens.

This creates a temporary safe representation of the expression.

---

## Original Implementation Fragment

Real implementation approach:

    X.setText(newText
        .replaceAll("mmHg", "MMHG")
        .replaceAll("mph",  "Mph")
        .replaceAll("mps",  "Mps")
        .replaceAll("mt",   "Mt")
        .replaceAll("mg",   "MG")

        // additional unit protection rules

        .replaceAll("(mHG|mMG|mmH|mp|mh|ms|mi|yd|ft|in|km|cm|mm|m|...)", "")

        // restore protected tokens

        .replaceAll("MMHG", "mmHg")
        .replaceAll("Mph",  "mph")
    );


The implementation uses uppercase aliases as temporary protected tokens.

Example:

    mmHg

becomes:

    MMHG


The parser can then safely process the remaining expression without confusing the internal "m" symbol with a standalone meter unit.

---

## Expression Tokenization

The same parsing layer separates mathematical operators and functions before evaluation.

Implementation fragment:

    String[] sp1 = y1.split(
        "snh|csh|tnh|asn|acs|atn|sin|cos|tan|lg|ln|abs|\\u221B|[V%^*/+\\-]"
    );


This creates a lightweight expression decomposition mechanism.

The parser separates:

- mathematical functions
- operators
- calculation components

before further processing.

---

## Engineering Reasoning

A full compiler-style lexer could solve this problem.

However, for a compact engineering calculator system, a complete parser architecture would introduce unnecessary complexity.

The chosen solution provides:

- predictable transformation order
- low implementation complexity
- easy extension with new units
- compatibility with human-readable formulas

---

## Pattern Definition

The reusable pattern:

    Protect complex structures

            ↓

    Transform simple structures

            ↓

    Restore original structures


This approach is useful when:

- tokens overlap
- replacement order affects correctness
- expressions are entered by users
- a lightweight DSL is required

---

## Applications

Possible applications:

- engineering calculators
- unit conversion engines
- scientific expression processors
- formula interpreters
- domain-specific languages

---

## Engineering Insight

The important part of this solution is not the string replacement itself.

The main architectural decision is controlling ambiguity before transformation.

Instead of increasing parser complexity, the system creates a temporary safe representation, performs controlled operations, and restores the original semantic structure.

This is an example of practical engineering design: solving a real parsing problem with a lightweight and maintainable mechanism.
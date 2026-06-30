# Unicode Arrow as Conversion Operator: Designing a Human-Readable Unit Conversion DSL

## Overview

This article describes a user-oriented expression design pattern used in an engineering calculation system to create a simple domain-specific language (DSL) for unit conversion.

The idea is to allow users to define conversions directly inside a text field using a natural mathematical notation.

Example:

    5.2km→mi

The expression itself contains:

- source value
- source unit
- conversion operator
- target unit


Instead of using separate input fields, buttons, or configuration menus, the system interprets the expression directly.

---

## Problem

Traditional unit converters usually require multiple UI components:

- value input field
- source unit selector
- destination unit selector
- conversion button

This increases interface complexity.

For engineering applications, users often think in expressions rather than forms.

Examples:

    10ft³ to m³

    100km to mi

    5psi to bar


The challenge was creating a compact input format that remains readable for humans and simple for the parser.

---

## Solution Concept

The system uses the Unicode arrow character:

    →

as a semantic separator between source and destination units.


Expression format:

    value + source unit → target unit


Example:

    25ft³→m³


The parser interprets:

    25

as value,

    ft³

as source unit,

and:

    m³

as target unit.

---

## Original Implementation Fragment

The user interface inserts the conversion operator directly into the expression field:

    bcuft.setOnAction(event -> {

        if (me == 0) {

            X.replaceSelection("ft³\u2192");

            me = 1;

        } else {

            X.replaceSelection("ft³");

        }

    });


The first action inserts:

    ft³→


The second action completes the target unit:

    ft³


This creates a guided input mechanism without additional UI controls.

---

## Parser Logic

The expression is later processed by splitting the input around the Unicode arrow:

    \u2192


Conceptually:

    25ft³→m³


becomes:

    source side | target side


Result:

    25ft³

and:

    m³


The calculation engine can then determine the conversion path.

---

## Why Unicode Was Used

The arrow symbol was chosen because it is:

- visually understandable
- close to mathematical notation
- rarely used inside unit names
- immediately recognizable as a transformation operator

The expression becomes self-explanatory.

Example:

    km→mi

is understood without additional labels.

---

## Engineering Reasoning

Instead of building a complex interface around the calculation engine, the system moves part of the interaction into the expression language itself.

The user input becomes both:

- a command
- a readable engineering statement


This reduces UI complexity while keeping the workflow flexible.

---

## Pattern Definition

The reusable pattern:

    Human-readable notation

            ↓

    Lightweight parsing rule

            ↓

    Engineering calculation


This approach is useful when:

- users already understand domain notation
- expressions are short
- the interface should remain minimal
- a full programming language is unnecessary

---

## Applications

Possible applications:

- engineering calculators
- scientific tools
- CAD-related utilities
- measurement conversion systems
- technical command interfaces

---

## Engineering Insight

A good engineering interface does not always require more controls.

Sometimes the best solution is to create a simple language that matches the user's mental model.

The Unicode arrow pattern transforms a text field into a compact engineering command interface while preserving readability and usability.
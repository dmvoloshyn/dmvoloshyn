# Engineering Pattern: Numeric Input Integrity Layer
## Protecting Business Data at the UI Boundary

---

## 1. Overview

In business applications, user input is not only a visual interaction layer. It is the first boundary where data integrity can either be preserved or lost.

A typical numeric input field assumes that the user is responsible for entering a correct value. However, in cost estimation systems, engineering applications, and financial software, a small editing mistake can silently change the meaning of the data.

Example:

`1.50 → 150`

The value remains syntactically valid, but the business meaning is completely different.

The Numeric Input Integrity Layer pattern introduces a protection mechanism directly at the input boundary.

The core idea:

> The input component should protect the semantic meaning of data, not only validate its format.

---

## 2. The Problem

Traditional numeric fields usually solve only a simple validation problem:

* allow digits
* allow decimal separators
* reject unsupported characters

The typical model:

`User Input → Validation → Accept / Reject`

This approach is sufficient for simple applications. However, real engineering and business systems require additional protection:

* users edit existing values
* users remove characters inside numbers
* different locales use different separators
* clipboard operations introduce unexpected formats
* editing should not silently change numerical meaning

The problem is not only invalid input. The problem is the **destructive transformation of valid input**.

---

## 3. Existing Approaches

### 3.1 Character Filtering

The simplest approach removes unsupported characters.

Example: `1a.50 → 1.50`

**Advantages:**
* simple implementation
* low maintenance cost

**Limitations:**
* does not understand user intention
* can silently modify values
* protects syntax but not meaning

### 3.2 Post-Validation After Editing

Another common approach:

`Input → Validation → Correction`

**Advantages:**
* clear separation between input and validation

**Limitations:**
* the incorrect transformation already happened
* recovery logic becomes more complex
* user experience becomes less predictable

### 3.3 Immediate Numeric Conversion

A more advanced design converts text immediately into a numeric model.

Architecture: `TextField → Parser → Numeric Model → Formatted Output`

**Advantages:**
* strong data representation
* suitable for complex domains

**Limitations:**
* editing becomes harder
* cursor management becomes more complicated
* partial numeric states are difficult to support

---

## 4. Numeric Input Integrity Layer Approach

The Numeric Input Integrity Layer introduces protection inside the editing process itself.

Instead of asking: *«Is the final value valid?»*

The system asks: *«Did this editing operation destroy the semantic structure of the number?»*

Example:

Before: `1.50`
The user deletes the separator.
Possible result: `150`

The integrity layer detects:
1. the original value contained a separator
2. the new value lost the separator
3. the numeric meaning changed

The separator is **restored automatically**. The system protects the transition between states, not only the final state.

---

## 5. Architectural Model

The pattern creates a dedicated boundary layer:

`User Interaction`
↓
`Numeric Input Integrity Layer`
↓
`Business Calculation Layer`
↓
`Cost Estimation Engine`

The architectural principle:

> Invalid semantic states should be prevented before entering the calculation domain.

This is especially important in estimation systems because incorrect values can propagate into quantities, prices, totals, and generated reports.

---

## 6. Engineering Concept

The important idea is not simply detecting a missing decimal separator. That problem is common.

The engineering value is:

> Preserving the continuity of user-created numerical meaning during mutation.

The input field becomes more than a text container. It becomes a controlled editing environment where state transitions are monitored and protected.

---

## 7. Practical Code Implementation

The implementation uses JavaFX TextFormatter as an interception layer between the user action and the final text state.

Every editing operation passes through a filter before being applied. The filter receives:
* previous text state
* requested modification
* resulting text state

**Original implementation logic:**

    UnaryOperator<TextFormatter.Change> filter = change -> {
        String oldText = change.getControlText();
        String newText = change.getControlNewText();

        if (change.isDeleted()) {
            boolean oldHasSep = oldText.contains(".") || oldText.contains(",");
            boolean newHasSep = newText.contains(".") || newText.contains(",");

            if (oldHasSep && !newHasSep) {
                String sep = formatNumber(1.1).contains(",") ? "," : ".";
                int pos = change.getRangeStart();

                String restored = newText.substring(0, pos) + sep + newText.substring(pos);
                change.setText(restored);
            }
        }
        return change;
    };

The filter analyzes the difference between the old and new state. If the editing operation removes a critical numerical separator, the system restores the structure before the value reaches the calculation layer.

---

## 8. Relation to System Architecture

This pattern belongs to the input integrity layer of the application architecture.

The complete flow becomes:

`Input Protection` → `Domain Processing` → `Calculation Engine` → `Document Generation`

A reliable system does not only require correct algorithms. It also requires reliable data entering those algorithms.

---

## 9. Relation to Previous Engineering Patterns

The Numeric Input Integrity Layer extends the same architectural principle used in previous patterns:

* **Mask–Unmask Token Safety Pattern:** Protects semantic meaning during text transformation.
* **String Rewrite Expression Engine:** Processes structured information after the input has been normalized.
* **Reactive Listener Model:** Provides controlled reaction to state changes.

The common principle:

> Preserve meaning before processing.

---

## 10. Limitations and Applicability

This pattern is not a replacement for complete numeric modeling or parsing systems.

It is optimal when:
* users directly edit numerical values
* values have business significance
* accidental modification has a high cost

**Typical applications:**
* cost estimation systems
* engineering software
* accounting applications
* measurement tools

For scientific computing with complex mathematical expressions, dedicated parsers and numerical models remain more appropriate.

---

## 11. Engineering Value

The main value of this pattern is not restoring a separator. The deeper architectural principle is:

> The UI boundary is part of the data integrity architecture.

A mature application does not wait until data reaches the calculation engine to discover that meaning has already been lost. 
The Numeric Input Integrity Layer creates a controlled bridge between human editing behavior and deterministic software processing.

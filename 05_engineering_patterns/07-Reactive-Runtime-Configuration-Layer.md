# Reactive Runtime Configuration Layer
## Dynamic Application State Switching in JavaFX

---

## 1. Overview

Modern desktop applications often contain runtime settings that affect the entire user interface:

* application language
* visual theme
* display modes
* user preferences
* interface behavior options

The traditional approach treats these changes as isolated updates:

`Configuration Change → Find Components → Update Values Manually`

This works for small applications. However, as the application grows, manual synchronization becomes increasingly complex. Every new UI component must know when and how to refresh its state.

The Reactive Runtime Configuration Layer pattern introduces another approach:

> Configuration changes are represented as application state transitions, and dependent components react automatically through bindings.

The main idea:

`Runtime State Change → Reactive Dependency Graph → Automatic UI Update`

---

## 2. The Problem with Traditional Runtime Configuration

A common implementation stores settings and applies them manually.

The process becomes:
Change configuration → update button text → update labels → update menus → refresh screens.

**Advantages:**
* simple for small applications
* direct control over updates

**Limitations:**
* every component requires explicit update logic
* configuration management becomes coupled with UI code
* new components increase synchronization complexity

The problem is not storing configuration. The problem is propagating configuration changes through the system.

---

## 3. Existing Approaches

### 3.1 Manual Component Refresh

The application keeps references to UI elements and updates them after a configuration change.

Typical flow:
`loadConfiguration() → button.setText() → label.setText() → menu.setText()`

**Advantages:**
* easy to understand
* direct control

**Limitations:**
* strong coupling
* repetitive code
* difficult maintenance as the UI grows

### 3.2 ResourceBundle-Based Localization

The standard Java approach uses external resource files.

Architecture:
`Resource Files → ResourceBundle → UI Components`

**Advantages:**
* standard Java solution
* good separation of translation data

**Limitations:**
* runtime switching requires additional refresh logic
* live updates are not automatic
* application state and presentation remain connected manually

### 3.3 Global State Management Systems

Large applications often introduce dedicated state stores.

Architecture:
`Application State → Subscribers → UI Updates`

**Advantages:**
* scalable
* explicit state management

**Limitations:**
* additional infrastructure
* unnecessary complexity for smaller desktop systems

---

## 4. Reactive Runtime Configuration Layer Approach

The proposed approach treats configuration as observable application state.

Instead of:
*Change configuration → manually update components*

the model becomes:
*Change configuration state → dependent components recalculate automatically*

The application maintains a reactive state trigger. When this state changes, all connected bindings update their values.

---

## 5. Architectural Model

The architecture becomes:

`Runtime Configuration State`
↓
`Reactive Binding Layer`
↓
`UI Components`
↓
`Updated Application View`

The configuration layer does not directly control visual elements. It changes state. The reactive dependency graph controls propagation.

---

## 6. Practical Implementation

The implementation uses JavaFX observable properties.

A configuration version property acts as a reactive trigger:

    private final IntegerProperty langVersion = new SimpleIntegerProperty(0);

Runtime translation values are stored in a map:

    private final Map<String, String> tr = new HashMap<>();

A reusable binding method connects UI elements to the configuration state:

    private StringBinding t(String key) {
        return Bindings.createStringBinding(
            () -> {
                String value = tr.get(key);
                return value == null ? key : value;
            },
            langVersion
        );
    }

A UI element subscribes once:

    lContractor.textProperty().bind(Bindings.concat(t("contractor"), ":"));

The language change updates only the configuration state:

    private void loadLang(Lang lang) {
        tr.clear();
        switch(lang) {
            case EN -> {
                tr.put("contractor", "Contractor");
            }
            case ES -> {
                tr.put("contractor", "Contratista");
            }
        }
        langVersion.set(langVersion.get() + 1);
    }

After the state change, all dependent bindings refresh automatically. No manual search through UI components is required.

---

## 7. Engineering Concept

The important idea is not storing translations in a HashMap. That is only an implementation detail.

The engineering pattern is:

> Runtime configuration becomes an observable state model instead of a sequence of imperative update commands.

Traditional model:
`Do update A → Do update B → Do update C`

Reactive model:
`State changed → Dependency graph reacts`

---

## 8. Relation to System Architecture

This pattern belongs to the runtime orchestration layer.

The system architecture becomes:

`Input Layer`
↓
`Processing Layer`
↓
`Calculation Engine`
↓
`Reactive Runtime Configuration Layer`
↓
`Presentation Layer`

The runtime layer acts as a communication mechanism between internal application state and visible behavior.

---

## 9. Relation to Previous Engineering Patterns

### Reactive Listener Execution Model
This pattern is a direct extension.
* Reactive Listener Model: `Event → Reaction`
* Reactive Runtime Configuration Layer: `State Change → Dependency Graph Update`

The first describes the mechanism. The second describes the architectural usage.

### Numeric Input Integrity Layer
Both patterns protect controlled state transitions.
* Numeric Input Integrity Layer: `User Action → Protected Value Change`
* Reactive Runtime Configuration Layer: `Configuration Change → Controlled Application Update`

### String Rewrite Expression Engine
Both follow the same architectural principle:

> System behavior should be produced through controlled transformations of state.

---

## 10. Applicability and Limitations

This pattern is optimal when:
* settings can change during runtime
* multiple components depend on shared configuration
* immediate UI updates are required

Suitable examples:
* desktop business applications
* engineering software
* interactive calculators
* dashboards

It is less useful when configuration is loaded once at startup and never changes.

---

## 11. Engineering Value

The value of this pattern is not dynamic language switching itself. The deeper architectural principle is:

> Application configuration should behave as a reactive state model.

This reduces coupling between configuration logic and presentation logic. The result is a system where runtime changes propagate naturally through the architecture instead of requiring manual synchronization.

The Reactive Runtime Configuration Layer transforms configuration management from a collection of update procedures into a controlled reactive execution model.

## Navigation

[Back to System Overview](../00_system/System-Overview.md)
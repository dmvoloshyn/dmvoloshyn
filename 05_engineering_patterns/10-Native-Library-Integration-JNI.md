# Native Library Integration Through JNI

## Java-to-Native Computational Boundary

### Abstract

High-level Java applications may need to reuse specialized native libraries when the required computational capability already exists outside the Java runtime.

This pattern defines an explicit integration boundary between Java application logic and native C++ computational libraries using the Java Native Interface (JNI).

### Architectural Model

Java Application
      ↓
JNI Integration Layer
      ↓
Native C++ Library
      ↓
Native Result
      ↓
Java Data Processing

The Java application remains responsible for application logic, workflow orchestration, validation, persistence, and user interaction.

The native library remains responsible for specialized computational operations.

### Core Principle

The integration boundary must prevent native implementation details from propagating through the complete application architecture.

JNI therefore acts as a controlled computational interface rather than simply a mechanism for calling native code.

### Engineering Objectives

- reuse specialized native computational capabilities;
- avoid unnecessary reimplementation;
- isolate platform-specific components;
- maintain a stable Java-side application architecture;
- provide controlled data exchange between runtimes;
- preserve separation between computation and presentation.

### Application

This pattern is used in scientific desktop software where Java/JavaFX application architecture integrates existing native C++ scientific libraries through JNI.

The pattern is particularly useful when specialized computational libraries already exist in native form and must be incorporated into a higher-level application workflow.

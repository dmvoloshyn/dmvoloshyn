# Dual-Mode Scientific Analysis Architecture

---

## Individual Measurement and Spatial-Temporal Dataset Analysis

---

## 1. Abstract

Scientific applications may need to support both detailed analysis of an individual measurement and analysis of multiple observations across spatial and temporal dimensions.

Treating these as completely separate applications creates duplicated data models and processing logic.

This pattern provides multiple analytical workflows over a shared scientific data architecture.

---

## 2. Architectural Model

              Persistent Research Data
                         ↓
           b Shared Data / Domain Model
                    ↙         ↘
                   ↓            ↓
      Single Measurement   Spatial-Temporal
           Analysis            Analysis
                   ↓            ↓
                 Shared Calculation
                 & Validation Logic

---

## 3. Single Measurement Mode

The individual-analysis workflow provides detailed examination of one research record.

Typical operations include:

- inspection of measurement data;
- derived calculations;
- analysis results;
- research notes;
- manual validation;
- automated quality assessment.

---

## 4. Spatial-Temporal Mode

The second workflow operates on selected groups of research records and supports analysis across:

- geographic dimensions;
- temporal dimensions;
- multiple observations;
- comparative datasets;
- deeper spatial-temporal tests.

---

## 5. Shared Infrastructure

Both modes can reuse:

- persistent research data;
- calculation services;
- validation mechanisms;
- structured data processing;
- History Journal;
- user notes;
- reporting infrastructure.

---

## 6. Engineering Objective

The objective is to provide different analytical workflows without duplicating the underlying scientific data architecture.

This allows a single persistent research environment to support both detailed record-level analysis and broader spatial-temporal investigation.

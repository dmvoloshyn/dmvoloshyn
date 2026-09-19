# Live-Data Grounding for Agentic Systems

---

## External Data as the Factual Execution Source

---

## 1. Abstract

An LLM may contain useful general knowledge but should not automatically be treated as the authoritative source for current domain data.

This pattern separates reasoning from factual data retrieval.

---

## 2. Architectural Model

```text
    User Request
           ↓
    LLM Reasoning
           ↓
    Tool Selection
           ↓
   Live External API
           ↓
Current Structured Data
           ↓
Validation / Processing
           ↓
     LLM Reasoning
           ↓
   Grounded Response
```

---

## 3. Core Principle

The model is used for reasoning and coordination, while factual domain information is retrieved from live external services.

This creates an explicit boundary between:

- probabilistic reasoning;
- deterministic retrieval;
- structured data;
- final response generation.

---

## 4. Hallucination-Risk Reduction

Grounding factual responses in retrieved external data reduces dependence on model-internal knowledge and provides a traceable path between the user's request and the information used to construct the response.

The objective is not to eliminate model uncertainty completely, but to reduce unsupported factual generation by requiring relevant information to pass through controlled data-retrieval paths.

---

## 5. Application

The pattern is implemented in the NASA Enterprise Mission Control Agent, where live NASA API data is used as the factual basis for research-oriented responses.


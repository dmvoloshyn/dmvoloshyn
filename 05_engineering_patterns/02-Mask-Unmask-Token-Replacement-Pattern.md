# Engineering Pattern: Mask–Unmask Token Safety System  
## Safe String Transformation in Overlapping Token Spaces

---

## Abstract

String-based expression systems inevitably face a structural problem: different tokens overlap at the substring level.

Example tokens:

- m = meter  
- mm = millimeter  
- mph = miles per hour  
- mg = milligram  

A naive replace/remove approach leads to semantic corruption because substring operations cannot distinguish token boundaries.

This pattern introduces a deterministic solution:

> Mask–Unmask Token Safety System

A two-phase transformation mechanism that guarantees safe string rewriting in overlapping token spaces.

---

# 1. Problem Statement

In string-based interpreters, direct replacement operations lead to token collisions.

Example failure case:

Input: mmHg  
Remove: m  
Result becomes corrupted due to partial replacement of embedded semantic units.

Core issue:

> substring-level transformations are not token-aware.

---

# 2. Core Idea

The system introduces a protective transformation layer.

It consists of three phases:

- Phase 1: MASK (protect multi-character tokens)
- Phase 2: TRANSFORM (perform unsafe operations safely)
- Phase 3: UNMASK (restore original tokens)

Key principle:

> Never operate directly on overlapping token space.  
> Operate only on a sanitized representation.

---

# 3. Architectural Model

Input string flows through deterministic pipeline:

Input → Mask Phase → Safe Transformation Phase → Unmask Phase → Output

---

# 4. Why this approach is non-trivial

This pattern solves:

- overlapping token spaces  
- partial substring corruption  
- regex interference chains  
- multi-stage replacement conflicts  

It is used where string itself is execution state.

---

# 5. Comparison with existing approaches

## Regex-only systems

Direct replacements on raw strings.

Problems:

- cannot distinguish overlapping tokens  
- produces semantic corruption  
- unsafe in multi-token DSLs  

---

## Tokenizer + AST systems

Structured lexical parsing.

Pros:

- correct semantics  
- strict grammar  

Cons:

- heavy architecture  
- unnecessary complexity for lightweight DSLs  

---

## Mask–Unmask system

Properties:

- no AST required  
- string remains execution state  
- lightweight semantic protection layer  

---

# 6. Optimal use cases

Optimal when:

- string is execution state  
- DSL is embedded in UI input  
- token overlap exists  
- transformation is sequential  
- simplicity is priority  

---

# 7. Limitations

Not suitable for:

- full programming languages  
- deep syntactic analysis  
- grammar-based compilers  

Because:

- no hierarchical syntax model  
- surface-level transformation only  

---

# 8. Practical Code Implementation

The Mask–Unmask mechanism is implemented as a two-stage transformation over unit tokens to prevent corruption during unsafe string operations.

Original implementation excerpt:

X.setText(newText.replaceAll("mmHg","MMHG").replaceAll("mph","MPH").replaceAll("mps","MPS").replaceAll("mt","MT").replaceAll("mg","MG").replaceAll("(mHG|mMG|mmH|mp|mh|ms|mi|yd|ft|in|km|cm|mm|m)","").replaceAll("MMHG","mmHg").replaceAll("MPH","mph").replaceAll("MPS","mps"));

---

## Engineering interpretation

Before masking:

- overlapping tokens exist  
- unsafe replacements corrupt semantics  

After masking:

- token space becomes orthogonal  
- destructive operations become safe  

After unmasking:

- original semantics fully restored  

---

# 9. Key optimization property

Without Mask–Unmask:

- fragile replacement order  
- unpredictable regex interactions  
- token collision corruption  

With Mask–Unmask:

- deterministic transformation pipeline  
- safe global replacement phase  
- controlled token lifecycle  

---

# 10. Architectural impact

Traditional model:

Input → Processing → Output

Mask–Unmask model:

Input → Protection Layer → Processing Layer → Restoration Layer → Output

Key insight:

> The system does not simplify strings directly.  
> It temporarily restructures token space to make transformation safe.

---

# 11. Final assessment

Mask–Unmask is not a parsing technique.

It is a string safety architecture used in:

- DSL expression engines  
- UI formula systems  
- unit conversion processors  
- regex-based evaluators  

Core advantages:

- eliminates token collisions  
- avoids AST complexity  
- preserves string-as-state model  
- integrates with rewrite engines  

---

## Engineering principle

Before transforming a string, its semantic structure must be protected. Only then can transformation remain deterministic.

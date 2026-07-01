# String Rewriting Expression Engine

## Expression Evaluation Without AST or Parser Frameworks

## Abstract

Most expression evaluators use a compiler-style architecture:

`Input → Lexer → Tokens → Parser → AST → Evaluation`

This pattern introduces another approach: **String Rewriting Expression
Evaluation**.

Instead of building an Abstract Syntax Tree, the engine repeatedly
transforms the original expression string:

1.  Find the next executable operation.
2.  Calculate the result.
3.  Replace the operation with the result.
4.  Continue until the expression is reduced.

Example:

``` text
2 + 3 * 4

2 + 12

14
```

The expression string becomes the execution state.

This is not a universal replacement for parsers. It is an optimized
architecture for compact domain-specific languages where simplicity and
transparency are more important than unlimited grammar complexity.

------------------------------------------------------------------------

# 1. The Core Pattern

Traditional architecture:

``` text
Input
↓
Lexer
↓
Parser
↓
AST
↓
Evaluation
```

String rewriting architecture:

``` text
Expression
↓
Find operation
↓
Evaluate
↓
Replace
↓
Repeat
```

The system operates directly on the user's expression instead of
creating another representation.

------------------------------------------------------------------------

# 2. Engineering Concept

This approach is closer to a term rewriting system.

Instead of:

> Build a model of the expression and execute the model

the architecture becomes:

> Transform the expression until the expression becomes the answer

------------------------------------------------------------------------

# 3. Originality

String rewriting itself is not a new mathematical concept.

Similar ideas exist in:

-   symbolic mathematics
-   algebraic simplification
-   rule engines
-   macro systems

The engineering originality is the practical combination:

-   user-facing formulas
-   arithmetic precedence
-   direct string reduction
-   DSL integration
-   no AST layer
-   minimal implementation

The expression text acts as:

-   input format
-   intermediate representation
-   execution state

------------------------------------------------------------------------

# 4. Comparison With Existing Approaches

## AST-Based Evaluation

Architecture:

``` text
Input → Lexer → Parser → AST → Evaluator
```

Advantages:

-   scalable
-   supports variables
-   supports complex grammar
-   suitable for programming languages

Disadvantages:

-   more code
-   more objects
-   more abstraction
-   higher implementation complexity

------------------------------------------------------------------------

## Shunting Yard

Architecture:

``` text
Infix expression → Postfix notation → Stack evaluation
```

Advantages:

-   mathematically proven
-   efficient
-   correct precedence handling

Disadvantages:

-   requires tokenization
-   requires stacks
-   requires additional parser logic

------------------------------------------------------------------------

## Regex-Based Calculation

Advantages:

-   very simple

Disadvantages:

Breaks down with:

-   nested expressions
-   functions
-   unary operators
-   complex precedence

------------------------------------------------------------------------

## String Rewriting Engine

Architecture:

``` text
Expression
↓
Locate operation
↓
Calculate
↓
Replace
↓
Continue
```

Advantages:

-   minimal architecture
-   low implementation cost
-   transparent debugging
-   natural integration with custom DSL syntax

------------------------------------------------------------------------

# 5. Where It Is Optimal

This pattern is optimal for:

-   engineering calculators
-   construction estimation systems
-   unit converters
-   formula editors
-   small embedded DSLs

It works best when:

-   grammar is controlled
-   syntax is limited
-   readability matters

------------------------------------------------------------------------

# 6. Where It Is Not Optimal

Not recommended for:

-   programming languages
-   large interpreters
-   symbolic mathematics systems
-   high-performance calculation engines

AST or compiled representations are better in those cases.

------------------------------------------------------------------------

# 7. Architectural Perspective

Traditional architecture:

``` text
Input
↓
Representation
↓
Execution
```

String rewriting:

``` text
Input
↓
Transformation
↓
Result
```

The main architectural advantage is removing unnecessary layers.

------------------------------------------------------------------------

# 8. Practical Code Implementation

The implementation usually contains:

## Operator Detection

Find:

``` text
*
/
+
-
```

## Operand Extraction

Example:

``` text
12*5
```

becomes:

``` text
12
*
5
```

## Calculation

``` text
12*5
```

becomes:

``` text
60
```

## Replacement

``` text
12*5+3
```

becomes:

``` text
60+3
```

The process repeats.

------------------------------------------------------------------------

# 9. Optimization Characteristics

## Memory

AST:

``` text
Expression
↓
Many objects
↓
Tree
```

String rewriting:

``` text
Expression
↓
Single mutable string
```

------------------------------------------------------------------------

## Development

AST:

-   higher initial cost
-   more infrastructure

String rewriting:

-   smaller codebase
-   faster implementation

------------------------------------------------------------------------

## Debugging

Intermediate states are visible:

``` text
5+3*2

5+6

11
```

This makes the execution process easier to inspect.

------------------------------------------------------------------------

# 10. Final Engineering Assessment

String Rewriting Expression Engine is not a universal parser
replacement.

It is a specialized engineering pattern optimized for:

-   compact DSLs
-   engineering calculators
-   formula systems
-   unit conversion tools

Its strength is not maximum theoretical performance.

Its strength is:

-   architectural simplicity
-   fewer components
-   smaller codebase
-   easier debugging
-   direct connection between rules and implementation

AST is superior for complex languages.

Shunting Yard is superior for formal expression parsing.

String rewriting is superior when the language is small, controlled, and
human-oriented.

The engineering lesson:

> The best architecture is not always the most powerful architecture.

> It is the architecture that most efficiently solves the actual
> problem.

# String Rewriting Expression Engine

## Expression Evaluation Without AST or Parser Frameworks

## Abstract

Most expression evaluators use a compiler-style architecture:

Input → Lexer → Tokens → Parser → AST → Evaluation

This pattern introduces another approach: **String Rewriting Expression
Evaluation**.

Instead of building an Abstract Syntax Tree, the engine repeatedly
transforms the original expression string.

The algorithm:

1.  Find the next executable operation.
2.  Calculate the result.
3.  Replace the operation with the result.
4.  Continue until the expression is reduced.

Example:

The expression 2 + 3 \* 4 is transformed step by step:

2 + 3 \* 4 → 2 + 12 → 14

The expression string itself becomes the execution state.

This is not a universal replacement for parsers. It is an optimized
architecture for compact domain-specific languages where simplicity,
transparency, and implementation efficiency are more important than
unlimited grammar complexity.

------------------------------------------------------------------------

# 1. The Core Pattern

Traditional architecture:

Input → Lexer → Parser → AST → Evaluation

String rewriting architecture:

Expression → Find operation → Evaluate → Replace → Repeat

The system operates directly on the user's expression instead of
creating another representation.

------------------------------------------------------------------------

# 2. Engineering Concept

This approach is closer to a term rewriting system.

Instead of:

"Build a model of the expression and execute the model"

the architecture becomes:

"Transform the expression until the expression becomes the answer"

------------------------------------------------------------------------

# 3. Originality

String rewriting itself is not a new mathematical concept.

Similar ideas exist in:

-   symbolic mathematics
-   algebraic simplification
-   rule engines
-   macro systems

The engineering originality is the practical combination of:

-   user-facing formulas
-   arithmetic precedence
-   direct string reduction
-   DSL integration
-   no AST layer
-   minimal implementation

The expression text acts simultaneously as:

-   input format
-   intermediate representation
-   execution state

------------------------------------------------------------------------

# 4. Comparison With Existing Approaches

## AST-Based Evaluation

Architecture:

Input → Lexer → Parser → AST → Evaluator

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

AST is the correct architecture for large languages and complex
interpreters.

------------------------------------------------------------------------

## Shunting Yard Algorithm

Architecture:

Infix expression → Postfix notation → Stack evaluation

Advantages:

-   mathematically proven
-   efficient
-   correct precedence handling

Disadvantages:

-   requires tokenization
-   requires stacks
-   requires additional parser logic

Shunting Yard is excellent for formal mathematical expression
processing.

------------------------------------------------------------------------

## Regex-Based Calculation

Advantages:

-   very simple implementation

Disadvantages:

It becomes difficult to maintain with:

-   nested expressions
-   functions
-   unary operators
-   complex precedence rules

Regex alone is usually not a complete expression architecture.

------------------------------------------------------------------------

## String Rewriting Engine

Architecture:

Expression → Locate operation → Calculate → Replace → Continue

Advantages:

-   minimal architecture
-   smaller codebase
-   transparent execution
-   easy debugging
-   natural integration with custom DSL syntax

------------------------------------------------------------------------

# 5. Where This Pattern Is Optimal

This pattern is optimal for:

-   engineering calculators
-   construction estimation systems
-   unit converters
-   formula editors
-   small embedded DSLs

It works best when:

-   grammar is controlled
-   syntax is limited
-   readability is important
-   users interact directly with expressions

------------------------------------------------------------------------

# 6. Where This Pattern Is Not Optimal

This approach is not recommended for:

-   programming languages
-   large interpreters
-   symbolic mathematics systems
-   high-performance calculation engines

In those cases, ASTs, bytecode, or compiled representations are more
appropriate.

------------------------------------------------------------------------

# 7. Architectural Perspective

Traditional architecture:

Input → Representation → Execution

String rewriting architecture:

Input → Transformation → Result

The main architectural advantage is removing layers that do not provide
value for the specific problem domain.

The expression remains the central object throughout the entire
execution process.

------------------------------------------------------------------------

# 8. Practical Code Implementation

The implementation usually contains several stages.

## Operator Detection

The engine searches for supported operations such as:

-   multiplication
-   division
-   addition
-   subtraction
-   mathematical functions

## Operand Extraction

A fragment such as 12\*5 is separated into:

12 → operator → 5

## Calculation

The operation is evaluated:

12\*5 becomes 60

## Replacement

The original fragment:

12\*5+3

becomes:

60+3

The cycle continues until the expression is fully reduced.

## Original Implementation Excerpt

The following excerpt represents the core execution mechanism of the String Rewriting Expression Engine.

It demonstrates how operator precedence is handled directly through evaluation order without AST, parser, or stack-based evaluation.

```java
do {

    if (x.matches(".*[*/].*")) {

        // multiplication and division have higher priority
        // evaluated directly on extracted operands

        Y5 = Y3 * Y4;

        // replace evaluated fragment back into the expression string

        break;
    }

    if (x.matches(".*[+-].*") 
        && !x.matches(".*[*/].*")) {

        // addition and subtraction are evaluated only
        // after higher priority operations are resolved

        Y5 = Y3 + Y4;

        break;
    }

}
while (x.matches(".*(snh|csh|tnh|sin|cos|tan|lg|ln|abs|[V%^*/+-]).*"));


------------------------------------------------------------------------

# 9. Optimization Characteristics

## Memory Efficiency

AST approach:

Expression → many objects → tree structure

String rewriting approach:

Expression → single mutable representation

The memory model is simpler.

------------------------------------------------------------------------

## Development Complexity

AST:

-   higher initial development cost
-   more infrastructure
-   more abstraction layers

String rewriting:

-   smaller implementation
-   faster development
-   fewer components

------------------------------------------------------------------------

## Debugging

String rewriting exposes intermediate states naturally.

Example:

5+3\*2 → 5+6 → 11

The transformation path is visible without additional debugging tools.

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

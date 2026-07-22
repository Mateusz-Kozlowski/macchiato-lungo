# Macchiato Lungo — Java Interpreter and Debugger

Macchiato Lungo is my implementation of a small procedural programming language interpreter in Java, developed as a two-part Object-Oriented Programming coursework project at the Faculty of Mathematics, Informatics and Mechanics, University of Warsaw.

The project models Macchiato programs as Java objects, executes them, and provides debugger-style execution control and memory inspection.

The original assignment specifications are available in:

- [`assignment1.md`](assignment1.md)
- [`assignment2.md`](assignment2.md)

## Highlights

- Implemented an interpreter for a small procedural language in Java.
- Modeled language constructs using an object-oriented class hierarchy.
- Supported integer expressions, variables, assignments, blocks, loops, conditionals, and print instructions.
- Implemented scoped variable declarations and variable shadowing.
- Added execution error handling with contextual variable-state reporting.
- Built an interactive debugger with continue, step, display, and exit commands.
- Extended the language with procedures, parameters, procedure calls, and dynamic variable binding.
- Added debugger memory dumps to a file.
- Created a builder-style Java API for constructing Macchiato programs programmatically.
- Added JUnit tests for language constructs.

## Language features

Macchiato programs are represented directly in Java code rather than parsed from source files.

Supported constructs include:

- blocks with local declarations,
- integer variables,
- arithmetic expressions,
- assignments,
- `for` loops,
- conditional instructions,
- print instructions,
- procedures with parameters,
- procedure calls,
- nested scopes and variable shadowing.

## Debugger

The interpreter can run programs in normal mode or debugging mode.

The debugger supports:

- `c` — continue execution,
- `s <number>` — execute a given number of steps,
- `d <number>` — display visible variables from the selected scope level,
- `e` — exit the debugger,
- `m <path>` — dump the current memory state to a file.

## Program construction API

Macchiato programs can be built through a fluent Java API inspired by the builder pattern.

Example:

```java
var program = new BlockBuilder()
    .declareVariable('x', Literal.of(101))
    .declareVariable('y', Literal.of(1))
    .declareProcedure("out", List.of('a'), new BlockBuilder()
        .print(Sum.of(Variable.named('a'), Variable.named('x')))
        .build()
    )
    .assign('x', Diff.of(Variable.named('x'), Variable.named('y')))
    .invoke("out", List.of(Variable.named('x')))
    .invoke("out", List.of(Literal.of(100)))
    .block(new BlockBuilder()
        .declareVariable('x', Literal.of(10))
        .invoke("out", List.of(Literal.of(100)))
        .build()
    )
    .build();
```

## Testing

The project includes JUnit tests for Macchiato language constructs and interpreter behavior.

## Assignment context

This project was developed in two stages.

The first stage focused on implementing the core Macchiato language, including program execution, expressions, variables, blocks, loops, conditionals, error handling, and a basic debugger.

The second stage extended the language with procedures, procedure calls, dynamic variable binding, memory dump support, a builder-style API for constructing programs, and JUnit tests.

For the full specifications, see:

- [`assignment1.md`](assignment1.md)
- [`assignment2.md`](assignment2.md)

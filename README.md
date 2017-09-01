
# CROAK

Math notation for humans.
    

## BASICS

All statements use polish notation.


### VALUES

    42
    x
    :x
    sqrt


### ASSIGNMENT

We differentiate between symbols and variables.

Symbols represent the literal symbol, while variables represent the value assigned to the symbol.

`x` is meaningless on its own.

`:x` refers to the literal "x" symbol on its own.

Assignment is a necessary evil.

    ≔ :x 42
    =  x 42


### ASSIGNMENT

    ≔ :x 42


### PRECEDENCE

Functions accept the two things immediately to their right.

There is no operator precedence.

If you want to group executions, use parentheses.

    = 6 (* 2 3)


### TYPES

TODO


### FUNCTIONS

Functions only take one argument.

    f 42
    
To construct functions that contain multiple arguments, just make chains of second-order functions.

    f 1 2 3
    
To do this, you can use lambdas.

    ≔ identity (λ :x x)

The "lambda" (abstraction) function accepts a _symbol_ and returns a function that accepts a mathematical statement.

TODO: type of lambdas


## NOTES

This would probably be better done on paper first.

Forget about types and stuff and just make it usable. Worry about making it "correct" later.

Think long and hard about monadic vs dyadic operators.

At some point in time, I want to redo all the symbols to make them "intuitive", and then make a font for beautiful, convenient typing experiences.

### RESEARCH

- https://en.wikipedia.org/wiki/Simply_typed_lambda_calculus
- https://en.wikipedia.org/wiki/Calculus_of_constructions


# CROAK

Math notation for humans.
    

## BASICS

All statements use polish notation.


### VALUES

    42
    x
    `x
    sqrt
    true


### ASSIGNMENT

We differentiate between symbols and variables.

Symbols represent the literal symbol, while variables represent the value assigned to the symbol.

`x` is meaningless on its own.

``x` refers to the literal "x" symbol on its own.

Later you'll see that the backtick is actually a deferred evaluation operator. 
It accepts text and returns a symbol.

Assignment is a necessary evil.

    ≔ `x 42
    =  x 42


### PRECEDENCE

Functions accept only one argument at a time.
Return a second function if you want to accept multiple arguments.
Currying makes this easy.

There is no operator precedence.

To group expressions, use spacing.

    =   4   + 2 2

    =   identity   λ `x x
    
In the above example, we showcase all three levels of grouping.
The tightest grouping is ``x`, which is a backtick operator and the expression `x` lumped together.
Next, we have `λ 'x x` which uses single spaces to let things breathe.
Lastly, we have the entire expression, which uses triple spaces to separate each subexpression.

If you want to group really complicated executions, use indentation.

    = true
      = 6 
        * 2 3
        
    = true
    | = 6 
    | | * 2 3
        
Each line is evaluated on its own and used as an argument for the parent function.


### TYPES

TODO


### FUNCTIONS

Functions only take one argument.

    g 42
    
To construct functions that contain multiple arguments, just make chains of second-order functions.

    f 1 2 3
    
To do this, you can use lambdas.

    ≔ f
      λ `x 
        λ `y 
          λ `z 
             + x 
               y

Lambdas may also accept an ordered set of symbols.

    =   4   λ [] 4
      
A lambda that accepts no arguments is just a value.

TODO: type of lambdas

## ARRAYS

The `[` operator returns `[` until it receives the `]` operator, which is a function that takes no values.

After it accepts its stop character, `[`, it returns an array of all the things that were passed into it.

BUG: we may have to break, and use lisp-style argument lists.
BUG: i.e. functions may have to accept all their arguments at once, to get around the stop character problem
BUG: this misses some mathematical elegance, but it will likely be easier to write


## NOTES

This would probably be better done on paper first.

Forget about types and stuff and just make it usable. Worry about making it "correct" later.

Think long and hard about monadic vs dyadic operators.

At some point in time, I want to redo all the symbols to make them "intuitive", and then make a font for beautiful, convenient typing experiences.
Making a font shouldn't be too difficult, right?

Do we want to keep `+`, `-`, `*`, `/`?

### RESEARCH

- https://en.wikipedia.org/wiki/Simply_typed_lambda_calculus
- https://en.wikipedia.org/wiki/Calculus_of_constructions

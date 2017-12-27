
# Croak

Math notation for humans.

Compare against https://en.wikipedia.org/wiki/List_of_mathematical_symbols_by_subject .

Structure like https://en.wikipedia.org/wiki/Outline_of_mathematics .

## Meta

## Foundations

## Numbers

## Structure

## Space

## Change

## Logic

## Discrete

## Applied


--------------------------------------------------------------------------------

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

TODO: group by underline?


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

## HYPEROPERATORS

"Hyperoperators" try to unite our favorite operations (succession, addition, multiplication, exponentiation...) in a nice family tree. Unfortunately, this usually ends up with very clumsy definitions that don't tend to exude the beauty in mathematics that we all strive to find. The recursive definitions are nice, but the variety of cases for `n <= 3` aren't pretty.
For instance, note that addition only has one inverse (subtraction), but exponentiation has two inverses (roots and logarithms).

The major divide between the two camps is their identities. Shifting something by 0 is no shift at all! While scaling something by 1 is no scale at all!

I think a good way to conceptualize the family of arithmetic operators is to split everything into "shift" and "scale". So let's create two hyperoperators (function-generating functions) to define these two groups.

TODO: https://en.wikipedia.org/wiki/Construction_of_the_real_numbers
TODO: these are both binary relations
TODO: FIELDS


### SHIFT 

When thinking in metric spaces, the shift operator moves the values in a space by a fixed amount.
Imagine a graph of a constant horizontal line, and then moving the y-axis up and down as the first argument gets larger or smaller. 

    shift : Number -> Number -> Number
    
At this point, shift is simply addition.

    ≔ add 
      shift

    ≔ identity
      shift 0

    ≔ increment 
      shift 1
          
    ≔ decrement
      shift -1

KLUDGE: use croak's metanotation


### SCALE

The first argument of the `scale` function determines the rate of growth.

    ≔ log
      scale -2

    ≔ divide
      scale -1

    ≔ ?
      scale 0

    ≔ multiply
      scale 1

    ≔ power
      scale 2

    ≔ exponent
      scale 2
          
    ≔ tetrate
      scale 3
      
The remaining two arguments are degree/repeat, followed by value.

Thus `λ   'x   scale 2 3 x` is equivalent to `x^3` in traditional notation.

TODO: scale -2.5
TODO: scale -1.5
TODO: scale -0.5
TODO: scale  0
TODO: scale  0.5
TODO: scale  1.5
TODO: scale  2.5

TODO: complex numbers (this will be necessary in finding the scale continuum)

TODO: https://en.wikipedia.org/wiki/Equation_x%CA%B8%3Dy%CB%A3
TODO: I REALLY like visualizing `e` this way! It's the only number that's also its own `x^y=y^x` pair. It's "caused" by the commutative nature of exponentiation.

## NOTES

This would probably be better done on paper first.

Forget about types and stuff and just make it usable. Worry about making it "correct" later.

Think long and hard about monadic vs dyadic operators.

At some point in time, I want to redo all the symbols to make them "intuitive", and then make a font for beautiful, convenient typing experiences.
Making a font shouldn't be too difficult, right?
First play around with a 16x8-pixel character set.

Do we want to keep `+`, `-`, `*`, `/`?

Get rid of terms like "y-axis" that refer to variables that aren't bound. `y` isn't actually a thing.

Base-12 is easier than base-10 for the human brain. Include this in the manifesto.

Include some recommendations for alternate number characters, but don't force them.

In a sense, the standard library defines the axioms. Don't worry about going too deep! Let everything develop organically over time.

Make this into a higher-level programming language! That would be a huge "selling-point" -- computer-assisted proofs, playgrounds, easier sharing, etc.


### RESEARCH

- https://en.wikipedia.org/wiki/Sequent_calculus
- https://en.wikipedia.org/wiki/Simply_typed_lambda_calculus
- https://en.wikipedia.org/wiki/Calculus_of_constructions

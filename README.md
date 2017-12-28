
# Quack

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

    =   identity   λ any `x x
    
In the above example, we showcase all three levels of grouping.
The tightest grouping is ``x`, which is a backtick operator and the expression `x` lumped together.
Next, we have `λ any 'x x` which uses single spaces to let things breathe.
Lastly, we have the entire expression, which uses triple spaces to separate each subexpression.

If you want to group really complicated executions, use indentation.

    = true
      = 6 
        * 2 3
        
Each line is evaluated on its own and used as an argument for the parent function.

TODO: group by underline? underlines are the only precedence
TODO: underlines should also be able to be used vertically. that leaves us with an analogue that can be used in type as well! which is the pipe
TODO:   so anything right of the bar is affectively grouped with the same priority as an underline
TODO:   so `λ reals 'x |scale 2 3 x` is equivalent to underlining the `scale 2 3 x`, because you're doing a 1-line grouping. it's equivalent to `<|` in Elm


### TYPES

TODO


### FUNCTIONS

Functions only take one argument.

    g 42
    
To construct functions that contain multiple arguments, just make chains of second-order functions.

    f 1 2 3
    
To do this, you can use lambdas.

    ≔ f
      λ reals `x 
        λ reals `y 
          λ reals `z 
            + x 
              y
            

Lambdas may also accept an ordered set of symbols.

    =   4   λ [] [] 4
      
A lambda that accepts no arguments is just a value.

TODO: types of lambdas
TODO: i think it makes sense to force explicit declarations of the domain -- this will reduce errors and clear confusion

BUG: i no longer like the syntactic-sugar for multiple arguments. it's probably better to promote point-free writing, rather than bound variables

## ARRAYS

Arrays are ordered sets.

The `[` operator returns `[` until it receives the `]` operator, which is a function that takes no values.

After it accepts its stop character, `]`, it returns an array of all the things that were passed into it.

    ≔ myArray
      [ 1 2 3 ]
      
Inline arrays are not recommended in plain-text environments. Without underlined grouping, you'll likely want to put your arrays in their own definitions.

BUG: we may have to break, and use lisp-style argument lists.
BUG: i.e. functions may have to accept all their arguments at once, to get around the stop character problem
BUG: this misses some mathematical elegance, but it will likely be easier to write

TODO: underlines may actually serve as a good way to group by syntax, arrays, tuples, and sets. I think it would be easier to write, but harder to type. This seems like a worthy trade-off.
TODO: if they want to group things in a text editor, they can use indentation and definitions. NO PRECEDENCE

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

KLUDGE: use quack's metanotation


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

Thus `λ reals 'x   scale 2 3 x` is equivalent to `x^3` in traditional notation.

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

### PROOFS

Our modern methods of proofs are very fishy.
Usually, it involves three operations on symbols: symbol replacement, reordering, and balanced application.
Basically, we take some expression involving equality, and then we list out the next "result" of some undocumented operation -- and it's for the reader to figure out what happened in between the steps. Usually, this involves applying arithmetic operations to "both sides" of an equality symbol, until it gets to the point where we can rearrange the symbols and replace it with a principle/theorem/lemma elsewhere in the text -- which is also unclear unless English comments are added in between.

Another major problem arises out of symbolic manipulation and arithmetic approximation/reduction. These are two VERY different things, and yet they're never explicitly talked about in any primary-, secondary-, or tertiary-level classroom.

Wouldn't it be better if we made these meta-mathematical practices more explicit?

    ≔ eulersIdentity
      λ reals 'theta
        = 
          + 
            cos theta
            * i
              sin theta
          ^ 
            * i theta
            e
             
    assert 
      forAll 
        reals
        = true
        eulersIdentity
        
Notice some things that are omitted in normal maths. First of all, it's never stated what are supposed to be free variables, and what aren't. In Euler's Identity, theta is a completely different thing than e and i.
Next, notice that people unfamiliar with Euler's Formula are aware of what is allowed as inputs! This also forces better clarity when it comes to plugging things in, and following messier proofs.
Also notice the distinction between assignment and equality! These two are usually conflated, which leads to MUCH confusion, even among professionals. Normally , Euler's Formula would be written as a weird mixture between assignment and equality -- the first expression usually means, "This statement holds true for all the free variables (which we haven't told you) on its entire domain (which we also haven't told you)."
Even more critically, things can't be wrong unless there's some idea of "errors" or "faults" or "failed assertions". In mathematics, this is vaguely mixed in in the assignment/equality stew. When writing out some inequality, the symbols stand on their own unless evaluated! 
Consider the statement `x ≠ 2x`. Normally, you'd just reduce this to `x=2x;x/x=2;1≠2` and be on your merry way. This is something that wouldn't make you blink in a classroom setting. But good mathemeticians should be asking, "Is this a declaration or an assertion? Is `x` defined elsewhere, or is it a free variable? If it's a variable, what is it allowed to be?". But once you FORCE yourself to write the function, context, the bigger picture starts to become clear.

    ≔ example1
      λ reals `x
        = x
          * 2 x
         
This is JUST a function. It sits there, and although we can clearly see that the inside is going to cause problems, we can't just write it off explicitly. Because remember, this is just a function whose range is boolean.

    assert
      forAll
        reals
        = false
        example1
        
Uh oh! This isn't exactly true. If this were a programming language, the compiler would throw an error. What's going on here?

    assert
      = true
        example1 0

    assert
      forAll
        except 0 reals
        = false
        example1
        
    assert 
      = example1
        ≠ 0
        
(Notice that in the last example, we're declaring the equality of two FUNCTIONS.)
        
Much better.
See what I mean about clarity? It's a little fact that would've slipped through the cracks. It may seem pedantic, but these kind of errors start plague grad students in universities worldwide.
So how do we reduce it?

First of all, we have to reconcile the fact that the symbol `x` doesn't mean anything outside of the anonymous function -- it was just a placeholder in the scope of the declaration.
If we're sticklers (which we are), we wouldn't allow you to mess with the symbols of the function after its been abstracted. This is problematic, because we want to divide both sides of the function by `x`, but we have no access to it! At this point, we can either "unabstract" the function by turning it back into a group of symbols with a replacement for `x`, OR we can map into the function. Let's do that!

    ≔ example2
      map= / example1

    assert
      = example2
        λ reals _ 
          = 1 2

    assert
      forAll
        reals
        = false
        example2
        
For clarity, `map=` accepts two functions. The first gets composed into both sides of the equality in the second function. That is, the first function intercepts the argument of its target, and then accepts the body/value/image of the function as its second argument.

TODO: explain how this makes "squaring both sides" errors more identifiable

So let's get back to Euler.

    assert
      allEqual?
        ⌠ ^ *iπ e
        | lhs eulersIdentity π
        | rhs eulersIdentity π
        | +   * i sinπ   cosπ
        | +   * i 0      -1
        | +       0      -1
        |                -1

    assert
      = 
        map=
          λ reals _ 
            + 1
          eulersIdentity
          π
        = + 
            ^ *iπ e
            1
          0

    map=
      λ reals _ 
        + 1
      eulersIdentity
      π
    // the result of the function should be evaluated and display on the right...
    
BUG: that last assertion is kinda useless. it just shows that "true is true". it's probably more useful, in that case, to evaluate the whole `map=` expression
BUG: map= and lhs/rhs becomes problematic for global equations, where the body is undefined. in fact, global equations/equalities are seeming like giant headaches
        
I suppose this doesn't really prove my point, so this should be taken out, but it's a nice thing to remember!

At the top level, all you can do is `define` and `assert`. Nothing else. Definitions bind variables to the global scope (or throw errors). Assertions do nothing (or throw errors).
In workbooks, writing an expression on the left without an assertion means you should "evaluate" it on the right. Or, with computers, typing an expression means it should dynamically show what's going on beside the statement.

Let's try another example: Fourier's proof that `e` is irrational.

    ≔ f
      λ nats `n 
        / !n 1
        ; denominator first!

    ≔ e
      sum 0 inf f

    ≔ g
      λ nats `n 
        / ^n2 1
        ; denominator first!
        
    assert true
      ascending?
         ⌠ = 2       Σ 0   1 f
         | = e       Σ 0 inf f
         | = 3 |+ 1 |Σ 0 inf g
         
This is actually a prime example of why we need Quack. I tried to transcribe the "spirit" of the proof on Wikipedia, and ended up still not seeing why the final result is true. I see that this proof obviously implies that `e` is not natural, but I'm having trouble seeing why it's not rational.
I think most simple proofs could use a single assertion. To show that a number is irrational, start with the number's definition (and the number) in some equality, subsitute the number for `/ b a` and transform it until you can assert one of the numbers is not an integer (or something like that).

I think the major trick is stating the assertion FIRST, and then trying to massage your definitions into a final expression that fits in your slots. Let's try another example to show that 22/7 exceeds π.

    ≔ start
      < 0 
        ∫ 0 1
          λ reals `x 
            /
              + 1 
                ^ 2
                  x
              * ^ 4
                  x
                ^ 4
                  - x
                    1

    assert true
    ; < π
    ;   / 7 22
      >>*
        ⌠ mapRHS
        |   >>* 
        |     ⌠ map∫
        |     |  >> 
        |     |   mapNumerator expandToPolynomial
        |     |   polynomialLongDivision
        |     | definiteIntegration
        |     | arithmeticReduction
        | map<
        |     + π
        start
        
I think this is getting much closer to what I was imagining -- the assertion contains ALL of the proof!
I'm not sure about that weird composition thing yet, but I think I'm headed in the right direction. Non-destructive, high-level symbolic manipulations will work well if functions maintain a "symbolic opinion" of their internal representation.
Note that the above only makes sense if `mapRHS` and `map<` don't change the VALUE of expressions -- they're onlyl allowed to rearrange symbols and rebalance things.

BUG: `=` returns a boolean, not a value. maybe the `assert` symbol should accept two values and return the first if they're equal, otherwise throw an error

TODO: proofs should be listed as the TRANSFORMATIONS -- not the intermediate results
TODO:   this is most easily done as a list of composed functions. applying it to an expression should give you the final result
TODO: induction and contradiction

TODO: (in)equality equations should be treated more like tuples than mappings to bool

TODO: I really don't like carrying equalities around.
TODO:   i think it's better to just list the transformations as a composed list of functions
TODO:     applying the steps to "both sides" should do the trick! just assert 
        
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

Make this into a higher-level programming language! That would be a huge "selling-point" -- computer-assisted proofs, type-checking/safety, playgrounds/workbooks, easier sharing, etc.

In editors, use "literate mathematics". Unindented is English, and indented is math. This fits nicely into existing formats like markdown.

This is going to become "Quack", and the music notation will be called "Chirp".

### RESEARCH

- https://en.wikipedia.org/wiki/Sequent_calculus
- https://en.wikipedia.org/wiki/Simply_typed_lambda_calculus
- https://en.wikipedia.org/wiki/Calculus_of_constructions

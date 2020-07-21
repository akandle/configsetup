# Terms, Definitions, General Descriptions

 - Currying
    - transforms a function taking multiple arguments, into chain of single argument functions
 - Lambda Calculus
    - functions are anonymous
    - functions accept one input variable
    - currying used for mulitple inputs
    - Lambda Terms
        - A Variable, such as x
        - Abstraction:
        > if t is term, and x variable then
        >    - Ax.t is a term where A is Lambda
        > Essentially the one input is bound inside the term t
        - Application:
        > if t and s are terms, then (ts) is term
        > Represents the application of a function t to an input s

## Definitions
- Tuple
    - Ordered sequence of elements
- Cons
    - Constructor (for list)
    - cons cell is pair of values
        - car and cdr
- car
    - Contents of Address Register
    - First value of list, or head
- cdr
    - Contents of Data Register
    - contains next cons cell

**Function Definition**

Let&#39;s take a look at a simple mathematical function definition in q:

f:{[x] x:x+2;x*x}

- A function is enclosed by a pair of curly braces { and }
- Parameters are enclosed by [and]. Passing parameters is optional. More on this later.
- Inside the function is a sequence of expressions.
- The value returned is that of the last expression in the sequence being evaluated.
- Since q is not typed, there is no need of explicitly defining the types of input parameters or the return value.
- _ **The sequence is evaluated left to right. However, the individual expressions are always evaluated from right to left.** _
- Assigning the function to function name(f in the case above) is optional. (Remember Lambda functions)

## Function Application

Let&#39;s take the first definition we had a look at and apply actual arguments to it.

f:{[x] x:x+2;x*x} /Definition
 f**[3]** /Applying the actual argument to function definition
 {[x] x:x+2;x*x}**[3]** /Case when the function assigned

    q)f:{[x] x:x+2;x*x}

    q)f[3]

25

### The Void Functions – Functions that return no value

Programmers coming from a different paradigm can use the below way to define functions that return no value.

{[p1;...;pn] e1; ...; em;}

The subtle difference from the function definition we looked above is placing the semicolon (;) at the end of the sequence of expressions.

    q)f:{[x] x*x;}

    q)f[2]

### Implicit Parameter – &#39;Let x, y and z be arguments&#39;

One can omit the parameters passed to a function since implicit parameters x, y and z are automatically defined for use.

    q)f:{x+y+z}

    q)f[1;2;3]

6

### Local and Global Variables

- Local variables are defined with a single _ **colon :** _ inside a function.
- A local variable is not visible outside its immediate scope of the definition.
- A local variable is not visible within the body of a local function defined in the same scope.

Examples:

    q)/Local variable 'a' inside a function

    q)f:{[x] a:5;x+a}

    q)f[4]

9

    q)/Local variable in not outside the scope of definition

    q)f

{[x] a:5;x+a}

    q)

    q)a

&#39;a

[0] a

^

#### **Assigning Global Variables within a Function**

The _ **double-colon ::** _ operator can be used to amend or assign global variables inside of a function.

    q)a:8

    q)f:{a::9;x+a}

    q)f[7]

16

    q)a

9

## Some Important Terminology

Some important terms for functions:

**Ambivalent Functions: ** A function that may be _applied_ to either one or two _arguments_; i.e. has both _unary_ and _binary_ applications. Example: deltas

**Binary Function:**  A function with valence 2.

**Infix Notation** : Writing an operator between its _arguments_

**Prefix Notation** : _Applying_ a function to its _argument/s_ by writing it to the left of them

**Postfix Notation:**  Will be looked at in the Adverbs section.

**Unary Function:**  A function with valence 1.
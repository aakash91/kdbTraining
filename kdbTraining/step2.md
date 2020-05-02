The first challenge that a new developer to q or a programmer coming from an OOPs background is the right to left order of evaluation.

Let’s take Java’s associativity and precedence for example

**Precedence order**

 When two operators share an operand the operator with the higher precedence goes first. For example, 1 + 2 * 3 is treated as 1 + (2 * 3), whereas 1 * 2 + 3 is treated as (1 * 2) + 3 since multiplication has a higher precedence than addition.

**Associativity**

 When an expression has two operators with the same precedence, the expression is evaluated according to its associativity. For example x = y = z = 17 is treated as x = (y = (z = 17)), leaving all three variables with the value 17, since the = operator has right-to-left associativity (and an assignment statement evaluates to the value on the right hand side). On the other hand, 72 / 2 / 3 is treated as (72 / 2) / 3 since the / operator has left-to-right associativity. Some operators are not associative: for example, the expressions (x <= y <= z) and x++– are invalid.

How does q handle this?

q simply follows the right to left for evaluation of an expression. For example,

    q) 4 * 2 + 3  /will be evaluated as 4*(2+3) 
Which outputs 20.

However, if we have

    q) 4+2*3  

4+(2*3), resulting in 10. 

What this does is make it easier for both the developer and the interpreter to evaluate an expression by a defined standard.

**Variable Assignment**

Going straight to an example,

    q) a:1 / this will assign the value 1 to the variable a 
One can reassign any other value to the variable a

    q) a:3.4  
A merged example of the order of evaluation and variable assignment:

    q)b:1+a:42  
The above expression first assigns the value 42 to a and adds 1 to the value of a. This addition is then assigned to variable b.
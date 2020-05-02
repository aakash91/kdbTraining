Before we get started with Adverbs, let&#39;s take a quick look at _ **q ** _grammar.

q object types:

- **Noun ** – The variables storing data.
- **Verb ** – The operators between nouns.
- **Adverb**  – Higher-order functions that modify the behavior of verbs on lists.

It is similar to any spoken language. Adverbs in q give one the power to avoid n-order loops and perform a highly complex operation in a single line of code.

Let&#39;s go over each of the Adverbs in q one by one with examples:

**Monadic each**

Let&#39;s say we have a list with depth 1
     q) l:1 2 3
 To get the count of list l, we can simply use the count function
     q) count l
 3

Let&#39;s now take another list, this time with depth 2
     q) l1:(1 2 3;4 5 6)
 The count of the list is 2 since the individual items are themselves lists.
     q) count l1

How does one get the length of each individual list forming the above list. This is where the adverb _ **each** _ comes in.

    q)l1:(1 2 3;4 5 6)

    q)count each l1

3 3

The function each takes one item at a time from the list l1 and then applies the count function to each one.

## Each-Both

Let&#39;s start with an example. We know we can perform an element-wise addition between lists using the below:

    q)1 2 3+3 4 5

4 6 8

The reason for this behavior is because + is an atomic operator and an atomic operator automatically applies to corresponding pairs of items when applied to lists of the same length.

But let&#39;s say we have the dyadic _ **join operator ,** __ _. It does not perform an element-wise operation between lists, rather it takes in both left and right arguments in their entirety to join.

    q)&quot;abc&quot;,&quot;cgf&quot;

&quot;abccgf&quot;

The challenge here is to perform the join element-wise. This is where we use the  **each-both adverb &#39;**

    q)1 2 3 +&#39; 4 5 6

5 7 9

    q)

    q)&quot;abc&quot;,&#39;&quot;cgf&quot;

&quot;ac&quot;

&quot;bg&quot;

&quot;cf&quot;

Remember that the lists on either side of each-both should be of the same length else one will encounter a length error.

## Each-left

An atomic operator like  **+**  is able to operate the right atom with all elements on left. Example:

    q)1 2 3+10

11 12 13

The _each-left_ adverb \: modifies a dyadic function so that it applies the second argument with each item of the first argument.

Let&#39;s take an example where we want to join a last name to multiple first names, where the

    q)(&quot;Hi&quot;;&quot;Hello&quot;;&quot;Ola&quot;) ,\: &quot; Mike&quot;

&quot;Hi Mike&quot;

&quot;Hello Mike&quot;

&quot;Ola Mike&quot;

## Each-right

Each-right works in the exact opposite way to Each-left.

The _each-right_ adverb /: modifies a dyadic function so that it applies the first argument to each item of the second argument.

Let&#39;s take the same two lists which we used for the each-left mathematical operation and see what we get.

    q)(1;2;3) +/: (4;5;6;7)

5 6 7

6 7 8

7 8 9

8 9 10

## Each-previous

The adverb _each-previous_ &#39;: provides a declarative way to perform a dyadic operation on each item of a list with its predecessor.

Since the initial item of the list does not have a predecessor, we must provide one in the left operand of the modified operator. One choice is the initial item of the source list. For example, to calculate the deltas of a list of prices.

    q)100 -&#39;: 100 99 101 102 101

0 -1 2 1 -1

**Iteration**

_ **over ** _and _ **scan** _ adverbs match closely with the normal iteration/loops that we might have seen in other programming languages.

### Over(/) for Accumulation

The over function works like recursion in q. It modifies a _ **dyadic** __ _function to accumulate results over a list.

Let&#39;s take addition for example:

    q)0+/ 1 2 3 4 5 6 7 8 9 19

64

- •	The left operand “0” is the initial value passed to the accumulator.
- The right operand is the list to be accumulated over.
- The operation starts with (0+1), then this result is added to 2 and so on and so forth.

Let&#39;s take an example where we create our own dyadic function to add over a list and simultaneously use the _ **0N** _ to print out each step

0N!x
 With a 0N on the left hand side, returns the right hand side after printing its unformatted

    q)addAList:{[x;y] 0N!(x,y);x+y}

    q)0 addAList/ 1 2 3 4 5 6 7 8 9

0 1

1 2

3 3

6 4

10 5

15 6

21 7

28 8

36 9

45

### **Monadic over for Accumulation**

One can get rid of the initial accumulator value by using the _ **monadic ** _form of over. Let&#39;s take an example:

    q)(+/) 1 2 3 4 5 6

21

- The parenthesis to enclose the function with over are mandatory.

## Over for iteration

When over(/) follows a _ **monadic ** _function, one can specify the number of times to iterate the same operation. Example:

    q)f:{0N!x;x:x+2}

    q)f/[5;4]

4

6

8

10

12

14

- The first argument passed is the number of iterations we want. It is 5 in this case.
- The second argument passed is the initial value passed to the list. It is 4 in this case.
- The 0N function shows the value of x passed to function f in each iteration.

### **Over for iteration until convergence**

Over can behave as a converge when following a _ **monadic ** _function. It keeps iterating until the last seen is produced. Example:

    q){0N!x;x*x}/[0.1]

0.1

0.01

0.0001

1e-08

1e-16

1e-32

1e-64

1e-128

1e-256

0f

0f

- The function keeps getting called until the last value 0 is produced.

### **Over with condition check**

Over can be limited in the number of its iterations by specifying _ **another function ** _which condition checks the input passed. Note this applies when over is following a _ **monadic ** _function. Example:

    q){0N!x;x+100}/[{1200\&gt;x};200]

200

300

400

500

600

700

800

900

1000

1100

1200

- The over function is modifying the first function.
- The function:{1200>x} condition checks each iteration by comparing the value of the second argument which is the input to the first function.

### Fold using over

This use-case is for functions with more than two arguments.

f/[x;y;z]
 Applies as:
f[f[… f[f[x;y0;z0];y1;z1]; … yn-2;zn-2];yn-1;zn-1]

Example:

    q){0N!(x;y;z);x+y+z}/[1 5 6;2 22;3 33]

(1 5 6;2;3)

(6 10 11;22;33)

61 65 66

- First Iteration: x=(1 5 6), y=2, z=3
- ((1;5;6)+2)+3=(6;10;11)
- Second Iteration: x=(6;10;11), y=22, z=33
- ((6;10;11)+22)+33=(61;65;66)

## Scan(\)

The _scan_ adverb \ is a higher-order function that behaves just like / except that it returns all the intermediate accumulations instead of just the final one. Whereas _over_ produces an aggregate function that collapses a list, _scan_ produces a function whose output has the same number of items as its input.

Let&#39;s look at the same examples we used for over:

    q)(+\) 1 2 3 4 5 6 7 8 9

1 3 6 10 15 21 28 36 45

What are the use-cases of this?

- Sometimes one wants the entire list of intermediary steps before coming to the final result, maybe to operate on this list of intermediary steps.

Note: All variations of over discussed above work with scan, just printing all steps during
In this section, let&#39;s go over some basic list operations such as:

- Indexed Retrieval
- Indexed Assignment
- Lists with Expressions
- Combining Lists
- Nested List operations
- Retrieving Multiple Items
- Find(?) index with an item
- Elided Indices
- Some useful list operations

**Indexed Retrieval**

On a general list L, the retrieval works as L[i] where i is the index of the item being retrieved.

    q)L:(1;2;4;3)

    q)L[2]

4

    q)L[3]

3

### Indexed Assignment

Indexing can also be used to assign values to items.

    q)L:1 2 4 6

    q)L[1]:9

    q)L

1 9 4 6

### Lists with Expressions

Any valid q expression can occur in list construction.

    q)L: 1 2 4

    q)L1: 1 5 6

    q)L2:(sum L;count L1)

    q)L2

7 3

### Combining Lists

The _ **join ** _operator is used for joining two lists. Its result is a new list in which (a copy of) the right operand is appended to the end of (a copy of) the left operand.

    q)L1:1 2 4

    q)L2:9 8 7

    q)L1,L2

1 2 4 9 8 7

### Indexing at depth

Indexing at depth is used to get items from nested lists.

    q)L:(1;(1;2);((3;4);(5;6)))

    q)L[1]

1 2

    q)L[1][1]

2

    q)

    q)/Alternate to above expression

    q)L[1;1]

2

### Retrieving Multiple Items

One can use a list of indices to a list to get the corresponding items in the list. L[I], where I is a list of indices.

    q)L:(1;(1;2);((3;4);(5;6)))

    q)L[1]

1 2

    q)L[1][1]

2

    q)

    q)/Alternate to above expression

    q)L[1;1]

2

    q)

    q)

    q)L: 1 2 3 4 5 6

    q)L[0 5]

1 6

    q)/Retrieve multiple lists by passing multiple lists of indices

    q)L[(1 2;3 4)]

2 3

4 5

### Find(?) index with item

The _ **find ** _operator _ **?** _ returns the index of the first occurrence of the value passed as its right argument.

    q)L:1 2 3 4 5 6

    q)L?2

1

**Some useful list operations**

- til
- distinct
- where
- group
- count

Examples of all below:

    q)/til takes a non-negative integer n and returns a list of n consecutive natural numbers starting at 0

    q)til 10

0 1 2 3 4 5 6 7 8 9

    q)/distinct returns the unique items in its list argument, in order of first occurence

    q)distinct 0 1 2 3 1 0

0 1 2 3

    q)/where returns the indices of 1b in a boolean list

    q)where 01101b

1 2 4

    q)/group takes a list and returns a dictionary in which east distinct item of the argument is mapped to the indices of its occurences, in order of occurence

    q)group &quot;mississippi&quot;

m| ,0

i| 1 4 7 10

s| 2 3 5 6

p| 8 9

    q)/count returns the number of elements in the first level of a list

    q)count (1;2;3;4;5)

5

    q)count (1;2;(3;4))

3

## **Mathematical Operations**

Mathematical operations between two lists work when both the lists are of same length else one is going to run into a length error.

One can also apply apply operations between an atom and a list.

    q)1+(10;11;12)

11 12 13

    q)(1;2;4)+(5;6;7)

6 8 11

    q)/Running into the length error when trying to add two lists of different lengths

    q)(1;2;4)+(1;4;8;9)

&#39;length

[0] (1;2;4)+(1;4;8;9)

## **Match ~**

The _ **match ** _operator _ **~** _ is used to compare two q entities and outputs 1b if they are identical else 0b.

    q)(1;2;3;4)~(1;2;3;4)

1b

    q)(1;2;3;4)~(1;2;4;3)

0b

## Relational Operations

    q)1=(1;2;3;1)

1001b

    q)(1;4;3;2)=(1;2;3;1)

1010b

    q)(2;3;5;7)>=(1;3;9;9)

1100b

    q)1<>(1;2;3;5)

0111b
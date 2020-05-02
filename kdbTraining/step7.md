Dictionary in general terms is a mapping between keys and values, a list of key-value pairs that is.

The concept remains the same in q. The distinction, however, lies in the way they are stored. In q, a Dictionary is an association between a list of keys and a list of values, both lists of equal length. _ **It is important to understand that dictionaries are stored as a pair of lists physically.** _

**Creating a Dictionary**

Let&#39;s create a simple dictionary and see what the _ **type ** _function returns.The command to create a dictionary is:

    q)d:`a`b`c!1 2 3

    q)d

a| 1

b| 2

c| 3

    q)type d

99h

## Dictionary Operations

Let&#39;s take a look at some common examples on dictionary operations:

- Getting keys and values of a dictionary
- Lookup
- Reverse Lookup with Find
- Amends and Upserts
- Extracting a Sub-dictionary
- Removing entries
- Merging dictionaries
- Arithmetic and Relational Operations

### Getting keys and values of a dictionary

Use:
 key {dictionary\_name} -\&gt; To get the list of keys of dictionary
 value {dictionary\_name} -\&gt; To get the list of values dictionary

    q)d:`a`b`c!(1 2 3;3 4 5;7 8 9)

    q)key d

`a`b`c

    q)type key d

11h

    q)value d

1 2 3

3 4 5

7 8 9

    q)type value d

0h

### Lookup

Use:
 d[key] -\&gt; where d is a dictionary, returns the value for the key

The lookup works the same way as a retrieval for a list. Instead of an index, one uses a key.

    q)d:`a`b`c!1 2 3

    q)d[`b]

2

### Amends and Upserts

Similar to lists, one can use keys instead of indices to amend values in a dictionary.

    q)d:`a`b`c!1 2 3

    q)d[`e]:5

    q)d

a| 1

b| 2

c| 3

e| 5

### Extracting a Sub-dictionary(#)

The _ **take ** _function _ **#** _ is used to retrieve a sub-dictionary when given a list of keys.

Use:
 \&lt;list of keys\&gt;#dictionary -\&gt; returns a dictionary with the provided keys and corresponding values

    q)d:`a`b`c!1 2 3

    q)`a`c#d

a| 1

c| 3

### Removing Entries

The _ **cut ** _function _ **\_** _is used to retrieve a sub-dictionary by removing the provided keys and their corresponding values.

Use:
 \&lt;list of keys\&gt; \_ dictionary -\&gt; Returns a sub-dictionary with the provided list of keys

    q)d:`a`b`c!1 2 3

    q)`a`c \_ d

b| 2

### Merging Dictionaries

The _ **join** _ function **,**  as we used for joining lists is used for joining dictionaries.

    q)d1:`a`b`c!1 2 3

    q)d2:`e`f`g!5 6 7

    q)d1,d2

a| 1

b| 2

c| 3

e| 5

f| 6

g| 7

### Arithmetic and Relational Operations

We have been noticing that all the operations on dictionaries discussed till now have almost been identical to those on lists. We know that this is not accidental by any chance.

A _ **q** _ Dictionary is literally just a pair of lists(Think of a dictionary as a named list). We have been using keys instead of indexes for operations. The same ideas carry over to mathematical and relational operations.

Let&#39;s jump straight into examples.

**Mathematical operations between a Dictionary and Atom**

    q)d:`a`b`c!1 2 3

    q)d+4

a| 5

b| 6

c| 7

    q)

    q)d-3

a| -2

b| -1

c| 0

    q)

    q)d\*2

a| 2

b| 4

c| 6

**Relational operations between a Dictionary and Atom**

    q)d:`a`b`c!1 2 3

    q)d=3

a| 0

b| 0

c| 1

    q)d\&gt;=2

a| 0

b| 1

c| 1

    q)d\&lt;=1

a| 1

b| 0

c| 0

    q)neg d

a| -1

b| -2

c| -3

**Mathematical operations between Dictionaries**

The operations happen between the matching elements.

    q)d1:`a`b`c!1 2 3

    q)d2:`a`c`e!4 5 6

    q)d1+d2

a| 5

b| 2

c| 8

e| 6

    q)d1-d2

a| -3

b| 2

c| -2

e| -6

    q)d1\*d2

a| 4

b| 2

c| 15

e| 6

**Exercise: Try relational operational between directions.**
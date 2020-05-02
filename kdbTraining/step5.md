A [List](https://en.wikipedia.org/wiki/List_(abstract_data_type) is an ordered collection of atoms or other lists. The members of the collection are called its items. Let&#39;s take a look at a simple list:

    q)(1 2 3)

1 2 3

    q)/or

    q)(1;2;3)

1 2 3

q/KDB+ is based around the idea of lists and vector processing. All data structures in  **q**  such as Dictionaries, Tables and Keyed Tables are built from lists.

Taking this idea further to the KDB+ database which is columnar in nature, which basically means that each column is stored as a separate list(as a file) on disk.

Additionally, Vector processing on lists and associated data structures is what makes q blazing fast in nature. More to follow on this.

**Types of List**

- Simple Lists
- Empty Lists
- Singleton Lists
- Mixed Lists

Let&#39;s glance over each of them one by one. Also, let&#39;s use the _ **type** _ function on them as we go.

**Simple Lists**

A list comprising of atoms of a uniform type are _ **simple lists.** _ These correspond to mathematical notation of a vector. Such lists are treated in a special manner in q. They take less storage and compute faster.

Example:

    q)/simple Integer list

    q)(2;1;3;6)

2 1 3 6

    q)type (2;1;3;6)

7h

    q)/simple symbol list

    q)(`kdb;`is;`fun)

`kdb`is`fun

    q)type (`kdb;`is;`fun)

11h

- _ **type ** _function on a simple list returns the  **positive num type**  associated with the corresponding data type. _ **h ** _is again the default short return type for function _ **type** _ as we discussed in the sections on Atoms.

## Singleton Lists(Using Enlist)

A singleton list is a list with a single atom inside it. How do I create one? Enter the _ **enlist ** _function.

The example distinguishes between an atom and an atom boxed into a list using _ **enlist** _ function.

    q)/Singleton list

    q)a:enlist 10

    q)type a

7h

    q)b:220

    q)type b

-7h

### Mixed Lists

Mixed lists are collections of different types of atoms. They might not seem intuitive at first but are quite useful when performing advanced analytics with data structures such as Dictionaries and Tables.

    q)/Mixed lists

    q)mixedList:(1;`symbol;&quot;a&quot;)

    q)mixedList

1

`symbol

&quot;a&quot;

    q)type mixedList

0h

### List of Lists

List of lists is a mixed list. You can have any number of levels while storing lists inside a list.

Examples Below:

    q)/List of lists

    q)l:((1;2;3);(4;5;6))

    q)l

1 2 3

4 5 6

    q)type l

0h
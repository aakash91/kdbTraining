**Table Definition**

Syntax:
 tbl:([]col1:List1;col2:List2;......;coln:Listn)

- The parenthesis enclosed contains a pair of square brackets with no enclosed element. (More on how they&#39;re used in this chapter)
- It is followed by a list of pair column names and list(col1:List1, col2:List2…so on)
- All lists should be of the same length.

Example:

q)tbl:([] a:1 2 3;b:`john`bob`moss)

q)tbl

a b

------

1 john

2 bob

3 moss

**Basic select query- q-sql works a bit different than traditional sql**

**q)select from tbl where a=1**

**a b**

**------**

**1 john**

**More to follow in the coming courses…..**
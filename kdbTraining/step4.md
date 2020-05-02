[Type Conversion](https://en.wikipedia.org/wiki/Type_conversion) is different ways of converting entity of one data type into another.

**The $(cast) operator**

Syntax: x $ y

Where x is a lower-case letter, symbol or non-negative short, returns y cast according to x. Let&#39;s jump straight into examples:

    q)/Converting String to Integer

    q)&quot;I&quot;$&quot;2&quot;

2i

    q)/Converting String to Float

    q)&quot;F&quot;$&quot;2&quot;

2f

    q)/Converting datetime to date

    q)`date$2020.01.01D00:00:00.001

2020.01.01

    q)/Converting datetime to month

    q)`month$2020.01.01D00:00:00.001

2020.01m
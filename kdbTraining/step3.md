**q ** has a rich set of data types which correspond to those of traditional programming languages. However, q provides a richer subset of time and date related data types which we discussed in the [introduction to this series](https://thinqkdb.wordpress.com/2018/12/16/introduction-to-kdb/). These data types facilitate time series data capture and analysis.

Let&#39;s go over each of these Data Type Categories one by one in brief below. But let&#39;s first see what all do we have available.

**Glance at Data Types First**

| **Type** | **Size** | **CharType** | **NumType** | **Notation** | **Null Value** |
| --- | --- | --- | --- | --- | --- |
| boolean | 1 | b | 1 | 1b | 0b |
| --- | --- | --- | --- | --- | --- |
| byte | 1 | x | 4 | 0x26 | 0x00 |
| short | 2 | h | 5 | 42h | 0Nh |
| int | 4 | i | 6 | 42i | 0Ni |
| long | 8 | j | 7 | 42j | 0Nj |
| real | 4 | e | 8 | 4.2e | 0Ne |
| float | 8 | f | 9 | 4.2 | 0n |
| char | 1 | c | 10 | &quot;z&quot; | &quot; &quot; |
| symbol | \* | s | 11 | `zaphod | ` |
| timestamp | 8 | p | 12 | 2015.01.01T00:00:00.000000000 | 0Np |
| month | 4 | m | 13 | 2006.07m | 0Nm |
| date | 4 | d | 14 | 2006.07.21 | 0Nd |
| (datetime) | 4 | z | 15 | 2006.07.21T09:13:39 | 0Nz |
| timespan | 8 | n | 16 | 12:00:00.000000000 | 0Nn |
| minute | 4 | u | 17 | 23:59 | 0Nu |
| second | 4 | v | 18 | 23:59:59 | 0Nv |
| time | 4 | t | 19 | 09:01:02.042 | 0Nt |

- **Type ** – Data type
- **Size ** – Bytes on memory
- **Char Type ** – The associated char type
- **Num Type ** – Each data type in q has an associated number for easy identification. The  **type**  function in the next section will clarify this.
- **Notation ** – An example
- **Null Value ** – Null value associated with the corresponding Data Type.

**Categories**

- Integer Data
- Floating point Data
- Boolean
- Text Data
- Temporal Data(Time- and Date-)
- Special Data Types which will have chapters of their own

**Integer Data**

- **int**

    q)1234567890i

- **short**

    q)-123h

- **long**

    q)42j

**Floating Point Data**

- **float** : Often called &quot;double&quot; in traditional languages. A float can hold (at least) 15 decimal digits of precision. It is denoted by optionally signed numeric digits with either a decimal point or an optional trailing type indicator f

    q)3.14159265

    q)1f

    q)1.0

- **Real** : This type is called &#39;float&#39; in some languages. A real can hold at least 6 decimal digits of precision.

    q)12.34e

**Boolean**

The _ **boolean** _ ** ** type uses one byte to store a bit and is denoted by the bit value with the trailing type indicator b. There are  **no**  keywords for &#39;true&#39; or &#39;false&#39;, nor are there separate logical operators for booleans.

    q)0b

    q)1b

**Text Data**

There are two atomic text types in q. They are more akin to the SQL types  **CHAR****   **and ** VARCHAR**than the character types of traditional languages.

- **char** :  It corresponds to a SQL  **CHAR**. It is denoted by a single character enclosed in double quotes.

    q)&quot;q&quot;

- **symbol** : A symbol is  **not**  a string. A symbol is akin to a SQL VARCHAR, in that it can hold an arbitrary number of characters, but is different in that it is atomic.
- The char &quot;q&quot; and the symbol `kdb are both atomic entities. A symbol is irreducible, meaning that the individual characters that comprise it are not directly accessible.

    q)`q

    q)`zookeeper

**Temporal Data**

- **date** : A _date_ is stored as a four-byte signed integer and is denoted by _yyyy.mm.dd_, where _yyyy_ represents the year, _mm_ the month and _dd_ the day. The underlying value is the count of days from Jan 1, 2000 – positive for post-millennium and negative for pre.

    q)2019.01.01

- **time** : If milliseconds are sufficient, use the time type, which stores the count of milliseconds from midnight in a 32-bit signed integer. It is denoted by hh:mm:ss.uuu where hh represents hours on the 24-hour clock, mm represents minutes, ss represents seconds, and uuu represents milliseconds.
-

    q)13:24:56.134

- **timespan** : If milliseconds are not sufficient, use the _timespan_ type, which stores the count of nanoseconds from midnight as a long integer.

    q)13:24:56.987654321

- **datetime** (_deprecated_) : A _datetime_ is the lexical combination of a date and a time, separated by T as in the ISO standard format. A _datetime _value stores in a float the fractional day count from midnight Jan 1, 2000.

    q)2000.01.01T12:00:00.000

- **timestamp** : It is the lexical combination of a date and a timespan, separated by D. The underlying timestamp value is a long representing the count of nanoseconds since the millennium. Post-millennium is positive and pre- is negative.

    q)2014.11.22D17:43:40.123456789

- **month** : The _month_ type is stored as a 32-bit signed integer and is denoted by _yyyy.mm_ with a trailing type indicator m. A month value is the count of months since the beginning of the millennium. Post-milieu is positive and pre is negative.

    q)2018.12m

- **minute** : The _minute_ type is stored as a 32-bit signed integer and is denoted by _hh:mm_. A minute value counts the number of minutes from midnight.

    q)12:30

- **second** : The _second_ type is stored as 32-bit signed integer and is denoted by _hh:mm:ss_. A second value counts the number of seconds from midnight.

    q)12:13:14
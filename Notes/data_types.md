# Data types
Q is a dynamically typed language, in which type checking is mostly unobtrusive. Each variable has the type of its currently assigned value and type promotion is automatic for most numeric operations. Types are checked on operations to homogenous lists

There are q data types to cover nearly all needs but a few basic types are used most frequently. In q3.0 and above, the basic integer type, called long, is a 64-bit signed integer. The basic floating point type in q is called float, often known as a "double" in many languages. This is an 8-byte value conforming to the IEEE floating-point specification.

```
q)98.6
```
**Aritmetic operations** on integer and float values are pretty much as expected except for division, which is written as % since / has been preempted for comments (as well as other uses). Sorry, that's just the way it is. Also note that division **always** results in a float.

```
q)2+3
5
q)2.2*3.0
6.6
q)4-2
2
q)4%2
2f
```

## Boolean values
Boolean values in q are stored in a single byte and are denoted as the binary values they really are with an explicit type suffix b. One way to generate boolean values is to test for equality.
```
q)42=40+2
1b
q)42=43
0b
```

## Date and Timespan
### Date
The two most useful temporal types are date and timespan; both represent integral counts. Under the covers, a date is the number of days since the millennium, positive for post and negative for pre.

```
q)2000.01.01 
0
q)2014.11.19 
5436
q)1999.12.31
-1
```
One interesting and useful feature of q temporal values is that, as integral values under the covers, they naturally participate in arithmetic. For example, to advance a date five days, add 5.
```
q)2000.01.01+5
2000.01.06
```

### Time
Similarly, a time value is represented by a timespan, which is a (long) integer count of the number of **nanoseconds since midnight**. It is denoted as,
```
q)12:00:00.000000000 / this is noon
0D12:00:00.000000000
```
To advance a time by one microsecond (i.e., 1000 nanoseconds) add 1000,
```
q)12:00:00.000000000+1000
0D12:00:00.000001000
```
 To verify that temporal values are indeed their underlying values, test for equality.
 ```
q)2000.01.01=0
1b
q)12:00:00.000000000=12*60*60*1000000000
1b
 ```
## Text (symbols)
Symbols are denoted by a leading back-quote (called "back tick" in q-speak) followed by characters. Symbols without embedded blanks or other special characters can be entered literally into the console.
```
q)`aapl
`aapl
q)`thisisareallylongsymbol
`thisisareallylongsymbol
```
Since symbols are atoms, any two can be tested for equality.
```
q)`aapl=`apl
0b
```
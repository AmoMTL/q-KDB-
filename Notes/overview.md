# q/KDB+ Overview
Arthur Whitney developed the q programming language and its database kdb+. Released by Kx Systems, Inc. in 2003, the primary design objectives of q are expressiveness, speed and efficiency.

[Q for Mortals: An introduction to q programming](https://code.kx.com/q4m3/) by Jeffry A. Borror

*Evaluation Order*:  While q is entered left-to-right, expressions are evaluated right-to-left or, as the q gods prefer, left of right – meaning that a function is applied to the argument on its right. There is no operator precedence and function application can be written without brackets. Punctuation noise is significantly reduced.

## [Data Types](data_types.md)

* Integers
* Arithmetic operators
* Boolean
* date/timespan

## [Lists](lists.md)
Operations:
* til
* Join/Concatnate lists
* extracting items from a list

## [Functions](functions.md)
* Functions on lists
* Factorial
* Operands | or &
* common applications of / (over): sum, prd, max, min
* scan (\\)

## [Examples](examples.md)
* Fiboncacci numbers
* Newton's method for $n^{th}$ roots

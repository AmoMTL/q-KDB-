# Examples
## Fibonacci numbers
We define the Fibonacci numbers recursively.

* Base case: the initial sequence is the list 1 1
* Inductive step: given a list of Fibonacci numbers, the next value of the sequence appends the sum of its two last items.

```
q){x, sum -2#x}1 1 2
1 1 2 3
q)fib: {x, sum -2#x}
q)10 fib/ 1 1
1 1 2 3 5 8 13 21 34 55 89 144
```
## Newton's method for $n^{th}$ roots

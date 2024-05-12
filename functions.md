# Functions
Functions in q correspond to “lambda expressions” or “anonymous functions” in other languages. This means that a function is a first-class value just like a long or float value – i.e., it acquires a name only once it is assigned to a variable.

Conceptually, a q function is a sequence of steps that produces an output result from an input value. Since q is not purely functional, these rules can interact with the world by reaching outside the context of the function. Such actions are called side effects and should be carefully controlled.

Function definition is delimited by matching curly braces { and }. Immediately after the opening brace, the formal parameters are names enclosed in square brackets [ and ] and separated by semi-colons. These parameters presumably appear in the body of the function, which follows the formal parameters and is a succession of expressions sequenced by semi-colons.

```
q){[x] x*x}
{[x] x*x}
q)sq:{[x] x*x}
q){[x;y] a:x*x; b:y*y; a+b}
{[x;y] a:x*x; b:y*y; a+b}
q)pyth:{[x;y] a:x*x; b:y*y; a+b}
```
To apply a function to arguments, follow it (or its name, if it has been assigned to a variable) by a list of values enclosed in square brackets and separated by semi-colons. This causes the argument expression to be evaluated first, then the expressions in the body of the function to be evaluated sequentially by substituting each resulting argument for every occurrence of the corresponding formal parameter. Normally the value of the final expression is returned as the output value of the function.
```
q){[x] x*x}[5]
25
q){[x;y;z] a:x*x*x; b:y*y; c:z; a+b+c}[1;2;3]
8
q)pyth[2;2]
8
q)sq[7]
49
```

## Functions on lists
Because q is a vector language, most of the built-in operators work on lists out of the box. In q-speak, such functions are atomic, meaning they recursively burrow into a complex data structure until arriving at atoms and then perform their operation. In particular, an atomic function operates on lists by application to the individual items. For example, plain addition adds an atom to a list, a list to an atom or two lists of the same length.
```
q)42+100 200 300
142 242 342
q)100 200 300+42
142 242 342
q)100 200 300+1 2 3
101 202 303
```
Perhaps surprisingly, this is also true of equality and comparison operators. (Recall the notation for simple boolean lists).
```
q)100=99 100 101
010b
q)100 100 100=100 101 102
100b
q)100<99 100 101
001b
```
## Iterators / (over)
Suppose that instead of adding things pair-wise, we want to add all the items across a list. The way this is done in functional languages is with higher order functions, or as they are called in q, iterators. Regardless of the terminology, the idea is to take the operation of a function and produce a closely related function having the same “essence” but applied in a different manner.

We tell q to start with the initial value of 0 in the accumulator and then modify + with the iterator / so that it adds across the list.

```
q)0 +/ 1 2 3 4 5
15
q)0 +/ 1+til 100
5050
```
There is nothing special about built-in operator + – we can use any operator or even our own function.
```
q)0 {x+y}/ 1 2 3 4 5 6
21
q)0 {(x*x)+(y*y)}/ 1 2 3
34
q)0 {x+(y*y)}/ 1 2 3
14
q)0 {x+y}/1+til 100
5050
```

In this situation we don't really need the flexibility to specify the initial value of the accumulator. It suffices to start with the first item of the list and proceed across the rest of the list. There is an even simpler form for this case.
```
q)(+/) 1 2 3 4 5
15
q)(+/) 1+til 100
5050
```
### Factorial
Change addition to multiplication for factorial.
```
q)(*/) 1+til 5
120
```
### Operands - | &
#### or |
| returns the larger of its operands.
```
q)42|98
98
q)(|/) 20 10 40 30
40
```
#### and &
& returns the smaller of its operands.
```
q)10&20
10
q)(&/) 20 10 30 40
10
```
### Common applications of / (over)
```
q)sum 1+til 10          / this is +/
55
q)prd 1+til 5           / this is */ -- note missing "o"
120
q)max 20 10 40 30       / this is |/
40
q)min 10 30 20 50       / this is &/
10
```

We record one more example of / for later reference. Recall from the previous section that applying the operator # to an atom produces a list of copies. Composing this with */ we get a multiplicative implementation of raising to a power without resorting to floating-point exponential.

```
q)(*/) 2#1.4142135623730949     /1.41421.. to the power of 2/
2f
q)n:3
q)(*/) n#10                     /10 to the power of 3/
1000
```

## \ (scan)
The higher-order function sibling to Over is Scan, written \. The process of Scan is the same as that of Over with one difference: instead of returning only the final result of the accumulation, it returns all intermediate values.

```
q)(+\) 1+til 10
1 3 6 10 15 21 28 36 45 55
q)(*\) 1+til 10
1 2 6 24 120 720 5040 40320 362880 3628800
q)(|\) 20 20 40 30
20 20 40 40
q)(&\) 10 30 5 40
10 10 5 5
```

Scan converts a binary function to a unary uniform function – i.e., one that returns a list of the same length as the input.

As with Over, common applications of Scan have their own names.
```
q)sums 1+til 10
1 3 6 10 15 21 28 36 45 55
q)prds 1+til 10
1 2 6 24 120 720 5040 40320 362880 3628800
q)maxs 20 10 40 30
20 20 40 40
q)mins 20 10 40 30
20 10 10 10
```
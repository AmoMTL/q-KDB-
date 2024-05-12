# Lists
The fundamental q data structure is a list, which is an ordered collection of items sequenced from left to right. The notation for a general list encloses items with ( and ) and uses ; as separator. Spaces after the semi-colons are optional but can improve readability.
```
q)(1; 1.2; `one)
1
1.2
`one
```
In the case of a homogenous list of atoms, called a simple list, q adopts a simplified format for both storage and display. The parentheses and semicolons are dropped. For example, a list of underlying numeric type separates its items with a space.
```
q)(1; 2; 3)
1 2 3
q)(1.2; 2.2; 3.3)
1.2 2.2 3.3
q)(2000.01.01; 2000.01.02; 2001.01.03)
2000.01.01 2000.01.02 2001.01.03
```
A simple list of **booleans** is juxtaposed with no spaces and has a trailing b type indicator.
```
q)(1b; 0b; 1b)
101b
```
A simple list of symbols is displayed with no separating spaces.
```
q)(`one; `two; `three)
`one`two`three
```
## Operations
### til
The most fundamental operation is til, which takes a non-negative integer n and returns the first n integers starting at 0 (n itself is not included in the result).
```
q)til 10
0 1 2 3 4 5 6 7 8 9
q)1+til 10
1 2 3 4 5 6 7 8 9 10
q)1+2*til 10
1 3 5 7 9 11 13 15 17 19
```
### Join/Concatnate lists
Another frequently used list primitive is Join , that returns the list obtained by concatenating its right operand to its left operand.
```
q)1 2 3,4 5
1 2 3 4 5
q)1 2 3,100
1 2 3 100
q)0,1 2 3
0 1 2 3
```
### Extracting items from lists
To extract items from the front or back of a list, use the Take operator #. Positive argument means take from the front, negative from the back.
```
q)2#til 10
0 1
q)-2#til 10
8 9
q)-2#1+til 10
9 10
```
Should you extract more items than there are in the list, # restarts at the beginning and continues extracting. It does this until the specified number of items is reached.
```
q)10#til 4
0 1 2 3 0 1 2 3 0 1
```
As with atoms, a list can be assigned to a variable and the items of a list can be accessed via indexing, which uses square brackets and is relative to 0.
```
q)L[0]
10
q)L[1]
20
q)L[2]
30
```

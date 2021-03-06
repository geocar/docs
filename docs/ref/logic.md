## `all`

Syntax: `all x` (unary, aggregate)

Returns a boolean atom `1b` if all items of `x` are non-zero, and otherwise `0b`. 

It applies to all data types except symbol, first converting the type to boolean if necessary.
```q
q)all 1 2 3=1 2 4
q)all 1 2 3=1 2 3
q)if[all x in y;....]   / use in control structure
```

!!! Note
    `all` is defined as `min` after converting to boolean, i.e. `all x` is equivalent to `min "b"$x`.


## `&` `and` (minimum)

Syntax: `x & y` (binary, atomic)  
Syntax: `x and y` (binary, atomic)

Returns the [minimum](arith-integer/#and-minimum) of its arguments; applies to all data types except symbol.

!!! Note "And numbers"
    The name `and` is used because it behaves as logical AND on boolean arguments, but is extended to _minimum_ on other data types


## `any`

Syntax: `any x` (unary, aggregate)

Returns a boolean atom `1b` if any item of `x` is non-zero, and otherwise `0b`; applies to all data types except symbol, first converting the type to boolean if necessary.
```q
q)any 1 2 3=10 20 4
0b
q)any 1 2 3=1 20 30
1b
q)if[any x in y;....]   / use in control structure
```

!!! note
    `any` is defined as `max` after converting to boolean, i.e. `any x` and `max "b"$x` are equivalent. 


## `not`

Syntax: `not x` (unary, atomic) 

Returns `0b` where `x` **not** equal to zero, and `1b` otherwise.

Applies to all data types except sym, and to items of lists, dict values and table columns.
```q
q)not -1 0 1 2
0100b
q)not "abc","c"$0
0001b
q)not `a`b!(-1 0 2;"abc","c"$0)
a| 010b
b| 0001b
```


## `null`

Syntax: `null x` (unary, atomic)

Returns `1b` where `x` is **null**.

Applies to all data types except enums, and to items of lists, dict values and table columns.
```q
q)null 0 0n 0w 1 0n
01001b
```

!!! Note "Enums"
    Enums always show as non-null.
    ```q
    q)a:``a
    q)`=`a$`            / non-enumerated and enumerated null symbol show as equivalent
    1b
    q)null`             / null symbol behaves as expected
    1b
    q)null`a$`          / enumeration of null symbol does not
    0b
    ```
    The intention was not to have nulls in the enums. That value is used to indicate "out of range". (Think of them as a way to represent foreign keys.) To test for an enumeration backed by a null symbol, one can use the equality test – but at the cost of CPU cycles:
    ```q
    q)a:10000000?`8
    q)v:`a$a
    q)\ts null v
    18 16777344
    q)\ts `=v
    66 268435648
    ```


## `|` `or` (maximum)

Syntax: `x|y` (binary, atomic)  
Syntax: `x or y` (binary, atomic)

Returns the [maximum](arith-integer/#or-maximum) of `x` and `y`. It applies to all data types except symbol.

!!! note "Or numbers" 
    The name `or` is used because it behaves as logical OR on boolean arguments, but is extended to _maximum_ on other data types.


# Operators and Control Flow

> After about 5 days spent understanding the fundamental data structures in C#, I am now ready to learn about operators and control flow (topics that I am already familiar with from other programming languages I use).

## Operators

Expressions are made up of operators and operands. Operators are symbols that perform operations on variables and values. The operands are the values that the operator works on.

Types of operators include:

### Arithmetic Operators

Name | Example | Description
---- | ------- | -----------
Unary Plus | `+a` | Returns the value of `a`
Unary Minus | `-a` | Returns the negative value of `a`
Postincrement | `a++` | Returns the value of a and then increments `a`
Preincrement | `++a` | Increments `a` and then returns the value of `a`
Postdecrement | `a--` | Returns the value of `a` and then decrements `a`
Predecrement | `--a` | Decrements `a` and then returns the value of `a`
Addition | `a + b` | Adds `a` and `b`
Subtraction | `a - b` | Subtracts `b` from `a`
Multiplication | `a * b` | Multiplies `a` and `b`
Division | `a / b` | Divides `a` by `b`
Modulus | `a % b` | Returns the remainder of `a` divided by `b`

### Bitwise Operators

Name | Example | Description
---- | ------- | -----------
Bitwise AND | `a & b` | Returns a 1 in each bit position for which the corresponding bits of both operands are 1
Bitwise OR | `a | b` | Returns a 1 in each bit position for which the corresponding bits of either or both operands are 1
Bitwise XOR | `a ^ b` | Returns a 1 in each bit position for which the corresponding bits of either but not both operands are 1
Bitwise NOT | `~a` | Inverts the bits of its operand
Left Shift | `a << b` | Shifts `a` left by `b` bits
Right Shift | `a >> b` | Shifts `a` right by `b` bits

### Comparison Operators

Name | Example | Description
---- | ------- | -----------
Equal | `a == b` | Returns true if `a` is equal to `b`
Not Equal | `a != b` | Returns true if `a` is not equal to `b`
Greater Than | `a > b` | Returns true if `a` is greater than `b`
Less Than | `a < b` | Returns true if `a` is less than `b`
Greater Than or Equal | `a >= b` | Returns true if `a` is greater than or equal to `b`
Less Than or Equal | `a <= b` | Returns true if `a` is less than or equal to `b`

### Logical Operators

Name | Example | Description
---- | ------- | -----------
Logical AND | `a && b` | Returns true if both `a` and `b` are true
Logical OR | `a || b` | Returns true if either `a` or `b` are true
Logical NOT | `!a` | Returns true if `a` is false

### Assignment Operators

Name | Example | Description
---- | ------- | -----------
Simple Assignment | `a = b` | Assigns the value of `b` to `a`
Addition Assignment | `a += b` | Adds `b` to `a` and assigns the result to `a`
Subtraction Assignment | `a -= b` | Subtracts `b` from `a` and assigns the result to `a`
Multiplication Assignment | `a *= b` | Multiplies `a` by `b` and assigns the result to `a`
Division Assignment | `a /= b` | Divides `a` by `b` and assigns the result to `a`
Modulus Assignment | `a %= b` | Assigns the remainder of `a` divided by `b` to `a`
Left Shift Assignment | `a <<= b` | Shifts `a` left by `b` bits and assigns the result to `a`
Right Shift Assignment | `a >>= b` | Shifts `a` right by `b` bits and assigns the result to `a`
Bitwise AND Assignment | `a &= b` | Performs a bitwise AND on `a` and `b` and assigns the result to `a`

**... and so on.**

### Ternary Operator

The ternary operator is a conditional operator that takes three operands. It is often used as a shortcut for the `if` statement.

```csharp
int a = 10;
int b = 20;
int result = (a > b) ? a : b;
```

> By the way, this is the only operator in C# that takes three operands.

## Control Flow

This is the order in which the program's code is executed. It is determined by the control flow statements in the program.
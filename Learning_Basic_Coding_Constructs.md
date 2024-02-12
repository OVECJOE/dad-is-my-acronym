# Learning How Basic Coding Constructs Are Expressed in C# - Day 4

> Today, I will be learning about variables, statements and expressions, comments and whitespace, and preprocessor directives in C#.

## Variables

> C# is static-typed language, which means that the type of a variable is known at compile time. The type of a variable is determined by the type of the value it holds. 

```csharp
int x = 10;
```

> Also, you may not assign a value to the variable you declared on the same line. 

```csharp
int x;
x = 10;
```

> You can use the `var` keyword to declare a variable without specifying its type. The type of the variable will be determined by the type of the value it holds.

```csharp
var x = 10;
```

> **NOTE:** You can only use the `var` keyword to declare a variable when you are initializing it on the same line. Hence `var x;` is invalid and will not compile.

### Definite Assignment

> A variable is said to be definitely assigned if it has been assigned a value. The C# compiler enforces definite assignment. This means that you must assign a value to a variable before you use it.

```csharp
int x;
Console.WriteLine(x); // This will not compile
```

### Scope

> The scope of a variable is the region of the program in which the variable is accessible. The scope of a variable is determined by the block in which it is declared. A block is defined  by a pair of curly braces `{}`.

```csharp
{
	int x = 10;
	Console.WriteLine(x); // This will compile
}

Console.WriteLine(x); // This will not compile
```

#### Potential Naming Conflicts

> If you declare a variable with the same name as another variable in an outer scope, the inner variable might hide the outer variable. **NOTE:** It is a good practice to avoid naming conflicts by using unique names for variables.

### Declaration Space

This is a region of code where a single name must not refer to two different entities. For example, you cannot declare two variables with the same name in the same block.

```csharp
int x = 10;
int x = 20; // This will not compile
```

> Neither will this work:

```csharp
int x = 10;
{
	int x = 20; // This will not compile
}
```

> because the inner block cannot declare a variable with the same name as a variable in the outer block.

### Constants

> A constant is a variable whose value cannot be changed. You can declare a constant using the `const` keyword.

```csharp
const int x = 10;
```

## Statements and Expressions

While variables are used to store data our code works with, we need to be able to perform operations on these variables. This is where statements and expressions come in.

### Statements

Informally, a statement in a method describes an action to be performed. A statement is often a complete instruction that the compiler can execute.

```csharp
int x = 10;
```

> The above line of code is a statement. It declares a variable `x` and assigns it the value `10`.

#### Types of Statements

1. Declaration Statements: These are statements that declare a variable and optionally assign a value to it.
2. Expression Statements: These are statements that evaluate an expression.
3. Selection Statements: These are statements that select one of many paths of execution.
4. Iteration Statements: These are statements that execute a block of code repeatedly.

The C# specification distinguishes between 13 different categories of statements, so I hear.

### Expressions

An expression is a sequence of operators and operands that specifies a computation. An expression can be used to compute a value.

```csharp
int x = 10;
int y = 20;
int z = x + y;
```

The simplest expressions are literals. A literal is a source code representation of a value. For example, `10` and `20` in the code snippet above are literals.

Expressions can involve operators which describe the computation to be performed. For example, `x + y` in the code snippet above is an expression that involves the `+` operator.

Operators can be unary, binary, or ternary. A unary operator operates on a single operand, a binary operator operates on two operands, and a ternary operator operates on three operands. For example, the `+` operator is a unary operator when it is used to indicate a positive number, and a binary operator when it is used to add two numbers or strings.

> Since literals are operands, operands are also expressions. Hence, `x` and `y` in the code snippet above are expressions. This means that expressions can be nested within other expressions. `x + y` is an expression that contains two other expressions `x` and `y`.

```csharp
double x = (-b + Math.Sqrt(b * b - 4 * a * c)) / (2 * a);
```

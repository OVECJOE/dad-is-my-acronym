# Fundamental Data Types in C# - Day 9

> Today I plan to learn about Tuples, Dynamic, and Object data types in C#.

## Tuples

Introduced in C# 7.0, tuples let you combine multiple fields to create a single value. The name **tuple** is meant to be a generalized version of words like double, triple, quadruple, and so on.

```csharp
(int X, int Y) point = (10, 20);
Console.WriteLine(point.X); // 10
```

Using `var` keyword:

```csharp
var point = (X: 10, Y: 20);
Console.WriteLine(point.X); // 10
```

> Note that if you initialize a tuple from existing variables, the compiler will infer the names of the tuple fields from the variable names.

```csharp
int x = 10, y = 20;
var point = (x, y);
Console.WriteLine(point.x); // 10
```

> Also, it is perfectly legal not to name the fields of a tuple. It defaults to `Item1`, `Item2`, etc.

```csharp
(int, int) point = (10, 20);
Console.WriteLine(point.Item1); // 10
```

> We can assign a tuple to another tuple if the types match.

```csharp
(int X, int Y) point = (10, 20);
(int Width, int Height) rectangle = point;
Console.WriteLine(rectangle.Width); // 10
```

> Tuple also supports `==` and `!=` comparison. It compares each field of the tuple - their types must match too.

```csharp
var point1 = (X: 10, Y: 20);
var point2 = (X: 10, Y: 20);
Console.WriteLine(point1 == point2); // True
```

### Deconstruction

Deconstruction is the process of breaking a tuple into its individual fields.

```csharp
(int X, int Y) point = (10, 20);
var (x, y) = point;
Console.WriteLine(x); // 10
```

## Dynamic

C# defines a type called `dynamic` that does not correspond to any CLR type. To the runtime, `dynamic` is just an `object`. The difference is that the compiler does not perform type checking on `dynamic` variables at compile time.

```csharp
dynamic name = "John";
// you can then change the type of the variable
name = 10;
Console.WriteLine(name); // 10
```

> Yeah, this feels like JavaScript, so I might feel tempted to use it too often. But, with the experience of encountering bugs at runtime in JavaScript, it's better to avoid using `dynamic` unless necessary.

### Why dynamic was introduced?

- **Interoperability with COM objects**:
	The COM (Component Object Model) is a binary-interface standard for software components introduced by Microsoft in 1993. It is used to enable inter-process communication and dynamic object creation in a large range of programming languages. It is also the basis of automatability of the Microsoft Office Suite and many other applications.

	A lot of Office's automation APIs used to be hard work to use from C#. To improve this, `dynamic` was one of the features introduced. As with all C# features, it was designed with broader applicability in mind and not simply as an Office interop feature.

When `dynamic` was introduced in C# 4.0, Microsoft went to considerable lengths to ensure that all dynamic behavior was as consistent as possible with the behavior you would have seen if the compiler had known at compile time what types you were going to be using. This means that the infrastructure supporting `dynamic`, **DLR**, has to replicate significant portions of C# behavior. However, the DLR hasn't been updated much since `dynamic` was added, which means that its capabilities represent how the language looked around a decade ago.


## Object

This is the last data type that get special recognition from the C# compiler. It is the ultimate base class of _almost_ all other types in C#. It is an alias for `System.Object` in the .NET framework.

```csharp
object obj = "Hello";
Console.WriteLine(obj); // Hello
```

A variable of type `object` can store any type of value for any type that derives from `System.Object`. This is because all types in C# derive from `System.Object` directly or indirectly. This includes numeric types, the `bool` and `string` types, and all user-defined types.

```csharp
object obj = 10;
Console.WriteLine(obj); // 10

obj = true;
Console.WriteLine(obj); // True

obj = new { Name = "John", Age = 30 };
Console.WriteLine(obj); // { Name = John, Age = 30 }
```

> Hence, `object` is the ultimate general-purpose container...

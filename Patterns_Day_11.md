# Patterns - Day 11

> Today, I am learning about patterns in C#.

One of the most important concepts in C# is the concept of patterns. Patterns are used to match the shape of data. They are used in `switch` statements, `is` expressions, and `case` statements.

The type of pattern used in a `switch` statement is called a **constant pattern**. It is used to match an expression with that pattern if it has the same value.

Another pattern is the _tuple_ pattern. It is used in `switch` statements to match a tuple with a pattern.

```csharp
var p = (3, 4);

switch (p)
{
	case (0, 0):
		Console.WriteLine("Origin");
		break;
	case var (x, y):
		Console.WriteLine($"({x}, {y})");
		break;
}
```

The `case var (x, y)` is a tuple pattern that matches any tuple and assigns the values to `x` and `y`.

Another pattern is the `type` pattern. It is used to match an expression with a type.

```csharp
switch (e)
{
	case int i:
		Console.WriteLine("It's an int");
		break;
	case string s:
		Console.WriteLine($"It's a string that is {s.Length} long");
		break;
}
```

The `case int i` is a type pattern that matches an expression of type `int` and assigns the value to `i`.

In the first example above, there was an example of a pattern I used in a `case` statement. It is called the **positional pattern**. Usually in the form below:

```csharp
case (<type> <var1>, <type> <var2>):
```

OR

```csharp
case var (<var1>, <var2>):
```

Positional patterns are an example of a recursive pattern i.e. they are patterns that can contain other patterns.

For example:

```csharp
case (int x, int y):
```

Contains two type patterns; `int x` and `int y`.

Whereas:

```csharp
case (2, int y):
```

Contains a constant pattern and a type pattern.

> A special case of a positional pattern is sited in the example below:

```csharp
case (var x, var y):
```

Though this looks like it consists of two type patterns, it is actually made up of two _var_ patterns. The `var` keyword is used to match any value and assign it to a variable. Meaning that unlike the type pattern, the `var` pattern does not check the type of the value.

> Crazy right? 😅

Though a positional pattern consisting of two type patterns may resemble deconstruction, the behavior is different. Such positional pattern performs three checks:

```csharp
case (int x, int y):
```

1. It checks if the value is a tuple.
2. It checks if the first element of the tuple is an `int`.
3. It checks if the second element of the tuple is an `int`.

Whereas , deconstruction performs only one check:

```csharp
var (x, y) = (3, 4);
```

It checks if the value is a tuple and assigns the first and second elements to `x` and `y` respectively.

Another up is the **discard** pattern. It is used to ignore a value. It is represented by the `_` symbol. It is best used when you want to ignore a value in a positional pattern.

```csharp
case (int x, _):
```

There is a subtle difference between the discard pattern and discarding a type pattern. Discarding a type pattern will still cause the value to be checked for type compatibility. The discard pattern, on the other hand, will not check the value at all.

> Discarding a type pattern:
```csharp
case (int x, int _):
```

Another recursive pattern is the **property pattern**. It is used to match a property of an object with a pattern.

```csharp
case string { Length: 0 }:
```

This property pattern starts with the type of the object and then uses the `{}` to specify the properties to match. In this case, it matches a string with a length of 0.

> I noticed that as a recursive pattern, it contains a type pattern plus property-based tests which can also contain other patterns.

Note that you can specify an output variable in a property pattern. For example:

```csharp
case string { Length: 0 } v:
```

An example of a property pattern with nested patterns:

```csharp
case string { Length: int length }:
```

This pattern matches a string with a length and assigns the length to the variable `length`.

You can get more specific with patterns using the `when` clause. It is used to add additional checks to a pattern. For example:

```csharp
case string s when s.Length == 0:
```

is equivalent to:

```csharp
case string { Length: 0 } s:
```

Patterns don't happen only in `switch` statements. They can also be used in `is` expressions. For example:

```csharp
if (e is int i)
{
	Console.WriteLine($"It's an int with a value of {i}");
}
```

> An example from the book I am learning C# from. It's a great book by the way. 😄

```csharp
switch (shape)
{
	case (int w, int h) when w < h: return "Portrait";
	case (int w, int h) when w > h: return "Landscape";
	case (int s, int _) when s > 0: return "Square";
	default: return "Unknown";
}
```

Can be re-written to use a `switch` expression as follow:

```csharp
return shape switch
{
	(int w, int h) when w < h => "Portrait",
	(int w, int h) when w > h => "Landscape",
	(int s, int _) when s > 0 => "Square";
	_ => "Unknown";
};
```

> I observed that the `switch` expression is more concise and easier to read. 😄

By the way, patterns in `is` expressions cannot use `when` clauses. It would be redundant since you can just use an `if` statement.

> I noticed that I didn't divide the content of today's learning into sections. I hope it's not too confusing. 😅 With that said, I am done for today and have successfully completed chapter 2 of the book I am learning C# from. 😄 **Such a wild ride!!!** :o

Next up, I will be learning about **Types** tomorrow as all code in C# programs must belong to a type.

> When I started learning about patterns today, I thought it was going to be about Regex. C# always has a way of surprising me. 😅

See you then! 😄👋🏽
# Fundamental Data Types in C# - Day 8

> I learnt about the `bool` and `char` data types in C# yesterday. Today, I will be learning about the `string` data type in C#.

## String Data Type

The `string` data type is used to store a sequence of characters (text). Strings are immutable, meaning that they cannot be changed after they are created.

All operations performed on a string will return a new string. Thus, all `string` methods are accessor methods and not mutator methods.

> The downside of this is that string processing can be inefficient, especially when working with large amounts of text. This creates a lot of garbage that needs to be collected by the garbage collector.

The mutable version of `string` is `StringBuilder`. It is more efficient when working with large amounts of text. Note that `StringBuilder` is conceptual similar to `string` but it is modifiable. Also, it has no special recognition from the C# compiler.

### Formatting Strings

C# provides a syntax that makes it easy to produce strings from a mixture of fixed text (or string literals) and information determined at runtime (such as the value of a variable). This is called string interpolation.

```csharp
string name = "John";
int age = 30;
string message = $"My name is {name} and I am {age} years old.";
```

> The `$` character is used to indicate that the string is an interpolated string. The `{}` characters are used to indicate that the value of the variable should be inserted into the string. This is similar to the `f` character in Python.

Embedded expressions in interpolated strings can also be complex.

```csharp
double opposite = 3, adjacent = 4;
string message = $"The hypotenuse of a right-angled triangle with opposite {opposite} and adjacent {adjacent} is {Math.Sqrt(opposite * opposite + adjacent * adjacent)}";
```

> I loved it when I realized that Visual Studio has a C# Interactive window that allows me to run C# code interactively. This is similar to the Python interactive shell.

Interpolated strings compile into code that uses the `string.Format` method. This method is also used to format strings in older versions of C#. This means that the `$` character is just a syntactic sugar for the `string.Format` method.

```csharp
string message = string.Format("My name is {0} and I am {1} years old.", name, age);
```

Some data types have more than one reasonable string representation. For example, the `DateTime` data type can be represented in different formats. The `ToString` method can be used to specify the format of the string representation.

```csharp
DateTime date = new DateTime(2021, 1, 1);
string message = date.ToString("yyyy-MM-dd");
```

Another example is the `double` data type. The `ToString` method can be used to specify the number of decimal places.

```csharp
double number = 3.14159;
string message = number.ToString("F2"); // 3.14
```

To include a format specifier in an interpolated string, use the `:` character.

```csharp
double number = 3.14159;
string message = $"The value of pi is {number:F2}";
```

When using string interpolation, you may need to use a format provider to specify the culture of the string representation. This can be done by passing the interpolated string into a variable of type `FormattableString` or `IFormattable`.

```csharp
double number = 3.14159;
string message = FormattableString.Invariant($"The value of pi is {number:F2}");
```

#### FormattableString static methods

This class has two static methods: `Invariant` and `CurrentCulture`.

- `FormattableString.Invariant` returns a `FormattableString` that uses the `InvariantCulture` format provider.
- `FormattableString.CurrentCulture` returns a `FormattableString` that uses the `CurrentCulture` format provider.

By passing an interpolated string to one of these methods, the compiler can then generate code that wraps the string in a `FormattableString` object.

`FormattableString` implements `IFormattable` and `IFormattable` has a `ToString` method that takes a `IFormatProvider` as an argument. This means that the `ToString` method can be used to specify the culture of the string representation.

```csharp
double number = 3.14159;
string message = FormattableString.Invariant($"The value of pi is {number:F2}");
string result = message.ToString(CultureInfo.GetCultureInfo("fr-FR"));
```

> namespace of `FormattableString` is `System` and namespace of `CultureInfo` is `System.Globalization`.

### Verbatim String Literals

A verbatim string literal is a string that is prefixed by the `@` character. This means that the string is interpreted literally, without any escape characters.

```csharp
string path = "C:\\Program Files\\Microsoft";
string path = @"C:\Program Files\Microsoft";
```

> You can use `@` in front of an interpolated string. It combines the benefits of verbatim string literals and interpolated strings.

```csharp
string path = $@"C:\Program Files\Microsoft\{name}";
```

Verbatim string literals also allow value to span multiple lines.

```csharp
string message = @"This is a
multi-line
string";
```

> I noticed that different systems have different line endings. For example, Windows uses `\r\n` while Unix uses `\n`. This can cause problems when working with multi-line strings. The `Environment.NewLine` property can be used to get the newline string for the current system.

```csharp
string message = $"This is a{Environment.NewLine}multi-line{Environment.NewLine}string";
```

> You can configure the line endings of your files using a `.gitattributes` file if you were using Git. This is useful when working with a team that uses different operating systems.

```git
# Set the default behavior, in case people don't have core.autocrlf set.
* text=auto
# If you want to enforce the same line endings for all files, use this instead.
* text eol=lf # or eol=crlf
```

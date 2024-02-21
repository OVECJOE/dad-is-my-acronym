# Fundamental Data Types in C# - Day 7

> On day 6, I learned about numeric data types which are used to store numeric values. I also learned about the promotion and casting of these types. `BigInteger` (a data type that is not traditionally supported by C# compiler) is used to store very large numbers. Today, I aim to learn more data types such as Boolean, Char, and String.

## Boolean Data Type

- The `bool` data type is used to store `true` or `false` values.
- It is used to represent the truth values of logic and is used in conditional statements.
- It is a value type and is stored in 1 byte of memory.
- It is used to represent the result of a comparison operation.

```csharp
bool isTrue = true;
bool isFalse = false;
```

> In conditional statements,
```csharp
if (isTrue)
{
	Console.WriteLine("This is true");
}
else
{
	Console.WriteLine("This is false");
}
```

> In comparison operations,
```csharp
int a = 10;
int b = 20;
bool result = a > b;
Console.WriteLine(result); // Output: False
```

> In logical operations,
```csharp
bool isTrue = true;
bool isFalse = false;
bool result = isTrue && isFalse;
Console.WriteLine(result); // Output: False
```

Note that while most C-like languages allow numeric types to stand in for boolean values, C# does not. This means that you cannot use an integer or a floating-point number in place of a boolean value.

```csharp
int a = 10;
if (a) // Error: Cannot implicitly convert type 'int' to 'bool'
{
	Console.WriteLine("This is true");
}
else
{
	Console.WriteLine("This is false");
}
```

## Char Data Type

This is used to store a single character. It is a value type and is stored in 2 bytes of memory. It is used to store characters such as letters, digits, and special characters.

```csharp
char letter = 'A';
char digit = '1';
char specialChar = '@';
```

In C#, a character is enclosed in single quotes and stored in a variable of type `char`. One `char` value is a 16-bit Unicode character representing a single UTF-16 code unit.

> A common mistake is to think that each `char` value represents a character. This is not always the case. A single character can be made up from multiple Unicode code points. For example, the character "é" is represented by two code points: U+0065 (LATIN SMALL LETTER E) and U+0301 (COMBINING ACUTE ACCENT).

```csharp
char[] chars = { 'c', 'a', 'f', 'e', (char) 0x301, 's' };
string text = new string(chars);
```

From the example above, the `text` variable contains the string "cafés". This is sequence of 6 `char` values, but only 5 characters.

### Unicode Combining Marks

Unicode defines a set of combining marks that can be used to modify the appearance of a base character. For example, the character "é" can be represented by the base character "e" followed by the combining acute accent mark. The combining acute accent mark is a Unicode code point U+0301.

```csharp
char e = 'e';
char acute = '\u0301';
string s = e + acute.ToString();
Console.WriteLine(s); // Output: é
```

Hence, any code point with a value greater than **65,535** is represented by a pair of `char` values. This is known as a _surrogate pair_. The standard defines rules for mapping code points to surrogate pairs in a way that the resulting code points have values in the range **0xD800** to **0xDFFF**, which are reserved for surrogate pairs.

> The .NET class library provides a StringInfo class that can help you work with surrogate pairs. Even .NET 3.0 introduced a new type called `Rune` to simplify working with multicode-unit sequences.
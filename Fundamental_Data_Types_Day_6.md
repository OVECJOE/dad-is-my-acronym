# Fundamental Data Types in C# - Day 6

> Finally, I have started the fun part of any programming language - Data Types. This is how I truly understand a language. Also, I hope that in the next 45 days, I will be able to understand the language enough to start building some of the cool projects that I have in mind.

## What are Data Types?

Data types are the classification or categorization of data items. They represent the kind of values that determine what operations can be performed on a particular set of data. In C#, everything is treated as an object, and every data type is associated with an object. You can declare a variable of a specific data type and assign a value to it. This assigned value will be stored in memory and can be used to perform various operations.

> .NET supports thousands of types in its class library, which can be extended by developers using custom types. Yet, a handful of types get handled specially by the runtime, and these are known as the fundamental data types.

There are two types of data types in C#:

1. Value types - These types hold their data in memory allocated on the stack. They are derived from the class `System.ValueType`. The value types directly contain data. Some examples of value types are `int`, `char`, and `float`, which stores numbers, alphabets, and floating-point numbers, respectively. When you declare an `int` type, the system allocates memory to store the value.
2. Reference types - These types hold a reference to the memory location of the actual data. They are derived from the class `System.Object`. Reference types don't store the data directly. Instead, they store the address of the memory location where the data is stored. Some examples of reference types are `object`, `string`, and `class`. When you declare a `string` type, the system allocates memory to store the reference to the string.

## The Fundamental Data Types in C# I Will be Covering

These data types include the following:

1. Numeric Data Types
2. Boolean Data Type
3. String and Character Data Types
4. Tuples
5. Dynamic Data Type
6. Object Data Type

### Numeric Data Types

- C# supports integer and floating-point arithmetic.
- There are signed and unsigned integer types and they come in various sizes.
- The most commonly used integer type is `int`, which is a 32-bit signed integer. It is not the least because it is large enough to store most values used in practice, without being too large to work with efficiently on modern hardware.

The following table lists the available numeric data types in C#:

| Data Type | Size (in bits) | Range | Precision | Default Value | Signed | CLR Name |
| --------- | -------------- | ----- | --------- | ------------- | ------ | -------- |
| byte | 8 | 0 to 255 | 0 | 0 | No | System.Byte |
| sbyte | 8 | -128 to 127 | 0 | 0 | Yes | System.SByte |
| ushort | 16 | 0 to 65,535 | 0 | 0 | No | System.UInt16 |
| short | 16 | -32,768 to 32,767 | 0 | 0 | Yes | System.Int16 |
| uint | 32 | 0 to 4,294,967,295 | 0 | 0 | No | System.UInt32 |
| int | 32 | -2,147,483,648 to 2,147,483,647 | 0 | 0 | Yes | System.Int32 |
| ulong | 64 | 0 to 18,446,744,073,709,551,615 | 0 | 0 | No | System.UInt64 |
| long | 64 | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 | 0 | 0 | Yes | System.Int64 |

#### Floating-Point Types

- Floating-point types represent real numbers.
- They are used when it is necessary to represent numbers with a fractional component, such as 3.14159.
- The `float` (32-bit) and `double` (64-bit) types are the most commonly used floating-point types.

The following table lists the available floating-point data types in C#:

| Data Type | Size (in bits) | Range | Precision | Default Value | CLR Name |
| --------- | -------------- | ----- | --------- | ------------- | -------- |
| float | 32 | ±1.5 x 10^-45 to ±3.4 x 10^38 | 7 digits | 0.0F | System.Single |
| double | 64 | ±5.0 x 10^-324 to ±1.7 x 10^308 | 15-16 digits | 0.0D | System.Double |

> There is also a third numeric representation in C#, the `decimal` type, which is a 128-bit data type suitable for financial and monetary calculations. It has a higher precision and a smaller range than the `float` and `double` types.

##### The `decimal` Data Type

The `decimal` type stores numbers as a sign bit (positive or negative), a 96-bit integer number, and a scaling factor used to divide the 96-bit integer and specify what portion of it is a decimal fraction. The scaling factor specifies the number of digits to the right of the decimal point. The `decimal` type can represent values ranging from 1.0 x 10^-28 to approximately 7.9 x 10^28 with 28-29 significant digits.

#### NOTES ON NUMERIC DATA TYPES

1. C# supports the use of underscores in numeric literals to improve readability and migitate making mistakes. For example, you can use the underscore to separate groups of digits in a large number, like 1_000_000.
2. You can tell the compiler that you want a specific type of number by appending a suffix to the number. For example, you can use the suffix `F` or `f` to indicate that a number is a `float` type, and `D` or `d` to indicate that a number is a `double` type. For unsigned integers, you can use the suffix `U` or `u` to indicate that a number is an `uint` type, and `L` or `l` to indicate that a number is a `long` type. So `545LU` is a `ulong` type, and `5.45D` is a `double` type.
3. `float`, `double`, and `decimal` support the use of the `E` or `e` suffix to indicate a number in scientific notation. For example, `1.5e2` is equivalent to `150.0`.
4. You can also write numbers in hexadecimal, octal, or binary notation. For example, `0x1F` is a hexadecimal number, `017` is an octal number, and `0b1101` is a binary number. This is useful when working with bit manipulation and low-level programming. It is also useful when you want to express a number in a format that is more readable to you **e.g. in exception handling**.

#### Numeric Data Type Conversion

- C# supports implicit and explicit type conversion.
- Implicit type conversion is done automatically by the compiler when the destination type is larger than the source type.
- Explicit type conversion is done manually by the programmer when the destination type is smaller than the source type. This is also known as casting. For example, you can cast a `long` to an `int` by writing `(int) myLong`.

> Do you know that **Promotions** is not a C# feature? It is a feature of the C# compiler. The C# compiler automatically promotes smaller types to larger types when necessary. For example, if you add an `int` to a `long`, the `int` is promoted to a `long` before the addition is performed.

> Also, explicit type conversion is usually employed when you want to perform a narrowing conversion, which is a conversion from a larger type to a smaller type. This is because the C# compiler does not automatically perform narrowing conversions. For example, if you want to convert a `long` to an `int`, you must do so explicitly.

- What happens when you want to add an `int` to a float? Remember that both are numeric types with same size. In this case, C# allows implicit conversion based on range, not precision.
- You can use the `checked` and `unchecked` keywords to control overflow checking. If you use the `checked` keyword, the compiler will check for overflow and throw an exception if it occurs. If you use the `unchecked` keyword, the compiler will not check for overflow, and the result will be truncated if overflow occurs.

```csharp
int x = int.MaxValue;
int y = 1;
int z = checked(x + y); // Throws an OverflowException
```

> You can also use the `checked` and `unchecked` keywords to control overflow checking for an entire block of code. For example, you can use the `checked` keyword to check for overflow in a block of code, and then use the `unchecked` keyword to disable overflow checking for the rest of the code.

```csharp
checked
{
	int x = int.MaxValue;
	int y = 1;
	int z = x + y; // Throws an OverflowException
}
```

#### BigInteger

This is also a numeric data type in C# and is a part of the .NET class library, but it gets no special treatment from the C# compiler. It is a type that can represent arbitrarily large integers. It is useful when you need to work with numbers that are larger than the range of the built-in numeric types.

```csharp
using System.Numerics;

BigInteger big = BigInteger.Parse("1234567890123456789012345678901234567890");
```

- The `BigInteger` type is a reference type, so it is stored on the heap, not the stack.
- The selling point of the `BigInteger` type is that it can represent arbitrarily large integers, limited only by the amount of memory available to the program.
- The `BigInteger` type is not as efficient as the built-in numeric types, so it should be used only when necessary.

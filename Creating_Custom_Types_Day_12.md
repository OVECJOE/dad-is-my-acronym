# Custom-Defined Types in C# - Day 12

C# allows you to create custom types. In fact, everything in C# belongs to a type. The most important type you can create is a class.

## Classes

Most of the types you will work with in C# will be classes. A class can contain both code and data, and it can to make some of its features publicly available, while keeping others private (or accessible within itself alone). This is called **Encapsulation**.

### Encapsulation

Encapsulation is the process of hiding the internal state of an object and requiring all interactions to be performed through an object's methods. It is a way to protect the data in an object from accidental corruption. Coming from other programming languages such as PHP, JavaScript, and Python, I am familiar with the concept of encapsulation. It is like a daily bread for me.

### Example

```csharp
public class Point
{
	private int _x;
	private int _y;
}
```

In the above example, the `Point` class has two private fields `_x` and `_y`. These fields are only accessible within the `Point` class. This is a good example of encapsulation. To make these fields accessible outside the class in a readonly manner, you can:

```csharp
public class Point
{
	private int _x;
	private int _y;

	public int X
	{
		get { return _x; }
	}

	public int Y
	{
		get { return _y; }
	}
}
```

In the above example, the `X` and `Y` properties are publicly accessible, but they are readonly. This means that you can only read the values of `_x` and `_y` from outside the `Point` class, but you cannot modify them. The `X` and `Y` properties are called **Read-Only Properties**.

Ordinary classes have two choices of access modifiers: `public` and `internal`. The `public` modifier makes the class accessible from anywhere in the program. The `internal` modifier makes the class accessible only within the same assembly. You can also use the `protected` modifier to make the class accessible only within the same assembly or by derived classes.

> Honestly, I am not sure what an assembly is in C#, but I think it is a collection of classes and other types that are used to build an application. I will learn more about it later.

The members of a class can also have access modifiers. The `public` modifier makes the member accessible from anywhere in the program. The `private` modifier makes the member accessible only within the same class. The `protected` modifier makes the member accessible only within the same class or by derived classes. `private` is the default access modifier for class members.

Fields hold data. Though a kind of variable, they differ from local variables in that they are declared within a class, not within a method. Fields can be `public`, `private`, `protected`, or `internal`. They can also be `readonly` or `const`. `readonly` fields can be assigned a value only once, either at the time of declaration or in a constructor. `const` fields are implicitly `static` and can be assigned a value only at the time of declaration.

> _What is the lifetime of a field?_ I think it is the same as the lifetime of the object that contains it.

What if I want to track information that does not belong to a specific object?

### Static Members

The `static` keyword lets us declare that a member is not associated with any particular instance of a class. It is shared by all instances of the class. A `static` member is also called a **class member**. You can access a `static` member without creating an instance of the class. You can also access a `static` member through an instance of the class, but this is not recommended.

```csharp
public class Point
{
	private int _x;
	private int _y;
	private static int _count;

	public Point(int x, int y)
	{
		_x = x;
		_y = y;
		_count++;
	}

	public static int Count
	{
		get { return _count; }
	}
}
```

In the above example, the `Count` property is a `static` member. It is used to track the number of `Point` objects that have been created. The `Count` property is a **Read-Only Property**. It is used to get the value of the `_count` field, but it cannot be used to set the value of the `_count` field.

To access a `static` member, you use the class name followed by the member name, like this:

```csharp
int count = Point.Count;
```

> Note that you cannot use the non-static members of a class from within a `static` member of the same class. This is because a `static` member is not associated with any particular instance of the class.

### Static Classes

Interestly, members are not the only things that can be `static`. A class can also be `static`. A `static` class is a class that cannot be instantiated. It is used to hold `static` members only. A `static` class is sealed, which means that it cannot be inherited. The `static` keyword is used to declare a `static` class.

> The `Math` class in the `System` namespace is a good example of a `static` class. It contains `static` members only.

```csharp
public static class Math
{
	public static double PI = 3.14159;
	public static double Sqrt(double x);
}
```

In the above example, the `Math` class is `static`. It contains `static` members only. The `PI` field and the `Sqrt` method are `static` members.

You can declare that you want to invoke static methods on certain classes without naming the class every time. This is done using the `using static` directive.

```csharp
using static System.Console;
using static System.Math;

class Program
{
	static void Main()
	{
		WriteLine(PI);
		WriteLine(Sqrt(144));
	}
}
```

In the above example, the `using static` directive is used to import the `Console` and `Math` classes. This allows you to invoke the `WriteLine` and `Sqrt` methods without naming the class every time.

### Constructors

A constructor is a special method that is used to initialize an object. It is called when an object is created. A constructor has the same name as the class and no return type. It can have parameters, but it does not have to. A constructor is called using the `new` keyword.

```csharp
public class Point
{
	private int _x;
	private int _y;

	public Point(int x, int y)
	{
		_x = x;
		_y = y;
	}
}
```

In the above example, the `Point` class has a constructor that takes two parameters. The constructor is used to initialize the `_x` and `_y` fields.

If you do not provide a constructor for a class, C# provides a default constructor. The default constructor takes no parameters and does nothing. It is used to create an object with default values.

```csharp
public class Point
{
	private int _x;
	private int _y;
}
```

In the above example, the `Point` class does not have a constructor. C# provides a default constructor for the `Point` class. The default constructor takes no parameters and does nothing.

To use a constructor, you call it using the `new` keyword.

```csharp
Point p = new Point(3, 4);
```

> This will be all for today. I will continue from Reference Types in C# tomorrow. I did learn about the `this` keyword today, but I didn't include it in the note. Note that I am still on **Classes**... an obviously vast topic.

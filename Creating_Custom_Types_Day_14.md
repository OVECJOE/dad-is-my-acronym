# Creating Custom Types in C# - Day 14

Classes are reference types. They are used to create objects. Classes can have fields, properties, methods, and events. They can also have constructors, destructors, and static members. Classes can be inherited from other classes. They can also implement interfaces.

In C#, structs are value types. They are used to create lightweight objects that have no identity. Structs can also have fields, properties, and methods. However, though they can also have constructors, they cannot have destructors. Additionally, structs cannot be inherited from other structs. They cannot implement interfaces.

```csharp
public struct Point
{
	public double _x;
	public double _y;

	public Point(double x, double y)
	{
		_x = x;
		_y = y;
	}

	public double X => _x;
	public double Y => _y;
}
```

It is common for values to support comparison. Though C# defines the default meaning for the `==` operator for reference types (which is equivalent to the `ReferenceEquals` method which compares identities), it is not meaningful for value types. Therefore, C# does not automatically support `==` for structs. However, it is possible to define the `==` operator for structs.

```csharp
public struct Point
{
	private double _x;
	private double _y;

	public Point(double x, double y)
	{
		_x = x;
		_y = y;
	}

	public double X => _x;
	public double Y => _y;

	public static bool operator ==(Point left, Point right)
	{
		return left.X == right.X && left.Y == right.Y;
	}

	public static bool operator !=(Point left, Point right)
	{
		return left.X != right.X || left.Y != right.Y;
	}

	public override bool Equals(object obj)
	{
		return obj is Point right && this == right;
	}

	public override int GetHashCode()
	{
		return (X, Y).GetHashCode();
	}
}
```

You can see that the `Equals` and `GetHashCode` methods have been overridden. This is because the `==` operator has been defined. The `Equals` method is used to compare two objects for equality. The `GetHashCode` method is used to generate a hash code for the object. The hash code is used to store the object in a hash table.

The correct implementation of the `GetHashCode` method must meet two requirements. First, whatever result an instance returns as its hash code must remain constant as long as the instance remains unchanged. Second, if two instances have equal values according to the `Equals` method, they must return the same hash code.

Because `int` has a range, it is possible for two different instances to return the same hash code. This is known as a hash collision. Hash collisions are an unavoidable consequence of hashing. However, the fewer hash collisions, the better. Therefore, it is important to implement the `GetHashCode` method correctly.

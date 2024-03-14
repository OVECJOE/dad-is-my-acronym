# Creating Custom Types in C# Contd. - Day 13

> I took two days off from learning C# and I am back today. I am going to continue with the custom types in C#...from **Reference Types** as I promised.

## Reference Types

Any type declared with the `class` keyword is a reference type.

	What is a reference type?

> If you create an instance of a reference type, the variable you use to store the instance does not actually contain the data that makes up the instance of that type. Instead, it contains a reference to the location in memory where the instance is stored.

Also note that, assignment of a reference type variable to another variable does not create a new instance of the type. Instead, it copies the reference. This means that both variables refer to the same instance of the type.

##### Example

```csharp
class Program
{
	static void Main(string[] args)
	{
		var person1 = new Person();
		person1.Name = "John";
		var person2 = person1;
		person2.Name = "Jane";

		Console.WriteLine(person1.Name);
	}
}
```

In the above example, the output will be `Jane` because `person1` and `person2` refer to the same instance of the `Person` type.

One thing to note about reference types is that when there is an absence of an instance, the reference type variable will be `null`. This is different from value types where the variable is assigned a default value.

##### Example

```csharp
class Program
{
	static void Main(string[] args)
	{
		Person person = null;
	}
}
```

### `Nullable<T>`

.NET provides a special (and wrapper) type called `Nullable<T>`, which allows you to assign `null` to a value type variable. This is useful when you want to represent the absence of a value in a variable that would normally contain a value type.

##### Example

```csharp
class Program
{
	static void Main(string[] args)
	{
		int? number = null;
	}
}
```

### Non-Nullable Reference Types

According to the book I am reading:

> The widespread availability of null references in programming languages dates back to 1965, when Tony Hoare, a British computer scientist, introduced the concept of the null reference in his paper "The Null Reference: What, Why, When?".

In the paper, Hoare described the null reference as his "billion-dollar mistake" because it has caused so many problems in software development. The null reference is a common source of bugs in software, and it is the cause of many runtime exceptions. This is because a nullable reference type makes it hard to know whether it's safe to access or perform an action on a reference type variable. C# throws a `NullReferenceException` if you try to and will typically crash your program.

To address this problem, C# 8.0 introduced nullable references. Though weirdly, nullable reference types are not enabled by default. You have to enable them in your project file. C# provides two dimensions of control over nullable reference types:

1. **Nullable annotations**: These are used to indicate whether a reference type variable can be `null` or not.
2. **Nullable Warning**: This is used to indicate whether the compiler should warn you about potential null reference errors.

To enable nullable warning context in your project, you need to add the following line to your project file:

```xml
<PropertyGroup>
	<Nullable>warnings</Nullable>
</PropertyGroup>
```

Or to enable it for a specific file, you can use the `#pragma` directive:

```csharp
#pragma warning enable nullable
```

And to revert back to the behavior of the project file, you can use:

```csharp
#pragma warning restore nullable
```

To enable nullable annotations context, you can change `warnings` to `enable` in the project file:

```xml
<PropertyGroup>
	<Nullable>enable</Nullable>
</PropertyGroup>
```

#### What does the compiler do for us in code where we have fully enabled non-nullability support?

1. First, it ensures that we don't dereference a method or property of a nullable reference type without first checking whether the reference is `null`.

2. Second, it warns us if we assign a nullable reference type to a non-nullable reference type without first checking whether the reference is `null`.

> Note: sometimes you don't want to disable warnings for the whole project and it would be irritating to use `#pragma` in every file. There is a way to tell C# that you know something it doesn't know. You can use the null-forgiving operator `!` to tell the compiler that you are sure that a nullable reference type is not `null`.

##### Example from the book I am reading

```csharp
string? referenceFromLegacyComponent = legacy.GetReferenceYouAreSureIsNotNull();
string nonNullableReferenceFromLegacyComponent = referenceFromLegacyComponent!;
```

> The null-forgiving operator is also called the _dammit operator_.

### Nullable Attributes

Type | Usage
---- | -----
`[AllowNull]` | Indicates that a parameter, field, or property can be assigned `null`.
`[DisallowNull]` | Indicates that a parameter, field, or property cannot be assigned `null`.
`[NotNull]` | Indicates that a parameter, field, or property cannot be assigned `null`.
`[NotNullWhen]` | Indicates that a parameter, field, or property is not `null` when another parameter, field, or property has a specific value. Used with `out` or `ref` parameters.
`[MaybeNull]` | Indicates that a parameter, field, or property can be assigned `null`.
`[MaybeNullWhen]` | Indicates that a parameter, field, or property can be `null` when another parameter, field, or property has a specific value. Used with `out` or `ref` parameters.
`[NotNullIfNotNull]` | Indicates that a parameter, field, or property is not `null` if another parameter, field, or property is not `null`.

### Reference Types and the Heap

When you create an instance of a reference type, the instance is stored on the heap. The heap is a region of memory that is used to store objects that are created at runtime. The heap is managed by the .NET runtime and is automatically cleaned up when an object is no longer in use.

---

This is all I wish to document about reference types in C#. It's a lot to take in and I am not sure I understand everything. I suppose to resume tomorrow with **Structs** (known as custom value types), but I feel the need to revisit all my previous notes and try to groom what I have learned so far. _I won't document that though._
# Creating Custom Types in C# - Day 15

> After about a week break, I am back to my C# (no? DAD) learning journey. I will go straight to the point today. I hope to work on a project soon once I am done with the current chapter as I am getting bored with not building anything. I must tell you: this chapter is a long one.

## Difference between `readonly` and `const` fields

`readonly` fields can be assigned a value either at the time of declaration or in the constructor of the class. They can be assigned a value at runtime. `const` fields can only be assigned a value at the time of declaration and cannot be changed at runtime. They are evaluated at compile time.

Also, `const` fields are more limited than `readonly` fields. For a `const` field, there are limited types that can be used. For example, you can't use a `DateTime` type for a `const` field. You can only use primitive types like `int`, `string`, `char`, `bool`, an enumeration type, etc. For most reference types, you can only use `null` as the value if `const` is used.

For constant fields in a strong sense, use `const`. For fields that are constant in the sense that they are initialized once and never changed, use `readonly`. This is because:

- `const` fields are evaluated at compile time and are stored in the metadata of the assembly. This means that the value of a `const` field is available to the client of the assembly without needing to load the assembly.

Also, while the initialization of a `readonly` field can be deferred until the constructor is called, the initialization of a `const` field is always immediate.

## Constructors

Constructors are special methods that are called when an instance of a class is created. They are used to initialize the fields of the class. They have the same name as the class and do not have a return type. They can be overloaded.

A constructor can be used to initialize the fields of a class. If a class does not have a constructor, the compiler will automatically create a default constructor for the class. The default constructor initializes all fields to their default values.

### Constructor Overloading

Constructors can be overloaded. This means that a class can have multiple constructors with different signatures. When a class has multiple constructors, the compiler will choose the constructor that matches the arguments passed to it.

```csharp
public class Person
{
	public string Name { get; set; }
	public int Age { get; set; }

	public Person()
	{
		Name = "John Doe";
		Age = 30;
	}

	public Person(string name)
	{
		Name = name;
		Age = 30;
	}

	public Person(string name, int age)
	{
		Name = name;
		Age = age;
	}
}
```

### Static Constructors

Static constructors are used to initialize static fields of a class. They are called automatically when the class is loaded into memory. They are called only once, when the class is loaded into memory for the first time.

Static constructors do not take any parameters and do not have an access modifier. They are called automatically by the runtime and cannot be called explicitly.

```csharp
public class Person
{
	public static int Count { get; set; }

	static Person()
	{
		Count = 0;
	}

	public Person()
	{
		Count++;
	}
}
```

### Constructor Chaining

Constructor chaining is the process of calling one constructor from another constructor. This is done using the `this` keyword.

```csharp
public class Person
{
	public string Name { get; set; }
	public int Age { get; set; }

	public Person() : this("John Doe", 30)
	{
	}

	public Person(string name) : this(name, 30)
	{
	}

	private Person(string name, int age)
	{
		Name = name;
		Age = age;
	}
}
```

#### Why use constructor chaining?

- Avoid code duplication: If you have multiple constructors that perform similar initialization, you can avoid code duplication by chaining the constructors.
- Encapsulation: By chaining constructors, you can ensure that all initialization logic is centralized in one place.
- Flexibility: Constructor chaining allows you to provide multiple ways to initialize an object.
- Maintainability: Constructor chaining makes it easier to add new constructors or modify existing ones.

## DeConstructors

Just as tuples can be deconstructed into individual variables, custom types can also be deconstructed into individual variables. This is done using the `Deconstruct` method.

```csharp
public class Person
{
	public string Name { get; set; }
	public int Age { get; set; }

	public Person(string name, int age)
	{
		Name = name;
		Age = age;
	}

	public void Deconstruct(out string name, out int age)
	{
		name = Name;
		age = Age;
	}
}
```

Where `out` is used to indicate that the variables are being passed by reference. This enables you to use the same syntax as tuple deconstruction.

```csharp
var person = new Person("John Doe", 30);
var (name, age) = person;
```

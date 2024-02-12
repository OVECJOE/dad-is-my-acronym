# Basic Terms (C#) - Day 3

## 1. Namespace

A namespace is a collection of currently defined symbolic names along with information about the object that each name references. You can think of it as a dictionary where the keys are the object names and the values are the objects themselves.

They are usually access within the code using the `using` keyword. For example, the following one-liner will allow you to access the `Console` class from the `System` namespace:

```csharp
using System.IO;

// access the Console class
Console.WriteLine("Hello, World!");
```

### Benefits of Using Namespaces

- **Avoiding Naming Conflicts**: Namespaces allow you to use the same name for different objects, as long as they are in different namespaces. For example, you can have a `Car` class in the `Vehicle` namespace and another `Car` class in the `Automobile` namespace.
- **Organizing Code**: Namespaces allow you to organize your code into logical groups. For example, you can have a `Math` namespace that contains all the classes and methods related to mathematics. Also, namespaces can be nested (or hierarchical).
- **Provide Clue to The Purpose**: Namespaces can provide a clue to the purpose of the classes and methods they contain. For example, if you see a class in the `System.IO` namespace, you can guess that it has something to do with input/output operations.

### Important Notes About Namespaces

- **Case Sensitivity**: Namespaces are case-sensitive. For example, `System` and `system` are two different namespaces.
- **Using Multiple Namespaces**: You can use multiple namespaces in a single file. For example, you can use the `System` and `System.IO` namespaces in the same file.
- Most .NET types are defined in a namespace. Microsoft-supplied types have distinctive namespaces. When the types are part of .NET Framework, the namespace is `System`. For example, the `Console` class is defined in the `System` namespace. When they are part of some Microsoft technology that is not a core part of .NET, they usually begin with `Microsoft`. Libraries from other vendors usually begin with the vendor's name, while open-source libraries usually begin with the name of the project.
- Especially with the `System` namespace, avoid creating a namespace with the same name as a .NET Framework namespace. This can lead to confusion and errors.

### Creating a Namespace

You can create a namespace using the `namespace` keyword. For example:

```csharp
namespace MyNamespace
{
	class MyClass
	{
		// ...
	}
}
```

## 2. Class

A class is a blueprint for creating objects (a particular data structure), providing initial values for state (member variables or fields), and implementations of behavior (member functions or methods). A class belongs to a namespace when implemented in a file.

```csharp
namespace MyNamespace
{
	class MyClass
	{
		// member variables
		private int myVar;

		// member methods
		public void MyMethod()
		{
			// ...
		}
	}
}
```

### Important Notes About Classes

- Classes are C#'s mechanism for defining entities that have both state and behavior.
- C# does not support global methods; all methods are members of some type.

## 3. Entry Point

The entry point of a C# program is the `Main` method. When the program is started, it is the first method that is invoked.

```csharp
using System;

namespace MyNamespace
{
	class MyClass
	{
		static void Main(string[] args)
		{
			Console.WriteLine("Hello, World!");
		}
	}
}
```

### Important Notes About Entry Point

- The `Main` method must be `static` and it must be `void` or return an `int`. If it returns an `int`, the return value is used as the program's exit code.
- Sometimes, the `Main` method can return `Task` or `Task<int>`, which enables one to make the `Main` method asynchronous.
- The `Main` method can take an array of strings as an argument. This array contains the command-line arguments that are passed to the program when it is started. The definition of the `Main` method must match the signature `static void Main(string[] args)` in this case.
  > Note: While other C-like languages include the file name as the first argument, C# does not include the file name in the `args` array. If no command-line arguments are passed, the `args` array will be empty.

## 4. Unit Tests

> The book I am reading approached development using **TDD** (Test-Driven Development). This means that the tests are written before the code. This is a good practice because it forces you to think about the requirements and the design of the code before you start writing it. It also helps you to write code that is testable and to ensure that the code is working as expected.

> Also, it used the MSTest framework for writing unit tests, which utilizes **attributes** heavily.

### Attributes

Attributes are a way to add metadata to your code. They are used to provide additional information about the code. They are enclosed in square brackets (`[]`) and are placed before the code element they are associated with.

```csharp
[Attribute]
class MyClass
{
	// ...
}
```

Most attributes do nothing on their own. They are used by the compiler, the runtime, or other tools to provide additional information about the code. For example, the `Obsolete` attribute is used to mark a method as obsolete. When you use this attribute, the compiler will generate a warning if you use the method in your code.

A testing framework like **MSTest** definitely uses attributes to mark classes, methods, and properties as test classes, test methods, and test properties, respectively.

### Some Attributes Used in MSTest

- **TestClass**: This attribute is used to mark a class as a test class. The class must be public and not abstract. It must also have a default constructor. MSTest will look for test methods in this class and ignore classes that do not have this attribute.
- **TestMethod**: This attribute is used to mark a method as a test method. The method must be public and not static. It must also have a return type of `void`. MSTest will look for methods with this attribute and execute them as test methods.
- **TestInitialize**: This attribute is used to mark a method that should be run before each test method in the class. The method must be public and not static. It must also have a return type of `void`. This method is used to initialize the test environment before each test method is run, such as setting up test data.

### Writing a Unit Test

```csharp
using Microsoft.VisualStudio.TestTools.UnitTesting;

namespace MyNamespace
{
	[TestClass]
	public class MyClassTest
	{
		[TestInitialize]
		public void TestInitialize()
		{
			// ...
		}

		[TestMethod]
		public void TestMethod1()
		{
			// ...
		}

		[TestMethod]
		public void TestMethod2()
		{
			// ...
		}
	}
}
```

> When I used Visual Studio to create a new test project, it automatically added a reference to the `Microsoft.VisualStudio.TestTools.UnitTesting` namespace in a file beginning with `Global...` (whose full name I cannot remember), where it made the namespace global. This means that I did not have to add the `using` directive to the test file.

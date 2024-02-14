# Using Visual Studio as Your IDE - Day 2

> I chose Visual Studio as my IDE because of the out-of-box features/tools that it provides for .NET development, especially using C#. I am still getting used to the IDE and learning how to use it effectively. The experience feels different from using Visual Studio Code.

## Notes on Visual Studio `Project`

1. A project, in Visual Studio, is a collection of source code files that are used to build an application.
2. Each project builds a single output called target.
3. This target can be a single file (executable file or library) or multiple files collectively representing a single entity, such as a web application (or a website).
4. Each project's output will be deployed as a single unit.

> Executables typically have a `.exe` extension (in Windows), and libraries have a `.dll` (meaning dynamic link library) extension. Note that .NET Core and .NET 5+ use `.dll` for executables as well.

5. Each project has a project file (with a `.csproj` extension) that contains the project's configuration and settings.

## Notes on Visual Studio `Solution`

1. A solution is a container for one or more projects. It is used to organize and manage multiple related projects.
2. In many real-world scenarios, a single application is built using multiple projects. For example, a system may have a website and desktop application, and both of these may share a common library. Each of these projects may have another project for unit tests. In order to manage these projects, we use a solution.
3. Visual Studio can only load a project if it is part of a solution. If you create a new project or open an existing project, Visual Studio will automatically create a new solution or add the project to an existing solution.
4. This is because most operations in Visual Studio are performed at the solution level, such as building, debugging, and deploying.
5. A solution file has a `.sln` extension and it doesn't use XML format like the project file. It is a text file that contains information about the projects in the solution.

# Level 1: Introduction
Learn how to create and run a C# console application.

### 1.2 Creating a Console Application 
Type the dotnet command that will create a new console application.

```sh
$ dotnet new console
```

### 1.3 Hello World Program
In our Program.cs file, let's create a simple console application that prints "Hello World!"

- Using a method from the Console class, print the following text to the console:

"Hello World!"

program.cs
```sh
using System;

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Hello World!");
    }
}
```

### 1.4 Resolving Dependencies 
Before we can run our application from the command line, we need to resolve the dependencies. Type the dotnet command that will restore our project.
```sh
$ dotnet restore
```

### 1.5 Running Our Application 
Now that we've created our application and resolved dependencies, let's use the dotnet command to run it and see what the output looks like.

```sh
> dotnet run

```


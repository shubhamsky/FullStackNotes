# C# Notes

## 1. Generics

- Need for generics?
  - The need for generics can be shown in below programs. The reason why generics where introduced can be understood very clearly from the below example of the programs involving list.

  - In below program 1 we have created a list to add numbers.

    ```csharp
    // Program 1
    public class List
    {
        public void Add(int number)
        {
            throw new NotImplementedException();
        }
        public int this[int index]
        {
            get {   throw new NotImplementedException(); }    
        }
    }
    ```

  - Below is the program for book list to hold list of type book.

    ```csharp
    // Program 2 
    public class BookList
    {
        public void Add(Book book)
        {
            throw new NotImplementedException();
        }
        public Book this[int index]
        {
            get {   throw new NotImplementedException(); }    
        }
    }
    ```

    ___Note:___ The above code is fine for creating book list. But the issue which can be concluded here is, for every new type of custom object we need to create a new custom list. And each custom list if any changes are done it might cause bugs and is not easy to manage when the number of object type increase. As for each type there will be a custom list.

  - In the below code we have created an Object List class which can be used to add any type of object to it.

    ```csharp
    // Program 3 for object List to add any object
    public class ObjectList
    {
        public void Add(Object value)
        {
            throw new NotImplementedException();
        }
        public Object this[int index]
        {
            get {   throw new NotImplementedException(); }    
        }
    }
    ```

    Now in the above program we can create any object list and add to it. But there is an issue of ___performance___. We need to do ___boxing___ and ___unboxing___ (value to reference type). Also for reference object types while fetching we need to typecast the object to specific type from the list. Also there is a type safety issue as any type of object now can be added to this list. It is very costly in terms of performance. It can be shown in the below program.

  ```csharp
    var numberList = new ObjectList();
    var book = new Book{ Isbn ="123", Title = "C# complete notes"};
    ObjectList.Add(book);

    // Here explicit type casting is required for Object to Book type
    Console.WriteLint(OjectList[0](Book).TItle);
  ```

  Hence, it can be concluded that, this is not the right approach to create a generalized list. All the above pointers led to the addition of ___Generics___ which addressed all of the issues.

  - Example of Generic List

  ```csharp
    public class GenericList<T>
    {
        public void Add(T value)
        {

        }

        public T this[int index]
        {
            get { throw new NotImplementedException(); }
        }
    }
  ```

  - In below code we have demonstrated on how to use generics to create a generic list.

  ```csharp
    var bookList = new GenericList<Book>();

    var book = new Book{ Isbn ="123", Title = "C# complete notes"};
    bookList.Add(book);
    Console.WriteLine(bookList[0].Title);

  ```

- C# Interview Preparation
  - Introduction to C#
    - History and Overview
    - Basic Syntax
    - Data Types and Variables
    - Operators
  - Control Structures
    - Conditional Statements
    - Switch Statements
    - Loops
    - Jump Statements
  - Arrays and Collections
    - Arrays
    - Lists
    - Dictionaries
  - Object-Oriented Programming (OOP)
    - Classes and Objects
    - Inheritance
    - Polymorphism
    - Encapsulation
    - Abstraction
  - Exception Handling
    - Try-Catch Blocks
    - Throw Statement
    - Finally Block
  - File Handling
    - Reading and Writing Files
    - File I/O Operations
  - LINQ (Language Integrated Query)
    - Basics of LINQ
    - LINQ to Objects
    - LINQ to XML
  - Delegates and Events
    - Delegate Declaration
    - Multicast Delegates
    - Events and Event Handling
  - Generics
    - Generic Classes
    - Generic Methods
    - Constraints
  - Advanced Topics
    - Asynchronous Programming (Async/Await)
    - Reflection
    - Attributes
    - Design Patterns
    - Dependency Injection
  - ASP.NET Core (if relevant)
    - Basics of ASP.NET Core
    - MVC Architecture
    - Routing
    - Controllers and Views
  - Entity Framework Core (if relevant)
    - Basics of Entity Framework Core
    - ORM (Object-Relational Mapping)
    - CRUD Operations

## 2. OOPS 

- Abstraction

- Polymorphism

- Inheritance

- Encapsulation

## 3. SOLID

- Single Responsibility Principle786@
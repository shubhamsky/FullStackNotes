# SOLID Principles in C#

This repository demonstrates the SOLID principles using C# examples. The SOLID principles are a set of five design principles intended to make software designs more understandable, flexible, and maintainable.

## Principles

1. **[Single Responsibility Principle (SRP)](#1-single-responsibility-principle-srp)**
2. **[Open/Closed Principle (OCP)](#2-openclosed-principle-ocp)**
3. **[Liskov Substitution Principle (LSP)](#3-liskov-substitution-principle-lsp)**
4. **[Interface Segregation Principle (ISP)](#4-interface-segregation-principle-isp)**
5. **[Dependency Inversion Principle (DIP)](#5-dependency-inversion-principle-dip)**

### 1. Single Responsibility Principle (SRP)

A class should have only one reason to change, meaning it should only have one job or responsibility.

#### Example:

```csharp
// Before SRP:
public class User {
    public void CreateUser() {
        // Code to create a user
        Console.WriteLine("User created.");
    }

    public void SendEmail() {
        // Code to send email
        Console.WriteLine("Email sent.");
    }

    public void GenerateReport() {
        // Code to generate a report
        Console.WriteLine("Report generated.");
    }
}
```

In this example, the User class has multiple responsibilities: creating a user, sending an email, and generating a report. This violates the SRP.

```csharp
// AFTER SRP:
public class User {
    public void CreateUser() {
        // Code to create a user
        Console.WriteLine("User created.");
    }
}

public class EmailService {
    public void SendEmail() {
        // Code to send email
        Console.WriteLine("Email sent.");
    }
}

public class ReportService {
    public void GenerateReport() {
        // Code to generate a report
        Console.WriteLine("Report generated.");
    }
}
```

Now, each class has a single responsibility: User is responsible for user-related operations, EmailService is responsible for sending emails, and ReportService is responsible for generating reports.

### 2. Open/Closed Principle (OCP)

Software entities should be open for extension but closed for modification.

```csharp
// Before OCP:
public class Rectangle {
    public double Width { get; set; }
    public double Height { get; set; }
}

public class AreaCalculator {
    public double CalculateRectangleArea(Rectangle rectangle) {
        return rectangle.Width * rectangle.Height;
    }
}
```

In this example, if we need to add a new shape, such as a circle, we would have to modify the AreaCalculator class, which violates the OCP.

```csharp
// After OCP:
public interface IShape {
    double Area();
}

public class Rectangle : IShape {
    public double Width { get; set; }
    public double Height { get; set; }

    public double Area() {
        return Width * Height;
    }
}

public class Circle : IShape {
    public double Radius { get; set; }

    public double Area() {
        return Math.PI * Radius * Radius;
    }
}

public class AreaCalculator {
    public double CalculateArea(IShape shape) {
        return shape.Area();
    }
}

```

Now, the AreaCalculator class is closed for modification but open for extension. We can add new shapes without modifying the AreaCalculator class.

### 3. Liskov Substitution Principle (LSP)

Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program.

```csharp
// Before LSP

public class Bird {
    public virtual void Fly() {
        // Fly logic
        Console.WriteLine("Flying.");
    }
}

public class Ostrich : Bird {
    public override void Fly() {
        throw new NotImplementedException("Ostriches can't fly.");
    }
}
```
Here, substituting Bird with Ostrich will cause an exception, violating the LSP.

```csharp
// After LSP:
public abstract class Bird {
    // Common bird properties and methods
}

public class FlyingBird : Bird {
    public void Fly() {
        // Fly logic
        Console.WriteLine("Flying.");
    }
}

public class Ostrich : Bird {
    // Ostrich specific properties
}
```

In this revised example, Ostrich does not override Fly, adhering to the LSP. FlyingBird is used for birds that can fly.

### 4. Interface Segregation Principle (ISP)

Clients should not be forced to depend on interfaces they do not use.

```csharp
// Before ISP:

public interface IWorker {
    void Work();
    void Eat();
}

public class Worker : IWorker {
    public void Work() {
        // Work logic
        Console.WriteLine("Working.");
    }

    public void Eat() {
        // Eat logic
        Console.WriteLine("Eating.");
    }
}

public class Robot : IWorker {
    public void Work() {
        // Work logic
        Console.WriteLine("Working.");
    }

    public void Eat() {
        throw new NotImplementedException("Robots don't eat.");
    }
}
```

Here, Robot is forced to implement Eat method it doesn't use, violating the ISP.

```csharp
// After ISP:

public interface IWorkable {
    void Work();
}

public interface IFeedable {
    void Eat();
}

public class Worker : IWorkable, IFeedable {
    public void Work() {
        // Work logic
        Console.WriteLine("Working.");
    }

    public void Eat() {
        // Eat logic
        Console.WriteLine("Eating.");
    }
}

public class Robot : IWorkable {
    public void Work() {
        // Work logic
        Console.WriteLine("Working.");
    }
}
```

Now, Robot only depends on IWorkable, adhering to the ISP. Worker depends on both IWorkable and IFeedable.

### 5. Dependency Inversion Principle (DIP)

High-level modules should not depend on low-level modules. Both should depend on abstractions.

```csharp
// Before DIP:
public class LightBulb {
    public void TurnOn() {
        // Turn on the light
        Console.WriteLine("Light turned on.");
    }

    public void TurnOff() {
        // Turn off the light
        Console.WriteLine("Light turned off.");
    }
}

public class Switch {
    private LightBulb _lightBulb;

    public Switch() {
        _lightBulb = new LightBulb();
    }

    public void Operate() {
        _lightBulb.TurnOn();
        // Operate the switch
    }
}
```

In this example, Switch is directly dependent on LightBulb, violating the DIP.

```csharp
// After DIP:
public interface ISwitchable {
    void TurnOn();
    void TurnOff();
}

public class LightBulb : ISwitchable {
    public void TurnOn() {
        // Turn on the light
        Console.WriteLine("Light turned on.");
    }

    public void TurnOff() {
        // Turn off the light
        Console.WriteLine("Light turned off.");
    }
}

public class Switch {
    private ISwitchable _device;

    public Switch(ISwitchable device) {
        _device = device;
    }

    public void Operate() {
        _device.TurnOn();
        // Operate the switch
    }
}
```

Now, Switch depends on the abstraction ISwitchable, and LightBulb implements ISwitchable. This adheres to the DIP, as both high-level and low-level modules depend on the abstraction.

These detailed examples should provide a clearer understanding of how to apply the SOLID principles in C# to create a more modular and maintainable codebase.

Follow me on [linkedin](https://www.linkedin.com/in/shubham-kumar-yadav-a39023106/) for more update on such posts.

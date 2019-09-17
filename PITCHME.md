### .NET 2

+++

### Topics

- C# classes
- Reference vs Value Types
- Entity Framework

---

#### C# Classes

```csharp
public class User {
    // properties
    public string username;

    // methods
    public string Greeting() 
    {
        return "Hello!";
    }

}
```

+++

### Constructors

- similar to Java
- can have multiple constructors
- constructors are not inherited

---

#### Getter/Setters

```csharp
public class User {
    // convention for private properties, start with underscore
    private string _username;

    // getter/setters
    public string username {
        get { return _username; }
        set { _username = value; }
    }
}
```

AutoImplemented Getter/Setters

```csharp
public class User {
    public string username { get; set; } 
}
```

---

#### Inheritance

```csharp
class Employee : User
{
    // code specific to admins
}

class Admin : User
{
    // code specific to admins
}
```

---

### Overriding Methods

```csharp
class User 
{
    public virtual void Greeting() 
    {
        Console.WriteLine("Hello");
    }
}

class Employee : User
{
    public override void Greeting()
    {
        Console.WriteLine("Hello Boss!");
    }
}
```

+++

- can declare properties and methods to be virtual
- only virtual methods can be overriden
- methods are non-virtual by default

---

### Abstract

```csharp
abstract class User
{
    public abstract int Greeting();
}

class Employee : User
{
    public override int Greeting();
}
```

+++

- abstract classes cannot be instantiated
- abstract methods MUST be implemented by child class

---

### Structs

```csharp
struct User 
{
    public string username;
    public string email
}
```

+++

- class is a reference type, struc is a value type
- structs cannot implement inheritance
- structs are more lightweight than classes
- only use structs if the data doesn't change
- read more [here](https://www.c-sharpcorner.com/blogs/difference-between-struct-and-class-in-c-sharp)

---

### Reference vs Value Types

- PENDING
- pointers vs values
- find some graphs
- some exercises on what are pointers and what aren't

---




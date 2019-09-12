## .NET - 1

---

### Topics

- C# Syntax
- Unit Testing
- Exercises
- Basic Web Server

---

### Basic Syntax

- similar to Java
- `public static void`
- all code in classes
- semicolons required

---

### Variables

```csharp
// comments

// basic variables
string x = "abc"
var x = "abc"

// arrays
int[] arr = new int[] { 7, 9, 21, 42, 58, 67, 88 };
arr[0] === 7

// lists
var list = arr.ToList();
list.Add(92)

// dictionary
var dict = new Dictionary<string, int>();
dict.Add()
```

+++

### Nullables

```csharp
// these 2 lines do the same thing
Nullable<int> x = null;
int? y = null;

// have to check null status
if (x.HasValue)
{
    // have to access value
    Console.WriteLine(x.Value == 123)
}
```

---

### Control Flow

+++

### If Else

```csharp
if(x == 123)
{
    // do something
}
else if (y == 456)
{
    // do something else
}
else 
{
    // do something else v2
}
```

+++

### Functions

```csharp
public static void Greeting(string msg) 
{
    Console.WriteLine(msg);
}
```

+++

### Loops

```csharp
for (int i = 0; i < 10; i++)
{
    Console.WriteLine("Value of i: {0}", i);
}

foreach (int element in numbers)
{
    Console.WriteLine(element);
}
```

---

### Exercise: Pig Latin






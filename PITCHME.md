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

1. find the first vowel
2. shift all non-vowels behind the section starting from the first vowel and adds <span class="text-gold">ay</span>
3. if the word starts with vowel, don't change it
4. if there is no vowel in the word, add <span class="text-gold">ay</span> behind.

+++

```csharp
public static string Convert(string word) {
    // write your code here
}

public static void Main() {
    Console.WriteLine(Convert("art").Equals("art"))
    Console.WriteLine(Convert("vowel").Equals("owelvay"))
    Console.WriteLine(Convert("nginx").Equals("inxngay"))
    Console.WriteLine(Convert("hello").Equals("ellohay"))
    Console.WriteLine(Convert("Dr").Equals("Dray"))
}
```

---

## Unit Testing

- MSTest
- NUnit
- xUnit

---

### Syntax

```csharp
 [TestClass]
public class FirstScenario
{
    [TestMethod]
    public void TestMethod1()
    {
        BinarySearch.Program.Main();
        Assert.AreEqual(123, 123);
    }
}
```

---

### Exercise: Binary Search

![image](https://www.mathwarehouse.com/programming/images/binary-vs-linear-search/binary-and-linear-search-animations.gif)

+++

Convert this to unit tests

```python
x = [7,9,21,42,58,67,88]

print(bsearch(x, 67) == 5)
print(bsearch(x, 9) == 1)
```

---

### Exercise: Tic Tac Toe

- 2 players
- display board in terminal
- player can enter board idx to place piece
- can switch to second player and vice versa
- will show who won or if its a draw
- write unit tests for the win/loss/draw conditions

---

### ASP.NET Webserver

---

1. create a project with the `ASP.NET Core Web Applications` template
2. create a folder named Controllers
3. add a new controller under it, `API Controller(Empty)`

---

### Controller

```csharp
namespace WebApplication2.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class UsersController : ControllerBase
    {
        // GET api/values
        [HttpGet]
        public ActionResult<IEnumerable<User>> Get()
        {
            User[] arr = new User[] {
                new User(5, "ming xiang", "mingxiangchan@gmail.com"),
                new User(8, "ming hao", "minghaochan2018@gmail.com"),
            };
            return arr;
        }
```

+++

### Similar to Java

- annotations look slightly different
- can auto-convert to json
- can convert class to json
- getter methods is not required

---

### Exercise: Todos

- GET <span class="text-blue">/todos?completed=true</span>
- GET <span class="text-blue">/todos/{id}</span>
- GET <span class="text-blue">/users?active=true</span>
- GET <span class="text-blue">/todos/{id}</span>

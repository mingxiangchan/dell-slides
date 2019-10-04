---
marp: true
---

### Intro to Java

---

#### Instructions

1. Install Java

    ```bash
    scoop bucket add java
    scoop install ojdkbuild8
    ```
2. Create a folder for today's java projects

---

#### Basics

1. create a file ending with `.java`
2. use the `class` snippet to auto create the class
3. ensure there is a `main` function with `public static void` before it
4. every line MUST end with semicolon `;`

---

#### Printing to Terminal

```java
String x  = "abc"
System.out.println(x)
```

Running file

```bash
java <filename>
```

---

#### Variables

requires type declaration

```java
int x = 123
char y = 'a'
boolean z = true
```

---

#### Strings vs Chars

```java
char x = 'a'
String name = "abc"
```


#### Arrays

```java
int[] x = {1,2,3}
Array<String> y = {"abc", "def"}
```

---

#### Maps

```java
Map<String, Integer> pokemon = Map.ofEntries(
    entry("charmander", 50),
    entry("squirtle", 20)
);
```

---

### Advanced

---

#### Primitives vs Non Primitives

```java
// primitives
int x = 123;
char y = 'a';
boolean z = true;

// not primitives
Integer x = 123;
Character y = 'a';
Boolean z = true;
String name = "John";
```

---

#### Array vs ArrayList

```java
import java.util.ArrayList;

// can contain primitives
int[] x = {1,2,3};
Array<char> y = {'a', 'b'};

// cannot contain primitives
ArrayList<int> x = {1,2,3}; // will raise error
ArrayList<Integer> x = Arrays.asList(1,2,3);

// or
Array<Integer> x = {1,2,3};
ArrayList<Integer> y = Arrays.asList(x);
```

---

`ArrayList` allows you to modify the array

```java
ArrayList<Character> x = Arrays.asList('a','b','c');
x.add('d'); // => {'a', 'b', 'c', 'd'}
x.get(2); // => 'c'
x.size(); // => 3
x.clear(); // => {}
x.remove(1); // => {'a', 'c'}
x.isEmpty(); // => false
```

---

#### Nested Arrays

```java
int[][] x = {{1,2},{3,4}};
Array<Array<int>> x = {{1,2},{3,4}};

// it can get a little complicated
char[] x = {'a','b'};
char[] y = {'c','d'};
ArrayList<char[]> z = new ArrayList<char[]>() // create empty array list;
z.add(x);
z.add(y);
```

---

### Map vs HashMap

```java
import java.util.HashMap;

HashMap<String, Integer> x = new HashMap<String, Integer>()
x.put("age", 28)
x.put("height", 183)
```

---

### Control Flow

---

#### If / Else

```java
if (x == y) {
  // do something
} else {
  // do something else
}
```

---

```java
if (123) { } // this will fail

if (true) { } // this will succeed
if (x == y) { } // this will succeed

// string equality
if ("abc".equals("abc")) { } // this is correct
if ("abc" == "abc") { } // this is incorrect
```

---

#### For / While Loops

```java
while (true) {
  // do something
}
```

```java
for (int i = 0; i < array.length(); i++) {
  // do something
}
```

---

#### Functions

```java
int sum(x int, y int) {
  return x + y;
}
```

is the same as

```ts
function sum(x: number, y: number): number {
  return x + y
}
```

---

### Exercises

---

#### Todo List

1. print a list of todos
2. for each todo, show whether it is completed or not

---

#### Tic Tac Toe

1. print a tic tac toe board (pre filled)
2. no user input
3. check whether there is a winner/loser/draw
4. print message saying who won / its a draw

---

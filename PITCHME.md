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
    scoop install maven
    ```

2. Instal [VS Code Java Extension Pack](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack)
3. Create a folder for today's java projects
4. Download [STS](https://download.springsource.com/release/STS4/4.4.0.RELEASE/dist/e4.13/spring-tool-suite-4-4.4.0.RELEASE-e4.13.0-win32.win32.x86_64.zip) (for 2 weeks later)

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

### Exercise: Todo List

1. print a list of todos
2. for each todo, show whether it is completed or not

_Expected Result:_

```txt
1. [ ] Shop for Groceries
2. [X] Analyze Oct sales data
3. [ ] Prepare project brief
```

---

### Exercise: Fibonacci

A fibonacci sequence is a sequence of numbers where the 3rd number is always the sumber of the 2 numbers before it.

```
1, 1, 2, 3, 5, 8, 13, 21, 34, 55
```

---

Try writing a `findFibonacci` function that does the following

```java
findFibonacci(0) // => 1
findFibonacci(1) // => 1
findFibonacci(2) // => 2
findFibonacci(3) // => 3
findFibonacci(4) // => 5
```

---

### Exercise: Binary Search

![bsearch](https://www.mathwarehouse.com/programming/images/binary-vs-linear-search/binary-and-linear-search-animations.gif)

---

### Task

Write a method that takes a target number and a sorted list of numbers in non-decreasing order and returns either the position of the number in the list, or "do not exist" to indicate the target number is not in the list.
For instance, `binary_search(32, [13, 19, 24, 29, 32, 37, 43])` should return `4`, since `32` is the fourth element of the list (counting from zero).

---

```java
  static int bsearch(int[] array, int target) {
    // your code
  }

  public static void main(String[] args) {
    int[] arr = {7,9,21,42,58,67,88};

    System.out.println(bsearch(arr, 67) == 5);
    System.out.println(bsearch(arr, 9) == 1);
  }
```

---

### Exercise: Pig Latin

1. create a function convert
2. it accepts a word string as an argument
3. finds the first vowel
4. shifts all non-vowels behind the section starting from the first vowel and adds ay
5. if the word starts with vowel, doesn't change it
6. if there is no vowel in the word, add ay behind.

---

| Word  | Pig Latin Version |
| ----- | ----------------- |
| art   | art               |
| vowel | owelvay           |
| nginx | inxngay           |
| hello | ellohay           |
| Dr    | Dray              |

---

```java
import java.util.Arrays;

/**
 * PigLatin
 */
public class PigLatin {
    static String convert(String word){
       // Your Code
    }

    public static void main(String[] args){
        System.out.println(convert("art").equals("art"));
        System.out.println(convert("vowel").equals("owelvay"));
        System.out.println(convert("nginx").equals("inxngay"));
        System.out.println(convert("hello").equals("ellohay"));
        System.out.println(convert("Dr").equals("Dray"));
    }
}
```

---

## Tic Tac Toe

1. print a tic tac toe board (pre filled)
2. no user input
3. check whether there is a winner/loser/draw
4. print message saying who won / its a draw

---

```java
  static String checkBoard(String board) {
    // your code
  }

  public static void main(String[] args) {
    // row
    System.out.println(checkBoard("XXX-O-O-O").equals("X"));
    // col
    System.out.println(checkBoard("OXXOX-O--").equals("O"));
    // diagonal
    System.out.println(checkBoard("XO--XO-OX").equals("X"));
    // draw
    System.out.println(checkBoard("XOXOXOXOX").equals("draw"));
  }
```

---

## Assignment: Sudoku Checker

1. try it out [here](https://sudoku.game/)
2. check row for potential solutions
3. check column for potential solutions
4. check 3x3 grid for potential solutions
5. find intersection all the 3 sets of solutions

---

```java
import java.util.Arrays;

public class Sudoku {
    static char[] checkSolution(String board, int cellIdx) {
        // your code here
    }

    static void displayBoard(String boardString) {
        String[] boardRows = { "", "", "", "", "", "", "", "", "" };
        char[] boardArray = boardString.toCharArray();
        for (int index = 0; index < boardString.length(); index++) {
            boardRows[index / 9] = boardRows[index / 9] + " " + boardArray[index];
            if (index % 9 == 2 || index % 9 == 5) {
                boardRows[index / 9] = boardRows[index / 9] + " |";
            }
        }
        System.out.println("-------------------------");
        for (int index = 0; index < 9; index++) {
            System.out.println("|" + boardRows[index] + " |");
            if (index == 2 || index == 5) {
                System.out.println("-------------------------");
            }
        }
        System.out.println("-------------------------");
    }

    public static void main(String[] args) {
          String board = "105802000090076405200400819019007306762083090000061050007600030430020501600308900";
          displayBoard(board);

          char[] solutionOne = {'4','7'};
          char[] solutionTwo = {'2','7'};

          boolean solveOne = Arrays.equals(checkSolution(board, 1), solutionOne);
          boolean solveTwo = Arrays.equals(checkSolution(board, 80), solutionTwo);
          System.out.println(solveOne);
          System.out.println(solveTwo);
      }
}
```

---

## Assignment 2: Sudoku Solver

-   optional
-   write a program to automatically solve a sudoku board
-   easy board: can solve with only elimination
-   hard board: can solve with guessing/backtracking

---

```java
public class SudokuSolver {
    static void displayBoard(String boardString){
        String[] boardRows = {"", "", "", "", "", "", "", "", ""};
        char[] boardArray = boardString.toCharArray();
        for(int index = 0; index < boardString.length(); index ++ ){
            boardRows[index/9] = boardRows[index/9] + " " + boardArray[index];
            if(index % 9 == 2 || index % 9 == 5){
                boardRows[index/9] = boardRows[index/9] + " |";
            }
        }
        System.out.println("-------------------------");
        for(int index = 0; index < 9; index ++ ){
            System.out.println("|" + boardRows[index] + " |");
            if(index == 2 || index == 5){
                System.out.println("-------------------------");
            }
        }
        System.out.println("-------------------------");
    }

    static String solve(String boardString){
        displayBoard(boardString);
        return "";
    }

    public static void main(String[] args) {
        // Easy Mode
        String solution = solve("105802000090076405200400819019007306762083090000061050007600030430020501600308900");
        System.out.println(solution.equals("145892673893176425276435819519247386762583194384961752957614238438729561621358947"));

        // // Hard Mode
        // String solution = solve("400000805030000000000700000020000060000080400000010000000603070500200000104000000");
        // System.out.println(solution.equals("417369825632158947958724316825437169791586432346912758289643571573291684164875293"));
    }
}
```

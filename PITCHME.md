### Automated Testing

---

### Activity

- Clone [this repository](https://github.com/matyb/java-koans)
- Open the folder in VS Code
- cd into the <span class="text-gold">koans</span> folder
- run the command <span class="text-gold">Start-Process run.bat</span>

+++

### Instructions

- read the instructions printed in the terminal
- adjust the code in the <span class="text-blue">koans/src</span> folder
- save the file
- check terminal for next instructions

---

### What is Testing

- writing code to test your code
- set up a scenario
- execute the scenario
- assess the outcome

---

### Why Write Tests

+++

#### When you build a house...

- discuss design
- draw blueprint
- build house
- at each stage, compare against blueprint

+++

#### When you write a program...

- discuss requirements
- write code!
- check if it passes/fails

+++

#### What does pass/fail mean?

- changes depending on scenario
- changes depending on inputs
- changes depending on output
- changes depending on person! (perspective)

+++

### Automated Testing ensures....

- completely objective
- explicitly state success/fail inputs/outputs

---

### How to Write Tests?

+++

### Mindset

- Given
- When
- Then

+++

@snap[west span-25]
@box[bg-blue text-white rounded box-padding](1. Given#Correct username and password)
@snapend

@snap[midpoint span-25]
@box[bg-orange text-white rounded box-padding](2. When#User tries to log in)
@snapend

@snap[east span-25]
@box[bg-pink text-white rounded box-padding](3. Then#User is logged in)
@snapend

+++

@snap[west span-25]
@box[bg-blue text-white rounded box-padding](1. Given#Incorrect username and password)
@snapend

@snap[midpoint span-25]
@box[bg-orange text-white rounded box-padding](2. When#User tries to log in)
@snapend

@snap[east span-25]
@box[bg-pink text-white rounded box-padding](3. Then#Show error message to user)
@snapend

+++

- e.g. Grab cancellation
- who cancelled? driver or passenger?
- when did they cancel?
- why did they cancel?
- what impact does it have

---

### Activity

Write out the Given, When, Then for Tic Tac TOe

+++

### Activity

Write out the Given When Then for a phone number checker program

- phone number
- country code
- area code
- hyphens / no-hypens
- spaces
- possible mobile providers

---

### Generate New Maven Project

```
mvn archetype:generate -DgroupId=learning -DartifactId=JunitOne -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

+++

### Update pom.xml

```xml
<dependency>
    <groupId>org.junit.platform</groupId>
    <artifactId>junit-platform-runner</artifactId>
    <version>1.5.1</version>
</dependency>
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-engine</artifactId>
    <version>5.5.1</version>
</dependency>
```

---

### JUnit

- the main testing framework for Java

---

### Writing your first test

```java
// inside the main folder
public class Game {
    public static String hello() {
        return "Hello World";
    }
}
```

```java
// inside the tests folder
public class GameTest {
    public void testHello() {
        assertEquals(Game.hello(), "Hello World");
    }
}
```

+++

### Rules

- must be inside the <span class="text-blue">test</span> folder
- method must be named <span class="text-blue">test___</span>

+++

### Example

```java
public class CheckerTest {
    public void testRowOneX() {
        // Given
        Checker checker = new Checker("XXX------");
        
        // When
        checker.run()

        // Then
        assertsEquals(checker.result, "Player X has won")
    }
}
```

---

### Exercise

Try doing the first 3 exercises [here](https://projecteuler.net/archives)

Use tests!

You can find the answers for your tests [here](https://github.com/nayuki/Project-Euler-solutions/blob/master/Answers.txt)

---

### Exercise

- create the tests for a Tic Tac Toe board checker
- write the code to fulfill the tests
- run the tests to make sure your code works

---

### Exercise: Sudoku Solver

- create the tests for a SudokuSolver
- it will check a blank cell on a Sudoku board
- it will show the potential solutions for row, column, and box
- board: 

```
105802000090076405200400819019007306762083090000061050007600030430020501600308900
```

---

### Assignment: Discount System

Build a discount app using a test driven app approach

+++

### Process

**Given** a product and discount

**When** applying the discount

**Then** what is the total price

+++

### Requirements

1. Absolute discounts
2. Percentage discounts
3. Validity period
4. Product-specific discounts
5. Applying discount on shopping cart
















## Intro to OOP

---

### What is OOP

- Object Oriented Programming
- build programs using objects that interact with each other

+++

#### Programming Fundamentals

**Data** -> variables

```java
bool isStudent = false;
```

**Operations** -> functions

```java
int sum(int x, int y) {
  return x + y;
}
```

+++

OOP tries to merge **data** and **operations** into **objects**

---

### OOP in java

- class
- methods
- properties
- constructors
- interface
- inheritance

---

### Class

- in Java, all code must be in a class
- the `class` contains `methods` and `properties`

+++

```java
class User {
  String name;
  bool isStudent;

  void sayHello() {
    System.out.println("Hello, my name is" + this.name)
  }
}
```

+++

### Properties

- must declare property type
- initial value can be declared, is optional

```Java
String name;
bool isStudent = false;
```

---

### Constructors

- used to construct an instance of a class
- construct using `new` keyword

```java
class User {
  String name;

  User() {
    this.name = "Ming Xiang";
  }
}

User newUser = new User();
```

+++

Can accept arguments

```java
class User {
  String name;

  User() {
    this.name = "Ming Xiang";
  }

  User(String inputName) {
    this.name = inputName;
  }
}

User userOne = new User("Ming Xiang");
User userTwo = new User("Ming Hao");
User userThree = new User("Evelyn");
```

+++

There can be multiple constructors

```Java
class User {
  String name;

  User(String inputName) {
    this.name = inputName;
  }
}

User userOne = new User();
User userTwo = new User("Ming Hao");
```

---

### Object Interaction

```java
Player player = new Player("John")
Monster monster = new Monster("Ogre")
player.hit(monster)
// prints out "John hits the Ogre for 15 damage"
// prints out "The Ogre has 20 HP remaining"
```

+++

```java
OrangeTree tree = new OrangeTree();
tree.oranges.size() // => 5
Orange orange = tree.pickOrange();
tree.oranges.size() // => 4
orange.size // => 10 cm
orange.state // => fresh
```

---

### Exercise 1

- create Player and Monster class
- implement the following properties for them
  - HP
  - Atk
- implement the following interactions for them
  - hit

+++

### Exercise 2

- create OrangeTree and Orange class
- from the previous example, figure out what properties and methods you need

+++

### Exercise 3

- create Car, Bus, Airplane, Engine, Wheel class
- Engine has `horsepower` property
- car is initialized with 4 wheels
- bus is initialized with 6 wheels
- airplane is initialized with 3 wheels
- the engine for each vehicle has different horsepower

+++

### Exercise 4

- create class for the following Dell products
  - desktop
  - laptop
  - mouse
  - keyboard
  - monitor

+++

- create child components for your primary product classes
  - e.g.
    - GPU
    - HDD
    - RAM
- implement price for every class
- some classes will have fixed price, some (e.g. laptop) is the sum of its parts
- implements methods to change the component
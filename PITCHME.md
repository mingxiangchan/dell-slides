---
marp: true
---

# Intro to OOP

---

## What is OOP

- Object Oriented Programming
- build programs using objects that interact with each other

---

## Programming Fundamentals

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

---

OOP tries to merge **data** and **operations** into **objects**

---

## OOP in java

- class
- methods
- properties
- constructors
- interface
- inheritance

---

## Class

- in Java, all code must be in a class
- the `class` contains `methods` and `properties`


```java
class User {
    // properties
    String name;
    bool isStudent;

    // methods
    void sayHello() {
        System.out.println("Hello, my name is" + this.name)
    }
}
```

---

## Properties

- must declare property type
- initial value can be declared, is **optional**

```Java
String name;
bool isStudent = false;
```

---

## Constructors

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

---

Constructors can accept arguments

```java
class User {
  String name;

  User(String inputName) {
    this.name = inputName;
  }
}

User userOne = new User("Ming Xiang");
User userTwo = new User("Ming Hao");
User userThree = new User("Evelyn");
```

---

There can be multiple constructors

```Java
class User {
  String name;

  User() {
    this.name = "Ming Xiang";
  }

  User(String inputName) {
    this.name = inputName;
  }
}

User userOne = new User();
User userTwo = new User("Ming Hao");
```



---

## Exercise 1

- create Player and Monster class
- implement the following properties for them
  - HP
  - Atk
- implement the following interactions for them
  - hit
---

```java
Player player = new Player("John")
Monster monster = new Monster("Ogre")
player.hit(monster)
// prints out "John hits the Ogre for 15 damage"
// prints out "The Ogre has 20 HP remaining"
System.out.println(player.atk == 15)
System.out.println(monster.hp == 20)

```

---

## Exercise 2

- create OrangeTree and Orange class
- from the previous example, figure out what properties and methods you need

---

```java
OrangeTree tree = new OrangeTree();
// hint: tree.oranges is an ArrayList
System.out.println(tree.oranges.size() == 5)

Orange orange = tree.pickOrange();

System.out.println(tree.oranges.size() == 4)
System.out.println(oranges.size == 10)
System.out.println(oranges.state.equals("fresh"))
```

---

# Advanced OOP

---

## Polymorphism

*English Definition* - Many Forms

---

## Similarities and Differences

|                  | Car | Bicycle | Airplane |
|------------------|-----|---------|----------|
| number of wheels | 4   | 2       | 3        |
| top speed        | 200 | 25      | 925      |
| number of wings  |     |         | 2        |

---

## Inheritance

Java uses the `extends` keyword to implement inheritance

```java
class Vehicle {
    int numWheels;
    int topSpeed;
}
```

```java
class Car extends Vehicle {
    int numWheels = 4;
    int topSpeed = 200;
}
```

```java
class Airplane extends Vehicle {
    int numWheels = 3;
    int topSpeed = 925;
    int numWings = 2;
}
```

---

Can group inherited items together, only accessing the shared properties.

```java
ArrayList<Vehicle> vehicles = new ArrayList<>();
vehicles.add(new Car());
vehicles.add(new Airplane());

for(int i=0;i< vehicles.size();i++){
    Vehicle x = vehicles.get(i);
    System.out.println(x.numWheels);
    System.out.println(x.topSpeed);
    // cannot access numWings, only exists on Airplane
}  
```

---

Can treat a child type as a parent type.

```java

import java.util.Random;

Random rand = new Random();
// Obtain a number between [0 - 49].
int n = rand.nextInt(50);

Vehicle x;

if (x > 25) {
  x = new Car();
} else {
  x = new Airplane();
}

System.out.println(x.numWheels);
System.out.println(x.topSpeed);
```

---

## Inheritance Characteristics

- children inherit all `properties` and `methods` from parent
- children can override the inherited `properties`/`methods` if needed
- accessing a child via the parent's type
  - can only access shared properties/methods
  - however will execute the child's version

---

## Exercise

- discuss the similarities and differences between
  - Human
  - Insect
  - Snake
  - Whale
  - Bird
- discuss how to categorize the above animals

---

- implement the previous animals as classes
- implement the categories and inheritance
- implement the following
  - create an array of animals
  - add 1 of each animal to the array
  - print info about the aggregrate shared properties
    - what is the average number of legs for animals?
    - how many animals have a spinal cord vs those who don't
    - etc.

---

### Encapsulation

---

Remember `public` & `private`?

```js
class ChatService implements OnInit {
    currentUser
    private users
    private messages

    public getUser(){}

    public getMessages(){}

    private setUser(){}
}
```

---

**public :** variables/functions are accessible outside of the class and within the class

**private :** variables/functions are only accessible within the class**

---

#### Encapsulation is about
- Controlling access to data and functions within a class

---

### Why Encapsulation?
- Prevent access by **class** that should not be concerned with said variable/function
- Information / functions should be on a need to know/use basis
- **Classes** should only be concerned with the immediate variables/function they require

---

#### By default, keep things private
- Only when something else requires access, should you consider making it public, and even then, may need to set a separate layer, e.g: `getUser()`
- Consider what should become private

---

### Exercise 1
User Login

---

```java
Website nextacademy = new Website("NextAcademy");
User user = new User("test", "password");

String password = "hacking";
nextacademy.login(user, password);
// Unsuccessful login!
nextacademy.isLoggedIn; // false

String password = "password";
nextacademy.login(user, password);
// test has logged in successfully to NextAcademy
nextacademy.isLoggedIn; // true

// user.password returns error
// user.username returns error
user.username(); // "test"
user.setUserName('newUserName','password');
user.username(); // "newUsername"
```

---

### Exercise 2 - Credit card system

Making Purchases on Ebay
- Create Customer, Ebay, Transaction, Visa class
- When a Customer makes a purchase, Ebay creates a Transaction
- Transaction has transactionId, platform, status and amountPayable
- Customer can go to Visa and input transaction details and credit card details

---

- Visa executes payment
- If payment does not exceed credit limit, payment is successful
- Visa notifies Ebay of payment status
- Ebay marks transactions as paid
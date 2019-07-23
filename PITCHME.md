# Advanced OOP

---

### Beans

- a class
- implements Serializable
- all properties are private
- contains getter methods for each property
- constains setter methods for each property

+++

```java
class User implements Serializable {
  private int age;

  int getAge() {
    return this.age;
  }

  void setAge(int age) {
    this.age = age;
  }
}
```

+++

```java
class User implements Serializable {
  private int age;
  private boolean isStudent;

  int getAge() {
    return this.age;
  }

  void setAge(int age) {
    this.age = age;
  }

  int getIsStudent() {
    return this.isStudent;
  }

  void setIsStudent(boolean isStudent) {
    this.isStudent = isStudent;
  }
}
```

---

### Exercise 1

- create a Laptop class
- add private properties
  - serial number
  - name
  - price
  - components -> String[]
- add getters and setters

---

### Factories

- objects that create other objects
- converts input into objects

+++

- convert array of strings into array of User
- convert CSV data into array of ProductOrder
- convert Admin into Employee

+++

```java
class EmployeeFactory {
  static Employee generateEmployee(Admin admin) {
    Employee employee = new Employee();

    employee.name = admin.name;
    employee.position = "admin";

    return employee
  }
}
```

---

### Exercise 2

- Car contains: name
- Vehicle contains: name, numWheels
- VehicleFactory converts Car to Vehicle

+++

### Exercise 3

- have a list of names
- Student contains: name, age
- StudentFactory converts list of names into array of Student, each with random age

---

https://github.com/sandromancuso/Gilded-Rose-Kata/tree/master/src/main/java/org/gildedrose
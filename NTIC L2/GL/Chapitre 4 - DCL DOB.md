# Lesson: Static Modeling with Class and Object Diagrams (DCL and DOB)

In this lesson, we will dive into the **static modeling** of a system using **Class Diagrams (DCL)** and **Object Diagrams (DOB)**. These diagrams are part of the Unified Modeling Language (UML) and are used to represent the structure of the system in its static state—essentially, how the system is organized at a given moment.

---

## 1. Static Modeling Overview

Static modeling focuses on describing the structure of the system at a specific point in time. It defines the system’s **classes**, **attributes**, **operations**, and the **relationships** between the entities. It answers the question: **What does the system contain?**

- **Class Diagrams (DCL)**: Show the internal structure of the system and the relationships between its entities.
- **Object Diagrams (DOB)**: Show instances of classes and their relationships at a particular moment.

---

## 2. Class Diagrams (DCL)

A **Class Diagram** represents the static structure of a system, illustrating the **classes** within the system, their **attributes**, **methods**, and how these classes are related.

### Key Components of a Class Diagram:
- **Classes**: Represent groups of similar objects with shared characteristics and behaviors.
    - **Attributes**: Properties of the class (e.g., `name`, `age`).
    - **Operations (Methods)**: Actions that can be performed on or by objects of the class (e.g., `getAge()`).
- **Relationships**: Associations between classes, such as:
    - **Association**: A simple relationship between two classes (e.g., a `Person` class and a `Car` class).
    - **Generalization (Inheritance)**: A "is-a" relationship between a superclass and a subclass (e.g., `Vehicle` → `Car`).
    - **Aggregation**: Represents a whole-part relationship where the part can exist independently of the whole (e.g., a `Library` has `Books`).
    - **Composition**: A stronger form of aggregation where the part cannot exist without the whole (e.g., `House` contains `Rooms`).

### Class Syntax in UML:
A class is typically represented with:
| ClassName       |
-------------------
| - attribute1    |
------------------
| + attribute2    |
-------------------
| + method1()     |
| # method2()     |
-------------------
- **Visibility**: `+` (public), `-` (private), `#` (protected).
- **Multiplicity**: How many instances of a class are related to another. For example, `1..*` means "one or more".

---

## 3. Object Diagrams (DOB)

An **Object Diagram** shows instances of the classes at a specific moment in time. It illustrates the **objects** (instances of classes), their **attributes** (with values), and the **relationships** between these objects.

- **Objects**: Represent real instances of a class.
- **Links**: Show the relationships between objects, typically represented by lines connecting the objects.

Object diagrams can be used to:
- Provide an example of how the system looks at a particular time.
- Show the state of an object, with its attributes and their values.

### Example:
If you have a **Person** class with attributes like `name` and `age`, an **Object Diagram** will show the instance of the class:
| person1: Person       |
-------------------------
| name = "John Doe"     |
------------------------------
| age = 30              |
-------------------------

---

## 4. Relationships in Class Diagrams

- **Association**: A connection between two classes (e.g., a `Person` **associates** with a `Car`). This can be simple or with specific multiplicities.
- **Inheritance (Generalization)**: Shows how a subclass inherits attributes and operations from a superclass (e.g., `Car` inherits from `Vehicle`).
- **Aggregation**: Represents a whole-part relationship where the part can exist independently of the whole (e.g., a `Library` has `Books`).
- **Composition**: A stronger form of aggregation where the part cannot exist without the whole (e.g., a `Room` cannot exist without a `House`).

---

## 5. Practical Example of Class Diagrams

Consider a library management system:

- **Classes**: `Book`, `Library`, `Member`
- **Attributes of Book**: `title`, `author`, `isbn`
- **Methods of Book**: `checkOut()`, `returnBook()`
- **Relationships**: 
    - **Library** "has" many **Books**, shown as an aggregation.
    - **Library** "has" many **Members**, shown as an aggregation.
    - **Member** "can borrow" **Books**, represented as an association.

### Class Diagram Example:
-------------------        -------------------
| Library                   |<>---->| Book           |
-------------------        -------------------
| - name: String       |               | - title: String      |
| + addBook()         |               | - author: String  |
| + removeBook()   |               | + checkOut()      |
-------------------        -------------------

-------------------
| Member           |
-------------------
| - name: String   |
-----------
| + borrowBook()   |
-----------------------
In this example:
- The `Library` has many `Books`, shown as an aggregation.
- The `Member` can borrow `Books`, represented as an association.

---

## 6. Abstract Classes and Methods

- **Abstract Class**: A class that cannot be instantiated. It often contains **abstract methods** that define a structure without implementing it. These methods must be implemented by subclasses.
    - Represented by an **italicized class name** or the `<<abstract>>` stereotype.
- **Abstract Method**: A method without a body, only defining the signature of the operation (e.g., `move()` in a `Vehicle` class).

---

## 7. Converting Class Diagrams to Code

The elements of a class diagram have direct counterparts in programming languages like Java or C++.

For example:
- A **class** in UML is directly mapped to a **class** in code.
- **Attributes** map to **variables**.
- **Methods** translate to **functions** or **methods** in code.
- **Associations** often result in references or arrays in the code.

---

## 8. Object Diagrams and Dynamic Systems

An **Object Diagram** reflects the system’s state at a given time. It shows **objects** and their **attribute values** at that moment. 

For example, a running system may create, modify, or delete objects dynamically. **Object Diagrams** are helpful for showing the exact state of a system during runtime.

---

## 9. Best Practices in Static Modeling

- Identify the **core classes** that represent real-world entities in the system.
- Establish the **relationships** between these classes, keeping in mind **multiplicity** and **visibility**.
- Use **abstract classes** and **methods** where necessary to create general templates for other classes.
- Ensure your model is **simple and clear** by avoiding unnecessary complexity or redundant classes.

---

## Conclusion

Class and Object Diagrams are foundational tools in **static modeling**. **Class Diagrams (DCL)** define the structure and relationships of the system, while **Object Diagrams (DOB)** illustrate how instances of those classes relate at a particular moment. These diagrams help in understanding the system’s structure and serve as a blueprint for development.

[[UNIV/NTIC L2/Génie Logiciel S3 2/Chap 4 (DCL DOB).pdf]]

---
## 🔗 Navigation
- **Module:** [[GL|◀ GL]]
- **Semester:** [[NTIC L2|◀ NTIC L2]]
- **Academic Home:** [[README|🏠 Home]]

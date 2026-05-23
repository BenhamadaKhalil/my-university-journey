# Lesson: Understanding Use Case Diagrams (Diagramme de Cas d'Utilisation)
#GL 
## Introduction

A **Use Case Diagram (DCU)** is a visual representation of the functional requirements of a system from the user's perspective. Before developing software, it's crucial to understand **what the software will be used for**. Use Case Diagrams help answer this question by modeling the system's functionalities and its interaction with users.

---

## Elements of a Use Case Diagram

A Use Case Diagram consists of three main elements:

1. **Actors**: External entities (people, processes, or systems) that interact with the system.
2. **Use Cases**: The functions or features that the system performs, triggered by actors.
3. **Relationships**: The connections between actors and use cases, and between different use cases.

---

## 1. Actors

An **actor** represents a set of roles played by an external entity (e.g., a person or another system) that interacts with the system. Actors can be:
- **Primary actors**: Direct users of the system's core functionalities (e.g., a customer in an e-commerce system).
- **Secondary actors**: Support or maintain the system without directly benefiting from its primary functions (e.g., a system administrator).

---

## 2. Use Cases

A **Use Case** represents a function or feature that the system performs. Use cases are often described using verbs in the infinitive form, such as:
- **Main Use Case**: A function that is visible from the outside (e.g., “Place Order”).
- **Internal Use Case**: A function that is not directly triggered by an actor but is related to other use cases (e.g., “Verify Stock”).

---

## 3. Relationships 

Relationships in a Use Case Diagram help define how actors interact with the system and how use cases interact with each other:

### 1. Association Relations  (Acteur -- CU)
- An **association** represents the interaction between an actor and a use case. It shows that the actor can trigger or initiate the use case.

### 2. Generalization Relations  (CU -- CU)
- A **generalization** indicates that one actor is a specialized version of another. All use cases available to the parent actor are also available to the child actor.

### 3. Include Relations  (CU -- CU)
- An **include** relationship indicates that one use case (Y) is included in another (X) during its execution. This relationship is used to avoid repetitive actions in multiple use cases.
- Example: “Check Stock” is included in “Place Order” if stock verification is required.

### 4. Extend Relations  (CU -- CU) 
- An **extend** relationship represents an optional use case that extends another use case under certain conditions. The extension occurs at a specific **extension point** within the extended use case.
- Example: "Verify Account Balance" could be an extended use case that occurs only if a withdrawal exceeds a certain amount.

---

## Steps to Create a Use Case Diagram

To create a Use Case Diagram, follow these steps:

1. **Specify the Subject**: Define the system you are modeling.
2. **Identify the Actors**: Determine who or what will interact with the system.
3. **Identify the Use Cases**: List the system's functionalities from the user’s perspective.
4. **Identify the Relationships**: Determine how actors and use cases interact and how use cases relate to each other.

---

## Example Exercise

Imagine you're modeling a system for managing a clinic:
- **Actors**: Patient, Doctor, Secretary, Admin.
- **Use Cases**: Book Appointment, Confirm Appointment, Update Medical Record, Check Schedule.

Now, use a Use Case Diagram to represent these interactions and relationships. Consider using **generalization** (e.g., the doctor could be a specialized version of the admin) and **include/extend** relationships to show how functions are shared or optionally triggered.

---

## Conclusion

A Use Case Diagram is a powerful tool in system design. It helps you:
- **Visualize the system’s functionality** from an external perspective.
- **Identify key interactions** between the system and its users.
- **Define system boundaries** by showing what is included and excluded.

By clearly representing how users will interact with the system, Use Case Diagrams are invaluable in planning, designing, and communicating system requirements.

[[Chapitre 3 -Practice]]

---
## 🔗 Navigation
- **Module:** [[GL|◀ GL]]
- **Semester:** [[NTIC L2|◀ NTIC L2]]
- **Academic Home:** [[README|🏠 Home]]

# Exercice 1: True/False Statements on Use Case Diagrams

1. **L’acteur 1 est responsable (peut déclencher) des cas : Cas 1, Cas 6**  
   **Answer**: True or False  
   **Explanation**: Check if **Actor 1** is responsible for triggering **Cas 1** and **Cas 6** in the diagram. If **Actor 1** can indeed trigger these use cases, the statement is true. Otherwise, it's false.

2. **L’acteur 1 peut être substitué par l’acteur 2**  
   **Answer**: True or False  
   **Explanation**: This checks for a **generalization relationship** between **Actor 1** and **Actor 2**. If **Actor 2** can completely replace **Actor 1**, meaning all actions of **Actor 1** are accessible by **Actor 2**, then the statement is true. Otherwise, it is false.

3. **L’acteur 2 est responsable des cas : Cas 1, Cas 6**  
   **Answer**: True or False  
   **Explanation**: Check if **Actor 2** is responsible for **Cas 1** and **Cas 6**. If **Actor 2** is indeed responsible for these cases, the statement is true. If not, it is false.

4. **Cas 1 peut être effectué sans Cas 3**  
   **Answer**: True or False  
   **Explanation**: This statement checks if **Cas 1** can be performed without the need for **Cas 3**. If **Cas 1** does not depend on **Cas 3** (i.e., they are independent), then the statement is true. Otherwise, if **Cas 3** is required to complete **Cas 1**, then the statement is false.

5. **Cas 2 est obligatoire pour Cas 1**  
   **Answer**: True or False  
   **Explanation**: This checks if **Cas 2** is a prerequisite for **Cas 1**. If **Cas 1** cannot be executed without **Cas 2**, the statement is true. If **Cas 2** is optional, the statement is false.

6. **La réalisation de Cas 3 consiste à exécuter Cas 4 et Cas 5**  
   **Answer**: True or False  
   **Explanation**: This checks if **Cas 3** includes or depends on **Cas 4** and **Cas 5** (i.e., **Cas 4** and **Cas 5** are sub-functions of **Cas 3**). If **Cas 3** involves the execution of both **Cas 4** and **Cas 5**, the statement is true. If not, the statement is false.

7. **L’acteur 3 doit intervenir dans la réalisation de Cas 3**  
   **Answer**: True or False  
   **Explanation**: This asks if **Actor 3** is required to execute **Cas 3**. If **Actor 3** is involved in the completion of **Cas 3**, the statement is true. If **Actor 3** is not needed, then the statement is false.

8. **L’acteur 2 est responsable de tous les cas primaires**  
   **Answer**: True or False  
   **Explanation**: If **Actor 2** is responsible for all the primary use cases (those that directly provide value to the system’s users), the statement is true. If **Actor 2** handles only some of the primary use cases, the statement is false.

---

# Exercice 2: Use Case Diagram for an ATM System

In this exercise, the goal is to model an **ATM System** that allows users to choose between withdrawing money and checking their account balance. The user must authenticate before performing either operation.

### **Actors**:
- **Client**: The user interacting with the ATM.
- **ATM System**: The machine that executes the actions.

### **Use Cases**:
- **Authenticate User**: The user must authenticate before proceeding with any operation.
- **Withdraw Money**: A client can withdraw money.
- **Check Account Balance**: A client can check their account balance.
- **Print Receipt**: Optionally, the client can request a receipt for the transaction.

### **Relationships**:
- **Client → Authenticate User**: The client must authenticate before any transaction.
- **Client → Withdraw Money**
- **Client → Check Account Balance**
- **Client → Print Receipt**: Optional for both "Withdraw Money" and "Check Account Balance."

### **Diagramming Notes**:
- Use an **include relationship** between "Authenticate User" and the other use cases, as authentication is required for both actions.
- Each use case ("Withdraw Money," "Check Account Balance") will include "Print Receipt" as an optional feature.

---

# Exercice 3: Travel Agency Use Case Diagram

### **Actors**:
- **Travel Agent**: Manages the travel arrangements.
- **Client**: The customer booking the travel.

### **Use Cases**:
- **Organize Trip**: The travel agent organizes the full trip, including transport and accommodation.
- **Book Train Ticket**: The agent books a train ticket for the trip.
- **Book Hotel Room**: The agent books a hotel room.
- **Book Taxi**: The agent arranges a taxi for the client upon arrival.
- **Generate Invoice**: The agent generates a detailed invoice for the client.

### **Relationships**:
1. **Organize Trip → Book Train Ticket**  
2. **Organize Trip → Book Hotel Room**  
3. **Organize Trip → Book Taxi**  
4. **Generate Invoice**: This use case is related to all other use cases, as it summarizes the whole trip.

### **Extension**:
- If the trip can also be made by plane, use an **extend relationship** to show that **Book Taxi** is only applicable if the trip is by train.

---

# Exercice 4: School Room and Equipment Reservation System

### **Actors**:
- **Teacher**: Responsible for making reservations.
- **Student**: Can view the room schedule.
- **Responsible Teacher**: Manages the schedule for the whole course.

### **Use Cases**:
- **Reserve Room**: Teachers can reserve rooms.
- **Reserve Equipment**: Teachers can reserve equipment like laptops or projectors.
- **View Room Schedule**: Both teachers and students can view the room schedule.
- **View Timetable**: Only teachers can view their individual timetables.
- **Edit Timetable**: Only the responsible teacher can edit the course-wide timetable.

---

This breakdown should now be formatted properly for pasting into Obsidian. Each exercise is divided clearly, and each answer is followed by an explanation, ready for your use.

Let me know if you need further assistance!

---
## 🔗 Navigation
- **Module:** [[GL|◀ GL]]
- **Semester:** [[NTIC L2|◀ NTIC L2]]
- **Academic Home:** [[README|🏠 Home]]

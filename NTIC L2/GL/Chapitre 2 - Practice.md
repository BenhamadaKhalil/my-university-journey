# Software Quality Factors

### 1. **Validity (Validité)**

- **English**: Validity refers to the software's ability to meet the functional requirements and perform the tasks it is intended to do, according to the needs of the user, under specified conditions.
- **Arabic**: **الصلاحية** تعني قدرة البرمجيات على تلبية المتطلبات الوظيفية وأداء المهام التي من المفترض أن تؤديها، وفقًا لاحتياجات المستخدم، تحت الظروف المحددة.

---

### 2. **Reliability (Fiabilité)**

- **English**: Reliability measures how consistently the software performs its required functions over time without failure. It reflects the system’s ability to function continuously as expected.
- **Arabic**: **الاعتمادية** تقيس مدى أداء البرمجيات لوظائفها المطلوبة باستمرار دون فشل. وهي تعكس قدرة النظام على العمل بشكل مستمر كما هو متوقع.

---

### 3. **Robustness (Robustesse)**

- **English**: Robustness refers to the software's ability to handle unexpected or abnormal conditions without crashing or producing incorrect results.
- **Arabic**: **الصلابة** تشير إلى قدرة البرمجيات على التعامل مع الحالات غير المتوقعة أو الشاذة دون التوقف أو إنتاج نتائج غير صحيحة.

---

### 4. **Extensibility (Extensibilité)**

- **English**: Extensibility is the software's ability to be easily modified to accommodate new requirements or functionalities without disrupting existing features.
- **Arabic**: **القابلية للتوسع** هي قدرة البرمجيات على التعديل بسهولة لتلبية المتطلبات أو الوظائف الجديدة دون التأثير على الميزات الحالية.

---

### 5. **Reusability (Réutilisabilité)**

- **English**: Reusability refers to the ability of the software or its components (modules, code, etc.) to be reused in different systems or for different purposes.
- **Arabic**: **إعادة الاستخدام** تعني قدرة البرمجيات أو مكوناتها (مثل الوحدات أو الأكواد) على إعادة استخدامها في أنظمة مختلفة أو لأغراض مختلفة.

---

### 6. **Compatibility (Compatibilité)**

- **English**: Compatibility measures how well the software can interact or work with other software or hardware. It’s essential for systems that must operate alongside other platforms.
- **Arabic**: **التوافق** يقيس مدى قدرة البرمجيات على التفاعل أو العمل مع برامج أو أجهزة أخرى. وهو أمر ضروري للأنظمة التي يجب أن تعمل جنبًا إلى جنب مع منصات أخرى.

---

### 7. **Efficiency (Efficacité)**

- **English**: Efficiency refers to the software’s ability to use system resources (such as CPU, memory, and storage) in an optimal way, without waste or unnecessary consumption.
- **Arabic**: **الكفاءة** تشير إلى قدرة البرمجيات على استخدام موارد النظام (مثل وحدة المعالجة المركزية، الذاكرة، والتخزين) بشكل مثالي، دون إهدار أو استهلاك غير ضروري.

---

### 8. **Portability (Portabilité)**

- **English**: Portability is the ease with which software can be transferred and run on different environments, such as various hardware or operating systems.
- **Arabic**: **قابلية النقل** هي سهولة نقل البرمجيات وتشغيلها في بيئات مختلفة، مثل الأجهزة أو أنظمة التشغيل المتنوعة.

---

### 9. **Integrity (Intégrité)**

- **English**: Integrity refers to the ability of the software to protect its data and code from unauthorized access or corruption, ensuring that the system is secure.
- **Arabic**: **النزاهة** تشير إلى قدرة البرمجيات على حماية بياناتها وشفراتها من الوصول غير المصرح به أو التلاعب، مما يضمن أن النظام آمن.

---

### 10. **Usability (Utilisabilité)**

- **English**: Usability measures how easy and intuitive it is for users to learn, use, and navigate the software. It includes how users interact with the system and how errors are handled.
- **Arabic**: **قابلية الاستخدام** تقيس مدى سهولة وتعليم المستخدمين واستخدامهم والتفاعل مع البرمجيات. وتشمل كيفية تفاعل المستخدمين مع النظام وكيفية التعامل مع الأخطاء.

---

## Summary for Understanding and Answering

- When answering questions about which quality factors are most important for different types of software (like **online banking**, **e-commerce**, etc.), think about **how the software will be used**:
  - **Online banking**: Security (integrity), reliability, and usability are critical because users want to access their accounts safely and easily.
  - **E-commerce**: Usability and reliability are key because users need to navigate the website easily and dependably to make purchases.
  - **Air Traffic Control**: Reliability and robustness are the highest priority since system failure can lead to disastrous consequences.
  - **ATMs**: Usability (easy to use) and security (protecting financial transactions) are most important for an ATM to function effectively in all situations.

### **Final Tips**:
- **Reliability** is always important for systems that need to be **available 24/7** (like online banking and air traffic control).
- **Usability** is a priority for user-facing systems like **e-commerce sites** and **ATMs** where user interaction is high.
- **Robustness** is vital in **critical systems** like **air traffic control** that must continue working under extreme conditions.

----------------------------------------------------------------------
# Functional vs Non-Functional Requirements

### 1. What Are Functional and Non-Functional Requirements?

#### **Functional Requirements**:
- **Definition**: Functional requirements describe **what the system should do**. They specify the **functions** or **services** the system must provide.
- **Example**: "The system must allow users to log in" is a functional requirement because it defines a specific action the system must perform.

#### **Non-Functional Requirements**:
- **Definition**: Non-functional requirements describe **how the system should perform**. They focus on the system's **qualities** or **attributes** (e.g., performance, usability, security).
- **Example**: "The system must be able to handle 1000 users at once" is a non-functional requirement because it focuses on the system's performance or capacity, not a specific function.

---

### 2. How to Identify Functional and Non-Functional Requirements?

To identify functional and non-functional requirements, analyze each statement and determine if it’s describing **what the system should do** (functional) or **how the system should perform** (non-functional).

---

### 3. Exercice 2: Identifying Requirements

#### **a. "The Ticket Dispenser should allow travelers to buy weekly coupons."**
- **Type**: **Functional Requirement**
- **Explanation**: This is describing a **specific function** of the system. It tells us what the system must do: allow travelers to buy weekly coupons. This is a **core functionality** of the system.

#### **b. "The code of the Ticket Dispenser must be written in Java."**
- **Type**: **Non-Functional Requirement**
- **Explanation**: This is specifying the **technology** used to develop the system, which doesn't describe what the system does. It’s a **constraint** on how the system should be developed, which makes it non-functional.

#### **c. "The Ticket Dispenser must be easy to use."**
- **Type**: **Non-Functional Requirement**
- **Explanation**: This refers to the **usability** of the system. It doesn’t define a specific function (like buying tickets) but describes how easy the system should be for users to operate, which is a **quality attribute** of the system.

#### **d. "The Ticket Dispenser must always be available."**
- **Type**: **Non-Functional Requirement**
- **Explanation**: This refers to the **availability** of the system, which is a performance characteristic. It doesn’t describe what the system will do, but rather how well it should perform. This requirement focuses on the **uptime** and reliability of the system.

#### **e. "The Ticket Dispenser must provide a contact number to call in case of failure."**
- **Type**: **Non-Functional Requirement**
- **Explanation**: This is specifying a **support feature**. While it's important for user experience, it doesn’t describe a function that the system should perform directly. It describes the **system's support** and how it should handle issues, which is a **non-functional aspect**.

---

### 4. How to Differentiate Between the Two Types of Requirements?

Here’s a simple rule of thumb to help you:

- **Functional Requirements** answer **"What does the system do?"**
  - Example: "The system should allow users to register."
  
- **Non-Functional Requirements** answer **"How well does the system do it?"**
  - Example: "The system should load within 2 seconds."

---

### 5. Additional Notes on Functional and Non-Functional Requirements

- **Functional Requirements** are directly linked to the **core functionalities** of the system.
  - **Example**: For an **ATM**, a functional requirement might be: "The ATM must allow users to withdraw cash."
  
- **Non-Functional Requirements** focus on the **quality**, **performance**, or **constraints** within which the system should operate.
  - **Example**: For an **ATM**, a non-functional requirement might be: "The ATM must ensure secure transactions by encrypting user data."

---

### Lesson Summary:

- **Functional Requirements**: Define what the system should do (specific tasks or actions).
- **Non-Functional Requirements**: Define how the system should perform or behave in certain conditions (attributes like usability, performance, and security).

---

### Steps to Follow:

1. **Identify**: Read each statement carefully.
2. **Determine**: Decide if the statement is describing a specific **function** (functional) or a **quality/attribute/performance** (non-functional).
3. **Categorize**: Use the definitions and examples to classify the requirement correctly.

---
------------------------------------------------------------------
#  System Design for a Polyclinic Management System

### 1. Analyzing the Requirements

Before jumping into the answers, let's review the key details in the exercise:

- **A polyclinic owner** wants to develop an application for managing internal tasks.
- The system must have roles for **doctors**, **secretaries**, **chiefs**, and **patients**, each with specific responsibilities.

#### **Key Requirements**:
- **Doctors** manage **patient records**, **prescriptions**, and **consultations**.
- **Chief (Administrator)** manages **doctors**, **nurses**, and **secretaries**.
- **Secretaries** manage **appointments** for patients.
- **Patients** need to **physically** go to the clinic to book appointments (in the initial scenario).

---

### 2. How to Answer Exercice 3

#### **Step 1: Identify Participants (Client and Users)**

- **Client**: 
  - The **polyclinic owner** is the client who requested the system.
  
- **Users**:
  - **Doctors**: Responsible for managing patient records, prescriptions, and consultations.
  - **Chief (Administrator)**: Manages the doctors, nurses, and secretaries and oversees the entire operation.
  - **Secretaries**: Manage patient appointments, ensuring that patients are scheduled for consultations with doctors.
  - **Patients**: They come to the polyclinic to book appointments and receive consultations.

#### **Step 2: Identify Functional Requirements**

Functional requirements describe **what** the system must do. These describe specific actions and functionalities that the system should provide.

- **Doctors**:
  - The system must allow doctors to manage patient records (view, add, edit patient information).
  - Doctors should be able to create and manage prescriptions for patients.
  - Doctors should track and manage consultations with patients (e.g., scheduling, documenting visit details).

- **Chief (Administrator)**:
  - The system must allow the chief to **manage staff** (doctors, nurses, secretaries).
  - The chief should be able to **view reports** on staff performance or patient visits.
  - The chief can **approve** or **assign tasks** to staff.

- **Secretaries**:
  - Secretaries should be able to **schedule appointments** for patients, checking the availability of doctors.
  - The system must allow secretaries to **update** appointments in case of cancellations or changes.
  - Secretaries may also need to send **reminders** to patients about upcoming appointments.

- **Patients**:
  - Patients should be able to **book appointments** for consultations.
  - The system must allow **patient registration** (e.g., collecting basic information about the patient).

#### **Step 3: Consider New Features for Online Appointment System**

If the clinic wants to introduce **online appointments** (as suggested), there will be:
1. **New Users**:
   - **Online Patients**: Patients who will be able to book appointments through a website or mobile app.
   
2. **New Functional Requirements**:
   - **Online Appointment Booking**: The system should allow patients to **book appointments online** through a web interface or mobile app.
   - **Patient Authentication**: Patients will need to create an **account** or log in to book appointments.
   - **Automated Notifications**: The system should send **notifications (SMS, email, etc.)** to patients when their appointments are booked, canceled, or changed.
   - **Availability Checks**: The system must show **doctor availability** in real-time, allowing patients to select an available time slot.

---

### 3. Key Concepts for System Design

In system design, we focus on identifying the **users** and their **needs** (functional requirements). We also take into account how the system will **scale** if new features are added (like online appointment booking).

---

### Lesson Summary

**Functional Requirements** describe **what** the system needs to do. For example, a doctor needs the ability to view patient records and add prescriptions. Non-functional requirements (which are not covered here but are important to know) focus on **how** well the system should perform (such as being secure, fast, and scalable).

#### **Steps to Follow for Exercice 3**:
1. **Identify the Participants**: Determine the **client** (polyclinic owner) and **users** (doctors, chief, secretaries, and patients).
2. **Identify Functional Requirements**: List all the actions each participant (user) needs to be able to perform, such as booking appointments or managing patient records.
3. **Consider New Features**: If adding new functionality, like online appointments, consider new users (e.g., online patients) and new system features (e.g., automated notifications, real-time availability checks).

---

### **Example Answer for Exercice 3**

#### **1. Participants**:
- **Client**: Polyclinic owner.
- **Users**:
  - **Doctors**: Manage patient records, prescriptions, consultations.
  - **Chief**: Manages staff (doctors, nurses, secretaries).
  - **Secretaries**: Schedule and manage appointments.
  - **Patients**: Book appointments.

#### **2. Functional Requirements**:
- **Doctors**: Manage patient records, prescriptions, and consultations.
- **Chief**: Manage staff, view reports, approve tasks.
- **Secretaries**: Schedule, update, and manage patient appointments.
- **Patients**: Book appointments.

#### **3. Online Appointment System**:
- **New Users**: Online patients.
- **New Requirements**: Online booking, patient authentication, notifications, availability checks.

---

### Conclusion:

By following these steps, you can systematically break down the exercise and design a solution for the polyclinic management system. This process helps you identify what needs to be done (functional requirements) and plan for any new features (like online appointments).

Let me know if you'd like further clarification or more examples!

---
## 🔗 Navigation
- **Module:** [[GL|◀ GL]]
- **Semester:** [[NTIC L2|◀ NTIC L2]]
- **Academic Home:** [[README|🏠 Home]]

# ⚛️ **Atomic Variables – Résumé**

Les **variables atomiques** (ex. `AtomicInteger`, `AtomicLong`, `AtomicBoolean`) permettent d’effectuer des opérations **thread-safe** (sans conflit entre threads) **sans utiliser** de blocs `synchronized` ou de verrous (`Lock`).  
Elles se trouvent dans le package :

```java
import java.util.concurrent.atomic.*;
```

---

### 1️⃣ **Méthodes principales :**

|Méthode|Description|Exemple|
|---|---|---|
|`get()`|Retourne la valeur actuelle.|`int x = count.get();`|
|`set(int newValue)`|Remplace la valeur actuelle par `newValue`.|`count.set(10);`|
|`getAndSet(int newValue)`|Remplace la valeur et renvoie l’ancienne.|`count.getAndSet(5);`|
|`compareAndSet(int expect, int update)`|Change la valeur **seulement si** elle est égale à `expect` (Compare-And-Swap).|`count.compareAndSet(5, 6);`|

---

### 2️⃣ **Méthodes d’incrémentation et décrémentation :**

|Méthode|Effet|Retour|
|---|---|---|
|`incrementAndGet()`|Ajoute **1** → renvoie **la nouvelle valeur**.|`++count` (atomique)|
|`getAndIncrement()`|Ajoute **1** → renvoie **l’ancienne valeur**.|post-incrément atomique|
|`decrementAndGet()`|Soustrait **1** → renvoie **la nouvelle valeur**.|`--count` (atomique)|
|`getAndDecrement()`|Soustrait **1** → renvoie **l’ancienne valeur**.|post-décrément atomique|

📘 **Exemple :**

```java
AtomicInteger stock = new AtomicInteger(5);
stock.incrementAndGet(); // 6
stock.getAndDecrement(); // retourne 6, mais stock = 5
```

---

### 3️⃣ **Méthodes d’ajout :**

|Méthode|Description|Exemple|
|---|---|---|
|`addAndGet(int delta)`|Ajoute `delta` et renvoie **la nouvelle valeur**.|`count.addAndGet(3); // +3`|
|`getAndAdd(int delta)`|Ajoute `delta` et renvoie **l’ancienne valeur**.|`count.getAndAdd(3); // renvoie avant ajout`|

📘 **Exemple :**

```java
AtomicInteger total = new AtomicInteger(10);
System.out.println(total.addAndGet(5)); // affiche 15
System.out.println(total.getAndAdd(2)); // affiche 15, total = 17
```

---

### 🧠 **En résumé :**

|Type d’opération|Méthode|Retour|
|---|---|---|
|Lecture/Écriture|`get()`, `set()`|Valeur actuelle / Nouvelle|
|Incrémentation/Décrémentation|`incrementAndGet()`, `getAndIncrement()`, etc.|Ancienne ou nouvelle valeur|
|Ajout personnalisé|`addAndGet(x)`, `getAndAdd(x)`|Ancienne ou nouvelle valeur|
|Vérification et mise à jour|`compareAndSet(old, new)`|`true` si succès|

---

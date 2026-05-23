# 📘 Chapitre 4 – Transactions & Contrôle de la Concurrence

_(Bases de Données Avancées)_

Source : _Transactions & Contrôle de la Concurrence_, Dr Bouanaka Chafia

---

## 🎯 Objectifs du chapitre

- Comprendre la **notion de transaction**
    
- Comprendre les **problèmes d’accès concurrent**
    
- Étudier les **mécanismes de contrôle de la concurrence**
    
- Maîtriser la **sérialisabilité** et les **verrous**
    
- Comprendre les **niveaux d’isolation SQL**
    

---

## 1️⃣ Notion de Transaction

### 🔹 Définition (cours)

> Une **transaction** est un ensemble séquentiel d’opérations exécutées par un seul utilisateur, qui transforme la base de données d’un **état cohérent** vers un **autre état cohérent**.

- Unité **logique** de travail
    
- Opérations primitives :
    
    - `Read(X)`
        
    - `Write(X)`
        

---

## 2️⃣ Exemple introductif : Transaction bancaire

### 📌 Virement bancaire

- Montant : **10 000 DA**
    
- Compte A (débité)
    
- Compte B (crédité)
    

### Avant transaction

```
A = 100000
B = 75000
```

### Opérations de la transaction T

```text
Read(A.solde)
A.solde = A.solde - 10000
Write(A.solde)

Read(B.solde)
B.solde = B.solde + 10000
Write(B.solde)
```

### Après transaction

```
A = 90000
B = 85000
```

👉 **Les deux opérations doivent réussir ensemble**, sinon être annulées.

---

## 3️⃣ Propriétés ACID des Transactions

### 🔹 A – Atomicité

- Tout ou rien
    
- Une transaction partiellement exécutée est **interdite**
    

📌 Exemple :

- Débit(A) effectué
    
- Crash avant Crédit(B)  
    ❌ BD incohérente → **ROLLBACK**
    

---

### 🔹 C – Cohérence

- Respect des **contraintes d’intégrité**
    
- La BD reste cohérente **après commit**
    

📌 Exemple bancaire :

```
A.solde + B.solde = constante
```

---

### 🔹 I – Isolation

- Une transaction **ne voit pas** les effets des autres transactions concurrentes
    
- Exécution **logiquement séquentielle**
    

---

### 🔹 D – Durabilité

- Après `COMMIT`, les changements sont **permanents**
    
- Même en cas de panne
    

---

## 4️⃣ Primitives d’une Transaction

|Étape|Primitive|
|---|---|
|Début|`BEGIN TRANSACTION`|
|Travail|SQL (SELECT, UPDATE, INSERT…)|
|Validation|`COMMIT`|
|Annulation|`ROLLBACK`|

---

## 5️⃣ États d’une Transaction

- ✅ **Exécution normale** → COMMIT
    
- ❌ **Suicide** → ROLLBACK volontaire
    
- ❌ **Assassinat** → ROLLBACK imposé (deadlock, panne)
    

---

## 6️⃣ Accès Concurrent à une Base de Données

### 🔹 Contexte multi-utilisateurs

- Plusieurs transactions s’exécutent **en même temps**
    
- Le SGBD **entrelace** leurs opérations
    

👉 Sans contrôle → **incohérences**

---

## 7️⃣ Problèmes d’Accès Concurrent (avec exemples)

---

### ❌ 1. Perte de mise à jour (Lost Update)

#### Scénario

- T1 et T2 modifient A simultanément
    

```text
A = 10
T1 lit A
T2 lit A
T1 écrit A = 20
T2 écrit A = 60
```

❌ Mise à jour de T1 perdue

---

### ❌ 2. Lecture impropre (Dirty Read)

- T2 lit une valeur modifiée par T1 **non validée**
    
- T1 fait ROLLBACK
    

📌 Résultat lu = valeur **invalide**

---

### ❌ 3. Lecture non reproductible

- T1 lit A
    
- T2 modifie A et commit
    
- T1 relit A → valeur différente
    

---

### ❌ 4. Objets fantômes

- T1 compte les tuples d’une table
    
- T2 insère un tuple
    
- T1 recompte → résultat différent
    

---

## 8️⃣ Ordonnancement des Transactions

### 🔹 Ordonnancement

> Séquence chronologique des opérations de plusieurs transactions

---

### 🔹 Ordonnancement sériel

- Transactions exécutées **l’une après l’autre**
    
- Toujours cohérent
    

---

### 🔹 Ordonnancement non sériel

- Opérations **entrelacées**
    
- Peut être cohérent ou non
    

---

### 🔹 Ordonnancement sérialisable

> Un ordonnancement est **sérialisable** s’il donne le même résultat qu’un ordonnancement sériel.

---

## 9️⃣ Équivalences & Sérialisabilité

### 🔹 r-équivalence (résultat)

- Même état final de la BD
    

### 🔹 v-équivalence (visibilité)

- Même valeurs lues
    

### 🔹 c-équivalence (conflit) ✅ la plus importante

- Même ordre des **opérations conflictuelles**
    

---

## 🔟 Graphe de Précédence (Test de c-sérialisabilité)

### 🔹 Principe

- Nœuds : transactions
    
- Arc Ti → Tj si conflit où Ti précède Tj
    

### 🔹 Règle

> ✔️ Ordonnancement **c-sérialisable** ⇔ graphe **sans cycle**

❌ Cycle → ordonnancement non sérialisable

---

## 1️⃣1️⃣ Verrous (Locking)

### 🔹 Objectif

- Garantir l’**isolation**
    
- Empêcher les anomalies concurrentes
    

---

### 🔹 Types de verrous

|Verrou|Symbole|Autorise|
|---|---|---|
|Partagé|S|Lecture|
|Exclusif|X|Lecture + Écriture|

---

### 🔹 Règles de compatibilité

|Verrou détenu|S demandé|X demandé|
|---|---|---|
|S|✅|❌|
|X|❌|❌|

---

## 1️⃣2️⃣ Algorithme de Verrouillage (2PL)

### Phase 1 – Verrouillage

- Acquisition des verrous (S / X)
    

### Phase 2 – Libération

- Libération des verrous après COMMIT / ROLLBACK
    

📌 Garantit la **c-sérialisabilité**

---

## 1️⃣3️⃣ Interblocage (Deadlock)

### 🔹 Exemple

- T1 attend un verrou détenu par T2
    
- T2 attend un verrou détenu par T1
    

❌ Attente circulaire

---

### 🔹 Solutions

- Timeout
    
- Graphe d’attente (détection de cycle)
    
- Annulation d’une transaction
    

---

## 1️⃣4️⃣ Niveaux d’Isolation SQL

|Niveau|Dirty Read|Non Reproductible|Fantômes|
|---|---|---|---|
|READ UNCOMMITTED|✅|✅|✅|
|READ COMMITTED|❌|✅|✅|
|REPEATABLE READ|❌|❌|✅|
|SERIALIZABLE|❌|❌|❌|

---

### 🔹 Choix du niveau

- **READ COMMITTED** → Oracle (par défaut)
    
- **REPEATABLE READ** → MySQL (par défaut)
    
- **SERIALIZABLE** → sécurité maximale, performances faibles
    

---

## 🧠 Résumé à mémoriser (examen)

> Une transaction est une unité logique atomique respectant ACID.  
> Les accès concurrents provoquent des anomalies corrigées par la sérialisabilité, les verrous et les niveaux d’isolation.

---

---
## 🔗 Navigation
- **Module:** [[NTIC L3/TABD/TABD|◀ TABD]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]

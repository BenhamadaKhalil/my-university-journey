Here is a **clean, structured, emoji-enhanced summary** of the TD1 lesson, ready to paste into **Obsidian**.

---

# 🧪 **Test et Qualité du Logiciel – TD1 Résumé**

### 🎓 _Construction du Graphe de Flot de Contrôle (GFC)_

📚 **Dr. DJENOUHAT Manel Amel – Université Constantine 2**

---

## 📌 1. Notion de Test Boîte Blanche

Le test structurel consiste à :

- 🔍 Inspecter le **code source**
    
- 🔁 Identifier les **chemins d’exécution** possibles
    
- 🎯 Choisir les **valeurs d’entrée** qui forcent ces chemins
    

---

## 📥 2. Entrées d’un Programme

Les _entrées_ sont les variables nécessaires à l’exécution.

### ✏️ Déclaration

```c
int a;
```

### 🟡 Initialisation

```c
int a = 2;
```

### 🔄 Affectation

```c
a = 2;
```

---

## 🔢 3. Incrémentation

- `i++` : post-incrémentation
    
- `++i` : pré-incrémentation
    

---

## 🧩 4. Graphe de Flot de Contrôle (GFC)

Un **GFC réductible** regroupe plusieurs instructions séquentielles en un seul bloc si elles s’exécutent sans interruption.

### 🟦 Types d’instructions représentés comme sommets

|Instruction|Sommet ?|
|---|---|
|Déclaration, affectation|✔️|
|Lecture, écriture|✔️|
|Début, fin|✔️|
|return|✔️|
|Case (dans switch)|❌|
|If, then, else|✔️ (sauf else seul)|
|For|✔️ (init, test, incrément)|
|While, Do-while|✔️|

---

## 🧱 5. Règles de Construction du GFC

### 🔹 **5.1 Séquence**

Instructions qui se suivent → un arc simple

```
1 → 2 → 3
```

---

### 🔹 **5.2 Conditionnelle (if puis actions)**

```
     (cond)
      / \
    oui non
     |    |
   Bloc   Suite
```

---

### 🔹 **5.3 Alternative (if–else)**

```
      (cond)
     /      \
  BlocA    BlocB
     \      /
       Suite
```

---

### 🔹 **5.4 Boucle While**

```
      (test)
       /  \
    oui   non
     |      |
   Bloc    Suite
     |
   retour
```

---

### 🔹 **5.5 Boucle Do-While**

```
  Bloc
    |
 (test)
   / \
 oui  non
  |     |
retour Suite
```

---

### 🔹 **5.6 Boucle For**

Transformée en while :  
1️⃣ initialisation  
2️⃣ test  
3️⃣ boucle  
4️⃣ incrémentation  
5️⃣ suite

---

### 🔹 **5.7 Switch avec break**

- Le `switch` évalue l’expression
    
- Le code saute au `case` correspondant
    
- Il continue jusqu’au `break`
    
- Si aucun `case` ne correspond → `default`
    

---

## 🧭 6. Étapes pour Résoudre un Exercice GFC

1. 📝 Identifier les **entrées** du programme
    
2. 🧠 Comprendre la **sémantique** du code
    
3. 🔢 **Numéroter** les instructions (réduire les blocs si nécessaire)
    
4. 🔗 Construire le **GFC** : sommets + arcs
    

---

If you want, I can also create:  
✨ un modèle Obsidian (template)  
🎨 un schéma GFC en ASCII ou image  
📄 un PDF propre pour impression

---
## 🔗 Navigation
- **Module:** [[NTIC L3/TQL/TQL|◀ TQL]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]

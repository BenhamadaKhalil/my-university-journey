# 📘 Diagramme d’États–Transitions

## 🔹 Événement interne de l’état (UML)

---

## 1️⃣ Introduction

Dans un **diagramme d’états-transitions UML**, un objet peut réagir à des événements de **deux façons** :

- En **changeant d’état** → transition
    
- En **restant dans le même état** → **événement interne**
    

📌 L’événement interne permet de **modéliser le comportement interne d’un état**, sans complexifier le diagramme avec des transitions inutiles.

---

## 2️⃣ Rappel : état et transition

### 🔹 État

Un **état** représente une situation durant la vie d’un objet pendant laquelle :

- il exécute une **activité**, ou
    
- il attend un **événement**
    

### 🔹 Transition

Une **transition** provoque un **changement d’état** suite à un événement.

```
État source ── événement / action ──▶ État cible
```

---

## 3️⃣ Définition de l’événement interne

### 📌 Définition

Un **événement interne** est un événement :

- traité **à l’intérieur d’un état**
    
- qui **ne provoque aucun changement d’état**
    
- mais qui déclenche une **action**
    

👉 L’objet **reste dans le même état**.

---

## 4️⃣ Différence : événement interne vs transition

|Critère|Événement interne|Transition|
|---|---|---|
|Change d’état|❌ Non|✅ Oui|
|Représentation|Dans l’état|Sur la flèche|
|Effet|Action locale|Passage à un autre état|
|Usage|Comportement interne|Changement de phase|

📌 **Règle clé (examen)**

> Si l’état ne change pas → événement interne

---

## 5️⃣ Types d’événements internes d’un état

Un événement interne est défini **dans le rectangle de l’état**, selon UML.

---

### 5.1 `entry` – Action d’entrée

#### 📌 Définition

Action exécutée **automatiquement à chaque entrée dans l’état**.

#### ✍ Exemple

```
État : Connecté
entry / afficherMenu()
```

👉 À chaque fois que l’objet entre dans `Connecté`, le menu est affiché.

---

### 5.2 `do` – Activité de l’état

#### 📌 Définition

Activité exécutée **tant que l’objet reste dans l’état**.

#### ✍ Exemple

```
État : Téléchargement
do / téléchargerFichier()
```

👉 L’activité s’exécute pendant toute la durée de l’état.

---

### 5.3 `exit` – Action de sortie

#### 📌 Définition

Action exécutée **juste avant de quitter l’état**, quelle que soit la transition.

#### ✍ Exemple

```
État : Paiement
exit / sauvegarderTransaction()
```

👉 L’action s’exécute avant tout changement d’état.

---

### 5.4 Événement interne explicite

#### 📌 Définition

Événement nommé qui déclenche une action **sans quitter l’état**.

#### ✍ Exemple

```
État : EnAttente
refresh / actualiserAffichage()
```

👉 L’événement `refresh` est traité, mais l’état reste `EnAttente`.

---

## 6️⃣ Exemple complet : Lecteur multimédia

### 🎵 État : Lecture

```
entry / afficherLecture()
do / lireMusique()
pause / diminuerVolume()
exit / sauvegarderPosition()
```

- `pause` est un **événement interne**
    
- L’état **ne change pas**
    
- Une action est exécutée
    

---

## 7️⃣ Exemple : Ascenseur

### 🚀 État : EnMarche

```
do / monter()
capteurObstacle / alerter()
```

👉 Le capteur se déclenche :

- l’ascenseur **reste en marche**
    
- une action est exécutée
    

---

## 8️⃣ Pourquoi utiliser des événements internes ?

- Réduire le nombre de transitions
    
- Simplifier le diagramme
    
- Clarifier le comportement interne
    
- Améliorer la lisibilité
    
- Respecter la sémantique UML
    

---

## 9️⃣ Bonnes pratiques (⭐ examen)

- Utiliser un événement interne si l’état **ne change pas**
    
- Utiliser `entry`, `do`, `exit` pour structurer le comportement
    
- Ne pas créer de transition inutile
    
- Réserver les transitions aux **changements d’état réels**
    

---

## 🔟 Erreurs fréquentes

❌ Utiliser une transition alors que l’état reste le même  
❌ Confondre événement interne et garde  
❌ Mettre une action sur une transition au lieu de `entry`  
❌ Multiplier les états inutilement

---

## ✅ Résumé synthèse (Obsidian)

- Événement interne = action **sans changement d’état**
    
- Défini **dans l’état**
    
- Types : `entry`, `do`, `exit`, `event`
    
- Simplifie les diagrammes
    
- Très important pour la modélisation UML
    

---

## 🧠 Phrase parfaite pour l’examen

> _Un événement interne est un événement traité à l’intérieur d’un état, déclenchant une action sans provoquer de transition vers un autre état._

---

If you want next:

- 📐 **Schéma UML annoté**
    
- 🧠 **QCM corrigés**
    
- ✍ **Exercice type examen**
    
- 📄 **Fiche ultra-résumé 1 page**
    

Just tell me 👌

---
## 🔗 Navigation
- **Module:** [[NTIC L3/GL2/GL2|◀ GL2]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]

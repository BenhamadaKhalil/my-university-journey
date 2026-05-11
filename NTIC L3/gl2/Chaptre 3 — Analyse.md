# 📘 Chapitre 3 — **Analyse (Unified Process)**

_(Lesson Summary – Obsidian Friendly)_

---

## 🎯 Objectif de l’analyse

L’analyse intervient **après la spécification des besoins** et pendant la **phase d’élaboration** du processus UP.

👉 Son but est de **transformer les besoins (cas d’utilisation)** en une **description orientée objet claire**, qui servira de base à la conception.

### L’analyse permet de :

- Identifier les **objets du domaine**
    
- Définir leurs **responsabilités**
    
- Décrire leurs **interactions**
    
- Préparer la **conception logicielle**
    

---

## 1️⃣ Position de l’analyse dans UP

```
Besoins → Cas d’utilisation → Analyse → Conception → Implémentation
```

📌 L’analyse **ne fait pas encore du code**, mais elle structure le futur système.

---

## 2️⃣ Le modèle d’analyse (vue globale)

Le **modèle d’analyse** est composé de **3 sous-modèles** :

### 1. Modèle fonctionnel

- Cas d’utilisation
    
- Scénarios
    
- Maquettes IHM (interfaces provisoires)
    

### 2. Modèle d’analyse objet

- Diagrammes de classes
    
- Classes du domaine
    
- Classes d’analyse
    

### 3. Modèle dynamique

- Diagrammes de séquence détaillés
    
- Diagrammes d’activités
    
- Diagrammes d’états / transitions
    

👉 Ces trois modèles travaillent **ensemble**.

---

## 3️⃣ Modèle d’analyse objet

---

### 3.1 Diagramme de classes (fondamental)

📌 Un **diagramme de classes** décrit la **structure statique** du système :

- Classes
    
- Attributs
    
- Méthodes
    
- Relations (association, héritage, composition…)
    

🎯 Rôle :

- Représenter les **concepts principaux**
    
- Servir de base à la **conception**
    

---

### 3.2 Classes de domaine

📌 Les **classes de domaine** représentent les **concepts métier réels**, indépendants de toute technologie.

👉 Elles décrivent **le vocabulaire du domaine**, pas le logiciel.

#### Exemples :

- Patient
    
- OffreEmploi
    
- Candidature
    
- Employeur
    
- Étudiant
    
- Facture
    

### Comment les identifier ?

✔ Analyse du texte métier

- **Noms** → classes ou attributs
    
- **Verbes** → relations
    

⚠️ Limites :

- Synonymes
    
- Ambiguïtés
    
- Concepts cachés
    

---

### ✍ Exemple (recrutement en ligne)

Texte :

> Le candidat soumet une candidature à une offre d’emploi.

- **Candidat** → classe
    
- **OffreEmploi** → classe
    
- **Candidature** → classe
    
- **Soumettre** → relation
    

---

## 4️⃣ Classes d’analyse (transition vers la solution)

Les **classes d’analyse** affinent les classes de domaine pour préparer la solution logicielle.

📌 Elles restent **indépendantes de la technologie**, mais structurent le système.

---

## 5️⃣ MVC comme cadre d’analyse

L’analyse utilise très souvent le **modèle MVC**.

### 🔷 MVC = Model – View – Controller

#### 🟦 Modèle

- Données
    
- Accès à la base de données
    
- Logique métier
    

#### 🟩 Vue

- Interface utilisateur
    
- Formulaires, pages, écrans
    

#### 🟥 Contrôleur

- Logique de décision
    
- Coordination entre Vue et Modèle
    

🎯 Objectif :  
👉 Séparer **données / interface / logique**

---

## 6️⃣ Diagramme de classes participantes (Jacobson ⭐⭐⭐)

Ces diagrammes font le **lien entre :**

- Cas d’utilisation
    
- Maquettes IHM
    
- Classes métier
    

### Trois types de classes :

#### 1️⃣ Classes Dialogue (Boundary)

- Interaction avec l’utilisateur
    
- Pages, formulaires, écrans
    
- Durée de vie courte (cas d’utilisation)
    

📌 Exemple :

- FormulairePostuler
    
- PageConnexion
    

---

#### 2️⃣ Classes Contrôle

- Logique du cas d’utilisation
    
- Coordonnent les actions
    

📌 Exemple :

- ControlePostulation
    
- ControleAuthentification
    

---

#### 3️⃣ Classes Entité

- Données persistantes
    
- Concepts métier
    

📌 Exemple :

- Candidat
    
- OffreEmploi
    
- Candidature
    

---

## 7️⃣ Modèle d’analyse dynamique

---

### 7.1 Diagramme de séquence détaillé

📌 Il **raffine** le diagramme de séquence système.

|Avant|Après|
|---|---|
|Système = boîte noire|Système = objets collaborants|

🎯 Objectifs :

- Attribuer les responsabilités
    
- Définir les messages
    
- Préciser les opérations
    

---

### Règles MVC (⚠️ examen)

- Acteur → Dialogue
    
- Dialogue → Contrôle
    
- Contrôle → Entité / Dialogue / Contrôle
    
- Entité → Entité uniquement
    

---

### ✍ Exemple simple

**Cas : Postuler à une offre**

1. Candidat → PagePostuler (Dialogue)
    
2. PagePostuler → ControlePostuler
    
3. ControlePostuler → Candidature (Entité)
    
4. Contrôle valide et enregistre
    
5. Réponse affichée à l’utilisateur
    

---

## 7.2 Diagramme d’états / transitions

📌 Décrit le **cycle de vie d’un objet**.

### Exemple : Candidature

```
Créée → Soumise → Acceptée / Refusée
```

🎯 Utilisé quand :

- L’objet change d’état
    
- Les règles dépendent de l’état
    

---

## ✅ Résumé ultra-clair (à mémoriser)

- Analyse = entre besoins et conception
    
- 3 modèles : fonctionnel, objet, dynamique
    
- Classes de domaine = concepts métier
    
- Classes d’analyse = solution logique
    
- MVC structure l’analyse
    
- Diagrammes participants = cœur de l’analyse
    
- Séquence détaillée = responsabilités des objets
    
- États = cycle de vie des objets
    

---

If you want next:

- 🧠 **Fiche “Questions d’examen + pièges”**
    
- 🖊 **Cas pratique corrigé (recrutement ou hôpital)**
    
- 📐 **Template Obsidian (classes, séquences, MVC)**
    

Just say the word 👌

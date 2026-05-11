# 📘 GL2 — Chapitre 4 : **Conception**

_(Résumé clair – Obsidian Friendly)_

---

## 1️⃣ Introduction à la conception

La **conception** est l’activité qui transforme le **modèle d’analyse** en une **solution technique concrète**, prête à être implémentée.

📌 Elle constitue le **pont entre l’analyse et l’implémentation**.

---

## 2️⃣ Analyse vs Conception

### 🔹 Analyse

- Se concentre sur le **métier**
    
- Décrit **ce que le système doit faire**
    
- Ignore les contraintes techniques
    
- Sert à clarifier les besoins du client
    

### 🔹 Conception

- Se concentre sur **comment le système sera réalisé**
    
- Prend en compte :
    
    - contraintes techniques
        
    - architecture
        
    - performances
        
    - sécurité
        
    - stockage
        
- Transforme le **modèle d’analyse** en **modèle de conception**
    

📌 **Phrase clé examen**

> L’analyse décrit le _quoi_, la conception décrit le _comment_.

---

## 3️⃣ Activité de conception (vue globale)

L’activité de conception produit le **modèle de conception**, à travers les étapes suivantes :

1. Identification des objectifs de conception
    
2. Raffinement des classes d’analyse
    
3. Décomposition du système
    
4. Spécification des interfaces
    
5. Identification des composants
    
6. Déploiement des composants
    

---

## 4️⃣ Identification des objectifs de conception

### 📌 Définition

Les objectifs de conception sont des **propriétés et critères** que le système doit respecter.

👉 Ils proviennent :

- des **besoins non fonctionnels**
    
- du **domaine d’application**
    
- des exigences du client
    

---

### 🔹 Exemples d’objectifs

- Performance (temps de réponse)
    
- Sécurité (chiffrement des données)
    
- Fiabilité / tolérance aux pannes
    
- Portabilité
    
- Maintenabilité
    
- Coût
    

✍ **Exemple** (système hospitalier) :

- Backup de la base de données
    
- Données patients cryptées
    
- Compatibilité avec différents matériels
    

⚠️ Tous les critères ne peuvent pas être optimisés en même temps → **compromis nécessaires**.

---

## 5️⃣ Raffinement des classes d’analyse

_(Classes de conception)_

### 📌 Définition

Les **classes de conception** sont des classes **suffisamment détaillées** pour être implémentées.

👉 Elles proviennent du **raffinement des classes d’analyse**, guidé par :

- diagrammes de classes participantes
    
- diagrammes de séquence détaillés
    

---

### 🔹 Raffinements effectués

- Ajout des **opérations**
    
- Typage des attributs et paramètres
    
- Définition des relations :
    
    - associations (navigabilité)
        
    - généralisations
        
    - dépendances
        

---

### 🔹 Caractéristiques d’une bonne classe de conception

- **Complétude** : fait tout ce qui est attendu
    
- **Suffisance** : rien de plus que nécessaire
    
- **Primitivité** : pas de redondance
    
- **Haute cohésion**
    
- **Faible couplage**
    

---

## 6️⃣ Décomposition du système

### 📌 Principe

Un système complexe est découpé en **sous-systèmes**.

### 🔹 Sous-système

- Partie cohérente du système
    
- Implémentable par une équipe
    
- Encapsule état et comportement
    

👉 La décomposition :

- découle des **besoins fonctionnels**
    
- regroupe les classes liées à des cas d’utilisation proches
    
- est **itérative** (fusion / division possible)
    

---

## 7️⃣ Spécification des interfaces

### 📌 Rôle

Définir comment les composants **communiquent entre eux**.

### 🔹 Deux types d’interfaces

- **Interface fournie** : service offert par le composant
    
- **Interface requise** : service dont le composant a besoin
    

📌 Les interfaces permettent :

- le remplacement d’un composant
    
- l’évolution indépendante
    

---

## 8️⃣ Diagramme de composants

### 📌 Définition

Le diagramme de composants modélise :

- les **composants logiciels**
    
- leurs **interactions**
    
- leurs **interfaces**
    

### 🔹 Composant

- Unité autonome
    
- Remplaçable
    
- Réutilisable
    
- Boîte noire (contenu caché)
    

### 🔹 Exemples

- JavaBeans
    
- Servlets
    
- Sous-systèmes
    
- Fichiers source
    

### 🔹 Relations

- Réalisation
    
- Dépendance
    

---

## 9️⃣ Diagramme de déploiement

### 📌 Rôle

Le diagramme de déploiement décrit :

- l’**architecture physique**
    
- la répartition des composants sur le matériel
    
- les **communications** entre nœuds
    

---

### 🔹 Éléments principaux

- **Nœud** :
    
    - ressource matérielle
        
    - mémoire, processeur, OS
        
- **Chemin de communication** :
    
    - Ethernet
        
    - USB
        
    - liaison réseau
        

✍ **Exemple**

- Serveur web
    
- Serveur BD
    
- Poste client
    
- Connexions réseau
    

---

## 🔟 Résumé global (révision rapide)

- Conception = transformation analyse → solution technique
    
- Basée sur objectifs non fonctionnels
    
- Raffinement des classes
    
- Décomposition en sous-systèmes
    
- Interfaces = communication & flexibilité
    
- Diagrammes clés :
    
    - classes de conception
        
    - composants
        
    - déploiement
        

---

## 🧠 Phrase parfaite pour l’examen

> _La conception transforme le modèle d’analyse en une solution technique en respectant les contraintes non fonctionnelles et en préparant l’implémentation._

---

# 📝 UP Requirements Engineering – Summary (Obsidian-Friendly)

## 1. Introduction

Many software projects fail due to poor **requirements management**.  
This step is essential because it defines **what the system must do** and ensures it meets **user expectations**.

Key activities:

- Recueillir les besoins (collect requirements)
    
- Analyser faisabilité & importance
    
- Rédiger des documents clairs
    
- Vérifier & valider les besoins
    
- Gérer les changements
    

Main causes of failure:

- Mauvaise identification des besoins
    
- Faible implication des utilisateurs
    
- Besoins ambigus, incomplets ou mal écrits
    
- Changements fréquents et non contrôlés
    
- Manque de validation
    

Importance:

- Crucial during **Inception** & **Elaboration**
    
- Impossible d’avancer sans une vision claire du système
    

---

## 2. Étude de cas — Système de recrutement en ligne

Application visant à aider les jeunes diplômés à trouver un emploi.

### Principales fonctionnalités

#### Employeur :

- Publier une annonce (profil, horaires, salaire, lieu, date d’expiration)
    
- Attendre la validation de l’administrateur
    
- Après expiration : consulter les candidatures et sélectionner les candidats
    

#### Chercheur d’emploi :

- Créer un CV (diplôme, compétences, expérience)
    
- Chercher des offres
    
- Vérifier les conditions
    
- Postuler **si profil compatible**
    
- Consulter les résultats après sélection
    

---

## 3. Étude préliminaire

Première étape du processus UP → créer une vision globale du projet.

### Objectifs :

- Comprendre le **problème** et le **contexte**
    
- Définir une première description globale du système (quoi, pourquoi, combien)
    
- Préparer le cahier des charges préliminaire
    

---

## 3.1 Analyse du domaine

Comprendre en profondeur le domaine du problème.

### Contenu du document d’analyse :

- **Glossaire** (employeur, candidature, validation…)
    
- **Connaissances générales** :
    
    - Algorithmes de matching
        
    - Classement des candidats
        
    - Sécurité des données
        
- **Systèmes existants** :
    
    - Exemples : iSmartRecruit, Nicoka, Monster, ATS
        

### Avantages :

- Améliore communication
    
- Clarifie les besoins
    
- Assure que les solutions répondent au vrai problème
    

---

## 3.2 Définition de la problématique & cadre du projet

### Problématique :

Explique **pourquoi** le projet existe (le besoin à satisfaire).

**Exemple (recrutement en ligne)** :

> Comment gérer efficacement un grand volume de candidatures tout en facilitant la sélection des profils qualifiés ?

### Objectifs (SMART)

#### Pour employeurs :

- Accéder à un vivier large
    
- Réduire coûts/délais grâce à l'automatisation
    
- Gérer le processus à distance (y compris entretien vidéo)
    

#### Pour candidats :

- Postuler facilement, sans déplacement
    
- Accéder à plus d’informations
    
- Avoir un processus rapide et transparent
    

---

## 3.3 Recueil des besoins

Base essentielle du projet → une mauvaise collecte = échec.

### Deux types de besoins :

#### 📌 **Besoins fonctionnels (BF)** → _ce que le système fait_

- Publier/ gérer les offres
    
- Créer/ modifier le CV
    
- Postuler
    
- Consulter offres, candidatures, résultats
    

#### 📌 **Besoins non fonctionnels (BNF)** → _qualités & contraintes_

- Authentification
    
- Sécurité et confidentialité
    
- Performance (rapidité)
    
- Compatibilité multi-appareils
    
- Conformité légale (RGPD)
    
- Interface ergonomique
    

### Sources de besoins :

- Utilisateurs
    
- Parties prenantes
    
- Systèmes externes
    
- Contraintes techniques/juridiques
    
- Matériel
    

### Méthodes de collecte :

- Analyse de documents existants
    
- Entretiens
    
- Questionnaires
    
- Ateliers / brainstorming
    

### Nature évolutive :

- Les besoins **changent** → processus itératif & incrémental
    

---

# ✅ Résumé final

Le succès d’un projet logiciel dépend en grande partie de la **qualité du recueil et de la gestion des besoins**.  
Le processus UP commence par l’étude préliminaire : analyse du domaine, définition de la problématique, objectifs et recueil des besoins fonctionnels & non fonctionnels.  
L’exemple du système de recrutement illustre ces activités.

---
# 📝 UP Requirements Engineering – **Complete Summary (Obsidian-Friendly)**

> **Continuation & completion of your summary**

---

## 4️⃣ Spécification des besoins (Requirements Specification)

After collecting needs, we must **formalize them** so they can be:

- Understood by all stakeholders
    
- Validated by the client
    
- Used as a base for design & development
    

👉 UP uses **UML Use Case Model** for this purpose.

### 🎯 Goals of specification

- Clarify system behavior from **user point of view**
    
- Detect inconsistencies early
    
- Validate requirements with client
    
- Prepare development & iterations
    

---

## 4.1 Identification des acteurs

### 📌 Acteur = rôle externe qui interagit avec le système

⚠️ **Actor ≠ User**

- One user can play **multiple roles**
    
- One actor represents a **type of interaction**
    

### Types d’acteurs

- **Acteurs primaires** → utilisent le système pour atteindre un objectif
    
- **Acteurs secondaires** → support, maintenance, systèmes externes
    

### Questions clés (exam ⭐):

- Qui utilise le système ?
    
- Qui interagit avec le système ?
    
- Qui maintient ou supervise le système ?
    

### Exemple (recrutement en ligne)

- Employeur (principal)
    
- Candidat (principal)
    
- Administrateur (secondaire)
    
- Système de paiement / email (secondaire)
    

---

## 4.2 Identification des cas d’utilisation (Use Cases)

### 📌 Cas d’utilisation = service rendu par le système à un acteur

Il décrit **ce que fait le système**, pas comment.

### Questions à se poser :

- Comment chaque acteur utilise le système ?
    
- Quelles fonctionnalités attend-il ?
    

### Exemple

**Employeur :**

- Publier une offre
    
- Gérer candidatures
    
- Sélectionner candidats
    
- S’authentifier
    

**Candidat :**

- Créer CV
    
- Rechercher offres
    
- Postuler
    
- Consulter résultats
    
- S’authentifier
    

---

## 4.3 Structuration des cas d’utilisation en packages

Quand le diagramme devient trop chargé → **packages**

### 🎯 Objectifs :

- Améliorer lisibilité
    
- Découper le système en sous-systèmes
    
- Faciliter la maintenance
    

### Exemples de packages :

- Gestion des offres
    
- Gestion des candidatures
    
- Authentification
    
- Administration
    

---

## 4.4 Relations entre cas d’utilisation (⚠️ très important en QCM)

### UML définit **3 relations principales**

#### 🔁 « include »

- Comportement **obligatoire**
    
- Évite la redondance  
    👉 ex: _Postuler_ **include** _S’authentifier_
    

#### 🔀 « extend »

- Comportement **optionnel**  
    👉 ex: _Postuler_ **extend** _Ajouter lettre de motivation_
    

#### 🔼 Généralisation / spécialisation

- Comportement commun partagé  
    👉 ex: _Utilisateur_ → _Employeur_, _Candidat_
    

⚠️ **Entre acteurs → seulement généralisation**

---

## 4.5 Description textuelle d’un cas d’utilisation

Un diagramme ne suffit pas → **fiche descriptive obligatoire**

### Contenu d’une fiche UC (exam ⭐⭐⭐):

- Nom du cas
    
- Acteurs
    
- Objectif
    
- Pré-conditions
    
- Post-conditions
    
- Scénario nominal
    
- Scénarios alternatifs
    
- Scénarios d’exception


### Exemple (simplifié)

**Cas : Postuler à une offre**

- Pré-condition : utilisateur authentifié
    
- Nominal :
    
    1. Le candidat choisit une offre
        
    2. Le système vérifie compatibilité
        
    3. Le candidat confirme
        
    4. Le système enregistre la candidature
        
- Exception : profil incompatible
    

---

## 4.6 Description graphique – Diagrammes UML

### 📊 Diagramme de séquence système

- Le système = **boîte noire**
    
- Montre la **chronologie des messages**
    
- Très demandé à l’examen
    

### Types de messages :

- Synchrone
    
- Asynchrone
    
- Réflexif
    
- Message de retour
    

### Fragments combinés (⚠️ à mémoriser)

- **alt** → if / else
    
- **loop** → boucle
    
- **break** → exception
    
- **ref** → appel d’un autre diagramme
    

---

## 5️⃣ Classement des cas d’utilisation & planification des itérations

UP = **itératif & incrémental**

### Deux critères essentiels :

1️⃣ **Priorité fonctionnelle** (client)  
2️⃣ **Risque technique** (chef de projet)

### Règles clés :

- Priorité haute + risque haut → itérations initiales
    
- Priorité basse + risque bas → itérations finales
    
- Cas primaires avant secondaires
    

👉 Sert à **planifier le développement**

---

## 6️⃣ Production des maquettes IHM

### 📌 Maquette = interface **non définitive**

- Simple dessin d’écran
    
- Aucun code
    
- Produit jetable
    

### Objectifs :

- Valider compréhension des besoins
    
- Faciliter communication client
    
- Détecter erreurs tôt
    

👉 Réalisées **très tôt** dans UP

---

## 7️⃣ Conclusion générale

### Pourquoi rappeler ces points ?

- Les développeurs & clients **ne parlent pas le même langage**
    
- Les besoins sont **volatils**
    
- Plusieurs acteurs → conflits possibles
    

📌 **Bonne étude préliminaire + bonne spécification = projet réussi**

---

## ✅ Résumé ultra-synthèse (pour révision rapide)

- Étude préliminaire → vision globale
    
- Analyse du domaine → comprendre le problème
    
- Besoins → fonctionnels & non fonctionnels
    
- Spécification → acteurs + cas d’utilisation
    
- UML → include / extend / généralisation
    
- UP → itératif & incrémental
    
- Maquettes → validation précoce
    

---

If you want next:

- 🧠 **Exam cheat sheet (QCM + pièges)**
    
- ✍️ **Cas pratique corrigé (comme à l’exam)**
    
- 📐 **Templates Obsidian (Use Case, UC description)**
    

Just tell me 👌
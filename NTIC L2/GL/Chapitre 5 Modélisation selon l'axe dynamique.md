# Types de Modélisation

1. **Modélisation Statique**: 
   - **But**: Représenter ce que le système EST.
   - **Exemples**: 
     - Diagramme de classes
     - Diagramme d'objets
     - Diagramme de composants
     - Diagramme de déploiement

2. **Modélisation Dynamique**: 
   - **But**: Représenter comment le système ÉVOLUE.
   - **Exemples**:
     - Diagramme d'activités (DAC)
     - Diagramme de séquence
     - Diagramme d'états-transitions
     - Diagramme de collaboration

3. **Modélisation Fonctionnelle**: 
   - **But**: Représenter ce que le système FAIT.
   - **Exemple**: 
     - Diagramme de cas d’utilisation

# Objectif du DAC

Le **Diagramme d'Activité (DAC)** permet de :

- **Modéliser le comportement d’un système** : Représenter le cheminement entre différentes activités, incluant les séquences, les choix, les itérations, et le parallélisme.
- **Représenter graphiquement le déroulement d’une méthode ou d’un cas d’utilisation** : Illustrer visuellement l’enchaînement des actions et décisions.
- **Décrire le flot de contrôle** : Montrer comment le système évolue d'une activité à l'autre en fonction des conditions et événements.

# 3. Utilisation du DAC

Le **Diagramme d'Activité (DAC)** est utilisé à différents stades du développement d'un système, notamment :

- **Analyse/Conception** :
  - Le DAC permet d'illustrer les **cas d’utilisation** de manière graphique, en traduisant la description textuelle en un modèle visuel.
  - Il aide à comprendre le flux d'activités impliquées dans un processus ou une fonctionnalité spécifique.

- **Réalisation** :
  - Le DAC fournit une **description précise des opérations**, ce qui permet de faciliter la **génération automatique du code**.
  - Les actions et transitions définies dans le DAC peuvent être directement traduites en code opérationnel pour le système.
# 4. Éléments d'un DAC

Les **éléments d'un Diagramme d'Activité (DAC)** sont composés de différentes entités permettant de modéliser les actions, transitions et contrôles au sein du système. Ces éléments incluent :

## 1. **Action**
- Les **actions** représentent les opérations ou instructions élémentaires effectuées par le système ou les acteurs.
- Types d'actions :
  - Affectation de valeur
  - Calcul
  - Émission ou réception d’un signal
- Une action est l'unité fondamentale exécutable dans une activité.

## 2. **Transition**
- Une **transition** représente le passage d'une action à une autre. Elle peut être :
  - **Automatique** : Déclenchée par la fin d’une action et initiant immédiatement la prochaine.
  - **Conditionnelle** : Déclenchée par un événement, mais ne peut être empruntée que si la condition (garde) est vraie.

## 3. **Nœuds**
Les nœuds sont utilisés pour structurer et contrôler le flux d’activités dans un DAC. Il existe plusieurs types de nœuds :
- **Nœud exécutable** : Représente une action ou un traitement à effectuer.
- **Nœud de contrôle** : Utilisé pour coordonner les flots entre différentes actions. Exemple :
  - Nœud initial : Débute l’activité.
  - Nœud final : Termine l’activité.
  - Nœud de décision : Permet de faire des choix conditionnels.
  - Nœud de fusion, bifurcation, union, etc.
- **Nœud d’objet** : Représente un flux de données entre actions. Ces nœuds peuvent être associés à des entrées/sorties pour spécifier les données passées entre les actions.

# 5. Transitions et Nœuds

## **Transitions**
- Les **transitions** représentent le passage entre les actions dans un Diagramme d'Activité. Elles peuvent être de deux types :
  - **Transition Automatique** : Déclenchée par la fin d'une action et entraîne immédiatement le début de la suivante.
  - **Transition Conditionnelle (ou Garde)** : Déclenchée par un événement, mais elle n'est empruntée que si une condition est remplie (garde).

- **Transitions gardées** : Si, dans un point de décision, aucune condition de garde n'est remplie, le modèle est considéré comme mal formé. Pour éviter ce problème, il est possible d'utiliser une garde de type `[else]`, validée si toutes les autres conditions sont fausses.

## **Nœuds de Contrôle**
Les **nœuds de contrôle** sont utilisés pour coordonner les flots entre les nœuds d'action. Il en existe plusieurs types :
- **Nœud de décision** : Permet de bifurquer selon une condition (ex. "Si X, alors Y").
- **Nœud de fusion** : Rassemble plusieurs flots alternatifs en un seul flot sortant. Il permet de gérer plusieurs flux entrants.
- **Nœud de bifurcation** : Définit plusieurs voies possibles à suivre à partir d'un nœud.
- **Nœud de fin** :
  - **Nœud final** : Terminer l'activité, ce qui interrompt tous les autres flots de contrôle.
  - **Nœud de fin de flot** : Permet d'arrêter un flux spécifique sans affecter les autres flots actifs.
- **Nœud initial** : Représente le début de l'activité. Il possède un arc sortant, mais pas d'arc entrant.

## **Fusion vs Union**
- **Nœud de Fusion** : Permet de rassembler plusieurs flots entrants en un seul flot sortant (accepte un flot parmi plusieurs).
- **Nœud d’Union** : Synchronise plusieurs flots concurrents, c’est-à-dire que l’arc sortant est activé uniquement lorsque tous les arcs entrants sont activés.

# 6.Nœud d'Objet**
Un **nœud d'objet** représente un flux de données entre les actions. Il permet de spécifier les valeurs passées en argument à une action et les valeurs de retour.

 Flots de Données

Les **flots de données** dans un Diagramme d'Activité (DAC) représentent les informations échangées entre les différentes actions ou activités. Ces flots sont essentiels pour comprendre comment les données circulent au sein du système pendant l'exécution des tâches.

## **Nœud d'Objet**
- Un **nœud d'objet** permet de représenter un flux de données entre actions. Il montre l’existence d’un objet ou de données générées par une action et utilisées par d'autres actions.
- Ces **objets** peuvent être des **valeurs retournées** ou des **arguments** passés à une action.
  
## **Pin d'Entrée/Sortie**
- Les **pins d'entrée/sortie** (petits carrés) sont utilisés pour spécifier les valeurs passées en argument à une action et les valeurs retournées par cette action.
- Cela permet de mieux comprendre comment les données circulent entre les actions.

## **Notations des Flots d'Objets**
- Les flots de données peuvent être représentés de deux manières :
  1. **Notation classique** : Le nom de l’objet ou de l’état est placé entre crochets, avec le nom de son type.
  2. **Avec des pins** : Les objets sont associés à des pins d’entrée/sortie, ce qui aide à spécifier le passage des données entre les actions.

## **Exemple de Flot de Données**
- Un flot de données pourrait représenter un **argument** d'une fonction, comme un **nom d'utilisateur**, ou une **valeur de retour**, comme un **solde bancaire**.

Les flots de données aident à comprendre la **relation** entre les différentes actions du système et sont cruciaux pour garantir que les processus exécutés échangent correctement les informations nécessaires.

# 7. Partitions et Couloirs

Les **partitions** (ou **couloirs**) sont utilisées dans un Diagramme d'Activité (DAC) pour organiser les actions en fonction des responsables ou des acteurs. Elles permettent de représenter visuellement la division des tâches et de préciser quelles entités (acteurs ou composants) sont responsables de quelles actions.

## **Rôle des Partitions**
- **Organiser les actions** : Les partitions permettent de regrouper les actions en fonction des responsables (acteurs ou entités). Cela aide à clarifier qui fait quoi dans un processus.
- **Responsabilités** : Chaque **partition** est souvent associée à un acteur spécifique ou à un rôle au sein du système, par exemple, un utilisateur, un système, ou un département.
  
## **Représentation Graphique**
- **Couloirs** : Les partitions sont souvent représentées par des lignes verticales ou horizontales, qui délimitent les différentes zones du diagramme.
  - **Lignes Verticales** : Utilisée pour séparer les actions en fonction des acteurs ou des départements.
  - **Lignes Horizontales** : Parfois utilisées pour une organisation différente, selon les besoins de modélisation.

## **Sous-partitions**
- Une **partition** peut elle-même être subdivisée en **sous-partitions**, permettant une organisation encore plus détaillée des responsabilités et des actions.
- Chaque sous-partition peut également être associée à un acteur ou à une entité différente.

## **Exemple d'Utilisation**
- Dans un processus de gestion des demandes, un couloir pourrait être dédié au **responsable des ressources humaines**, un autre à **l'employé**, et un autre à **l'administration**. Chaque acteur aurait des actions spécifiques dans leur couloir respectif.

Les partitions et couloirs permettent ainsi une vue plus claire et structurée des rôles et des responsabilités dans un système complexe.

# 8. Transitions Fork/Join

Les **transitions Fork** et **Join** sont utilisées dans un Diagramme d'Activité (DAC) pour gérer la synchronisation de plusieurs flots de contrôle. Elles permettent de traiter des situations où plusieurs actions doivent être exécutées simultanément ou doivent se synchroniser à un certain point.

## **Transition Fork**
- Une **transition de type Fork** se produit lorsqu'un nœud de synchronisation a plusieurs transitions en sortie.
- **Objectif** : Diviser un flot de contrôle en plusieurs flots parallèles. Chaque flot peut être exécuté indépendamment des autres.
- **Représentation** : Un seul nœud avec plusieurs arcs sortants, permettant de lancer plusieurs actions simultanément.

## **Transition Join**
- Une **transition de type Join** se produit lorsqu'un nœud de synchronisation a plusieurs transitions en entrée.
- **Objectif** : Synchroniser plusieurs flots de contrôle en un seul flot. Cela signifie que le flot de contrôle ne peut continuer que lorsque tous les flots entrants sont arrivés à ce nœud.
- **Représentation** : Un seul nœud avec plusieurs arcs entrants, permettant de réunir les flots parallèles.

## **Exemple d'Utilisation**
- **Fork** : Dans un système de traitement parallèle, après une demande de traitement, le système peut décider de traiter plusieurs tâches en même temps (ex. calculer deux valeurs indépendamment).
- **Join** : Ces deux tâches parallèles devront se synchroniser à un moment donné avant que le processus puisse se poursuivre, ce qui nécessite un nœud de type Join.

Les transitions Fork et Join sont essentielles pour gérer la **concurrence** et la **synchronisation** dans les processus complexes d’un système.

# 9. Nœuds de Fin

Les **nœuds de fin** sont utilisés dans un Diagramme d'Activité (DAC) pour marquer la fin d'une activité ou d'un flot de contrôle. Ils sont essentiels pour indiquer clairement le point où un processus ou une séquence d'actions se termine.

## Types de Nœuds de Fin

1. **Nœud de fin d’activité** :
   - **Objectif** : Ce nœud marque la fin de toute l’activité en cours. Tous les autres flots de contrôle dans l'activité sont interrompus et détruits.
   - **Effet** : Lorsqu'un nœud de fin d’activité est atteint, toute l'activité associée est terminée et toutes les actions qui y sont liées sont abandonnées.
   
2. **Nœud final** :
   - **Objectif** : Ce nœud termine l’activité globale et tous les flots de contrôle liés à cette activité. Il marque la fin complète du processus.
   - **Effet** : Il interrompt tous les flots actifs dans l’activité et abandonne toute tâche en cours.

3. **Nœud de fin de flot** :
   - **Objectif** : Ce nœud marque la fin d'un flot spécifique sans affecter les autres flots actifs dans l’activité.
   - **Effet** : La fin du flot ne signifie pas nécessairement que l'activité entière est terminée. Ce nœud est utilisé lorsque certains flots doivent se terminer, mais que d'autres peuvent encore continuer.

## Fonctionnement des Nœuds de Fin
- **Nœud de fin d’activité** : Arrête tous les processus dans l’activité.
- **Nœud de fin de flot** : Arrête uniquement un flot spécifique, sans interrompre l'activité complète. Cela permet de gérer des processus parallèles de manière indépendante.

## Exemple d’Utilisation
- Un **nœud final** pourrait être utilisé dans un processus de commande où une fois que la commande est traitée et le paiement effectué, tout le processus est considéré comme terminé.
- Un **nœud de fin de flot** pourrait être utilisé dans un processus où plusieurs étapes parallèles sont exécutées, mais certaines peuvent être arrêtées indépendamment des autres (par exemple, l'achèvement de l'examen d'une commande pendant que le paiement est toujours en cours).

Les nœuds de fin sont cruciaux pour la gestion de la **fin des processus** et la **coordination des flots de contrôle** dans un système.

---
## 🔗 Navigation
- **Module:** [[GL|◀ GL]]
- **Semester:** [[NTIC L2|◀ NTIC L2]]
- **Academic Home:** [[README|🏠 Home]]

# TP ToDo List avec Flutter 📝

Bienvenue dans ce TP où nous allons construire une application de ToDo List de A à Z avec Flutter ! Ce sera l'occasion de mettre en pratique de nombreuses notions fondamentales, comme les widgets `Stateless` et `Stateful`, la navigation, et bien plus encore.

## Introduction 🚀

Votre mission, si vous l'acceptez, est de construire une application mobile qui permet aux utilisateurs d'ajouter, de visualiser et de supprimer des tâches à faire. L'application sera constituée de plusieurs écrans et comportera une interface utilisateur intuitive.

## Partie 1: Mise en place de l'environnement 🌱
**Durée estimée**: 15 minutes

### Objectifs
- Installer Flutter (si ce n'est pas déjà fait).
- Créer un nouveau projet Flutter.

### Étapes
1. Assurez-vous d'avoir Flutter et Dart installés sur votre machine.
2. Lancez la commande : `flutter create todo_list_app` pour créer un nouveau projet.
3. Ouvrez le projet dans votre IDE préféré.

## Partie 2: Création de l'interface principale 🎨
**Durée estimée**: 1 heure

### Objectifs
- Construire l'interface utilisateur de l'écran principal.
- Comprendre la différence entre `StatelessWidget` et `StatefulWidget`.

### Étapes
1. Dans `main.dart`, créez un `StatefulWidget` appelé `MainScreen`.
2. Dans ce widget, définissez un `Scaffold` avec un `AppBar` ayant le titre "Ma ToDo List".
3. Ajoutez un `ListView.builder` pour afficher la liste des tâches.
4. Pour l'instant, créez une liste fictive de tâches et affichez-les dans le `ListView`.

## Partie 3: Ajout de nouvelles tâches 📌
**Durée estimée**: 1 heure

### Objectifs
- Naviguer vers un nouvel écran pour ajouter une tâche.
- Utiliser des champs de texte pour la saisie de l'utilisateur.

### Étapes
1. Créez un nouveau fichier `add_task.dart`.
2. Dans ce fichier, construisez un nouvel écran avec un champ de texte pour saisir le titre de la tâche. Utilisez un `TextField` pour permettre à l'utilisateur de saisir une nouvelle tâche. N'oubliez pas d'associer un `TextEditingController`.
3. Ajoutez un bouton "Ajouter" pour valider la saisie.
4. Une fois le bouton pressé, ajoutez la nouvelle tâche à la liste et revenez à l'écran principal.

## Partie 4: Suppression de tâches 🗑️
**Durée estimée**: 45 minutes

### Objectifs
- Permettre à l'utilisateur de supprimer une tâche.
- Mettre en pratique la gestion de l'état avec `setState`.

### Étapes
1. Pour chaque élément de la liste, ajoutez un icône de suppression.
2. Lorsque l'utilisateur appuie sur cet icône, supprimez la tâche correspondante de la liste.
3. Assurez-vous que la liste est mise à jour correctement à l'aide de `setState`.

## Partie 5: Finalisation et améliorations 🌟
**Durée estimée**: 1 heure

### Objectifs
- Améliorer l'interface utilisateur.
- Tester l'application pour s'assurer de sa stabilité.

### Étapes
1. Ajoutez des styles et des animations pour améliorer l'expérience utilisateur.
2. Testez l'application sur différents appareils et résolutions pour vous assurer de sa compatibilité.
3. Corrigez tous les bugs éventuels.

---

Bravo ! 🎉 Vous avez maintenant une application de ToDo List fonctionnelle. Vous avez mis en pratique plusieurs concepts fondamentaux de Flutter et vous êtes prêt à explorer davantage les capacités de ce framework. Bon codage ! 🚀🌍
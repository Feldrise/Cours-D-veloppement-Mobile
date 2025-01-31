# TP : Gestion des États avec Riverpod et Modélisation avec Freezed 🚀

## Introduction

Bienvenue dans ce TP où nous plongerons profondément dans la gestion des états avec Riverpod et la modélisation avec Freezed. Vous allez découvrir comment ces outils peuvent simplifier votre développement avec Flutter et améliorer la structure de votre code.

## Partie 0 : Documentation de Riverpod

Afin de comprendre ce qu'est Riverpod et son intérêt, vous pouvez lire la documentation :

## Partie 1: Introduction à Riverpod et Freezed 🌊

**Durée estimée: 30min**

### Objectifs

- Comprendre le rôle et les avantages de Riverpod
- Se familiariser avec la modélisation des données via Freezed

### Étapes

1. **Installation de Riverpod et Freezed**:

   - Ajoutez les dépendances suivantes à votre fichier `pubspec.yaml`:

     ```yaml
     dependencies:
       flutter_riverpod: latest_version
       freezed_annotation: latest_version

     dev_dependencies:
       build_runner: latest_version
       freezed: latest_version
     ```

   - Exécutez `flutter pub get` pour installer les dépendances.

2. **Création d'un modèle Freezed**:

   - Créez un fichier `models/user.dart`.
   - Définissez un modèle `User` avec Freezed:

     ```dart
     import 'package:freezed_annotation/freezed_annotation.dart';

     part 'user.freezed.dart';

     @freezed
     class User with _$User {
       const factory User({required String name, required int age}) = _User;
     }
     ```

   - Exécutez la commande `flutter pub run build_runner build` pour générer les fichiers nécessaires.

3. **Utilisation basique de Riverpod**:
   - Créez un provider simple avec Riverpod.
     ```dart
     final exampleProvider = Provider<int>((ref) => 42);
     ```

🎉 Bravo! Vous avez maintenant une base sur Riverpod et Freezed!

## Partie 2: Gestion des états avec Riverpod et ConsumerWidget 🌟

**Durée estimée: 45min**

### Objectifs

- Comprendre comment Riverpod gère les états
- Découvrir le `ConsumerWidget` et son utilisation

### Étapes

0. **Rajout d'un ProviderScope**

   - Pour pouvoir utiliser Riverpopd il faut que votre Widget principal soit entouré d'un `ProviderScope`

1. **Création d'un StateNotifierProvider**:

   - Créez un `StateNotifier` pour gérer une liste d'utilisateurs.

     ```dart
     class UserNotifier extends StateNotifier<List<User>> {
       UserNotifier() : super([]);

       void addUser(User user) {
         state = [...state, user];
       }
     }

     final userProvider = StateNotifierProvider<UserNotifier, List<User>>((ref) => UserNotifier());
     ```

2. **ConsumerWidget**:

   - Créez un nouveau widget qui hérite de `ConsumerWidget`.
   - Utilisez ce widget pour afficher la liste des utilisateurs.

     ```dart
     class UserList extends ConsumerWidget {
       @override
       Widget build(BuildContext context, WidgetRef ref) {
         final users = ref.watch(userProvider);

         return ListView.builder(
           itemCount: users.length,
           itemBuilder: (context, index) => ListTile(title: Text(users[index].name)),
         );
       }
     }
     ```

3. **Ajout d'utilisateurs**:
   - Implémentez une fonctionnalité pour ajouter des utilisateurs à la liste.

🌟 Vous avez maintenant une compréhension solide de la gestion des états avec Riverpod et ConsumerWidget!

## Partie 3: Approfondissement avec Riverpod et Freezed 🧠

**Durée estimée: 45min**

### Objectifs

- Renforcer votre compréhension des concepts Riverpod et Freezed.
- Mettre en pratique la gestion de l'état et la modélisation des données dans des scénarios concrets.

### Étapes

1. **Création et affichage d'un profil utilisateur**:

   - En utilisant le modèle `User` que vous avez créé précédemment avec Freezed, créez un nouveau provider pour un utilisateur unique.
     ```dart
     final selectedUserProvider = StateProvider<User?>((ref) => null);
     ```
   - Dans votre interface, ajoutez un bouton qui, lorsqu'il est cliqué, définit un utilisateur sélectionné (par exemple, le premier de votre liste).
   - Affichez les détails de cet utilisateur sélectionné dans un nouveau widget. Assurez-vous d'utiliser `ConsumerWidget` pour observer les changements d'état.

2. **Modification des détails de l'utilisateur**:

   - Ajoutez une fonctionnalité qui permet de modifier l'âge de l'utilisateur sélectionné.
   - Pour cela, créez un champ de saisie (`TextField`) et un bouton "Mettre à jour". Lorsque ce bouton est pressé, l'âge de l'utilisateur sélectionné devrait être mis à jour avec la valeur entrée.

3. **Recherche d'utilisateur**:

   - Implementez une barre de recherche pour filtrer la liste des utilisateurs par nom.
   - Pour ce faire, créez un nouveau `StateNotifier` qui gérera une chaîne de recherche et filtrera la liste des utilisateurs en conséquence.

     ```dart
     class SearchNotifier extends StateNotifier<String> {
       SearchNotifier() : super('');

       void updateSearch(String value) {
         state = value;
       }
     }

     final searchProvider = StateNotifierProvider<SearchNotifier, String>((ref) => SearchNotifier());
     ```

4. **Affichage conditionnel**:
   - Intégrez une fonctionnalité qui, si la liste des utilisateurs filtrée est vide (c'est-à-dire qu'aucun utilisateur ne correspond à la recherche), affiche un message tel que "Aucun utilisateur trouvé".

🔄 Testez toutes ces nouvelles fonctionnalités pour vous assurer de leur bon fonctionnement!

## Partie 4: Exercices de Réflexion 🤔

**Durée estimée: 30min**

### Objectifs

- Réfléchir aux meilleures pratiques et à la logique de la gestion de l'état.

### Étapes

1. **Discussion sur les avantages de Riverpod**:

   - Notez 3 avantages majeurs de l'utilisation de Riverpod pour la gestion de l'état par rapport aux autres solutions que vous connaissez.

2. **Rétrospective sur Freezed**:

   - Quels sont, selon vous, les avantages principaux de l'utilisation de Freezed pour la modélisation des données dans Flutter?

3. **Scénario Hypothétique**:
   - Imaginez que votre application doit maintenant gérer des milliers d'utilisateurs. Comment optimiseriez-vous la performance de votre application en utilisant Riverpod?

🌐 Partagez vos réflexions avec vos pairs et discutez des différentes approches possibles.

## Conclusion 🌟

Vous avez maintenant une compréhension approfondie et pratique de Riverpod et Freezed dans Flutter. Gardez toujours à l'esprit que la pratique régulière est la clé pour maîtriser n'importe quel outil ou concept. Continuez à explorer, à coder et à apprendre! 🎉🚀

## [BONUS] Partie 3: Exploration approfondie de Riverpod et Freezed 🕵️

**Durée estimée: 45min**

### Objectifs

- Renforcer la compréhension des concepts précédemment abordés
- Pratiquer l'utilisation de Riverpod et Freezed à travers des exercices pratiques

### Étapes

1. **Thème sombre et clair**:

   - Intégrez une fonctionnalité permettant à l'utilisateur de basculer entre un thème sombre et un thème clair pour votre application.
   - Utilisez Riverpod pour gérer le thème actuel de l'application.

2. **Modification du modèle User**:

   - Ajoutez un champ `email` à votre modèle `User` avec Freezed.
   - Regénérez les fichiers nécessaires en exécutant la commande `flutter pub run build_runner build`.

3. **Création d'une interface de saisie d'utilisateur**:

   - Dans votre application, ajoutez un formulaire permettant d'ajouter un nouvel utilisateur. Ce formulaire devra avoir des champs pour le nom, l'âge et l'e-mail.
   - Lorsque l'utilisateur valide le formulaire, utilisez le `StateNotifier` pour ajouter cet utilisateur à la liste.

4. **Affichage détaillé d'un utilisateur**:
   - Lorsque l'on clique sur un utilisateur de la liste, ouvrez une nouvelle page affichant ses détails (nom, âge, e-mail).
   - Pour un challenge supplémentaire, essayez d'implémenter une fonctionnalité pour modifier ou supprimer cet utilisateur.

🌍 Fin de cette partie! Vous avez fait un excellent travail en renforçant votre maîtrise de Riverpod et Freezed. Continuez à explorer et à expérimenter pour maîtriser encore plus ces outils!

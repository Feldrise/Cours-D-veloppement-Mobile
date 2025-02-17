# TP : Création d'une Application ToDo avec Flutter et une API

Salut à tous ! 😃 Aujourd'hui, nous allons plonger dans le monde fascinant des appels réseau avec Flutter. Nous allons créer une application ToDo qui interagit avec une API pour lire et écrire des données. Prêts à relever le défi ? C'est parti ! 🚀

## Partie 1 : Configuration initiale

### Objectifs

- Mettre en place un nouvel environnement de projet Flutter.
- Se familiariser avec la documentation de l'API que nous allons utiliser.

### Étapes

1. Créez un nouveau projet Flutter en utilisant la commande :

```bash
flutter create todo_app
```

2. Ouvrez le projet dans votre IDE préféré.
3. Familiarisez-vous avec la documentation de l'API disponible à l'adresse : [https://dummyjson.com/docs/todos](https://dummyjson.com/docs/todos). Prenez quelques minutes pour explorer les différentes routes et les données disponibles. 🧐

## Partie 2 : Mise en place des appels réseau avec modélisation des données

### Objectifs

- Intégrer les bibliothèques nécessaires pour gérer les appels réseau et la modélisation des données.
- Créer des modèles pour les données renvoyées par l'API en utilisant Freezed.
- Créer des fonctions pour lire des données via l'API.

### Étapes

1. Ajoutez les dépendances nécessaires à votre `pubspec.yaml` :

```yaml
dependencies:
  http: ^1.1.0
  freezed_annotation: ^2.4.1
  json_annotation: ^4.8.1

dev_dependencies:
  build_runner: ^2.4.6
  freezed: ^2.4.2
  json_serializable: ^6.7.1
```

2. Créez un nouveau fichier `models/todo_model.dart`. Dans ce fichier, nous allons définir notre modèle de données avec Freezed.

```dart
import 'package:freezed_annotation/freezed_annotation.dart';

part 'todo_model.freezed.dart';
part 'todo_model.g.dart';

@freezed
class TodoResponse with _$TodoResponse {
  factory TodoResponse({
    required List<Todo> todos,
    required int total,
    required int skip,
    required int limit,
  }) = _TodoResponse;

  factory TodoResponse.fromJson(Map<String, dynamic> json) => _$TodoResponseFromJson(json);
}

@freezed
class Todo with _$Todo {
  factory Todo({
    required int id,
    required String todo,
    required bool completed,
    required int userId,
  }) = _Todo;

  factory Todo.fromJson(Map<String, dynamic> json) => _$TodoFromJson(json);
}
```

3. Exécutez la commande suivante pour générer les fichiers nécessaires pour Freezed :

```bash
flutter pub run build_runner build
```

4. Créez un nouveau fichier `api_service.dart` pour gérer tous les appels réseau.

5. Dans ce fichier, créez une fonction pour récupérer la liste des tâches ToDo depuis l'API en utilisant le modèle que nous venons de définir.

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;
import 'models/todo_model.dart';

class ApiService {
  final String baseUrl = 'URL_DE_LAPI';

  Future<TodoResponse> fetchTodos() async {
    final response = await http.get(Uri.parse(baseUrl));
    if (response.statusCode == 200) {
      return TodoResponse.fromJson(json.decode(response.body));
    } else {
      throw Exception('Failed to load todos');
    }
  }
}
```

6. Vous pouvez maintenant utiliser la fonction `fetchTodos` pour récupérer les données de l'API et les convertir en objets Dart grâce à notre modèle Freezed.

## Partie 3 : Intégration dans l'application

### Objectifs

- Intégrer les fonctions d'appel réseau dans l'application.
- Afficher la liste des tâches récupérées depuis l'API.

### Étapes

1. Dans votre écran principal, créez une variable d'instance de `ApiService` pour pouvoir appeler la fonction `fetchTodos`.

```dart
final apiService = ApiService();
```

2. Utilisez un `FutureBuilder` pour récupérer et afficher la liste des tâches depuis l'API.

```dart
FutureBuilder<TodoResponse>(
  future: apiService.fetchTodos(),
  builder: (context, snapshot) {
    if (snapshot.connectionState == ConnectionState.waiting) {
      return CircularProgressIndicator();
    }

	if (snapshot.hasError) {
      return Text('Erreur : ${snapshot.error}');
    }

    final todos = snapshot.data!.todos;
    return ListView.builder(
      itemCount: todos.length,
      itemBuilder: (context, index) {
        final todo = todos[index];
        return ListTile(
          title: Text(todo.todo),
          trailing: Icon(
            todo.completed ? Icons.check_box : Icons.check_box_outline_blank,
          ),
        );
      },
    );
  }
)
```

## Partie 4 : Projet complet

### Objectifs

- Créer une application ToDo complète avec une interface utilisateur intuitive.
- Utiliser une API pour stocker, récupérer, mettre à jour et supprimer des tâches.
- Appliquer les meilleures pratiques de développement Flutter et de gestion des appels réseau.

### Étapes

1. **Interface Utilisateur :**

   - Créez une interface utilisateur propre et intuitive avec une barre d'applications, une liste de tâches et un bouton flottant pour ajouter de nouvelles tâches.
   - Chaque élément de la liste doit afficher le nom de la tâche et un indicateur pour montrer si la tâche est complétée ou non.
   - Ajoutez une fonctionnalité pour marquer une tâche comme complétée en cliquant dessus.

2. **Ajout et Suppression de Tâches :**

   - En cliquant sur le bouton flottant, une boîte de dialogue ou une nouvelle page s'ouvre pour permettre à l'utilisateur d'ajouter une nouvelle tâche.
   - Chaque élément de la liste doit également avoir une icône ou un bouton pour supprimer la tâche via un appel API.

3. **Mise à jour des Tâches :**

   - En cliquant longuement sur une tâche, l'utilisateur peut la modifier.
   - Une boîte de dialogue ou une nouvelle page s'ouvre avec le nom actuel de la tâche, permettant à l'utilisateur de le mettre à jour.
   - Les modifications doivent être envoyées à l’API et mises à jour en temps réel dans l'application.

4. **Gestion des Appels API :**

   - Implémentez des appels réseau pour récupérer, ajouter, modifier et supprimer des tâches via l’API.
   - Utilisez `http` pour interagir avec l’API et Freezed pour modéliser les données.
   - Assurez-vous que toutes les actions (ajout, suppression, mise à jour) sont correctement reflétées dans l’API.

5. **Bonus : Thèmes et Personnalisation :**
   - Ajoutez une fonctionnalité pour changer le thème de l'application (clair/sombre).
   - Permettez à l'utilisateur de personnaliser l'apparence de l'application (couleurs, polices, etc.).

### Rendu Attendu

1. **Code Source :**

   - Votre projet Flutter complet avec tous les fichiers source.
   - Assurez-vous que votre code est propre, bien commenté et suit les meilleures pratiques de développement Flutter.

2. **Interaction avec l'API :**

   - Un test démontrant que l’application fonctionne avec l’API et gère bien les appels réseau.

3. **Documentation :**

   - Un fichier README.md décrivant votre application, les fonctionnalités implémentées et les instructions pour exécuter l'application.
   - Des captures d'écran montrant différentes parties de votre application en action.

4. **Réflexion Personnelle :**
   - Vos réflexions sur ce que vous avez appris et comment vous pourriez améliorer l'application à l'avenir.

### Évaluation

Votre travail sera évalué sur les critères suivants :

1. **Fonctionnalité :** Votre application fonctionne-t-elle comme prévu sans bugs ni erreurs ?
2. **Gestion des Appels API :** Avez-vous correctement structuré vos requêtes et géré les erreurs ?
3. **Qualité du Code :** Votre code est-il propre, bien organisé et suit-il les meilleures pratiques ?
4. **Interface Utilisateur :** Votre design est-il intuitif et esthétiquement plaisant ?
5. **Documentation et Réflexion :** Avez-vous correctement documenté votre travail et fourni des réflexions perspicaces ?

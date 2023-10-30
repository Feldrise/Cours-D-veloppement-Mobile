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

3. (Bonus) Ajout de Tâches :
   - Comme l'API ne stocke pas les tâches en base de données, cette partie est un exercice bonus. Vous pouvez créer un formulaire pour ajouter une nouvelle tâche et l'envoyer à l'API.
   - Notez que ces tâches ne seront pas persistantes, mais cela vous donnera une bonne pratique sur la gestion des formulaires et l'envoi de données à une API.

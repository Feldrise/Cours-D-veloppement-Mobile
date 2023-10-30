# TP : Application ToDo avec Flutter, SQLite et Freezed

Salut à tous ! 😃 Aujourd'hui, nous allons construire une application ToDo robuste en utilisant Flutter, SQLite et Freezed pour une gestion optimale des données. Prêts à plonger dans le monde du stockage local ? C'est parti ! 🚀

## Partie 1 : Configuration initiale, intégration de SQLite et Freezed
**Durée estimée :** 45 minutes

### Objectifs
- Mettre en place un nouvel environnement de projet Flutter.
- Intégrer SQLite et Freezed à votre projet.

### Étapes
1. Créez un nouveau projet Flutter :
```bash
flutter create todo_app_sqlite_freezed
```
2. Ouvrez le projet dans votre IDE.
3. Ajoutez les dépendances nécessaires à votre `pubspec.yaml` :
```yaml
dependencies:
  sqflite: ^2.3.0
  freezed_annotation: ^2.4.1
  json_annotation: ^4.8.1

dev_dependencies:
  build_runner: ^2.4.6
  freezed: ^2.4.2
  json_serializable: ^6.7.1
```
4. Exécutez `flutter pub get` pour installer les nouvelles dépendances.

## Partie 2 : Modélisation des données avec Freezed et initialisation de SQLite
**Durée estimée :** 1 heure 15 minutes

### Objectifs
- Créer un modèle pour les tâches ToDo avec Freezed.
- Initialiser la base de données SQLite dans le `main.dart`.
- Créer des fonctions pour lire, écrire, mettre à jour et supprimer des tâches.

### Étapes
1. Créez un nouveau fichier `models/todo_model.dart`. Définissez votre modèle de données avec Freezed :
```dart
import 'package:freezed_annotation/freezed_annotation.dart';

part 'todo_model.freezed.dart';
part 'todo_model.g.dart';

@freezed
class Todo with _$Todo {
  factory Todo({
    int? id,
    required String task,
    required bool isCompleted,
  }) = _Todo;

  factory Todo.fromJson(Map<String, dynamic> json) => _$TodoFromJson(json);
}
```
2. Exécutez la commande suivante pour générer les fichiers nécessaires pour Freezed :
```bash
flutter pub run build_runner build
```
Bien sûr ! Le `DatabaseHelper` est une classe qui encapsule toutes les opérations liées à la base de données SQLite. Elle permet de centraliser la logique de la base de données, rendant ainsi le code plus propre et plus facile à gérer. Voici une version plus détaillée du `DatabaseHelper` :

3. **Initialisation et Singleton :**
   - Nous utilisons le modèle Singleton pour s'assurer qu'il n'y a qu'une seule instance de `DatabaseHelper` dans toute l'application. Cela évite les problèmes potentiels de multiples accès à la base de données.
   - La base de données est initialisée une seule fois et est stockée dans une variable privée `_database`.

```dart
class DatabaseHelper {
  final _dbName = 'todoApp.db';
  final _dbVersion = 1;
  final _tableName = 'todos';

  DatabaseHelper._privateConstructor();
  static final DatabaseHelper instance = DatabaseHelper._privateConstructor();

  static Database? _database;
  Future<Database> get database async {
    if (_database != null) return _database!;
    _database = await _initDatabase();
    return _database!;
  }
}
```

4. **Création de la base de données :**
   - Lorsque la base de données est initialisée pour la première fois, la méthode `_onCreate` est appelée pour créer la table.

```dart
_initDatabase() async {
  String path = join(await getDatabasesPath(), _dbName);
  return await openDatabase(path,
      version: _dbVersion, onCreate: _onCreate);
}

Future _onCreate(Database db, int version) async {
  await db.execute('''
    CREATE TABLE $_tableName (
      id INTEGER PRIMARY KEY,
      task TEXT NOT NULL,
      isCompleted INTEGER NOT NULL
    )
  ''');
}
```

5. **Opérations CRUD :**
   - Ces fonctions permettent de créer, lire, mettre à jour et supprimer des tâches dans la base de données.

```dart
// Insert a new task
Future<int> insert(Todo todo) async {
  Database db = await instance.database;
  return await db.insert(_tableName, todo.toMap());
}

// Get all tasks
Future<List<Todo>> getAllTodos() async {
  Database db = await instance.database;
  var todos = await db.query(_tableName);
  return todos.map((e) => Todo.fromMap(e)).toList();
}

// Update a task
Future<int> update(Todo todo) async {
  Database db = await instance.database;
  return await db.update(_tableName, todo.toMap(),
      where: 'id = ?', whereArgs: [todo.id]);
}

// Delete a task
Future<int> delete(int id) async {
  Database db = await instance.database;
  return await db.delete(_tableName, where: 'id = ?', whereArgs: [id]);
}
```

## Partie 3 : Intégration dans l'application

### Objectifs
- Afficher la liste des tâches depuis la base de données SQLite.
- Ajouter des fonctionnalités pour créer, mettre à jour et supprimer des tâches.

### Étapes
1. Dans votre écran principal, utilisez le `FutureBuilder` pour intégrer les fonctions de la base de données et afficher la liste des tâches.
2. Ajoutez un widget, comme un `FloatingActionButton`, pour permettre à l'utilisateur d'ajouter de nouvelles tâches.
3. Ajoutez des fonctionnalités pour mettre à jour et supprimer des tâches en utilisant des gestes, comme un balayage pour supprimer.

## Partie 4 : Finalisation et tests

### Objectifs
- Tester l'application pour s'assurer que tout fonctionne comme prévu.
- Identifier et résoudre les éventuels bugs.

### Étapes
1. Lancez votre application et testez toutes les fonctionnalités.
2. Assurez-vous que les données sont correctement stockées et récupérées depuis la base de données SQLite.

Félicitations ! 🎉 Vous avez maintenant une application ToDo solide qui utilise SQLite pour le stockage local des données et Freezed pour une gestion optimale des modèles. Vous avez fait un excellent travail aujourd'hui ! N'hésitez pas à explorer davantage et à ajouter d'autres fonctionnalités à votre application. Bon codage ! 👩‍💻👨‍💻
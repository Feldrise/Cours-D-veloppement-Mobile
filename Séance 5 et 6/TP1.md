# Travaux Pratiques: Découverte de Firebase avec Flutter

## Partie 1: Introduction à Firebase
**Durée estimée:** 1 heure

### Objectifs
- Comprendre ce qu'est Firebase et comment il peut être utile dans le développement d'applications mobiles.
- Installer Firebase dans votre projet Flutter.
- Découverte de quelques services clés proposés par Firebase.

### Étapes

#### 1. Qu'est-ce que Firebase? 
Firebase est une plateforme de développement d'applications mobiles et web proposée par Google. Elle offre une variété de services comme l'authentification, la base de données en temps réel, l'analyse, etc., qui aident à accélérer le développement, améliorer la qualité de l'app et optimiser la base d'utilisateurs. 😄

#### 2. Pré-requis
- Assurez-vous d'avoir un compte Google.
- Assurez-vous d'avoir installé Flutter et configuré un émulateur Android ou iOS sur votre machine.

#### 3. Création d'un projet Firebase 
- Rendez-vous sur la [console Firebase](https://console.firebase.google.com/).
- Cliquez sur "Ajouter un projet" et suivez les instructions pour créer un nouveau projet Firebase. 🚀

#### 4. Ajout de Firebase à votre projet Flutter
Suivez les instructions sur la [page d'installation de Firebase pour Flutter](https://firebase.google.com/docs/flutter/setup?platform=android) pour ajouter Firebase à votre projet Flutter. 

- **Étape 1:** Commencez par ajouter la dépendance `firebase_core` à votre fichier `pubspec.yaml` comme ceci :
```yaml
dependencies:
  flutter:
    sdk: flutter
  firebase_core: ^1.6.0
```
- **Étape 2:** Exécutez `flutter pub get` dans votre terminal pour installer la nouvelle dépendance.

- **Étape 3:** Suivez les instructions spécifiques à la plateforme (Android/iOS) sur la page d'installation pour configurer Firebase dans votre projet.

#### 5. Initialisation de Firebase
Dans votre fichier `main.dart`, assurez-vous d'initialiser Firebase avant d'appeler `runApp()` comme ceci :
```dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp(
    options: DefaultFirebaseOptions.currentPlatform,
  );
  runApp(MyApp());
}
```

#### 6. Exploration de Firebase Console
- Retournez à la [console Firebase](https://console.firebase.google.com/) et explorez quelques-uns des services proposés. Par exemple, jetez un œil à l'authentification, la base de données Firestore, et les analytics. 😎

#### 7. Réflexion
Prenez un moment pour réfléchir sur comment vous pourriez utiliser certains de ces services dans vos projets futurs. Notez vos idées.

---

Cette première partie vous a permis de découvrir Firebase et d'initialiser Firebase dans votre projet Flutter. Dans la partie suivante, nous plongerons dans la création d'une application simple utilisant Firebase pour stocker et récupérer des données. 🎉

## Partie 2: Exploration des Notions de Base de Firebase
**Durée estimée:** 1 heure 30 minutes

### Objectifs
- Comprendre et utiliser Firebase Authentication.
- Comprendre et utiliser Cloud Firestore pour stocker et récupérer des données.
- Découvrir comment lire et écrire des données dans Cloud Firestore.

### Étapes

#### 1. Configuration de Firebase Authentication
- Rendez-vous sur la [console Firebase](https://console.firebase.google.com/), sélectionnez votre projet et naviguez vers l'onglet Authentication.
- Activez l'authentification par e-mail/mot de passe en cliquant sur "Configurer la méthode de connexion" et activez "E-mail/Mot de passe". 😊

#### 2. Ajout de la Dépendance
- Ajoutez la dépendance `firebase_auth` à votre fichier `pubspec.yaml`.
```yaml
dependencies:
  flutter:
    sdk: flutter
  firebase_core: ^1.6.0
  firebase_auth: ^3.3.3
```
- Exécutez `flutter pub get` dans votre terminal pour installer la nouvelle dépendance.

#### 3. Authentification Utilisateur
- Créez une nouvelle page pour l'authentification et utilisez `FirebaseAuth` pour permettre aux utilisateurs de se créer un compte et de se connecter.

```dart
import 'package:firebase_auth/firebase_auth.dart';
import 'package:flutter/material.dart';

class AuthPage extends StatefulWidget {
  @override
  _AuthPageState createState() => _AuthPageState();
}

class _AuthPageState extends State<AuthPage> {
  final _emailController = TextEditingController();
  final _passwordController = TextEditingController();

  void _register() async {
    try {
      UserCredential userCredential = await FirebaseAuth.instance.createUserWithEmailAndPassword(
        email: _emailController.text,
        password: _passwordController.text,
      );
      // Utilisateur enregistré avec succès
    } on FirebaseAuthException catch (e) {
      // Gérer les erreurs
    }
  }

  // ... rest of the code

}
```

#### 4. Configuration de Cloud Firestore
- Naviguez vers l'onglet Firestore Database dans la [console Firebase](https://console.firebase.google.com/) et cliquez sur "Créer une base de données".
- Sélectionnez le mode de test pour votre base de données et suivez les étapes pour la configurer. 🚀

#### 5. Ajout de la Dépendance
- Ajoutez la dépendance `cloud_firestore` à votre fichier `pubspec.yaml`.
```yaml
dependencies:
  flutter:
    sdk: flutter
  firebase_core: ^1.6.0
  cloud_firestore: ^2.5.0
```
- Exécutez `flutter pub get` dans votre terminal pour installer la nouvelle dépendance.

#### 6. Lecture et Écriture dans Firestore
- Créez une nouvelle page pour afficher une liste de données à partir de Firestore et permettre aux utilisateurs d'ajouter de nouvelles données.

```dart
import 'package:cloud_firestore/cloud_firestore.dart';
import 'package:flutter/material.dart';

class FirestorePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    CollectionReference notes = FirebaseFirestore.instance.collection('notes');

    return Scaffold(
      appBar: AppBar(
        title: Text('Notes'),
      ),
      body: StreamBuilder<QuerySnapshot>(
        stream: notes.snapshots(),
        builder: (context, snapshot) {
          if (snapshot.hasError) {
            return Text('Something went wrong');
          }

          if (snapshot.connectionState == ConnectionState.waiting) {
            return Text("Loading");
          }

          return ListView(
            children: snapshot.data!.docs.map((DocumentSnapshot document) {
              Map<String, dynamic> data = document.data()! as Map<String, dynamic>;
              return ListTile(
                title: Text(data['title']),
                subtitle: Text(data['content']),
              );
            }).toList(),
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () async {
          await notes.add({
            'title': 'New Note',
            'content': 'This is the content of the new note',
          });
        },
        child: Icon(Icons.add),
      ),
    );
  }
}
```
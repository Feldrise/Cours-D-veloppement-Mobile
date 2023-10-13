# TP : Exploration des Widgets Stateless dans Flutter 🚀

## Introduction
Flutter, en tant que framework, est basé sur le concept de widgets pour construire l'interface utilisateur. Dans ce TP, nous allons explorer l'un des types de base de widgets : les **Stateless Widgets**. Ils sont utiles lorsque le contenu de votre widget ne change pas au cours du temps. 🔄

## Partie 1 : Création d'un Stateless Widget Simple
**Durée estimée : 20 minutes** 🕒

### Objectifs :
- Comprendre le fonctionnement d'un Stateless Widget.
- Créer un Stateless Widget personnalisé.

### Étapes :
1. **Initialisation d'un nouveau projet Flutter**:
    ```bash
    flutter create tp_stateless_widgets
    cd tp_stateless_widgets
    ```

2. **Création d'un Stateless Widget**:
    Dans `lib/main.dart`, remplacez le code existant par le suivant :
    ```dart
    import 'package:flutter/material.dart';

    void main() => runApp(MyApp());

    class MyApp extends StatelessWidget {
      @override
      Widget build(BuildContext context) {
        return MaterialApp(
          title: 'TP Stateless Widgets',
          theme: ThemeData(primarySwatch: Colors.blue),
          home: MyStatelessWidget(title: 'Mon Premier Stateless Widget 🥳'),
        );
      }
    }
    ```

3. **Ajout du Stateless Widget personnalisé**:
    Juste en dessous de `MyApp`, ajoutez votre nouveau Stateless Widget :
    ```dart
    class MyStatelessWidget extends StatelessWidget {
      final String title;

      MyStatelessWidget({required this.title});

      @override
      Widget build(BuildContext context) {
        return Scaffold(
          appBar: AppBar(title: Text(title)),
          body: Center(
            child: Text(
              'Bienvenue dans le monde des Stateless Widgets! 🌍',
              style: TextStyle(fontSize: 20),
            ),
          ),
        );
      }
    }
    ```

4. **Lancez votre application** :
    ```bash
    flutter run
    ```
   Vous devriez voir votre application affichant le texte au centre de l'écran.

## Partie 2 : Utilisation de Propriétés dans les Stateless Widgets
**Durée estimée : 15 minutes** 🕒

### Objectifs :
- Comprendre comment passer des propriétés aux Stateless Widgets.
- Afficher des données dynamiques à partir des propriétés du widget.

### Étapes :
1. **Modification de `MyStatelessWidget`**:
    Changez la propriété `title` pour accepter un nom d'utilisateur :
    ```dart
    final String username;
    MyStatelessWidget({required this.username});
    ```

    Mettez à jour la fonction `build` pour saluer l'utilisateur :
    ```dart
    Text(
      'Salut $username, bienvenue dans le monde des Stateless Widgets! 🌍',
      style: TextStyle(fontSize: 20),
    ),
    ```

2. **Mise à jour de `MyApp`**:
    Changez l'utilisation de `MyStatelessWidget` pour passer un nom d'utilisateur :
    ```dart
    home: MyStatelessWidget(username: 'Alice'),
    ```

3. **Relancez votre application** pour voir le message de bienvenue mis à jour.

---

😀 **Félicitations**! Vous avez réussi à créer et utiliser des Stateless Widgets dans Flutter. 🎉

---

## Partie 3 : Intégration d'une Liste de Stateless Widgets
**Durée estimée : 30 minutes** 🕒

### Objectifs :
- Apprendre à utiliser les listes pour afficher plusieurs widgets.
- Créer un Stateless Widget réutilisable.

### Étapes :
1. **Création d'une Liste de Messages**:
    Dans `lib/main.dart`, ajoutez une nouvelle liste de messages :
    ```dart
    final List<String> messages = [
      'Bonjour Zoé 🌞',
      'Bien joué pour la partie précédent 🎉',
      'Les Stateless Widgets sont incroyables, n\'est-ce pas? 🚀',
      'Continuez à coder ! 💻'
    ];
    ```

2. **Création d'un Stateless Widget pour un Message**:
    Créez un nouveau Stateless Widget nommé `MessageCard` juste en dessous de `MyStatelessWidget` :
    ```dart
    class MessageCard extends StatelessWidget {
      final String message;

      MessageCard({required this.message});

      @override
      Widget build(BuildContext context) {
        return Card(
          child: Padding(
            padding: EdgeInsets.all(16.0),
            child: Text(
              message,
              style: TextStyle(fontSize: 18),
            ),
          ),
        );
      }
    }
    ```

3. **Utilisation de `ListView.builder` pour afficher les messages**:
    Dans `MyStatelessWidget`, remplacez le `Text` actuel par le suivant :
    ```dart
    ListView.builder(
      itemCount: messages.length,
      itemBuilder: (context, index) {
        return MessageCard(message: messages[index]);
      },
    )
    ```

4. **Lancez votre application** pour voir la liste de messages.

---

## Partie 4 : Styling et Personnalisation des Stateless Widgets
**Durée estimée : 30 minutes** 🕒

### Objectifs :
- Améliorer l'aspect visuel des Stateless Widgets.
- Utiliser différentes propriétés pour personnaliser les widgets.

### Étapes :
1. **Stylisation de la `MessageCard`**:
   Ajoutez une bordure, une marge et une ombre à votre `MessageCard` :
   ```dart
   Card(
     elevation: 5.0,
     margin: EdgeInsets.symmetric(vertical: 10.0, horizontal: 15.0),
     child: ...
   )
   ```

2. **Personnalisation de la police**:
   Changez la police du message pour la rendre plus attrayante :
   ```dart
   Text(
     message,
     style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
   )
   ```

3. **Ajout d'une icône à la `MessageCard`**:
   Utilisez le widget `ListTile` pour ajouter une icône à côté de chaque message :
   ```dart
   ListTile(
     leading: Icon(Icons.message),
     title: Text(
       message,
       style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
     ),
   )
   ```

4. **Relancez l'application** pour voir les améliorations visuelles.

---

🥳 **Bravo**! Vous avez non seulement appris à travailler avec des Stateless Widgets, mais vous avez également découvert comment afficher des listes et personnaliser vos widgets. Pensez à toujours explorer la documentation Flutter pour en savoir plus sur les widgets et leurs propriétés.

---

## Partie 5 : Conception d'une Carte d'Information Personnelle
**Durée estimée : 45 minutes** 🕒

### Objectifs :
- Concevoir un Stateless Widget personnalisé à partir des spécifications données.
- Encourager la créativité et l'autonomie en laissant les étudiants décider de la mise en page et du style.

### Étapes :

1. **Comprendre la Tâche**:
    Votre mission, si vous l'acceptez, est de concevoir une carte d'information pour un profil utilisateur. Cette carte doit afficher au minimum le nom, le métier et une icône ou une image représentant l'utilisateur. Vous êtes libres de choisir le design, les couleurs, et toute autre information que vous souhaiteriez ajouter.

2. **Conception du Widget**:
   Créez un nouveau Stateless Widget, nommé `UserProfileCard`, qui prendra en entrée le nom, le métier, et l'image ou l'icône de l'utilisateur en bonus.

   Exemple de structure :
   ```dart
   class UserProfileCard extends StatelessWidget {
     final String name;
     final String job;
     final ImageProvider? image;

     UserProfileCard({required this.name, required this.job, this.image});

     @override
     Widget build(BuildContext context) {
       // Votre code ici
     }
   }
   ```

3. **Intégration dans l'Application**:
    Remplacez l'un des messages dans votre liste par votre nouveau widget `UserProfileCard`. 

4. **Liberté de Création**:
    C'est là que les choses deviennent intéressantes ! Utilisez tous les widgets, styles et couleurs que vous avez appris jusqu'à présent pour rendre cette carte aussi attrayante que possible. Pensez à consulter la documentation Flutter ou à chercher des idées en ligne si vous êtes bloqués. 🌍

5. **Bonus**:
   Pour ceux qui terminent rapidement et veulent un défi supplémentaire : ajoutez des fonctionnalités interactives à votre carte, comme un appui long pour afficher plus d'informations ou un double tap pour "aimer" le profil.

6. **Présentation et Feedback**:
    Une fois que tout le monde a terminé, prenez quelques minutes pour partager vos créations avec le groupe. C'est l'occasion d'obtenir des retours, d'échanger des astuces et de s'inspirer des autres. 💡

---

🚀 **Félicitations pour avoir terminé ce TP** ! La maîtrise des Stateless Widgets est essentielle pour devenir un développeur Flutter efficace. Continuez à explorer, à apprendre et à créer !
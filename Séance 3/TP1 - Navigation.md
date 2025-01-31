# TP Navigation et Routage avec Flutter 🚀

Bienvenue à cette session de travaux pratiques ! Aujourd'hui, nous allons explorer l'un des aspects fondamentaux de toute application mobile : la **navigation** et le **routage**. Prêt à naviguer dans le monde merveilleux de Flutter ? 🛶

Bien sûr, voyons cela !

---

## Partie 1: Création d'une page de détails et navigation basique 📄➡️📄

### Objectifs

- Initialiser un nouveau projet Flutter.
- Comprendre la structure basique d'une nouvelle page dans Flutter.
- Savoir comment naviguer vers une nouvelle page et revenir à la précédente.

### Étapes

1. **Initialisation du nouveau projet**

   Ouvrez votre terminal ou invite de commandes et entrez:

   ```
   flutter create mon_app_navigation
   ```

   Puis, naviguez dans le répertoire du projet:

   ```
   cd mon_app_navigation
   ```

2. **Ouverture du projet**

   Ouvrez le projet dans votre éditeur de code favori (par exemple, Visual Studio Code ou Android Studio).

3. **Création du fichier pour la page de détails**

   Créez un nouveau dossier `lib/pages` (ceci est juste une suggestion pour organiser vos fichiers, mais vous pouvez choisir une autre structure si vous le souhaitez). Dans ce dossier, créez un nouveau fichier `detail_page.dart`.

4. **Définition de la page de détails**

   Dans `detail_page.dart`, créez une nouvelle `StatefulWidget` appelée `DetailPage`. Assurez-vous d'importer le package Flutter nécessaire en haut du fichier:

   ```dart
   import 'package:flutter/material.dart';
   ```

   Structure de `DetailPage` :

   ```dart
   class DetailPage extends StatefulWidget {
       @override
       _DetailPageState createState() => _DetailPageState();
   }

   class _DetailPageState extends State<DetailPage> {
       @override
       Widget build(BuildContext context) {
           return Scaffold(
               appBar: AppBar(
                   title: Text('Page de Détails'),
               ),
               body: Center(
                   child: Text('Bienvenue sur la page de détails! 🌟'),
               ),
           );
       }
   }
   ```

5. **Navigation depuis la page principale**

   Retournez à `lib/main.dart`. Assurez-vous d'importer votre `detail_page.dart` en haut du fichier:

   ```dart
   import 'pages/detail_page.dart';
   ```

   Dans votre `MyApp` widget (ou équivalent, si vous avez renommé la classe de démarrage), ajoutez nouveau widget avec un bouton. Lorsque ce bouton est pressé, il devrait naviguer vers `DetailPage`:

   ```dart
   ElevatedButton(
       child: Text('Aller à la page de détails'),
       onPressed: () {
           Navigator.push(
               context,
               MaterialPageRoute(builder: (context) => DetailPage()),
           );
       },
   )
   ```

6. **Test de l'application**

   Lancez votre application avec `F5` (si vous êtes sur VS Code) ou le bouton "Run" de votre éditeur. Vous devriez voir votre page principale avec le bouton. En cliquant sur ce bouton, vous devriez être dirigé vers la "Page de détails".

---

## Partie 2: Passage de données entre les pages

**Durée estimée**: 1 heure et 15 minutes ⏳

### Objectifs

- Comprendre comment envoyer des données d'un écran à un autre.
- Utiliser les données transmises pour afficher un contenu dynamique.

### Étapes

1. **Mise à jour de `DetailPage`** :

   - Commencez par modifier le constructeur de `DetailPage` pour qu'il accepte une chaîne en tant que paramètre.

   ```dart
   class DetailPage extends StatefulWidget {
       final String message;

       DetailPage({required this.message});

       // Reste du code...
   }
   ```

   - Ensuite, à l'intérieur du widget `State`, utilisez cette variable pour afficher le message reçu.

   ```dart
   @override
   Widget build(BuildContext context) {
       return Scaffold(
           appBar: AppBar(title: Text('Page de Détails')),
           body: Center(
               child: Text(widget.message),
           ),
       );
   }
   ```

2. **Passage des données depuis `main.dart`** :

   - Dans le bouton de votre page principale (`main.dart`), lors de la navigation, passez une chaîne en tant qu'argument à `DetailPage`.

   ```dart
   ElevatedButton(
       child: Text('Aller à la page de détails'),
       onPressed: () {
           Navigator.push(
               context,
               MaterialPageRoute(
                   builder: (context) => DetailPage(message: 'Salut de la page principale!'),
               ),
           );
       },
   )
   ```

3. **Validation** :

   - Lancez votre application et cliquez sur le bouton pour naviguer vers `DetailPage`.
   - Assurez-vous que le message "Salut de la page principale!" s'affiche bien au centre de `DetailPage`.

4. **Approfondissement (optionnel)** :
   - Essayez de passer d'autres types de données, comme des nombres ou des objets personnalisés, pour mieux comprendre comment fonctionne le passage de données entre les écrans.

---

## Partie 3: Utilisation du routage nommé pour une navigation structurée

### Objectifs

- Apprendre les avantages du routage nommé pour une meilleure structure et une meilleure lisibilité.
- Mettre en œuvre le routage nommé pour naviguer entre plusieurs pages.
- Gérer les routes inconnues ou non définies.

### Étapes

1. **Configuration initiale des routes**

   Commencez par définir une map des routes dans votre `MaterialApp` dans `main.dart`. Cette map associe un nom de route (chaîne de caractères) à une fonction de construction de page.

   ```dart
   MaterialApp(
       initialRoute: '/',
       routes: {
           '/': (context) => MainPage(),
           '/details': (context) => DetailPage(),
       },
   )
   ```

   > NOTE : Vous serez peut-être ammené à créer vous même une nouvelle page "MainPage" et il vous faut enlever le passage de données à la DetailPage 😉

2. **Naviguer vers une nouvelle page**

   Pour naviguer en utilisant le routage nommé, vous allez remplacer votre ancienne méthode de navigation par `Navigator.pushNamed()`.

   Mettez à jour le code de votre bouton comme suit :

   ```dart
   ElevatedButton(
       child: Text('Aller à la page de détails'),
       onPressed: () {
           Navigator.pushNamed(context, '/details');
       },
   )
   ```

3. **Gestion des routes non définies**

   Il est possible que votre application tente d'accéder à une route que vous n'avez pas définie. Pour gérer ces scénarios, vous pouvez utiliser le paramètre `onGenerateRoute` de `MaterialApp`.

   ```dart
   onGenerateRoute: (settings) {
       // Si la route n'est pas trouvée dans la map des routes.
       if (settings.name == '/some-undefined-route') {
           return MaterialPageRoute(builder: (context) => NotFoundPage());
       }
       return null; // Si null, l'application utilise "routes" pour effectuer la navigation.
   }
   ```

   Ici, nous avons défini une simple page `NotFoundPage()` pour gérer les routes non trouvées. Vous pouvez personnaliser cette page selon vos besoins.

4. **Test de votre application**

   Lancez votre application et naviguez vers la page de détails en utilisant le bouton. Essayez également de naviguer vers une route non définie pour voir comment votre application gère ce cas.

5. **(Optionnel) Ajout de transitions personnalisées**

   Si vous voulez aller plus loin, vous pouvez ajouter des transitions personnalisées lors de la navigation entre vos pages. Pour cela, utilisez le paramètre `onGenerateRoute` pour définir la transition que vous souhaitez.

   💡 Notez que cela peut nécessiter des connaissances supplémentaires sur les animations Flutter, alors sentez-vous libre d'explorer ceci en fonction de votre niveau de confort et de temps.

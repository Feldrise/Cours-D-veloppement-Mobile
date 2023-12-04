# Travaux Pratiques : Maîtrise des Permissions dans Flutter 🛠️📲

## Partie 1 : Comprendre et Implémenter la Gestion des Permissions

### Objectifs
L'objectif de cette partie est de vous donner une compréhension approfondie de la gestion des permissions dans Flutter. Vous allez apprendre à demander, vérifier et gérer les permissions pour accéder aux fonctionnalités de l'appareil comme la caméra, le GPS, etc. 🌟

### Théorie : Comprendre les Permissions dans Flutter
1. **Permissions dans les Applications Mobiles**:
   - Les permissions sont des règles qui définissent quelles fonctionnalités de l'appareil votre application peut utiliser. Par exemple, accéder à la caméra, aux contacts, à la localisation, etc.
   - Les permissions aident à protéger la vie privée des utilisateurs en leur permettant de contrôler quelles données et fonctionnalités sont accessibles aux applications.

2. **Gestion des Permissions dans Android et iOS**:
   - Sur **Android**, les permissions sont déclarées dans le fichier `AndroidManifest.xml`. Il existe deux types de permissions : normales et dangereuses. Les permissions dangereuses nécessitent l'accord explicite de l'utilisateur.
   - Sur **iOS**, les permissions sont demandées au moment de l'utilisation et doivent être décrites dans le fichier `Info.plist`.

3. **Utilisation de Packages Flutter pour les Permissions**:
   - Flutter utilise des packages pour gérer les permissions de manière plus simple. Un package couramment utilisé est `permission_handler`.
   - Ce package permet de demander des permissions, de vérifier leur statut et de les gérer de manière uniforme sur Android et iOS.

### Exercices Pratiques
1. **Ajout de Permissions dans `AndroidManifest.xml` et `Info.plist`**:
   - Ajoutez la permission de localisation dans `AndroidManifest.xml`:
     ```xml
     <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
     <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
     ```
   - Ajoutez la description de la permission dans `Info.plist` pour iOS:
     ```xml
     <key>NSLocationWhenInUseUsageDescription</key>
     <string>This app needs access to location when in use.</string>
     ```

2. **Installation du Package `permission_handler`**:
   - Ajoutez `permission_handler` à votre `pubspec.yaml` et installez-le.

3. **Demande de Permission à l'Utilisateur**:
   - Créez une fonction pour demander la permission de localisation et affichez un message selon la réponse de l'utilisateur:
     ```dart
     Future<void> requestLocationPermission() async {
       var status = await Permission.locationWhenInUse.request();
       if (status.isGranted) {
         print("Permission accordée");
       } else if (status.isDenied) {
         print("Permission refusée");
       } else if (status.isPermanentlyDenied) {
         openAppSettings(); // Ouvre les paramètres de l'app pour changer la permission
       }
     }
     ```

4. **Tester la Demande de Permission**:
   - Intégrez cette fonction dans une interface utilisateur simple avec un bouton pour demander la permission.
   - Testez l'application sur différents appareils ou émulateurs pour voir comment la demande de permission se comporte.

5. **Gestion des Réponses de Permission**:
   - Modifiez votre application pour gérer correctement les différentes réponses de permission (accordée, refusée, refusée de manière permanente).
   - Affichez des messages appropriés à l'utilisateur dans chaque cas.

🚀 Ces exercices vous aideront à maîtriser la gestion des permissions dans vos applications Flutter. C'est une compétence essentielle pour garantir une bonne expérience utilisateur et respecter leur vie privée. Bon travail et n'hésitez pas à poser des questions !
# Travaux Pratiques : Création d'une Application de Galerie Photo avec Gestion des Permissions dans Flutter 📸📱

## Objectif Général
Concevoir une application Flutter qui accède à la galerie de photos de l'utilisateur. Vous apprendrez à demander et gérer les permissions pour accéder aux photos, et à afficher une sélection de photos sur l'écran.

## Partie 1 : Configuration Initiale

### Objectifs
- Mettre en place l'environnement de base pour le développement d'une application accédant aux photos de l'utilisateur.

### Étapes
1. **Création d'un Nouveau Projet Flutter**:
   - Ouvrez votre IDE et créez un nouveau projet Flutter.

2. **Configuration des Fichiers de Permission**:
   - Pour Android, dans `AndroidManifest.xml`, ajoutez :
     ```xml
     <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
     ```
   - Pour iOS, dans `Info.plist`, ajoutez :
     ```xml
     <key>NSPhotoLibraryUsageDescription</key>
     <string>Cette application nécessite l'accès à votre galerie pour afficher les photos</string>
     ```

## Partie 2 : Installation des Packages Nécessaires

### Objectifs
- Installer et configurer les packages Flutter nécessaires pour gérer l'accès aux photos.

### Étapes
1. **Ajoutez le Package `permission_handler`**:
   - Ajoutez `permission_handler` à votre `pubspec.yaml`.
   - Exécutez `flutter pub get`.

2. **Ajoutez le Package `image_picker`**:
   - Ajoutez `image_picker` à `pubspec.yaml` pour accéder aux photos.
   - Exécutez `flutter pub get`.

## Partie 3 : Demande de Permission d'Accès aux Photos

### Objectifs
- Apprendre à demander la permission d'accéder à la galerie de photos de l'utilisateur.

### Étapes
1. **Demande de Permission**:
   - Créez une fonction pour demander la permission d'accès aux photos en utilisant `permission_handler`.
   - Gérez les différents cas de réponse de l'utilisateur.

2. **Interface Utilisateur pour la Demande de Permission**:
   - Intégrez un bouton dans votre application qui, lorsqu'il est pressé, déclenche la demande de permission.

## Partie 4 : Affichage des Photos

### Objectifs
- Utiliser l'accès à la galerie pour afficher des photos sélectionnées par l'utilisateur.

### Étapes
1. **Sélection des Photos**:
   - Utilisez `image_picker` pour permettre à l'utilisateur de sélectionner des photos de sa galerie.
   - Gérez les cas où l'utilisateur refuse l'accès ou annule la sélection.

2. **Afficher les Photos Sélectionnées**:
   - Créez un widget pour afficher les photos sélectionnées.
   - Assurez-vous que les images s'affichent correctement une fois sélectionnées.

## Partie 5 : Test et Validation

### Objectifs
- Tester l'application pour s'assurer qu'elle fonctionne comme prévu sur différents appareils.

### Étapes
1. **Tests sur Divers Appareils**:
   - Lancez l'application sur différents émulateurs et appareils physiques.
   - Vérifiez que les permissions sont correctement demandées et gérées.

2. **Débogage**:
   - Identifiez et résolvez les problèmes qui surviennent lors de l'utilisation de l'application.
   - Assurez-vous que l'application se comporte correctement dans les différents cas de figure (permission accordée, refusée, etc.).

## Conclusion
Bravo 🌟! Vous avez créé une application Flutter qui gère efficacement les permissions pour accéder à la galerie de photos. Cet exercice enrichit votre expérience dans la gestion des permissions et l'interaction avec les médias stockés sur un appareil mobile.
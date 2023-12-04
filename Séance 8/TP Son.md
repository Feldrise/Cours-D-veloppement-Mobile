# Travaux Pratiques : Création d'une Application d'Enregistrement Vocal avec Gestion des Permissions dans Flutter 🎙️📱

## Objectif Général
Développer une application Flutter qui permet à l'utilisateur d'enregistrer sa voix. Cet exercice se concentrera sur la demande et la gestion des permissions pour l'accès au microphone, ainsi que sur l'enregistrement et la lecture des fichiers audio.

## Partie 1 : Configuration Initiale

### Objectifs
- Préparer l'environnement de développement pour une application d'enregistrement vocal.

### Étapes
1. **Création d'un Nouveau Projet Flutter**:
   - Lancez votre IDE et créez un nouveau projet Flutter.

2. **Configuration des Fichiers de Permission**:
   - Pour Android, dans `AndroidManifest.xml`, ajoutez :
     ```xml
     <uses-permission android:name="android.permission.RECORD_AUDIO"/>
     ```
   - Pour iOS, dans `Info.plist`, ajoutez :
     ```xml
     <key>NSMicrophoneUsageDescription</key>
     <string>Cette application a besoin d'accéder à votre microphone pour l'enregistrement vocal</string>
     ```

## Partie 2 : Installation des Packages Nécessaires

### Objectifs
- Installer et configurer les packages Flutter pour la gestion des permissions et l'enregistrement audio.

### Étapes
1. **Ajoutez le Package `permission_handler`**:
   - Ajoutez `permission_handler` à votre `pubspec.yaml`.
   - Exécutez `flutter pub get`.

2. **Ajoutez le Package `flutter_sound`**:
   - Ajoutez `flutter_sound` à `pubspec.yaml` pour gérer l'enregistrement et la lecture audio.
   - Exécutez `flutter pub get`.

## Partie 3 : Demande de Permission d'Accès au Microphone

### Objectifs
- Comprendre et implémenter la demande de permission pour l'utilisation du microphone.

### Étapes
1. **Demande de Permission**:
   - Créez une fonction pour demander la permission d'accès au microphone en utilisant `permission_handler`.
   - Gérez les différents cas de réponse de l'utilisateur.

2. **Interface Utilisateur pour la Demande de Permission**:
   - Intégrez un bouton dans votre application qui, lorsqu'il est pressé, demande la permission d'accès au microphone.

## Partie 4 : Enregistrement et Lecture Audio

### Objectifs
- Mettre en œuvre l'enregistrement et la lecture de fichiers audio dans l'application.

### Étapes
1. **Fonctionnalité d'Enregistrement**:
   - Utilisez `flutter_sound` pour permettre à l'utilisateur d'enregistrer sa voix.
   - Ajoutez des boutons pour démarrer et arrêter l'enregistrement.

2. **Fonctionnalité de Lecture**:
   - Ajoutez la possibilité de lire les enregistrements effectués.
   - Assurez-vous de gérer correctement les fichiers audio (stockage et accès).

## Partie 5 : Test et Validation

### Objectifs
- Tester l'application sur différents appareils pour s'assurer de son bon fonctionnement.

### Étapes
1. **Tests sur Divers Appareils**:
   - Testez l'application sur différents émulateurs et appareils physiques.
   - Vérifiez que les permissions sont correctement demandées et que l'enregistrement/lecture fonctionne comme prévu.

2. **Débogage**:
   - Identifiez et résolvez les problèmes rencontrés lors de l'utilisation de l'application.
   - Assurez-vous que l'application gère correctement les différents états de permission.

## Conclusion
Félicitations 🎉! Vous avez créé une application Flutter capable d'enregistrer et de lire des fichiers audio, tout en gérant les permissions nécessaires. Ce projet pratique renforce vos compétences dans la création d'applications interactives et multimédias sur Flutter.
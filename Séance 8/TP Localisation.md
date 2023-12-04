# Travaux Pratiques : Création d'une Application de Localisation avec Gestion des Permissions dans Flutter 🌍📱

## Objectif Général
Développer une application Flutter qui utilise la localisation de l'utilisateur. Vous apprendrez à demander et gérer les permissions de localisation, et à afficher la position actuelle de l'utilisateur sur l'écran.

## Partie 1 : Préparation de l'Environnement de Développement

### Objectifs
- Configurer votre environnement pour le développement d'une application de localisation.
- Comprendre l'importance des permissions pour accéder à la localisation.

### Étapes
1. **Créez un Nouveau Projet Flutter**:
   - Lancez votre IDE préféré et créez un nouveau projet Flutter.

2. **Configurez les Fichiers de Permission**:
   - Dans `AndroidManifest.xml`, ajoutez les permissions suivantes :
     ```xml
     <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
     <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
     ```
   - Pour iOS, dans `Info.plist`, ajoutez :
     ```xml
     <key>NSLocationWhenInUseUsageDescription</key>
     <string>Nous avons besoin de votre localisation pour cette démo</string>
     ```

## Partie 2 : Installation des Packages Nécessaires

### Objectifs
- Installer et configurer les packages Flutter nécessaires pour gérer la localisation et les permissions.

### Étapes
1. **Ajoutez le Package `permission_handler`**:
   - Modifiez votre `pubspec.yaml` pour inclure `permission_handler`.
   - Exécutez `flutter pub get` pour installer le package.

2. **Ajoutez le Package `geolocator`**:
   - Ajoutez `geolocator` à `pubspec.yaml` pour la gestion de la localisation.
   - Exécutez `flutter pub get`.

## Partie 3 : Demande de Permission de Localisation

### Objectifs
- Apprendre à demander la permission de localisation à l'utilisateur.

### Étapes
1. **Demande de Permission**:
   - Créez une fonction pour demander la permission de localisation en utilisant `permission_handler`.
   - Gérez les différents cas : permission accordée, refusée, et refusée de manière permanente.

2. **Interface Utilisateur pour la Demande de Permission**:
   - Créez un bouton dans votre application qui, lorsqu'il est pressé, déclenche la demande de permission.

## Partie 4 : Affichage de la Localisation

### Objectifs
- Utiliser la localisation de l'utilisateur pour afficher ses coordonnées GPS.

### Étapes
1. **Obtenir la Localisation Actuelle**:
   - Utilisez `geolocator` pour obtenir la position actuelle de l'utilisateur.
   - Gérez les erreurs potentielles (par exemple, localisation désactivée).

2. **Afficher la Localisation**:
   - Créez un widget pour afficher les coordonnées GPS (latitude et longitude) de l'utilisateur.
   - Mettez à jour l'interface utilisateur pour afficher la localisation dès qu'elle est disponible.

## Partie 5 : Test et Débogage

### Objectifs
- Tester l'application sur différents appareils et s'assurer qu'elle fonctionne correctement.

### Étapes
1. **Tests sur Émulateur/Appareil**:
   - Exécutez l'application sur un émulateur ou un appareil physique.
   - Vérifiez si les permissions sont correctement demandées et gérées.

2. **Débogage**:
   - Surveillez la console pour les erreurs ou problèmes.
   - Assurez-vous que la localisation s'affiche correctement lorsque la permission est accordée.

## Conclusion
Félicitations 🎉! Vous avez maintenant une application Flutter qui gère les permissions de localisation et affiche la position de l'utilisateur. Cet exercice vous donne une base solide pour intégrer des fonctionnalités de localisation dans vos futures applications mobiles.
# TP: Maîtriser les Widgets Stateful avec Flutter 🚀

---

## Introduction
Bienvenue dans ce TP dédié aux widgets Stateful dans Flutter! 😃 Aujourd'hui, vous allez plonger dans le monde des widgets interactifs en Flutter et voir comment ils peuvent être utilisés pour créer des applications dynamiques.

## Partie 1: Créer un Compteur
**Durée estimée**: 30 minutes

### Objectifs
- Comprendre et utiliser un `StatefulWidget` 
- Manipuler l'état local d'un widget pour refléter les interactions de l'utilisateur.

### Étapes:
1. **Configuration initiale**: Créez un nouveau projet Flutter et assurez-vous d'avoir une application avec une `Scaffold` de base.
  
2. **Création du Stateful Widget**: Dans le fichier `main.dart`, créez un nouveau `StatefulWidget` appelé `Counter`. 

    ```dart
    class Counter extends StatefulWidget {
      @override
      _CounterState createState() => _CounterState();
    }
    
    class _CounterState extends State<Counter> {
      int _count = 0;
    }
    ```

3. **Affichage du compteur**: Dans le widget `_CounterState`, utilisez un `Column` pour afficher un `Text` montrant la valeur actuelle de `_count` et un bouton pour augmenter cette valeur. 

    ```dart
    @override
    Widget build(BuildContext context) {
      return Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          Text('Compte actuel: $_count', style: TextStyle(fontSize: 24)),
          ElevatedButton(
            onPressed: () {
              setState(() {
                _count++;
              });
            },
            child: Text('Ajouter +1'),
          ),
        ],
      );
    }
    ```

4. **Testez votre application**: Exécutez votre application et assurez-vous que chaque fois que vous appuyez sur le bouton, la valeur du compteur augmente. 🎉

---

## Partie 2: Toggle Button
**Durée estimée**: 20 minutes

### Objectifs
- Utiliser un `StatefulWidget` pour gérer le changement d'état d'un bouton.
- Intégrer les concepts d'états et d'interactivité.

### Étapes:
1. **Création du Stateful Widget**: Dans le même fichier `main.dart`, créez un nouveau `StatefulWidget` appelé `ToggleButton`. 

    ```dart
    class ToggleButton extends StatefulWidget {
      @override
      _ToggleButtonState createState() => _ToggleButtonState();
    }
    
    class _ToggleButtonState extends State<ToggleButton> {
      bool _isActive = false;
    }
    ```

2. **Création de l'interface utilisateur**: Affichez un `ElevatedButton` qui change de couleur et de texte en fonction de l'état de `_isActive`.

    ```dart
    @override
    Widget build(BuildContext context) {
      return ElevatedButton(
        style: ElevatedButton.styleFrom(
          primary: _isActive ? Colors.green : Colors.red,
        ),
        onPressed: () {
          setState(() {
            _isActive = !_isActive;
          });
        },
        child: Text(_isActive ? 'Activé' : 'Désactivé'),
      );
    }
    ```

3. **Testez votre widget**: Intégrez votre `ToggleButton` dans l'interface principale de votre application et assurez-vous qu'il fonctionne comme prévu. 👍

---

🚀 Vous devriez maintenant avoir une meilleure compréhension de la façon dont Flutter gère les états locaux et comment les utiliser pour créer des interfaces utilisateur interactives.

# TP: Exploration Avancée des Widgets Stateful avec Flutter 🚀

---

## Partie 3: Créer un Slider Interactif
**Durée estimée**: 25 minutes

### Objectifs
- Utiliser le widget `Slider` pour permettre à l'utilisateur d'ajuster une valeur numérique.
- Afficher dynamiquement la valeur choisie par l'utilisateur.

### Étapes:
1. **Configuration du State**: Créez un nouveau `StatefulWidget` appelé `InteractiveSlider`. Ajoutez une variable d'état `_currentValue` initialisée à 0.

    ```dart
    class InteractiveSlider extends StatefulWidget {
      @override
      _InteractiveSliderState createState() => _InteractiveSliderState();
    }
    
    class _InteractiveSliderState extends State<InteractiveSlider> {
      double _currentValue = 0;
    }
    ```

2. **Intégration du Slider**: Ajoutez un widget `Slider` et un widget `Text` pour afficher la valeur courante.

    ```dart
    @override
    Widget build(BuildContext context) {
      return Column(
        children: [
          Slider(
            value: _currentValue,
            onChanged: (newValue) {
              setState(() {
                _currentValue = newValue;
              });
            },
            min: 0,
            max: 100,
          ),
          Text('Valeur actuelle: ${_currentValue.toStringAsFixed(2)}')
        ],
      );
    }
    ```

---

## Partie 4: Checklist Dynamique
**Durée estimée**: 40 minutes

### Objectifs
- Créer une liste d'articles.
- Permettre à l'utilisateur de cocher ou décocher les articles.
- Utiliser le widget `ListView.builder` pour un rendu dynamique.

### Étapes:
1. **Configuration du State**: Créez un nouveau `StatefulWidget` appelé `DynamicChecklist`. Initiez une liste d'articles avec une valeur booléenne pour indiquer si l'article est coché.

    ```dart
    class DynamicChecklist extends StatefulWidget {
      @override
      _DynamicChecklistState createState() => _DynamicChecklistState();
    }
    
    class _DynamicChecklistState extends State<DynamicChecklist> {
      List<Map<String, bool>> items = [
        {"Pain": false},
        {"Lait": false},
        {"Café": false},
      ];


    }
    ```

2. **Afficher la liste**: Utilisez le widget `ListView.builder` pour afficher dynamiquement chaque article de la liste.

    ```dart
    @override
    Widget build(BuildContext context) {
      return ListView.builder(
        itemCount: items.length,
        itemBuilder: (context, index) {
          return CheckboxListTile(
            title: Text(items[index].keys.first),
            value: items[index].values.first,
            onChanged: (bool? newValue) {
              setState(() {
                items[index][items[index].keys.first] = newValue!;
              });
            },
          );
        },
      );
    }
    ```

3. **Testez votre widget**: Intégrez votre `DynamicChecklist` dans l'interface principale de votre application. Essayez de cocher et décocher différents articles pour voir si tout fonctionne correctement.

---

## Partie 5: Barre de Progression Animée
**Durée estimée**: 30 minutes

### Objectifs
- Utiliser le widget `LinearProgressIndicator`.
- Animer la barre de progression pour simuler un téléchargement ou un chargement.

### Étapes:
1. **Configuration du State**: Créez un nouveau `StatefulWidget` appelé `AnimatedProgressBar`. Initiez une variable d'état `_progress` à 0.

    ```dart
    class AnimatedProgressBar extends StatefulWidget {
      @override
      _AnimatedProgressBarState createState() => _AnimatedProgressBarState();
    }
    
    class _AnimatedProgressBarState extends State<AnimatedProgressBar> {
      double _progress = 0;
    }
    ```

2. **Création de la barre de progression**: Ajoutez un widget `LinearProgressIndicator` et un bouton pour démarrer l'animation.

    ```dart
    @override
    Widget build(BuildContext context) {
      return Column(
        children: [
          LinearProgressIndicator(value: _progress),
          ElevatedButton(
            onPressed: _animateProgressBar,
            child: Text("Démarrer l'animation"),
          )
        ],
      );
    }
    ```

3. **Animation de la barre de progression**: Créez une fonction `_animateProgressBar` qui augmente progressivement la valeur de `_progress` jusqu'à ce qu'elle atteigne 1 (100%).

    ```dart
    void _animateProgressBar() async {
      while (_progress < 1) {
        await Future.delayed(Duration(milliseconds: 100));
        setState(() {
          _progress += 0.05;
        });
      }
    }
    ```

4. **Testez votre widget**: Intégrez votre `AnimatedProgressBar` dans votre application. Cliquez sur le bouton pour voir la barre de progression s'animer.

---

🔥 Bravo! Vous avez réussi à compléter des exercices avancés sur les widgets Stateful de Flutter. À travers ces exercices, vous avez renforcé votre compréhension des concepts d'état local et de mise à jour de l'interface utilisateur en fonction des interactions.

🚀 Poursuivez cette dynamique! Essayez d'imaginer d'autres widgets interactifs ou de les intégrer dans des applications plus complexes pour consolider davantage vos compétences. Et rappelez-vous, la pratique est la clé! 😉👍
---
title: Le Musicien du Midi (2/2)
categories: [m1ndbr34k_2025, Steganographie_m1ndbr34k_2025]
tags: [Steganographie]  
image: '/assets/images/m1ndbr34k/logo.png'
---

## 𝄞 Introduction

![Intro](/assets/images/m1ndbr34k_2025/Steganographie/Le_Musicien_du_Midi_2/intro.png)

---

## 𝄞𝄞 Solution

Dans ce challenge, un fichier **.midi** est fourni. Grâce au premier défi, les joueurs ont normalement pu se familiariser avec le format **MIDI**, ce qui leur permet d’aborder ce deuxième niveau dans de bonnes conditions.

En examinant ce fichier **MIDI** de la même manière que dans le premier challenge :

![midi](/assets/images/m1ndbr34k_2025/Steganographie/Le_Musicien_du_Midi_2/midi.webp)

On observe un spectre ne contenant aucune information exploitable, accompagné d’un son particulièrement désagréable.

Il est donc nécessaire de comprendre le fonctionnement interne d’un fichier **.midi** afin de pouvoir le manipuler et révéler le message caché.

--- 
## Note-on | Note-off

Les termes **note-on** et **note-off** désignent des événements spécifiques dans un fichier MIDI. Ils décrivent respectivement le début et la fin de la lecture d'une note.

- **Note-on** : indique le moment où une note commence à être jouée. Cet événement précise quelle note jouer, sa vélocité (intensité) et le canal MIDI utilisé.
    
Par exemple :
    
- **Note-on** pour la note "C4" (do central) avec une vélocité de 80 (sur une échelle de 0 à 127).
- **Note-off** : marque la fin de la note, c’est-à-dire quand elle cesse de sonner.

Ces deux événements sont fondamentaux pour la construction d’une séquence musicale en **MIDI**. Un fichier **MIDI** est donc essentiellement une suite de **note-on** et de **note-off**, définissant la durée et l'intensité de chaque note jouée.

Nous allons examiner les événements **note-on** dans notre fichier **.midi**.

Pour cela, plusieurs méthodes existent. Ici, nous allons utiliser le module **mido** en Python, qui permet de lire et manipuler des fichiers **MIDI**.

Voici un petit script :

```python
from mido import MidiFile

mid = MidiFile('remy.mid')

for i, track in enumerate(mid.tracks):
    print('Track {}: {}'.format(i, track.name))
    for msg in track:
        print(msg)
```

Ce script, réalisable en quelques secondes avec l'aide de la documentation officielle **Mido**, permet d'afficher les différents champs présents dans notre fichier **.mid**.

![midi2](/assets/images/m1ndbr34k_2025/Steganographie/Le_Musicien_du_Midi_2/midi2.webp)

On retrouve ici les événements **note_on** et **note_off**. Il est normal d’observer plusieurs événements liés aux mêmes notes (si vous avez bien compris leur fonctionnement).

On peut remarquer que les numéros de notes ressemblent à des valeurs **ASCII**. Nous allons donc extraire ces valeurs issues des événements **note_on** pour les interpréter en caractères ASCII.

Voici un script pour cela :

```python
from mido import MidiFile

mid = MidiFile('remy.mid')

FLAG = []

for i, track in enumerate(mid.tracks):
    print('Track {}: {}'.format(i, track.name))
    for msg in track:
        for i in str(msg).splitlines():
            if i.startswith('note_on'):
                chunk  = i.split()
                for m in chunk:
                    if m.startswith('note='):
                        valeur_note = int(m.split('=')[1])
                        FLAG.append(valeur_note)

for i in FLAG:
    print(chr(i), end="")
```
En récupérant la valeur des champs **note_on** et en les convertissant en caractères **ASCII**, nous pouvons ainsi reconstituer le FLAG !

![flag](/assets/images/m1ndbr34k_2025/Steganographie/Le_Musicien_du_Midi_2/flag.webp)

𝄞 FLAG : `MB{note_hidden_message}`𝄞

# Projet de Traitement Audio WAV

## Description
Ce projet est une application console en C++ permettant de manipuler des fichiers audio au format WAV. Il permet de générer des sons à partir d'une partition musicale textuelle et de les sauvegarder au format WAV ou de les jouer directement.

## Structure du Projet
- `biblioWAV.h` : Fichier d'en-tête contenant les déclarations des fonctions de manipulation WAV
- `biblioWAV.cpp` : Implémentation des fonctions de génération et lecture WAV
- `main.cpp` : Programme principal gérant la lecture des partitions et la génération sonore

## Fonctionnalités Détaillées

### Génération de Sons
- Génération de sons sinusoïdaux purs
- Contrôle de la fréquence (hauteur du son)
- Contrôle de la durée des notes
- Fondu d'entrée/sortie (fade in/out) pour éviter les clics
- Stéréo (2 canaux)

### Format de Partition
Le programme accepte des fichiers texte contenant:
- Tempo en BPM (battements par minute)
- Notes au format: `<octave> <note> <altération> <durée>`
  - Octave: numéro de l'octave (ex: 4)
  - Note: do, ré, mi, fa, sol, la, si
  - Altération: # (dièse), b (bémol) ou - (naturel)
  - Durée: 1 (ronde), 2 (blanche), 4 (noire), etc.

Exemple de partition:
```
120 // Tempo
4 do - 4  // do4 noire
4 ré # 8  // ré#4 croche
4 mi - 2  // mi4 blanche
```

### Manipulation WAV
- Format PCM 16 bits
- Fréquence d'échantillonnage: 44100 Hz
- Stéréo (2 canaux)
- Amplitude maximale: 32760

## Installation et Prérequis

### Matériel
- PC avec Windows (7/8/10/11)
- Carte son compatible Windows
- Haut-parleurs ou écouteurs

### Logiciel
- Visual Studio 2022
- Windows SDK 10.0+
- Compilateur supportant C++11

## Compilation et Exécution

1. Cloner le dépôt ou télécharger les sources
2. Ouvrir `Nick_Suebang-TP02-2333658.sln` dans Visual Studio
3. Sélectionner la configuration:
   - Debug/Release
   - x64 recommandé
4. Compiler (F7)
5. Exécuter (F5)

## Utilisation

### Ligne de Commande
```bash
Nick_Suebang-TP02-2333658.exe <fichier_partition.txt>
```

### Fonctions Principales
```cpp
// Jouer une séquence de notes
void JouerSons(float frequences[], float dureesMillisecondes[], int n);

// Sauvegarder en WAV
bool EcrireSons(float frequences[], float dureesMillisecondes[], int n, 
                const string& nomFichierSortie);

// Lire une partition
bool lirePartition(const string NomFichier, float frequences[], 
                  float dureesEnMillisecondes[], int& taille);
```

## Format WAV en Détail

### En-tête RIFF (12 octets)
```
Offset  Taille  Description
0-3     4       "RIFF"
4-7     4       Taille totale - 8
8-11    4       "WAVE"
```

### En-tête Format (24 octets)
```
12-15   4       "fmt "
16-19   4       Taille section format (16)
20-21   2       Format audio (1 = PCM)
22-23   2       Nombre canaux (2)
24-27   4       Fréquence échantillonnage (44100)
28-31   4       Débit binaire moyen
32-33   2       Bloc d'alignement
34-35   2       Bits par échantillon (16)
```

### Section Données
```
36-39   4       "data"
40-43   4       Taille des données
44+     ...     Données audio (échantillons)
```

## Traitement du Signal

### Génération des Sons
1. Calcul de la fréquence selon la note
2. Génération d'une onde sinusoïdale
3. Application d'une enveloppe (fade in/out)
4. Quantification 16 bits

### Paramètres Audio
- Fréquence d'échantillonnage: 44100 Hz
- Résolution: 16 bits
- Canaux: 2 (stéréo)
- Volume maximal: 32760 (-0.5 dB)

## Gestion des Erreurs

### Validation des Entrées
- Vérification du fichier partition
- Validation du format des notes
- Contrôle des valeurs de fréquence
- Vérification des durées

### Messages d'Erreur
- Fichier introuvable
- Format de partition invalide
- Erreur d'écriture WAV
- Erreur de lecture

## Performances et Limitations

### Capacités
- Jusqu'à 1000 notes par partition
- Fichiers WAV jusqu'à 4 GB
- Fréquences: 20 Hz à 20000 Hz

### Limitations
- Format PCM uniquement
- Pas de compression
- Pas d'effets audio complexes
- Mémoire limitée par RAM disponible

## Support et Contact

### Signalement de Bugs
1. Vérifier la dernière version
2. Documenter le problème
3. Créer une issue sur GitHub

### Contribution
1. Fork du projet
2. Branche feature/bugfix
3. Pull Request avec description

### Contact
- GitHub: [profil]
- Email: [adresse]

## Licence
Projet sous licence MIT
Copyright (c) 2024 Nick Suebang

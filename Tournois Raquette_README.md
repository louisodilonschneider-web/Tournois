# 🏓🏸 Tournoi EPS — Gestionnaire de tournois Tennis de Table & Badminton

> Application web autonome destinée aux enseignants d'EPS et aux responsables UNSS.  
> Un seul fichier HTML, aucune installation, aucune connexion internet requise.

---

## Sommaire

1. [Présentation](#présentation)
2. [Démarrage rapide](#démarrage-rapide)
3. [Fonctionnalités détaillées](#fonctionnalités-détaillées)
   - [Onglet 1 — Configuration](#onglet-1--configuration)
   - [Onglet 2 — Élèves & Poules](#onglet-2--élèves--poules)
   - [Onglet 3 — Phase de poules](#onglet-3--phase-de-poules)
   - [Onglet 4 — Tournoi final](#onglet-4--tournoi-final)
   - [Onglet 5 — Classement général](#onglet-5--classement-général)
4. [Modes et formats de tournoi](#modes-et-formats-de-tournoi)
5. [Mode UNSS](#mode-unss)
6. [Outils transversaux](#outils-transversaux)
7. [Import d'élèves](#import-délèves)
8. [Export et impression](#export-et-impression)
9. [Mode démo](#mode-démo)
10. [Réinitialisation](#réinitialisation)
11. [Compatibilité technique](#compatibilité-technique)
12. [Structure du fichier](#structure-du-fichier)

---

## Présentation

Cette application permet de gérer intégralement un tournoi sportif scolaire, de la saisie des élèves jusqu'au classement final. Elle couvre deux contextes d'utilisation :

| Contexte | Description |
|---|---|
| **EPS (cours)** | Utilisation en classe, saisie rapide, tournoi direct |
| **UNSS (compétition)** | Niveaux par joueur, groupes/classes, répartition équilibrée des poules |

---

## Démarrage rapide

1. Ouvrir le fichier `tournoi-eps.html` dans un navigateur (Chrome, Firefox, Edge, Safari)
2. **Onglet Configuration** : choisir le sport, le mode (EPS ou UNSS) et les règles de match
3. **Onglet Élèves & Poules** : saisir les élèves ou utiliser les données de test
4. Générer les poules, les valider
5. **Phase de poules** : saisir les scores match par match
6. Cliquer sur **Terminer les poules** pour lancer le tournoi
7. **Tournoi final** : saisir les scores dans n'importe quel ordre
8. **Classement** : mis à jour en temps réel

> **Astuce** : utilisez le bouton ⚡ **Mode démo** dans la barre latérale pour remplir automatiquement tous les scores et voir le tournoi complet en quelques secondes.

---

## Fonctionnalités détaillées

### Onglet 1 — Configuration

#### Sport
- 🏓 Tennis de table
- 🏸 Badminton

#### Mode
- **EPS** : saisie simple, pas de notion de niveau ni de groupe
- **UNSS** : chaque élève a un niveau (1 à 5) et un groupe/classe

#### Règles de match
Deux systèmes de score disponibles, configurables séparément pour les poules et le tournoi :

| Paramètre | Description | Exemple |
|---|---|---|
| **Points** | Premier joueur à atteindre N points gagne | Premier à 11 pts |
| **Sets** | Meilleur des N sets, chaque set à M points | Meilleur des 3 sets à 11 pts |

#### Format du tournoi
Voir la section [Modes et formats de tournoi](#modes-et-formats-de-tournoi).

---

### Onglet 2 — Élèves & Poules

#### Saisie des élèves
- Saisie manuelle (prénom, nom, et en mode UNSS : niveau 1-5, groupe/classe)
- Import rapide par copier-coller (texte)
- Import depuis un fichier PDF (extraction automatique du texte)
- Chargement de données de test : 12, 15, 16 ou 18 élèves répartis sur 3 groupes

#### Composition des poules
Quatre types de composition disponibles :

| Type | Principe |
|---|---|
| **Hétérogène** | Mélange des niveaux dans chaque poule (un fort, un moyen, un faible) |
| **Homogène** | Niveaux similaires regroupés ensemble |
| **Mixte** | Mélange aléatoire |
| **Libre** | Aucune contrainte |

> En mode UNSS avec composition hétérogène, l'algorithme garantit en plus qu'**aucun élève du même groupe** ne se retrouve dans la même poule (sous réserve de faisabilité mathématique).

#### Taille des poules
3, 4 ou 5 joueurs par poule.

#### Tirage
- **Aléatoire** : chaque clic sur « Nouveau tirage » génère une répartition différente
- **Manuel** : glisser-déposer les élèves dans les poules souhaitées

Un **aperçu** est présenté avant validation. Les conflits de groupe résiduels sont signalés en rouge.

---

### Onglet 3 — Phase de poules

- Tous les matchs d'une poule sont listés dans un ordre calculé pour **éviter qu'un joueur enchaîne deux matchs consécutifs** (algorithme de planification avec temps de repos)
- Saisie des scores directement dans le tableau (mode points) ou via une fenêtre de dialogue (mode sets)
- **Classement en temps réel** de chaque poule, visible en en-tête
- Le bouton **Terminer les poules** apparaît quand tous les matchs sont joués

Critères de classement en poule :
1. Points de victoire (2 pts victoire, 1 pt défaite)
2. Différence de points marqués/encaissés

---

### Onglet 4 — Tournoi final

- Le tableau est généré automatiquement depuis le classement des poules
- **Remplissage libre** : cliquer sur n'importe quel match disponible (encadré en orange) dans n'importe quel ordre
- Les résultats se propagent automatiquement vers les tours suivants et vers les tableaux de consolation
- Les **sauts de tour (byes)** sont automatiquement attribués aux meilleures têtes de série quand le nombre de joueurs n'est pas une puissance de 2

#### Tableaux de consolation
Dès l'ouverture de l'onglet, les tableaux de consolation sont affichés avec des emplacements « En attente ». Ils se remplissent automatiquement au fur et à mesure que les matchs du tableau principal sont joués :

- Perdants des 8èmes → tableau de consolation des 8èmes
- Perdants des quarts → tableau de consolation des quarts
- Perdants des demi-finales → petite finale (3e/4e place)
- etc.

**Personne ne reste sans jouer.** Chaque élève joue jusqu'au bout et obtient une position précise dans le classement.

---

### Onglet 5 — Classement général

- Mis à jour en temps réel après chaque résultat
- Classement du 1er au dernier, avec médailles 🥇🥈🥉 pour le podium
- Pour chaque joueur : poule d'origine et parcours détaillé
- Ordre UNSS : vainqueur principal → vainqueur consolation → perdant principal → perdant consolation, par niveau de tour

---

## Modes et formats de tournoi

### 🔄 Consolation (recommandé EPS)
Chaque joueur éliminé du tableau principal rejoint un **tableau de consolation parallèle** correspondant à son tour d'élimination. Tout le monde joue jusqu'à la fin.

- Un perdant en quarts peut encore viser la 5e place
- Classement précis du 1er au dernier

### ⚡ Double élimination (recommandé compétition)
On ne quitte le tournoi qu'après **deux défaites**. Format inspiré des compétitions UNSS.

- Tableau principal (Winners Bracket)
- Tableau de repêchage (Losers Bracket)
- Grande Finale : vainqueur WB vs vainqueur LB

### 🌐 Tournoi unique
Tous les élèves, quelle que soit leur poule d'origine, sont réunis dans **un seul grand tableau** avec consolation. Idéal pour les petits effectifs ou quand on veut éviter la séparation en Tournoi A/B.

---

### Gestion des effectifs

| Nombre de joueurs | Organisation |
|---|---|
| < 8 joueurs | Tournoi unique automatique |
| ≥ 8 joueurs | Scindé en **Tournoi A** (meilleurs de poule) et **Tournoi B** (autres) |
| Format « Tournoi unique » | Tous ensemble, quelle que soit la taille |

---

## Mode UNSS

Activé depuis l'onglet Configuration. Fonctionnalités supplémentaires :

- **Niveau** par joueur : de 1 (débutant) à 5 (expert)
- **Groupe/Classe** par joueur (ex : 6A, 5B)
- Composition hétérogène intelligente : les forts sont répartis dans différentes poules, les élèves du même groupe sont séparés
- Affichage des badges de niveau dans les aperçus de poules
- Colonne groupe visible dans la liste des élèves

---

## Outils transversaux

### Barre latérale

| Bouton | Fonction |
|---|---|
| ⚙️ Configuration | Retour aux paramètres |
| 👥 Élèves & Poules | Saisie et répartition |
| 🏅 Phase de poules | Saisie des résultats de poule |
| 🏆 Tournoi final | Tableaux et scores |
| 📊 Classement | Résultats finaux |
| ⚡ Mode démo | Remplissage automatique |
| 🔄 Réinitialiser | Remise à zéro complète |

---

## Import d'élèves

### Import texte
Ouvrir le dialogue « Import d'élèves » (onglet Texte).  
Un élève par ligne, dans l'un de ces formats :

```
Prénom Nom
Prénom Nom Niveau Groupe
```

**Exemples :**
```
Marie Dupont
Jean Martin 3 6A
Sophie Bernard 4 6B
```

### Import PDF
Onglet PDF dans le même dialogue. Deux méthodes :

1. **Glisser-déposer** un fichier PDF sur la zone prévue
2. **Cliquer** pour parcourir et sélectionner le fichier

L'application tente d'extraire automatiquement les noms depuis le PDF. Si l'extraction automatique échoue (PDF scanné, encodage complexe), la zone de texte s'affiche vide et permet une saisie manuelle.

> **Note** : l'extraction PDF fonctionne bien pour les PDF générés par ordinateur (listes d'appel, exports de logiciels de vie scolaire). Les PDF scannés/photographiés ne contiennent pas de texte extractible.

### Données de test
Le bouton **🧪 Données de test** charge instantanément un jeu d'élèves fictifs :

| Option | Élèves | Groupes | Niveaux couverts |
|---|---|---|---|
| 12 élèves | 12 | 6A, 6B, 6C | 1 à 5 |
| 15 élèves | 15 | 6A, 6B, 6C | 1 à 5 |
| 16 élèves | 16 | 6A, 6B, 6C | 1 à 5 |
| 18 élèves | 18 | 6A, 6B, 6C | 1 à 5 |

---

## Export et impression

Chaque onglet dispose d'une barre d'export :

| Onglet | Options disponibles |
|---|---|
| Élèves & Poules | 📥 CSV élèves · 🖨️ Imprimer liste |
| Phase de poules | 🖨️ Imprimer poules |
| Tournoi final | 🖨️ Imprimer tableau |
| Classement | 📥 CSV classement · 🖨️ Imprimer classement |

### Impression
L'impression est optimisée : la barre latérale, les boutons et les barres d'outils disparaissent. Seul le contenu de l'onglet en cours s'imprime.

### Export CSV
Les fichiers CSV sont encodés en UTF-8 avec BOM (compatible Excel). Deux formats :

**CSV élèves** (mode EPS) :
```
Prénom,Nom
Marie,Dupont
Jean,Martin
```

**CSV élèves** (mode UNSS) :
```
Prénom,Nom,Niveau,Groupe
Marie,Dupont,3,6A
Jean,Martin,4,6B
```

**CSV classement** :
```
Position,Joueur,Poule,Parcours
1,"MARTIN Lucas","Poule A","Finale 🏆 Principal"
2,"BERNARD Emma","Poule B","Finale ✓ Consolation"
```

---

## Mode démo

Le bouton ⚡ **Mode démo** dans la barre latérale remplit automatiquement tous les scores avec des résultats aléatoires crédibles.

**Prérequis** : la phase de poules doit être lancée (onglet Phase de poules visible).

**Déroulement :**
1. Une fenêtre de progression s'affiche
2. Les matchs de poules sont remplis un à un (avec délai animé)
3. Si les poules se terminent, le tournoi est construit automatiquement
4. Les matchs du tournoi sont remplis dans l'ordre de disponibilité
5. À la fin, l'onglet Classement s'affiche

Le bouton **✕ Arrêter** interrompt le mode démo à tout moment.

> **Cas d'usage** : démonstration à des élèves, test rapide d'une configuration, vérification du classement final avant le vrai tournoi.

---

## Réinitialisation

Le bouton 🔄 **Réinitialiser** (barre latérale, en rouge) remet l'application à son état initial après confirmation :

- Suppression de tous les élèves
- Suppression de toutes les poules et matchs
- Suppression du tournoi et des classements
- Retour à l'onglet Configuration
- Tous les onglets sauf Configuration redeviennent inaccessibles

> ⚠️ Cette action est irréversible. Les données ne sont pas sauvegardées automatiquement. Pour conserver un classement, exporter le CSV ou imprimer avant de réinitialiser.

---

## Compatibilité technique

| Critère | Détail |
|---|---|
| **Fichier unique** | Un seul fichier `.html`, sans dépendance externe |
| **Connexion internet** | Non requise |
| **Installation** | Aucune |
| **Navigateurs** | Chrome 90+, Firefox 88+, Edge 90+, Safari 14+ |
| **Taille du fichier** | ~75 Ko |
| **Polices** | Polices système (Arial Narrow, system-ui) — aucun chargement réseau |
| **Stockage** | Aucune donnée persistée (tout est en mémoire, perdu à la fermeture) |
| **Accessibilité mobile** | Responsive design, sidebar réduite sur petit écran |

---

## Structure du fichier

```
tournoi-eps.html
├── <style>          CSS complet inline (variables, composants, print)
├── <body>
│   ├── #sidebar     Navigation + boutons transversaux
│   └── #main
│       ├── #tab0    Configuration
│       ├── #tab1    Élèves & Poules
│       ├── #tab2    Phase de poules
│       ├── #tab3    Tournoi final
│       └── #tab4    Classement
│   ├── #modal-import   Import texte / PDF
│   ├── #modal-match    Saisie de score
│   ├── #toast          Notifications
│   └── #demo-overlay   Overlay mode démo
└── <script>         ~77 fonctions JavaScript
    ├── STATE         Objet S (état global)
    ├── NAVIGATION    goTab, enTab
    ├── CONFIG        setSport, setMode, setFmt, validateConfig
    ├── STUDENTS      addStudent, renderStudents, compOrder
    ├── POULES        buildPoulesMatches, schedRest, renderPoulesM
    ├── TOURNAMENT    buildCons, buildDE, propagate, refreshT
    ├── RANKING       updateRk, consSt, deSt
    ├── EXPORT        exportCSV, printTab, dlCSV
    ├── IMPORT PDF    handlePdfFile, doImport
    ├── DEMO MODE     runAutoDemo, fillRandomScore
    └── UTILS         resetAll, showToast, sleep
```

---

## Algorithmes clés

### Distribution hétérogène des poules (snake UNSS)
Les élèves sont triés par niveau décroissant, mélangés aléatoirement à l'intérieur de chaque groupe de niveau, puis distribués en zigzag (snake) dans les poules. Un post-traitement par échanges garantit qu'aucun élève du même groupe ne partage une poule (dans la limite du possible).

### Planification des matchs de poules avec repos
Algorithme glouton : les matchs sont réordonnés pour qu'aucun joueur ne joue deux matchs consécutifs. Si aucun échange sans conflit n'est possible, le prochain match disponible est placé à la suite.

### Bracket de consolation pré-câblé
Les tableaux de consolation sont construits **à l'initialisation** du tournoi avec des emplacements vides liés aux matchs du tableau principal via des références `fl[]`. Quand un match est joué, le perdant est automatiquement injecté dans son emplacement de consolation par propagation en cascade récursive.

### Byes en cascade
Quand un joueur se retrouve seul dans un match (adversaire `null`), le match est immédiatement résolu en bye et la résolution se propage récursivement à tous les matchs en aval, garantissant qu'aucun match ne reste bloqué.

---

*Application développée pour un usage pédagogique EPS/UNSS. Fichier autonome, redistribuable librement.*

# TP6
### Test & outils de corrections
:alarm_clock: Remise le [15 novembre 23h59](https://www.timeanddate.com/countdown/generic?iso=20201115T235959&p0=165&msg=Remise+TP4&font=cursive)
## Objectifs
## Consignes à respecter
- Indications de type (*Type hints*)
- Respecter [guide de codage](https://github.com/INF1007-Gabarits/Guide-codage-python) et normes pep8
- Attention aux:
  - En-têtes de fichier et fonction (voir règles 33 et 89 du guide, d'autres exemples [ici](https://www.datacamp.com/community/tutorials/docstrings-python))
  - Chiffres magiques
- noms de variables et fonctions adéquats (concis, compréhensibles)
- Aucun ajout de librairie supplémentaire qui altérerait l'esprit du TP. Cet exercice travaille beaucoup avec les matrices. S'il est vrai que du code très efficace pour gérer les opérations matricielles a déjà été écrit par d'autres (librairie *numpy* par exemple), l'intérêt ici est que vous développiez une compréhension du code, pas simplement d'appeler des fonctions haut niveau qui font tout le travail pour vous.. Par exemple la fonction transposer() doit être implémentée directement, l'utilisation du numpy.T est triviale et ne demandes par vraiment de compréhension de votre part.
## Mise en contexte
Ce 4e TP s'orchestre autour du [jeu 2048](https://fr.wikipedia.org/wiki/2048_(jeu_vid%C3%A9o)), devenu très populaire lors de sa sortie en 2014. Si vous avez besoin d'un petit rafraîchissement mémoire ou si vous ne connaissez pas du tout le jeu, suivez le lien Wikipédia.
L'objectif est donc de "combiner" successivement des tuiles occupées par les mêmes puissances de 2 afin d'obtenir le nombre **2048** et gagner la partie. À chaque tour de jeu, on déplace l'ensemble des tuiles dans une des 4 directions de base (haut, bas, gauche, droite) et une nouvelle tuile **2** apparaît à un emplacement non occupé aléatoire.    

![grille_2048](https://upload.wikimedia.org/wikipedia/commons/thumb/8/83/2048_Monotonicity.png/270px-2048_Monotonicity.png)
> Grille du jeu en cours de partie  

Attention! C'est un jeu dangereusement satisfaisant et addictif.  

![grille_2048_victoire](https://upload.wikimedia.org/wikipedia/commons/thumb/2/28/2048_finished_game.png/270px-2048_finished_game.png)

> Victoire, la tuile 2048 est obtenue après de tonitruants efforts!  

Vous aurez donc à compléter la logique du jeu (*2048/logique.py)* et implémenter une série de tests (*2048/tests.py* afin de vérifier que les nombreux états limites de votre implémentation sont fonctionnels. Nous avons complété l'interface graphique du jeu (*2048/gui.py*) et vous n'avez pas a y toucher. L'acronyme anglais *GUI* signifie *graphical user interface*.

## Partie 1: Logique du jeu
Le fichier *logique.py* ne contient pas de *main*, mais seulement les fonctions qui seront appelées par le code de l'interface graphique (*gui.py*).
Référez-vous aux constantes définies dans le fichier *constantes.py* afin de limiter l'utilisation de *chiffres magiques*. Vous pouvez définir de nouvelles constantes si cela vous est utile.

L'ordre de définition des fonctions suit un ordre de lecture logique, mais vous pouvez remplir le code dans l'ordre que vous désirez.  

Il y a 3 groupes de fonctions à implémenter:
### 1. Les fonctions responsables de l'état du jeu (initialier la partie, état actuel de la partie) 
```python
# Initialisation du jeu.
def demarrer_jeu():
  ...
  return ...
```
```python
# Retourne une nouvelle matrice 4x4 remplie de 0.
def initialiser_nouvelle_matrice():
  ...
  return ...
```
```python
# Ajoute une nouvelle tuile 2 ou 4 dans la grille à un emplacement vide aléatoire def ajouter_nouveau_2_ou_4(grille):
  ...
  return ...
```
```python
# Retourne l'état du jeu.
def get_etat_jeu_courant(grille):
  ...
  return ...
```
### 2. Les fonctions d'opérations sur les matrices (compression, inversion, fusion, etc.)

Dans le but de limiter la taille du code à écrire, nous allons effectuer un petit tour de passe-passe. Même s'il existe 4 directions de mouvement pour le joueur (haut, bas, gauche, droite), la procédure sera de transformer les matrices (avec les opérations transposition et inverse) et d'obtenir la *matrice équivalente* qui nécessiterait une translation **à gauche** afin de réaliser l'opération (droite, haut, bas) réellement voulue.

Ainsi, les opérations comprimer(matrice) et fusionner(matrice) n'ont a être définies que pour une compression & fusion vers la gauche.
```python
# Comprime la matrice de jeu.
def comprimer(matrice):     ...
return ...
```
```python
# Fusionne les éléments de la matrice de jeu après une compression 
def fusionner(matrice):
  ...
  return ...
```
```python
# Produit la matrice inverse d'une matrice
def inverser(matrice):
  ...
  return ...
```
```python
# Produit la matrice transposée d'une matrice 
def transposer(matrice):
  ...
  return ...
```
### 3. Les 4 fonctions définissant les actions du joueur (déplacement haut,bas,gauche,droite)<

Comme expliqué au point 2, le mouvement de base est la translation à gauche. Les 3 autres mouvements sont définis en fonction celui-ci.
```python
# Bouge la matrice vers la gauche
def faire_translation_gauche(matrice): 
  ...
  return ...
```
```python
def faire_translation_droite(matrice):
    ...
    return ...
```
```python
#  Bouge la matrice en haut
def faire_translation_haut(matrice):
    ...
    return ...
```
```python
#  Bouger la matrice en bas
def faire_translation_bas(matrice):
    ...
    return ...
```

## Partie 2: Rédactions des tests
Comme vu en classe, il est très important de tester extensivement le code écrit. C'est malheureusement une pratique souvent ignorée par manque de temps ou d'intérêt. Mais comme pour toute autre bonne pratique ee génie informatique/logiciel, les conséquences négatives d'une telle décision finissent par nous rattraper tous.

Dans le cas spécifique d'un jeu, qui dépend d'une interaction constante entre le joueur et la logique de jeu (à travers les commandes), les tests sont encore plus importants. Il vous sera donc demandé de tester l'ensemble des fonctions définies dans *logique.py*

Le fichier *tests.py* contient un exemple de code rédigé pour tester UN cas d'utilisation d'UNE fonction (à noter que le test en tant que tel n'est pas implémenté). 
```python
# Tests 
def tester_inverser_matrice_identite():
    matrice = [[1, 0, 0, 0],
               [0, 1, 0, 0],
               [0, 0, 1, 0],
               [0, 0, 0, 1]]
    ...
    return ...
return ...

# Affichage des tests
def ecrire_resultat_test(test, resultat):
    reussite_ou_echec = ("Échec", "Réussite")[resultat]
    print(test + "..." + reussite_ou_echec)


if __name__ == '__main__':
    ecrire_resultat_test(tester_inverser_matrice_identite.__name__, tester_inverser_matrice_identite())
```

### À faire

Votre code doit tester les cas (valeurs d'entrées et d'exécutions) **limites** des fonctions afin de repérer d'éventuelles erreurs de logique. Il vous est demandé de rédiger un petit rapport en Markdown (créez un fichier rapport_tests.md dans le dépôt git) où vos expliquerez vos choix en termes de tests et valeurs limites. Discutez de votre stratégie de tests et du choix des valeurs testées)

**N'oubliez pas d'ajouter (git add) le fichier dans le *tracking* Git. Sinon il ne sera pas ajouté sur GitHub.**

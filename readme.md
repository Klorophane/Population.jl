# Populations.jl
Génère une simulation dans l'espace et le temps de plusieurs populations dont l'interaction est qualifiée par les modèles suivants:

   ***Relation prédateur-proie*** (Les prédateurs mangent les prois)
   ***Relation de competition*** (Les prédateurs compétitionnent entre eux, les prois compétitionnent parfois entre elles aussi)
   ***Relation de symbiose*** (Les deux especes prospèrent conjointement)
    ***Relation de parasitisme*** (L'une des espèces prospère au dépens de l'autre)

L'ampleur de ces relations est influencée par les traits de la cellule géographique et ceux de la population en question. L'affichage graphique se fait sur une grille de couleurs. Il est possible d'appliquer des masques à la grille pour mettre en évidence des attributs spécifiques (seulement voir la nourriture dans chaque case par exemple).

## Populations
Chaque population possède les attributs suivants

    1. Taille de la population
    2. Paramètres
        - Temps de gestation
        - Taux de reproduction
        - Taux de mortalité
        - Coefficient de déplacement
        - Dispersion
    3. Traits

Les paramètres dépendent des traits de la cellule et des traits de la population qui l'occupe.

## Cellules
Chaque représente une aire geographique de 1 $\textrm{km}^2$. Elles renferment l'information complète sur chaque population présentes. Elles possèdent un certain nombre de traits (type de terrain, température, etc...) ayant un impact sur les diverses populations présentes.

## Grille
La grille est crée comme une liste de cellules. Chaque cellule est initialisée avec des traits et des populations de façon à créer le monde désiré. La grille spatiale est choisie de sorte que les conditions aux limites soient
périodiques.

L'évolution temporelle de la grille se fait par défaut à chaque jour. À chaque pas de la simulation, il faut :

    1. Effectuer les déplacements des populations de chaque case. Il faut
    d'abord calculer les mouvement de chacune des populations avant d'effectuer
    le mouvement.

    2. Effectuer l'évolution des populations. D'après les nouvelles conditions,
    effectuer l'évolution des populations (taille et paramètres).

    3. Effectuer l'évolution des cellules (ressources, climat).


## Dictionnaire des traits de cellule :

### Types de terrain
***Les plaines*** permettent le libre déplacement des populations. Elles agissent donc comme des corridors de dispersion. Les plaines sont riches en ressources tant  pour les prédateurs que pour les proies, mais la compétition y est forte et l'eau est rare.
***Les montagnes*** limitent les déplacements des espèces non-aviaires. Les ressources y son limitées.
***Les forêts*** limitent les déplacements des espèces non-aviaires. Les ressources
y sont abondantes.
***Les milieux hydriques*** limitent les déplacements des espèces non-aviaires et/ou non-aquatiques.
***Les lacs*** sont infranchissables par les espèces non-aviaires et/ou non-aquatiques.

### Climat
***L'altitude*** influence la température et les précipitations.
***la Température*** La température affecte l'ensemble des paramètres d'une population conformément à son habitat préféré.
***Les précipitations*** affectent l'ensemble des paramètres d'une population conformément a son habitat préféré. Les zones de précipitation sont infranchissables par les espèces aviaires. Les précipitations augmentent les réserves d'eau de la cellule.
***Les événements climatiques*** Peuvent affecter tout paramètre d'une cellule ou d'une population. Permet de modéliser des sécheresses, éruption volcanique ou autre.

### Ressources
***La nourriture*** régule le taux de natalité des proies. Les ressources varient d'une cellule à l'autre selon la température et les précipitations. Les omnivores peuvent aussi bénéficier partiellement de la nourriture (50% de leurs besoins).
***L'eau*** Est nécessaire pour toutes les populations. Affecte le taux de mortalité et de natalité de toutes les espèces conformément à leur habitat préféré. La valeur en eau de chaque cellule dépend de la  du type de terrain et des précipitations.


## Dictionnaire de traits de population

***Les jeunes*** sont vulnérables aux maladies et a la prédation, mais ont un taux de mortalité naturel moins élevé. Ils ne contribuent pas au taux de natalité.
***Les adultes*** n'ont pas de modificateurs spécifiques.
***Les vieux*** sont vulnérables aux maladies et a la prédation. Leur taux de mortalité de base est fortement accru.
***Les malades*** les individus malades ne contribuent pas au taux de natalité
et ont un taux de mortalité plus élevé.
***Spécial*** Ce modificateur peut affecter n'importe quel paramètre de la population. Généralement il sert à générer des exceptions (ex. le déplacement des singes n'est pas limité par la foret...)

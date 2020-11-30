# Slide 1
Les 2 précédents algorithmes (R-CNN et Fast-R-CNN) utilise ce que l'on appel la recherche sélective pour déterminé les regions proposés. La méthode de recherche sélective étant lente et consommatrice en termes de temps de calcul ce qui réduit les performances du réseau. Afin d'éliminé cette élément ralentissant le processus, Shaoqing Ren et al. ont proposé un algorithme de détection d'objet qui remplace la recherche sélective et laisse le réseau apprendre la proposition de zones.
Cette algorithme est donc ajouté à Fast R-CNN et nommé Region Proposal Network (RPN) créant ainsi le Faster R-CNN

# Slide 2

L’architecture du RPN est assez particulière. Le RPN fait glisser une fenêtre en long et en large de l’image, au centre de laquelle se trouve ce que les auteurs ont appelé l’ancre. L’ancre est simplement le pixel central d’une fenêtre.
Cette fenêtre est de longueur et taille variable comme visible

Bien entendu, les régions qui contiennent un objet peuvent avoir différentes tailles et différents aspects (l’aspect est le ratio longueur / largeur). 
Dans le cas du RPN, au moment de l’entraînement du réseau, le développeur choisit K1 tailles et K2 aspects différents. Dans le RPN original K1 = K2 = 3. 
Il y a donc, par défaut, 3 x 3 = 9 types de zone pour chaque ancre. Autrement dit, chaque ancre pourra être le centre de 9 zones différentes potentielles, correspondantes aux tailles et aux aspects choisit.

Pour chacune de ces régions, le RPN dispose de deux mécanismes :
* un système de classification
* un système de régression

# Slide 3
Le classifieur a pour objectif d’assigner une probabilité à une région de contenir un objet tandis que le système de régression adapte les coordonnées de la région. La probabilité d’une région de contenir un objet est notée p ou pi (probabilité de la zone i de contenir un objet). Les coordonnées (4 points) de chaque région sont notées t (ou ti pour la région i), t est donc un vecteur de taille 4.

Un RPN est un réseau qui est paramétré au fur et à mesure de l’apprentissage. 

RPN utilise généralement une fonction log-loss car elle est plus intéressante que la simple précision, parce qu’elle permet de nuancer à quel point notre prédiction est proche de la valeur réelle.

# Slide 4

# Slide 5
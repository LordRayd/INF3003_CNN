# Slide 1
La méthode Fast R-CNN est semblable à celle de R-CNN, car faite également par Ross Girshick et al, sa seul différence est que l'on donne non pas les propositions de zones mais l'image au CNN et que ce dernier nous renvoie un ensemble de carctéristiques.

A partir de cette ensemble de caractéristique, on identifie les propositions de zones/regions et on les déformes en carrés. Ensuite en utilisant une couche de *Region of Interest* (RoI) on les remodele afin qu'ils est une taille fixe afin qu'on puissent les donnés a une couche connecté.
A partir du vecteur de RoI, on utilise une couche softmax pour prédire la classe de la région et les valeurs de décalage pour le cadre de délimitation (BoundingBox).

La principal raison de son efficacité vient du fait 
que l'on a pas a donner 2000 regions/zones au CNN à chaque itérations. Ainsi l'opération de convolution n'est exécuté qu'une seul fois et renvoie un ensemble de caractéristiques


# Slide 2
On peut  voir ici la différence entre le temps d'entrainement d'un model Fast R-CNN et un simple R-CNN. La méthode Fast est 10 fois plus rapide à entrainé que la version de base et 21% plus rapide à tester si l'on utilise les propositions de régions. Mais si l'on ne prend pas en compte ces dernières alors la méthode est 146 fois plus rapide.
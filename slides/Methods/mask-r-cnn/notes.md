# Slide 1
Mask R-CNN s’appuie sur les performances de la méthode de classification Faster R-CNN en ajoutant 
la prédiction du masque de l’instance en parallèle de la classification et de la regression.

La partie du calcul est independante des autres branches et est un petit reseau entierement connecté 
appliqué à chaque *Region of Interest* (RoI), prédissant un masque de segmentation de manière pixel à pixel.

Parce que la segmentation au niveau des pixels nécessite un alignement beaucoup plus fin que les cadres de délimitation,
Mask R-CNN améliore la couche de pooling ou mise commun, appelé RoI Align afin qu'elle puisse etre meilleur et plus précise par rapport au zone de l'image d'origine.

La couche RoIAlign est conçue pour corriger le désalignement d'emplacement causé par la quantification dans le pool RoI.
RoIAlign supprime la quantification de hachage, afin que les entités extraites puissent être correctement alignées avec les pixels d'entrée.
L'interpolation bilinéaire est utilisée pour calculer les valeurs d'emplacement en virgule flottante dans l'entrée.

# Slide 2
On peut voir ici le travail de la branche de prédiction du masque. A gauche on trouve l'image d'entrée et a droite les différents masques trouvés.

# Slide 3
On peut voir ici le rendu final de l'algorithme qui affiche des cadres d'encadrement comme fait Faster R-CNN. Cependant on voit également les masques qui sont appliqués à chaque *"objets"*  
# Slide 1
Les 2 précédents algorithmes (R-CNN et Fast-R-CNN) utilise ce que l'on appel la recherche sélective pour déterminé les regions proposés comme contenant un objet. La méthode de recherche sélective est lente et consommatrice en termes de temps de calcul ce qui réduit les performances du réseau. Afin d'éliminé cette élément ralentissant le processus, Shaoqing Ren et al. ont proposé un algorithme de détection d'objet qui remplace la recherche sélective et laisse le réseau apprendre la proposition de zones.
Cette algorithme est donc ajouté à Fast R-CNN et nommé Region Proposal Network (RPN) créant ainsi le Faster R-CNN

# Slide 2
L'algorithme de RPN commence avec l'image que l'on souhaite analyser qui est donné au BackBone CNN.
L'image est dans un premier temps redimmensionné pour que son coté le plus court soit de 600 px et
le plus long n'exède pas 1000 px.

Les caractéristiques de sortie du BackBone CNN sont en général plus petite que l'image de départ suivant le stride du CNN.
Par exemple, pour le BackBone VGG, comme montré sur l'image le stride, est de 16.
Ce qui veut dire que 2 pixels consécutif dans les caractéristiques de sortie du backbone corresponde a 2 points séparer par 16 pixel
dans l'image de départ.

Pour chaque point de l'ensemble des caractéristiques de sortie, 
le reseau doit apprendre si un objet est present a ces positions dans l'image de depart et estimer sa taille. 
Cette tâche est réalisé en placant des ancres sur l'image de départ à chacune des positions donnés dans l'ensemble des caractéristiques sortant du Backbone CNN. 
Ces ancres indique les possibles objets de différente taille et proportions a cette emplacement.
Sur l'image on peut voir qu'il y a 9 ancres possibles car on a 3 tailles differentes et 3 proportions differente possibles donc 3x3 = 9. 
Ont affine ensuite affiner les coordonnées de ces ancres pour donner des cadres de délimitation en tant que «propositions d’objet» ou régions d’intérêt.

Premièrement, on applique une convolution de 3 x 3 avec 512 blocs sur l'ensemble de caractéristique qui sort du BackBone, ce qui nous donne en ensemble de 512-d caractéristique pour chaque coordonnée.

Cette étape est suivies de 2 étapes distinct :
* une couche de convolution de 1x1 avec 18 blocs pour la classification de l'objet
* une couche de convolution de 1x1 avec 36 blocs pour la regression de le boite englobant l'objet

C'est 18 blocs qui servent à la classification retourne 
les probabilités de chaque element de l'ensemble des caractéristique du Backbone de contenir, dans les 9 ancres du point, un objet.

Les 36 blocs retourne une sortie qui  est utilisée pour donner les 4 coefficients de régression de chacune des 9 ancres pour 
chaque point de l'ensemble des caractéristiques du Backbone.
Cette regression de coefficient est utilisé pour amélioré les coordonnées des ancres qui contiennet un objet.

# Slide 3
Il y a plusieurs fait intéressant à connaitre sur cette algorithme.

Lors de l'entrainement, toutes les ancres qui traversent la bordure sont ignoré afin qu'ils ne contribuent pas à la perte.
Ce qui permet de reduire le nombre d'ancre d'une image de, par exemple, 20k ancres de bases à 6k ancres.
Une ancre est considéré comme positive lorsqu'elle valide une des 2 conditions suivantes :
* L'ancre à la plus grande *Intersection Over Union(IoU)*, mesure de chevauchement, avec une boite de vérité fondamentale.
* Si l'ancre à une IoU plus grande que 0.7 avec n'importe quelle boite de vérité fondamentale. 
La meme boite de vérité fondamentale peut permettre à plusieurs ancres d'être considéré coomme possitive
Une ancre est labellisé comme étant négative si toutes ses boites de vérité fondamentale ont une IoU inférieur à 0.3
Les ancres restantes ne sont pas pris en compte dans l'entrainement du RPN.

Les cefficient de regression sont appliqués au ancre afin d'obtenir une position précise, 
cela permet d'avoir des cadres de délimitation précis. 

Tous les cadres de délimitations sont rangé par rapport à leur score de classification
Ensuite une suppression non maximale est appliquée avec un seuil de 0,7.

De haut en bas, tous les cadres de délimitations qui ont une IoU supérieure à 0,7 avec un autre cadre de délimitation sont supprimées.
Ainsi, la zone de délimitation avec le score le plus élevé est conservée pour un groupe de cadre qui se chevauchent.

Tous ça permet d'obtenir environ 2k propositions de cadre de delimitation par image, et ainsi de remplacer la recherche selective.

# Slide 4
On cherche a savoir ici si la différence en temps d'exécution est si importante et on peut voir que l'algorithme Faster R-CNN est 
245 fois plus rapide que l'algorithme de R-CNN et 11 fois plus rapide que l'agorithme Fast R-CNN. 
L'utilisation d'un autre selecteur de zones est donc bien plus efficace en terme de temps

# Slide 5
On obtient bien un algorithme capable de reconnaitre tout objet pour peut qu'il est été entrainé à les reconnaitre avec une rapidité imprésionnante.
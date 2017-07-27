Vous connaissez sans doute le célébrissime **[Géogébra](https://fr.wikipedia.org/wiki/GeoGebra)** qui permet de faire facilement de la géométrie avec votre ordinateur. Saviez-vous que l'on peut aussi l'utiliser pour réaliser des animations et ainsi simuler des systèmes cinématiques ? J'ai par exemple réalisé il y a quelques temps une simulation de commande de profondeur 'MAD' (comprendre à très gros débattement) pour un **aéromodèle** de voltige. En effet, jouer simplement sur le bras de levier du servomoteur n'était pas envisageable car cela aurait maximisé l'imprécision en faible débattement de la commande (ce qui est problématique vous vous en doutez). Voici donc un modèle pour tenter de pallier à ce problème : 

![Voici donc un modèle pour tenter de pallier à ce problème][1] 

La courbe décrite par le point K correspond à la valeur de l'angle de droite en fonction de celle de l'angle de gauche. On observe bien un comportement quasi-linéaire pour des valeurs proches de 90° (faible débattement), ce qui permet un contrôle fin de la trajectoire (par exemple en phase d'atterrissage), ainsi qu'un débattement élevé de la gouverne qui permettra de réaliser des figures acrobatiques ! Vous pouvez retrouver le fichier d'exemple [ici][2].

 [1]: http://sivigik.com/wp-content/uploads/2016/01/54287_anim_rapide2.gif
 [2]: http://sivigik.com/rsrc/profondeurMAD.ggb

Jusqu'ici vous pensiez que l'[Arduino][1] n'était pas assez puissante pour gérer des effets 3D sur un écran, mais laissez-moi vous convaincre du contraire avec deux petites vidéos présentant des moteurs " 3D " à l'aide d'une simple carte Arduino UNO et d'un écran bicolore (oui de la 3D en noir et blanc ça existe). 

# Raycasting 

Vous avez peut-être déjà vu l'[expérience de moteur de Raycasting][2] de klafyvel, mais ici je vous propose de découvrir un moteur de [Raycasting][3] assez sympathique, car son créateur a su remplacer le manque de couleurs par un affichage des textures inspirées tout droit de [Wolfestein 3D][4] : 

<iframe width="560" height="315" src="https://www.youtube.com/embed/GlCye0TyHrE" frameborder="0" allowfullscreen></iframe>

C'est relativement assez fluide n'est-ce pas ? Vous trouverez le code source [ici][5]. 

# Un moteur gérant la rotation de polygones complexes 

Ici encore, on se retrouve en arrière au bon temps des débuts de la 3D... sauf qu'ici ce n'est pas un moteur de type FPS comme au dessus, mais plutôt un moteur capable de gérer des solides complexes (appelés polygones) et le rendu est, ma foi, assez agréable ! Voilà une vidéo assez amusante, car le programme génère un charmant lapin et le fait tourner sur lui-même : 

<iframe width="560" height="315" src="https://www.youtube.com/embed/v6AAVCrupcY" frameborder="0" allowfullscreen></iframe>

C'est peut être un peu lent à votre goût (2 FPS), mais ça fonctionne ! Vous voulez comprendre le fonctionnement du programme ? Pas de problème c'est par [ici][6]. 

# Ça peut aussi vous intéresser :

*   [Le moteur qui gère les polygones complexes en 15 FPS !][7]
*   [Un simple cube géré par l'Arduino][8]
*   [Un pavé et une pyramide affichés en même temps][9]
*   [Un moteur de Raycasting fluide et en couleur avec l'Arduino][10]
*   [Un moteur de Raycasting (pas fluide) en couleur avec l'Arduino et un écran tactile !][11]

 [1]: http://sivigik.com/2015/06/larduino/
 [2]: http://m.youtube.com/watch?v=ZCd-GvIVBWM
 [3]: https://fr.m.wikipedia.org/wiki/Raycasting
 [4]: https://fr.m.wikipedia.org/wiki/Wolfenstein_3D
 [5]: https://github.com/jaburns/lcd-wolf3d
 [6]: http://hastebin.com/kadajezagu.diff
 [7]: https://youtu.be/LyPZS6XqAXE
 [8]: https://youtu.be/xaIRlSmjBT8
 [9]: https://www.youtube.com/watch?v=p4ztTsJPnDM
 [10]: https://youtu.be/iHNqnbSxd6c
 [11]: https://youtu.be/BxW5ZtcXx0E

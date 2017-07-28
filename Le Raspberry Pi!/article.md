# <span style="color: #ff6600;">Drôle de fruit !</span>

Si vous faites des recherches sur comment cuisiner les framboises de manière originale autre qu'en tarte, vous êtes au bon endroit. Un peu plus sérieusement, vous aviez déjà entendu parler du "Raspberry Pi" ? 

Cette petite carte qui s'installe dans de nombreux projets, peut aussi se transformer en media-center ou encore remplacer les anciennes tour dans nos ateliers par exemple... Si vous ne la connaissez pas, je vais tâcher à travers cet article de vous faire une présentation rapide pour vous montrer l'intérêt de l'employer dans vos projets. 

# <span style="color: #ff6600;">Qu'est-ce que c'est ?</span>

Un Raspberry Pi est un nano-ordinateur basé sur un processeur ARM, permettant d’exécuter différents systèmes d'exploitation libres comme GNU/Linux. Tous les composants sont sur un seul circuit imprimé de la taille d'une carte de crédit, ce qui le rend utilisable dans de très nombreux projets. Il est vendu sans boitier. 

[<img class="aligncenter wp-image-227 size-full" src="/media/article/5/attachments/Raspberry_Pi_-_Model_A.jpg" alt="Raspberry_Pi_-_Model_A" width="600" height="600" />][1]Source: [Wikipédia][2]

Le Raspberry Pi a été développé pour le domaine de l'éducation, il permet la découverte du monde de la programmation dans les écoles, plus particulièrement l'apprentissage de langages interprétés comme le Python. Comme nous l'avons vu dans l'introduction, il est souvent utilisé dans les projets personnels. Par exemple la fabrication de robot nécessitant du traitement d'image pour se repérer dans l'espace en temps réel, le Raspberry Pi répond parfaitement à ce besoin. Son port GPIO lui permet d'ajouter toutes sortes de périphériques que l'on peut acheter ou fabriquer soi-même. Il existe une immense diversité de périphériques : allant du contrôle de moteurs pas à pas, à des écrans LCD, en passant par des clavier.

[<img class="aligncenter wp-image-226 size-full" src="http://sivigik.com/wp-content/uploads/2015/06/raspberry-pi-with-tft-lcd-demo.jpg" alt="raspberry-pi-with-tft-lcd-demo" width="800" height="600" />][3] Source: [Raspberry Pi][4]

Lors de l'achat d'un Raspberry Pi on peut choisir parmi plusieurs kits, c'est-à-dire : soit acheter le Raspberry Pi seul (uniquement la carte mère avec ses composants dessus) ; soit avec une carte SD contenant un OS basé sur un noyau Linux (qui peut être Raspbian ou encore Pidora) ; soit un kit très complet qui contient une multitude de composants pour commencer à faire des mini projets, il y a dans ce genre de kit un bloc d'alimentation, une mini caméra, une clé WI-FI, un clavier et une souris, un boitier de protection pour le Raspberry Pi, et toutes sortes de câbles pour les périphériques.

[<img class="aligncenter wp-image-228 size-full" src="/media/article/5/attachments/Official_Raspberry_Pi_case.jpg" alt="Official_Raspberry_Pi_case" width="600" height="900" />][5] Source: [Wikipédia][6]

Ce nano-ordinateur est bien entendu aussi utilisable comme ordinateur de secours : quand votre PC vous lâche, que vous en êtes réduit à devoir attendre l'arrivée d'un nouveau PC et que vous n'en avez pas d'autres (c'est rare de ne pas avoir de vieille tour sous XP, mais ça peut arriver), le Raspberry Pi sera là pour vous permettre de continuer à réaliser des projets, mais aussi de faire des recherches internet sur votre navigateur préféré ou même encore de regarder des vidéos. 

# <span style="color: #ff6600;">Caractéristiques</span>

Il existe à ce jour au total 5 modèles de Raspberry Pi qui sont apparus successivement, ils ont donc une puissance de calcul qui augmente à chaque nouvelle version. La première version apparue et qui s'est fait connaitre dans le monde entier est la version A. Elle a été commercialisée à partir du 29 février 2012, pour la modique somme de 25€, elle a alors rapidement connu un grand succès : en moins d'un an le million d'unités vendues est atteint. Voyons maintenant les caractéristiques de certains modèles de Raspberry Pi : 

*   **Modèle A :** il possède un processeur ARM1176JZF-S (ARMv6), cadencé à 700MHz, il peut être overclocké jusqu'à 1GHz avec un dissipateur thermique, accompagné de 256Mo de RAM. Il possède plusieurs ports de communication par exemple : GPIO, S2C, I2C, SPI, avec une sortie audio stéréo et 2 sorties vidéo: HDMI (fullHD 1080 p) et composite, puis un port USB 2.0 et bien sûr un port d'alimentation (micro-USB). Il n'y a pas de mémoire présente sur le Rasperry Pi pour stoker OS, il doit donc être contenu sur une carte SD (sont supportés les formats : SDHC, MMC et SDIO). Sa consommation est de 320 mA.

*   **Modèle B 512Mo :** comme son nom de modèle l'indique, sa principale caractéristique nouvelle est l'ajout de 256 Mo de RAM au 256 Mo déjà présent, puis l'ajout d'une autre port USB 2.0. Par contre sa consommation est plus importante que pour le premier modèle : 500 mA.

*   **Modèle 2 : **De nombreuses améliorations y sont apportées par rapport aux versions précédentes, un accent a été porté sur sa puissance, le processeur ARM1176JZF-S est remplacé par un quadricœur ARM Cortex-A7 cadencé à 900 Mhz, ce qui le rend six fois plus puissant que le type B, une fois de plus la quantité de RAM est doublée, elle est maintenant de 1 Go. Il comporte 4 ports USB 2.0 et sa consommation est descendue à 400 mA. Tous ces différents modèles possèdent les mêmes dimensions : 85,60 mm × 53,98 mm × 17 mm, mis à part le modèle A+ : 65 mm × 53,98 mm × 17 mm. 

# <span style="color: #ff6600;">Documentations :</span>

*   [Le site officiel de Raspberry Pi][7]
*   [Le Wikipédia du Raspberry Pi][8]

 [1]: /media/article/5/attachments/Raspberry_Pi_-_Model_A.jpg
 [2]: https://fr.wikipedia.org/wiki/Raspberry_Pi#/media/File:RaspberryPi.jpg
 [3]: /media/article/5/attachments/raspberry-pi-with-tft-lcd-demo.jpg
 [4]: http://blog.iteadstudio.com/wp-content/uploads/image/2013_05/raspberry-pi-with-tft-lcd-demo.jpg
 [5]: /media/article/5/attachments/Official_Raspberry_Pi_case.jpg
 [6]: https://fr.wikipedia.org/wiki/Raspberry_Pi#/media/File:Official_Raspberry_Pi_case.jpg
 [7]: https://www.raspberrypi.org/
 [8]: https://fr.wikipedia.org/wiki/Raspberry_Pi

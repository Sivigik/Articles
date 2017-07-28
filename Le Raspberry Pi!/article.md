# <span style="color: #ff6600;">Dr�le de fruit !</span>

Si vous faites des recherches sur comment cuisiner les framboises de mani�re originale autre qu'en tarte, vous �tes au bon endroit. Un peu plus s�rieusement, vous aviez d�j� entendu parler du "Raspberry Pi" ? 

Cette petite carte qui s'installe dans de nombreux projets, peut aussi se transformer en media-center ou encore remplacer les anciennes tour dans nos ateliers par exemple... Si vous ne la connaissez pas, je vais t�cher � travers cet article de vous faire une pr�sentation rapide pour vous montrer l'int�r�t de l'employer dans vos projets. 

# <span style="color: #ff6600;">Qu'est-ce que c'est ?</span>

Un Raspberry Pi est un nano-ordinateur bas� sur un processeur ARM, permettant d�ex�cuter diff�rents syst�mes d'exploitation libres comme GNU/Linux. Tous les composants sont sur un seul circuit imprim� de la taille d'une carte de cr�dit, ce qui le rend utilisable dans de tr�s nombreux projets. Il est vendu sans boitier. 

[<img class="aligncenter wp-image-227 size-full" src="/media/article/5/attachments/Raspberry_Pi_-_Model_A.jpg" alt="Raspberry_Pi_-_Model_A" width="600" height="600" />][1]Source: [Wikip�dia][2]

Le Raspberry Pi a �t� d�velopp� pour le domaine de l'�ducation, il permet la d�couverte du monde de la programmation dans les �coles, plus particuli�rement l'apprentissage de langages interpr�t�s comme le Python. Comme nous l'avons vu dans l'introduction, il est souvent utilis� dans les projets personnels. Par exemple la fabrication de robot n�cessitant du traitement d'image pour se rep�rer dans l'espace en temps r�el, le Raspberry Pi r�pond parfaitement � ce besoin. Son port GPIO lui permet d'ajouter toutes sortes de p�riph�riques que l'on peut�acheter ou fabriquer soi-m�me. Il existe une immense diversit� de p�riph�riques : allant du contr�le de moteurs pas � pas, � des �crans LCD, en passant par des clavier.

[<img class="aligncenter wp-image-226 size-full" src="http://sivigik.com/wp-content/uploads/2015/06/raspberry-pi-with-tft-lcd-demo.jpg" alt="raspberry-pi-with-tft-lcd-demo" width="800" height="600" />][3] Source: [Raspberry Pi][4]

Lors de l'achat d'un Raspberry Pi on peut choisir parmi plusieurs kits, c'est-�-dire : soit acheter le Raspberry Pi seul (uniquement la carte m�re avec ses composants dessus) ; soit avec une carte SD contenant un OS bas� sur un noyau Linux (qui peut �tre Raspbian ou encore Pidora) ; soit un kit tr�s complet qui contient une multitude de composants pour commencer � faire des mini projets, il y a dans ce genre de kit un bloc d'alimentation, une mini cam�ra, une cl� WI-FI, un clavier et une souris, un boitier de protection pour le Raspberry Pi, et toutes sortes de c�bles pour les p�riph�riques.

[<img class="aligncenter wp-image-228 size-full" src="/media/article/5/attachments/Official_Raspberry_Pi_case.jpg" alt="Official_Raspberry_Pi_case" width="600" height="900" />][5] Source: [Wikip�dia][6]

Ce nano-ordinateur est bien entendu aussi utilisable comme ordinateur de secours : quand votre PC vous l�che, que vous en �tes r�duit � devoir attendre l'arriv�e d'un nouveau PC et que vous n'en avez pas d'autres (c'est rare de ne pas avoir de vieille tour sous XP, mais �a peut arriver), le Raspberry Pi sera l� pour vous permettre de continuer � r�aliser des projets, mais aussi de faire des recherches internet sur votre navigateur pr�f�r� ou m�me encore de regarder des vid�os. 

# <span style="color: #ff6600;">Caract�ristiques</span>

Il existe � ce jour au total 5 mod�les de Raspberry Pi qui sont apparus successivement, ils ont donc une puissance de calcul qui augmente � chaque nouvelle version. La premi�re version apparue et qui s'est fait connaitre dans le monde entier est la version A. Elle a �t� commercialis�e � partir du�29 f�vrier 2012, pour la modique somme de 25�, elle a alors rapidement connu un grand succ�s : en moins d'un an le million d'unit�s vendues est atteint. Voyons maintenant les caract�ristiques de certains mod�les de Raspberry Pi : 

*   **Mod�le A :** il poss�de un processeur ARM1176JZF-S (ARMv6), cadenc� � 700MHz, il peut �tre overclock� jusqu'� 1GHz avec un dissipateur thermique, accompagn� de 256Mo de RAM. Il poss�de plusieurs ports de communication par exemple :�GPIO, S2C, I2C, SPI, avec une sortie audio st�r�o et 2 sorties vid�o: HDMI (fullHD 1080 p) et composite, puis un port USB 2.0 et bien s�r un port d'alimentation (micro-USB). Il n'y a pas de m�moire pr�sente sur le Rasperry Pi pour stoker OS, il doit donc �tre contenu sur une carte SD (sont support�s les formats :�SDHC, MMC et SDIO). Sa consommation est de 320 mA.

*   **Mod�le B 512Mo :** comme son nom de mod�le l'indique, sa principale caract�ristique nouvelle est l'ajout de 256 Mo de RAM au 256 Mo d�j� pr�sent, puis l'ajout d'une autre port USB 2.0. Par contre sa consommation est plus importante que pour le premier mod�le : 500 mA.

*   **Mod�le 2 : **De nombreuses am�liorations y sont apport�es par rapport aux versions pr�c�dentes, un accent a �t� port� sur sa puissance, le processeur�ARM1176JZF-S est remplac� par un quadric�ur ARM Cortex-A7�cadenc� � 900 Mhz, ce qui le rend six fois plus puissant que le type B, une fois de plus la quantit� de RAM est doubl�e, elle est maintenant de 1 Go. Il comporte 4 ports USB 2.0 et sa consommation est descendue � 400 mA. Tous ces diff�rents mod�les poss�dent les m�mes dimensions :�85,60 mm � 53,98 mm � 17 mm, mis � part le mod�le A+ :�65 mm � 53,98 mm � 17 mm. 

# <span style="color: #ff6600;">Documentations :</span>

*   [Le site officiel de Raspberry Pi][7]
*   [Le Wikip�dia du Raspberry Pi][8]

 [1]: /media/article/5/attachments/Raspberry_Pi_-_Model_A.jpg
 [2]: https://fr.wikipedia.org/wiki/Raspberry_Pi#/media/File:RaspberryPi.jpg
 [3]: /media/article/5/attachments/raspberry-pi-with-tft-lcd-demo.jpg
 [4]: http://blog.iteadstudio.com/wp-content/uploads/image/2013_05/raspberry-pi-with-tft-lcd-demo.jpg
 [5]: /media/article/5/attachments/Official_Raspberry_Pi_case.jpg
 [6]: https://fr.wikipedia.org/wiki/Raspberry_Pi#/media/File:Official_Raspberry_Pi_case.jpg
 [7]: https://www.raspberrypi.org/
 [8]: https://fr.wikipedia.org/wiki/Raspberry_Pi

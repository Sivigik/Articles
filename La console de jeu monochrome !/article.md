# La Master328

![master328][1] Je vais vous présenter ici la console de jeu monochrome (noir et blanc) que j'avais réalisé en 2013. Elle est basée sur un ATmega328p et elle est programmable sous [Arduino][2]. La Master328 (un mélange entre MasterSystem et ATmega328) est peut-être mon premier réel projet d'électronique programmé. À l'origine, après avoir découvert une librairie permettant de connecter une carte Arduino à un écran TV (j'ai nommé [TV-Out][3]) et que l'on pouvait fabriquer sa propre carte Arduino sur BreadBoard (ou platine d'expérimentation) j'ai tout de suite eu l'idée de me fabriquer une console de jeu. Après quelques recherches sur le net, un peu déçu, je trouve que cette idée n'est pas originale et qu'elle avait déjà été réalisée et même commercialisée (voir [Hackvision][4])... Mais cela ne m'a pas découragé pour autant et j'ai décidé de me lancer dans ce projet ! 
# Principe de fonctionnement 
La console se présente sous la forme d'une manette reliée à la TV et à une prise secteur. En plus de pouvoir afficher à l'écran, elle peut aussi produire du son. On peut résumer son fonctionnement sous forme de schéma : 

![schemaboite][5] 

Le schéma électronique de la console s'organise ainsi : 

![schemaelec][6] 

# TV-Out 
Comme je disais, TV-Out est une librairie Arduino. Il a d'abord fallu comprendre comment elle fonctionnait et comment l'utiliser. Pour cela, un tutoriel m'a bien aidé, celui de [tronixstuff][7], en effet, il expose pas mal les possibilités de cette librairie. Pour afficher quelque chose sur une télévision avec Arduino il suffit donc de deux résistances et d'une fiche RCA ! De plus, cette librairie permet aussi d'afficher des images Bitmap monochromes sur sa TV; un autre [tutoriel][8] explique comment procéder. Schéma du branchement du câble vidéo : ![video][9] Voici une vidéo de la démo de cette librairie : <iframe width="480" height="360" src="http://www.youtube.com/embed/Ei3JZ67CUbo?rel=0" frameborder="0" allowfullscreen></iframe> **Produire du son :** Nativement, TV-Out gère le son (utiliser la fonction *TV.tone()*). De la même manière que pour l'image, il faut relier l'Arduino avec un câble RCA à la TV, la seule différence étant que cela n'utilise qu'une seule résistance. Il y a aussi la possibilité d'utiliser la fonction [tone()][10] (à la manière d'un buzzer) présente de base sur Arduino, il suffira de définir le bon pin de sortie pour le son et le son se jouera sur votre TV. Schéma du branchement du câble son : 
![audio][11] 

# Liste du matériel utilisé 
Voici la liste des achats (les prix peuvent avoir évolués) que j'ai effectué : 

*   1 [Platine d'essais à pastilles (75x100x1.5mm)][12] : 1.67€ *C'est une plaque trouée où l'on va souder les composants dessus. L'avantage c'est qu'elle est peu chère comparé au coût de fabrication d'un circuit imprimé. Le principe est simple, il y a du cuivre sous chaque trous et il suffit de relier par un fil soudé deux trous pour créer un bout de piste.*
*   1 [Microcontrôleur ATmega328 (boot Arduino)][13] : 7.11€ *C'est le cerveau de la console, c'est lui qui gère l'affichage, le son et les boutons. Je l'ai pris avec le boot Arduino (coûte plus cher que sans) mais il existe cependant un moyen de le [booter soi-même][14].*
*   1 [Bloc d'alimentation 9V/DC 660 mA][15] : 5.84€ *C'est ce qui va permettre d'alimenter notre console en électricité.*
*   2 [Condensateurs radiaux 105°C 10 µF 25V][16] : 0.16€ *Il vont servir à stabiliser l'alimentation électrique.*
*   2 [Condensateurs céramiques traversant 22 pF 100 V/DC][17] : 0,51€ *Ils vont diminuer la fréquence de résonance parallèle du Quartz.*
*   1 [Résistance 1k ohms][18] : 0,13€ *Elle est utile pour l'affichage.*
*   1 [Résistance 10k ohms][19] : 0,13€ *Elle est primordiale pour le bouton RESET.*
*   3 [Résistances 330 ohms][20] : 0.39€ *2 résistances sont utilisées pour les branchements RCA et la dernière pour la LED témoin.*
*   6 [Boutons poussoirs normalement ouvert][21] : 1,74€ *5 boutons pour jouer et un bouton pour réinitialiser la console.*
*   1 [Quartz 16 Mhz][22] : 0,42€ *C'est un composant qui va osciller à une fréquence stable, il va fournir une base de temps à l'ATmega328.*
*   1 [Régulateur MC 7805CT ON Semiconductor][23] : 0,46€ *Il permet d'abaisser une tension entre 6V et 12V (il vaut mieux toutefois entre 7V et 12V) à une tension de 5V.*
*   1 [Embase Châssis Alimentation 2.1Mm][24] : 0,79€ *C'est la prise où on va brancher notre alimentation.*
*   1 [Embase RCA 2 pôles femelle droite][25] : 1€ *Ce sont les prises où on va brancher nos câbles RCA à relier à la TV.*
*   1 [Socle CI de précision 28 Bro.][26] (prendre un pas adapté à l'ATmega328P) : 1,63€ *C'est le socle qui va accueillir le microcontrôleur, il est utile car il permet de ne pas souder directement le microcontrôleur et de pouvoir ainsi le débrancher et brancher à sa guise. Toutefois, celui que j'ai acheté était trop large et j'ai dû le rétrécir.*
*   1 [LED 2.25V 20 mA][27] : 0.20€ *La LED témoin qui va nous communiquer l'état de l'alimentation du circuit.* ... pour un total d'une vingtaine d'euros (prix de Conrad) ! Ce qui correspond à peu près au prix d'une carte Arduino Uno. Et voici la liste d'outils que j'ai utilisés (et que je possédais déjà) : 

*   un fer à souder *... Pour souder les composants.*
*   du fil électrique fin *Pour relier les composants entre-eux.*
*   Une carte Arduino UNO ou un programmateur AVR *Afin de pouvoir programmer le microcontrôleur.*
*   un ordinateur *Pour envoyer le programme à l'Arduino.*
*   un câble USB Standar A-B *pour connecter l'Arduino à l'ordinateur.*
*   2 Câbles RCA *Pour relier la console à la TV.*
*   1 Télévision *Pour afficher les jeux.*

# Tests

**Sur Arduino :** Pour tester la librairie TV-Out, je l'ai tout d'abord testé sur Arduino Uno. 

![testarduino][28] 

**Et sur BreadBoard :** Avant de commencer à souder les composants, je les ai tout d'abord testé sur BreadBoard, j'ai tout simplement fait un test du programme basique d'Arduino (Blink). Voici une photo de ce premier test (alimenté sans Arduino Uno, directement avec l'alimentation branchée au secteur !) : ![test1][29] On remarque que la LED témoin était déjà présente. Pour réaliser ce premier test, je suis allé notamment sur ce site : <http://arduino.cc/en/Main/Standalone> qui explique comment mettre l'Arduino sur BreadBoard et quels sont les composants à utiliser. 

# Conception réelle 
Une fois les tests effectués et que je m'étais assuré que tous les composants fonctionnaient, j'ai enfin soudé les composants sur la platine. Comme on peut le voir sur cette image j'ai d'abord scotché les composants afin de les maintenir aux positionnements corrects et ainsi pouvoir les souder facilement : 

![scotchcompo][30] 

On remarque 4 marques noirs qui correspondent aux endroits à percer (afin de placer des vis qui maintiendront la carte dans un support). Il m'a ensuite fallu repérer chaque pin de l'ATmega328 afin de pouvoir les relier aux bons composants (en faisant attention aux problèmes de sens) : 

![mastermaping][31] 

Et j'ai ainsi pu les souder : 

![soud][32] 

J'ai aussi pu mettre au point une technique pour limiter les branchements des boutons : 

![boutons][33] 

Et après quelques temps de soudure.... la Master328 fut terminée !!! ![fin][34] Il ne reste plus qu'à lui confectionner un boîtier mais elle est fonctionnelle. 

# Programmation 

Pour la programmer, c'est simple. il faut le logiciel Arduino sur un ordinateur et une Arduino Uno (et le câble USB). On peut aussi programmer l'ATmega328 depuis un programmateur AVR. Il faut ensuite retirer (avec un petit tournevis plat) le microcontrôleur de la carte Arduino Uno (système de levier) et le remplacer par celui qui commande la Master328 : 

![deboite][35] 

Là on téléverse tout simplement vers la carte un des jeux. 

![arduinoprog][36] 

# Les jeux 

Voici maintenant une présentation des jeux de la Master328 qui, je le rappelle, sont en noir et blanc. 

**Kirby's : Start Eater** 

![kirbys][37] 

Kirby's est un jeu de plateforme 2D développé pour la Master328 par moi-même (avec l'aide de klafyvel). Ce jeu n'est pas terminé et le gameplay n'est pas encore décidé, mais je compte le terminer bientôt. Les possibilités se résument à faire marcher et sauter Kirby pour l'instant. Les commandes du jeu sont les touches directionnelles pour aller à droite et à gauche et le bouton d'action A pour sauter. [Télécharger le jeu][38] 

**Starfield** 

![starfield][39] 

Considéré comme le premier jeu réellement jouable sur Master328, il n'est cependant qu'un portage de [ce Starfield][40] sur cette console (changement des pins des boutons). Il a été entièrement programmé par Mário Vairinhos. Le principe du jeu est que vous incarnez un vaisseau spatial en vue à la première personne et vous devez éviter les astéroïdes qui vous foncent dessus. Les commandes du jeu sont les touches directionnelles pour se déplacer. [Télécharger le jeu][41] 

**Wolfestein** 

![wolfestein][42] 

Wolfestein (en référence à un des tout premiers FPS en 3D de l'histoire du jeu vidéo) est un jeu 3D (pour comprendre le code, il faut se renseigner sur le [Raycasting][43] ) en vue FPS et entièrement en noir et blanc ! Initialement programmé [par Jeremy Burns][44] pour être joué sur un écran LCD contrôlé par Arduino, il a été adapté pour la Master328 avec l'aide de [smeezekitty][45]. Malheureusement, même si le fonctionnement est correct, le jeu comporte un énorme défaut : sa lenteur. En effet, les calculs de rendu pseudo-3D sont trop lourds pour l'Atmega328. Au niveau gameplay, rien n'est prévu d'autre que pouvoir se balader, arme en main, dans un labyrinthe en 3D. Les commandes du jeu sont les touches directionnelles pour se déplacer et les touches d'action pour effectuer une rotation. [Télécharger le jeu][46]
 
# Vidéo de fonctionnement

<iframe width="420" height="315" src="//www.youtube.com/embed/UHuyO6P8dqw" frameborder="0" allowfullscreen></iframe> 

# Créer un jeu 

Ces instructions sont la base pour programmer des jeux sur la Master328, mais il faut bien entendu aussi avoir préalablement des connaissances dans le langage Arduino. Les jeux de Master328 sont en noir et blanc avec une résolution maximale de 128x96 pixels. Il faut noter que les jeux ne peuvent pas dépasser plus de 32 256 bytes et l'ATmega328 doit donc être reprogrammée à chaque changement de jeu. 

**Référence TV-Out :** Les jeux se programment sous l'IDE Arduino, je vais présenter ici quelques fonctions principales qu'il faut utiliser pour programmer un jeu, à savoir que [la référence complète][47] de la librairie TV-Out comporte beaucoup plus de fonctions. 

```c++
#include "TVout.h"
TVout TV;
```

Ces deux lignes doivent être obligatoirement présentes au tout début de chaque programme. Elle servent à intégrer la librairie TV-Out. 

```c++
TV.begin(_NTSC); // pour les systèmes NTSC ou
TV.begin(_PAL); // pour les systèmes PAL
```

Cette ligne doit être mise dans le *void setup()*. Les télévisions d'Europe sont en principe des systèmes PAL, il faut donc prendre uniquement la seconde ligne si vous en possédez une. Le système NTSC est réservé en général pour l'Amérique. Pour en savoir plus, rendez-vous sur [Wikipédia][48]. 

```c++
TV.clear_screen();
```

Cette fonction permet d'effacer l'intégralité de ce qui est présent à l'écran. 

```c++
TV.fill_screen(1);
```

Cette fonction permet de remplir l'intégralité de l'écran en blanc (contraire de la précédente). 

```c++
TV.select_font(font4x6); // pour utiliser la police de caractère 4x6 ou
TV.select_font(font6x8); // pour utiliser la police de caractère 6x8 ou
TV.select_font(font8x8); // pour utiliser la police de caractère 8x8
```

Cette fonction permet de sélectionner la police de caractère à utiliser pour l'affichage du texte. Par exemple, la police 4x6 affichera des caractères dans un rectangle de 4x6 pixels. 

```c++
TV.set_cursor(x,y);
```

Cette fonction permet de définir les coordonnées du texte à afficher. 

```c++
TV.print("Hello, world..."); // pour afficher un texte
TV.print(); // pour faire un retour à la ligne
```

Enfin cette fonction vous permet d'afficher un texte. 

```c++
TV.print_char(x,y,c); // c étant la variable correspondante au caractère à afficher
```

Cette fonction permet d'afficher un caractère à des coordonnées définies. À chaque caractère correspond un numéro et il doit être attribué à la variable pour l'afficher. 

```c++
TV.set_pixel(x,y,z);
```

Cette fonction permet d'afficher un pixel à des coordonnées définies. La variable z peut prendre trois valeurs : 0 pour un pixel noir, 1 pour un pixel blanc ou 2 pour inverser la couleur du pixel de ces coordonnées. 

```c++
TV.draw_line(x1,y1,x2,y2,colour);
```

Cette fonction permet de dessiner une ligne entre le point aux coordonnées (x1,y1) et (x2,y2). La couleur est définie de la même manière que pour la fonction précédente. 

```c++
TV.draw_rect(x,y,w,h,colour,fill);
```

Cette fonction permet de dessiner un rectangle en définissant les coordonnées du point en haut à gauche (x,y) la largeur w et la hauteur h, la couleur se définie comme précédemment et fill correspond à la couleur de l'intérieur du rectangle. 

```c++
TV.draw_circle(x,y,r,colour,fill);
```

Cette fonction permet de dessiner un cercle. Il faut définir les coordonnées du centre (x,y), la taille du rayon, la couleur du cercle et la couleur de l’intérieur du cercle. 

```c++
TV.bitmap(x,y,bmp)
```

Cette fonction sert à placer une image bitmap bmp au coordonnées (x,y). Pour en savoir plus, voir le [tutoriel pour insérer une image bitmap][49]. 

**Définir les boutons :** La Master328 possède 6 boutons de contrôle et ils doivent être définis dans chaque programmes afin de pouvoir être utilisés. 

```c++
#define BT_UP           2
#define BT_DOWN         12
#define BT_LEFT         4
#define BT_RIGHT        3
#define BT_A            6
#define BT_B            8
```

Placer ces lignes en tout début de programme pour définir les pins des boutons. 

```c++
pinMode(BT_UP   ,INPUT);digitalWrite(BT_UP   ,HIGH);
pinMode(BT_DOWN ,INPUT);digitalWrite(BT_DOWN ,HIGH);
pinMode(BT_LEFT ,INPUT);digitalWrite(BT_LEFT ,HIGH);
pinMode(BT_RIGHT ,INPUT);digitalWrite(BT_RIGHT ,HIGH);
pinMode(BT_A ,INPUT);digitalWrite(BT_A ,HIGH);
pinMode(BT_B ,INPUT);digitalWrite(BT_B ,HIGH);
```

Ces lignes doivent être présentent obligatoirement dans la fonction *void setup()*. 

```c++
if(digitalRead(BT_UP)==LOW) // exemple pour le bouton UP
{
    ... // placer ici le contenu du if
}
```

Voici comment détecter l'appui sur un bouton et déclencher une action.

 [1]: http://www.heberger-image.fr/data/images/97988_master328wood.png
 [2]: http://sivigik.com/2015/06/larduino/
 [3]: http://code.google.com/p/arduino-tvout/
 [4]: https://nootropicdesign.com/hackvision/
 [5]: http://www.heberger-image.fr/data/images/29913_Master328.png
 [6]: http://www.heberger-image.fr/data/images/44539_35888_masterelec.png
 [7]: http://tronixstuff.com/2011/05/30/tutorial-video-output-from-your-arduino/
 [8]: http://f5mna.free.fr/ArduiTVout.htm
 [9]: http://www.heberger-image.fr/data/images/17161_audio328.png
 [10]: http://arduino.cc/en/reference/tone
 [11]: http://www.heberger-image.fr/data/images/37622_video328.png
 [12]: http://www.conrad.fr/ce/fr/product/529580/?insert=62&insertNoDeeplink&productname=Platine-dessais-a-pastilles-75x100x15mm-WR-Rademacher-VK-C-811-2
 [13]: http://www.conrad.fr/ce/fr/product/092026/?insert=62&insertNoDeeplink&productname=Microcontroleur-ATmega-328-memoire-flash-32-kB-RAM-2-kB-boitier-PDIP-Arduino-A000048
 [14]: http://arduino.cc/en/Tutorial/ArduinoToBreadboard
 [15]: http://www.conrad.fr/ce/fr/product/514209/?insert=62&insertNoDeeplink&productname=Bloc-dalimentation-9-VDC-660-mA-VOLTCRAFT-FPPS-9-6W
 [16]: http://www.conrad.fr/ce/fr/product/445591/?insert=62&insertNoDeeplink&productname=Condensateur-Radial-105C-10F-25V-4x5-Pas-15mm-Yageo-S5025M0010B1F-0405
 [17]: http://www.conrad.fr/ce/fr/product/531975/?insert=62&insertNoDeeplink&productname=Condensateur-ceramique-serie-RDC-22-pF-100-VDC-5-Pas-5-mm-COG-1-pcs-Holystone-RDCN220J101DKA
 [18]: http://www.conrad.fr/ce/fr/product/405256/?insert=62&insertNoDeeplink&productname=Resistance-couche-carbone-axiale-forme-0411-1-k-05-W-5-
 [19]: http://www.conrad.fr/ce/fr/product/405370/Resistance-couche-carbone-axiale-forme-0411-10-k-05-W-5-
 [20]: http://www.conrad.fr/ce/fr/product/405191/Resistance-couche-carbone-axiale-forme-0411-330-05-W-5-
 [21]: http://www.conrad.fr/ce/fr/product/701749/?insert=62&insertNoDeeplink&productname=Poussoir-Fsm2Jh-Tyco-1825910-2
 [22]: http://www.conrad.fr/ce/fr/product/155145/?insert=62&insertNoDeeplink&productname=Quartz-16000000-MHz-boitier-HC494H-stabilite-de-frequence-50-ppm-EuroQuartz-16000MHZ-HC494H-30504018PFATF
 [23]: http://www.conrad.fr/ce/fr/product/175030/?insert=62&insertNoDeeplink&productname=Regulateur-de-tension-positive-MC7805CT-boitier-TO-220-Contenu-1-pcs-ON-Semiconductor
 [24]: http://www.conrad.fr/ce/fr/product/733946/?insert=62&insertNoDeeplink&productname=Embase-Chassis-Alim21Mm
 [25]: http://www.conrad.fr/ce/fr/product/064738/?insert=62&insertNoDeeplink&productname=Embase-RCACinch-2-poles-adaptateur-droit-connexion-a-souder-a-visser-sur-chassis
 [26]: http://www.conrad.fr/ce/fr/product/184877/?insert=62&insertNoDeeplink&productname=Socle-CI-de-precision-28Bro-Dorure-075m-Preci-Dip-110-83-628-41-001101
 [27]: http://www.conrad.fr/ce/fr/product/184543/Diode-LED-radiale-5-mm-coloris-rouge-angle-225-V-20-mA-L-53-HD?ref=searchDetail
 [28]: http://www.heberger-image.fr/data/images/28870_Kirby_s.png
 [29]: http://www.heberger-image.fr/data/images/25273_Photo0090.jpg
 [30]: http://www.heberger-image.fr/data/images/29162_Photo0092.jpg
 [31]: http://www.heberger-image.fr/data/images/59901_mastermaping.png
 [32]: http://www.heberger-image.fr/data/images/46416_Photo0105.jpg
 [33]: http://www.heberger-image.fr/data/images/14752_BOUTONss.png
 [34]: http://www.heberger-image.fr/data/images/94014_master328fin.png
 [35]: http://www.heberger-image.fr/data/images/65960_20140601_160726.jpg
 [36]: http://www.heberger-image.fr/data/images/90922_arduinowolf.png
 [37]: http://www.heberger-image.fr/data/images/78630_Kirby_s.png
 [38]: http://www.mediafire.com/download/uxo36qly3m8ic6r/Kirby.rar
 [39]: http://www.heberger-image.fr/data/images/14735_starfimg.png
 [40]: http://noperation.wordpress.com/2012/11/27/arduino-starfield/
 [41]: http://www.mediafire.com/download/mfxuzkfj4bglxr2/starfield.rar
 [42]: http://www.heberger-image.fr/data/images/13926_wolfimg.png
 [43]: http://fr.wikipedia.org/wiki/Raycasting
 [44]: http://www.youtube.com/watch?v=GlCye0TyHrE
 [45]: http://www.youtube.com/watch?v=hJseUSElyZg
 [46]: http://www.mediafire.com/download/nq5nu5wbhcsu6g6/Wolfenstein3D.rar
 [47]: https://code.google.com/p/arduino-tvout/wiki/FunctionalDescription
 [48]: http://fr.wikipedia.org/wiki/Phase_Alternating_Line
 [49]: http://f5mna.free.fr/arduino/Tvout_johnny.zip

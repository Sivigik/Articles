# <span style="color: #ff6600;">Le PowerTiny</span> Vous en avez marre d'avoir pour quête principale de trouver une prise ou un port USB quand vous sortez de chez vous? Les 

**powerbanks** du commerce ne vous satisfont pas ? Vous avez des batteries à recycler ? La réponse à toutes ces questions est simple : **PowerTiny** le chargeur nomade à faire chez soi, simple, puissant et économique! ![](/media/article/10/attachments/)
## <span style="color: #ff6600;">Liste des composants:</span>

*   Une Batterie de PC portable, celle que j'ai choisie avait 4 éléments 3,7 V de 2500 mAh
*   Un convertisseur DC-DC de type Boost, facilement trouvable sur Ebay (par exemple)[<img class="size-medium wp-image-761 aligncenter" src="http://sivigik.com/wp-content/uploads/2016/08/DC-DC-converteur-300x300.jpg" alt="DC-DC converteur" width="300" height="300" />][2]
<li style="text-align: left;">
   Un Attiny 84
</li>
*   Programmateur ISP (j'utilise une [arduino][3])
*   Des MOSFET (récupérés sur une carte mère de PC portable), transistor, résistances, condensateurs, DEL, ....
*   Matériel de prototypage de circuit imprimé

## <span style="color: #ff6600;">Fabrication d'une protection de batterie</span> Les batteries de type LiPo sont très sensibles aux décharges brutales et déchargement trop important ( < 3 V), il ne faut donc pas relier directement le transformateur à la batterie, un circuit intermédiaire doit surveiller les charges qui passent. Pour cela : soit vous utilisez un circuit de protection récupérable sur des batteries de Smartphones, la vidéo suivante explique très bien comment réaliser sa propre powerbank facilement (sans PCB à réaliser): 

[Fabriquer un chargeur portable : Incroyables Expériences [88] Batterie externe USB / Power bank][4] ou alors vous le faites vous-même ! J'ai choisi d'utiliser un microcontrôleur pour diminuer la quantité de composants à utiliser, et donc de diminuer la place (le circuit étant entièrement réalisable sans microcontrôleur). Le circuit de charge (diode D6 et résistance R6) n'est pas de moi, je l'ai pris dans la vidéo du dessus, j'ai seulement ajouté un MOSFET pour éviter que la batterie se décharge après avoir débranché le chargeur. (Le connecteur de droite sert uniquement à envoyer le programme et à déboguer.) 
###  <span style="color: #0000ff;">Schéma :</span>

![](/media/article/10/attachments/sécurité-1-1024x720.jpg]
### <span style="color: #0000ff;">Réalisation de circuit imprimé :</span> La partie en bas à gauche sur le schéma n'est pas présente sur les photos de la réalisation, car je l'ai ajouté plus tard pour résoudre un bug, il permet de RESET quand on fait charger la powerbank, ce qui fait sortir la puce du mode " économie d'énergie " (consomme seulement 300 µA)  quand la batterie est complètement vide. Gravure du circuit au perchlorure de fer: 

[<img class="aligncenter wp-image-755 size-large" src="http://sivigik.com/wp-content/uploads/2016/08/IMG_5337-1024x768.jpg" alt="IMG_5337" width="1024" height="768" />][6] Nettoyage à l'eau, puis à l'acétone pour enlever le vernis restant : [<img class="aligncenter wp-image-756 size-large" src="http://sivigik.com/wp-content/uploads/2016/08/IMG_5338-1024x768.jpg" alt="IMG_5338" width="1024" height="768" />][7] Perçage des trous: [<img class="aligncenter wp-image-757 size-large" src="http://sivigik.com/wp-content/uploads/2016/08/IMG_5339-1024x768.jpg" alt="IMG_5339" width="1024" height="768" />][8] Soudage des premiers composants : [<img class="aligncenter wp-image-758 size-large" src="http://sivigik.com/wp-content/uploads/2016/08/IMG_5340-1024x768.jpg" alt="IMG_5340" width="1024" height="768" />][9] [<img class="aligncenter wp-image-759 size-large" src="http://sivigik.com/wp-content/uploads/2016/08/IMG_5341-1024x768.jpg" alt="IMG_5341" width="1024" height="768" />][10] Je n'ai malheureusement pas pris en photo le circuit final, je compte sur vous pour utiliser votre imagination ! 
## <span style="color: #ff6600;">Fabrication du boîtier</span> J'ai réalisé le boîtier à l'aide d'un logiciel de 

[conception 3D][11] pour obtenir des fichiers compatibles avec le logiciel de l'imprimante 3D. [<img class="wp-image-764 size-full aligncenter" src="http://sivigik.com/wp-content/uploads/2016/08/Capture2.jpg" alt="Capture2" width="969" height="693" />][12] [<img class="wp-image-765 aligncenter" src="http://sivigik.com/wp-content/uploads/2016/08/Capture-1024x721.jpg" alt="Capture" width="969" height="682" />][13]   
## <span style="color: #ff6600;">Le résultat</span> Après beaucoup de difficulté pour faire rentrer le circuit imprimé, le transformateur, les ports USB, ... le boîtier et fermé avec 4 vis, puis un coup de peinture noire et voila le résultat : 

[<img class="wp-image-760 size-large aligncenter" src="http://sivigik.com/wp-content/uploads/2016/08/IMG_5452-1024x768.jpg" alt="IMG_5452" width="1024" height="768" />][1] Vous pouvez maintenant recharger jusqu'à 4 fois votre portable !  

 [1]: /media/article/10/attachments/IMG_5452.jpg
 [2]: /media/article/10/attachments/DC-DC-converteur.jpg
 [3]: http://sivigik.com/2015/06/larduino/
 [4]: https://www.youtube.com/watch?v=b_hZYqCtE9U
 [5]: /media/article/10/attachments/sécurité-1.jpg
 [6]: /media/article/10/attachments/IMG_5337.jpg
 [7]: /media/article/10/attachments/IMG_5338.jpg
 [8]: /media/article/10/attachments/IMG_5339.jpg
 [9]: /media/article/10/attachments/IMG_5340.jpg
 [10]: /media/article/10/attachments/IMG_5341.jpg
 [11]: http://sivigik.com/2016/02/introduction-a-la-cao/
 [12]: /media/article/10/attachments/Capture2.jpg
 [13]: /media/article/10/attachments/Capture.jpg

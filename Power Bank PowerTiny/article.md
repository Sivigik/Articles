# <span style="color: #ff6600;">Le PowerTiny</span> Vous en avez marre d'avoir pour qu�te principale de trouver une prise ou un port USB quand vous sortez de chez vous? Les 

**powerbanks** du commerce ne vous satisfont pas ? Vous avez des batteries � recycler ? La r�ponse � toutes ces questions est simple : **PowerTiny** le chargeur nomade � faire chez soi, simple, puissant et �conomique! ![](/media/article/10/attachments/)
## <span style="color: #ff6600;">Liste des composants:</span>

*   Une Batterie de PC portable, celle que j'ai choisie avait 4 �l�ments 3,7 V de 2500 mAh
*   Un convertisseur DC-DC de type Boost, facilement trouvable sur Ebay (par exemple)[<img class="size-medium wp-image-761 aligncenter" src="http://sivigik.com/wp-content/uploads/2016/08/DC-DC-converteur-300x300.jpg" alt="DC-DC converteur" width="300" height="300" />][2]
<li style="text-align: left;">
  �Un Attiny 84
</li>
*   Programmateur ISP (j'utilise une [arduino][3])
*   Des MOSFET (r�cup�r�s sur une carte m�re de PC portable), transistor, r�sistances, condensateurs, DEL, ....
*   Mat�riel de prototypage de circuit imprim�

## <span style="color: #ff6600;">Fabrication d'une protection de batterie</span> Les batteries de type LiPo sont tr�s sensibles aux d�charges brutales et d�chargement trop important ( < 3 V), il ne faut donc pas relier directement le transformateur � la batterie, un circuit interm�diaire doit surveiller les charges qui passent. Pour cela : soit vous utilisez un circuit de protection r�cup�rable sur des batteries de Smartphones, la vid�o suivante explique tr�s bien comment r�aliser sa propre powerbank facilement (sans PCB � r�aliser): 

[Fabriquer un chargeur portable : Incroyables Exp�riences [88] Batterie externe USB / Power bank][4]�ou alors vous le faites vous-m�me ! J'ai choisi d'utiliser un microcontr�leur pour diminuer la quantit� de composants � utiliser, et donc de diminuer la place (le circuit �tant enti�rement r�alisable sans microcontr�leur). Le circuit de charge (diode D6 et r�sistance R6) n'est pas de moi, je l'ai pris dans la vid�o du dessus, j'ai seulement ajout� un MOSFET pour �viter que la batterie se d�charge apr�s avoir d�branch� le chargeur. (Le connecteur de droite sert uniquement � envoyer le programme et � d�boguer.) 
### �<span style="color: #0000ff;">Sch�ma :</span>

![](/media/article/10/attachments/s�curit�-1-1024x720.jpg]
### <span style="color: #0000ff;">R�alisation de circuit imprim� :</span> La partie en bas � gauche sur le sch�ma n'est pas pr�sente sur les photos de la r�alisation, car je l'ai ajout� plus tard pour r�soudre un bug, il permet de RESET quand on fait charger la powerbank, ce qui fait sortir la puce du mode " �conomie d'�nergie " (consomme seulement 300 �A) �quand la batterie est compl�tement vide. Gravure du circuit au perchlorure de fer: 

[<img class="aligncenter wp-image-755 size-large" src="http://sivigik.com/wp-content/uploads/2016/08/IMG_5337-1024x768.jpg" alt="IMG_5337" width="1024" height="768" />][6] Nettoyage � l'eau, puis � l'ac�tone pour enlever le vernis restant : [<img class="aligncenter wp-image-756 size-large" src="http://sivigik.com/wp-content/uploads/2016/08/IMG_5338-1024x768.jpg" alt="IMG_5338" width="1024" height="768" />][7] Per�age des trous: [<img class="aligncenter wp-image-757 size-large" src="http://sivigik.com/wp-content/uploads/2016/08/IMG_5339-1024x768.jpg" alt="IMG_5339" width="1024" height="768" />][8] Soudage des premiers composants : [<img class="aligncenter wp-image-758 size-large" src="http://sivigik.com/wp-content/uploads/2016/08/IMG_5340-1024x768.jpg" alt="IMG_5340" width="1024" height="768" />][9] [<img class="aligncenter wp-image-759 size-large" src="http://sivigik.com/wp-content/uploads/2016/08/IMG_5341-1024x768.jpg" alt="IMG_5341" width="1024" height="768" />][10] Je n'ai malheureusement pas pris en photo le circuit final, je compte sur vous pour utiliser votre imagination ! 
## <span style="color: #ff6600;">Fabrication du bo�tier</span> J'ai r�alis� le bo�tier � l'aide d'un logiciel de 

[conception 3D][11] pour obtenir des fichiers compatibles avec le logiciel de l'imprimante 3D. [<img class="wp-image-764 size-full aligncenter" src="http://sivigik.com/wp-content/uploads/2016/08/Capture2.jpg" alt="Capture2" width="969" height="693" />][12] [<img class="wp-image-765 aligncenter" src="http://sivigik.com/wp-content/uploads/2016/08/Capture-1024x721.jpg" alt="Capture" width="969" height="682" />][13] � 
## <span style="color: #ff6600;">Le r�sultat</span> Apr�s beaucoup de difficult� pour faire rentrer le circuit imprim�, le transformateur, les ports USB, ... le bo�tier et ferm� avec 4 vis, puis un coup de peinture noire et voila le r�sultat : 

[<img class="wp-image-760 size-large aligncenter" src="http://sivigik.com/wp-content/uploads/2016/08/IMG_5452-1024x768.jpg" alt="IMG_5452" width="1024" height="768" />][1] Vous pouvez maintenant recharger jusqu'� 4 fois votre portable ! �

 [1]: /media/article/10/attachments/IMG_5452.jpg
 [2]: /media/article/10/attachments/DC-DC-converteur.jpg
 [3]: http://sivigik.com/2015/06/larduino/
 [4]: https://www.youtube.com/watch?v=b_hZYqCtE9U
 [5]: /media/article/10/attachments/s�curit�-1.jpg
 [6]: /media/article/10/attachments/IMG_5337.jpg
 [7]: /media/article/10/attachments/IMG_5338.jpg
 [8]: /media/article/10/attachments/IMG_5339.jpg
 [9]: /media/article/10/attachments/IMG_5340.jpg
 [10]: /media/article/10/attachments/IMG_5341.jpg
 [11]: http://sivigik.com/2016/02/introduction-a-la-cao/
 [12]: /media/article/10/attachments/Capture2.jpg
 [13]: /media/article/10/attachments/Capture.jpg

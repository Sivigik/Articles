# <span style="color: #ff6600">Introduction</span>

<p style="text-align: justify">
  Il y a quelques ann�es j'ai r�cup�r� un ch�ssis de voiture sans permis sur lequel il restait dessus le diff�rentiel et la cr�maill�re.�Au d�but j'avais install� un moteur de 5 CV � essence, il avait suffisamment de couple pour d�neiger jusqu'� 30 cm de neige, mais il ne pouvait pas d�passer les 20 km/h (mesur�s avec un compteur de v�lo). Donc j'ai voulu voir ce que cela pouvait donner avec un moteur �lectrique.
</p>

# <span style="color: #ff6600">La r�alisation</span> Maintenant nous allons voir comment j'ai converti la propulsion thermique en �lectrique. 

## <span style="color: #ff9900">Le moteur</span>

<p style="text-align: justify">
  J'avais un ancien d�marreur de voiture, il consommait une cinquantaine d'amp�res sous 12 V, soit une puissance d'� peu pr�s 600 W. Le probl�me �tait qu'il poss�dait qu'un seul palier, il a donc fallut que je lui en fasse un deuxi�me du c�t� de la poulie, pour pouvoir m'en servir.
</p>

![image1][1] On voit sur cette image l'installation du roulement � billes pour pouvoir mettre en place son support. 
## <span style="color: #ff9900">Les batteries</span>

![image2][2] J'ai mis tout simplement des batteries au plomb. <p style="text-align: justify">
  Je les ai ensuite branch�s en d�rivation, pour avoir la capacit� la plus importante possible, pour cela j'ai utilis� du c�ble �lectrique en aluminium de 12 mm�, cela n'emp�chait pas les c�bles de chauffer lors du fonctionnement du moteur.
</p>

## <span style="color: #ff9900">La transmission</span>

<p style="text-align: justify">
  La transmission est faite � l'aide d'une courroie et deux poulies, une sur le moteur et l'autre sur l'axe d'entr�e de la " boite de vitesse ". Le moteur tenu pas deux boulons, un qui sert de charni�re, l'autre fix� � une tige filet�e, pour permettre de r�gler, l'�cart la tension de la courroie.
</p>

![image3][3] Nous voyons les fixations du moteur sur cette image. 
## <span style="color: #ff9900">Contr�le du moteur</span>

<p style="text-align: justify">
  Cette partie n'est pas termin�e, pour l'instant il y a seulement qu'un gros interrupteur activ� par la p�dale d'acc�l�rateur. Je compte mettre au point un onduleur, cr�� � partir de transistors de puissance de type MOSFET, avec leur driver de type UCC 37322P et UCC 37321P, et un ATmega328P pour le contr�le de l�excitation des bobines du moteur.
</p>

 [1]: http://www.heberger-image.fr/data/images/51597_moteur.jpg
 [2]: http://www.heberger-image.fr/data/images/77824_avant_1.jpg
 [3]: http://www.heberger-image.fr/data/images/49565_transmission_2.jpg
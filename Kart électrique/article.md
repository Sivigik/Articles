# <span style="color: #ff6600">Introduction</span>

<p style="text-align: justify">
  Il y a quelques années j'ai récupéré un châssis de voiture sans permis sur lequel il restait dessus le différentiel et la crémaillère. Au début j'avais installé un moteur de 5 CV à essence, il avait suffisamment de couple pour déneiger jusqu'à 30 cm de neige, mais il ne pouvait pas dépasser les 20 km/h (mesurés avec un compteur de vélo). Donc j'ai voulu voir ce que cela pouvait donner avec un moteur électrique.
</p>

# <span style="color: #ff6600">La réalisation</span> Maintenant nous allons voir comment j'ai converti la propulsion thermique en électrique. 

## <span style="color: #ff9900">Le moteur</span>

<p style="text-align: justify">
  J'avais un ancien démarreur de voiture, il consommait une cinquantaine d'ampères sous 12 V, soit une puissance d'à peu près 600 W. Le problème était qu'il possédait qu'un seul palier, il a donc fallut que je lui en fasse un deuxième du côté de la poulie, pour pouvoir m'en servir.
</p>

![image1][1] On voit sur cette image l'installation du roulement à billes pour pouvoir mettre en place son support. 
## <span style="color: #ff9900">Les batteries</span>

![image2][2] J'ai mis tout simplement des batteries au plomb. <p style="text-align: justify">
  Je les ai ensuite branchés en dérivation, pour avoir la capacité la plus importante possible, pour cela j'ai utilisé du câble électrique en aluminium de 12 mm², cela n'empêchait pas les câbles de chauffer lors du fonctionnement du moteur.
</p>

## <span style="color: #ff9900">La transmission</span>

<p style="text-align: justify">
  La transmission est faite à l'aide d'une courroie et deux poulies, une sur le moteur et l'autre sur l'axe d'entrée de la " boite de vitesse ". Le moteur tenu pas deux boulons, un qui sert de charnière, l'autre fixé à une tige filetée, pour permettre de régler, l'écart la tension de la courroie.
</p>

![image3][3] Nous voyons les fixations du moteur sur cette image. 
## <span style="color: #ff9900">Contrôle du moteur</span>

<p style="text-align: justify">
  Cette partie n'est pas terminée, pour l'instant il y a seulement qu'un gros interrupteur activé par la pédale d'accélérateur. Je compte mettre au point un onduleur, créé à partir de transistors de puissance de type MOSFET, avec leur driver de type UCC 37322P et UCC 37321P, et un ATmega328P pour le contrôle de l’excitation des bobines du moteur.
</p>

 [1]: http://www.heberger-image.fr/data/images/51597_moteur.jpg
 [2]: http://www.heberger-image.fr/data/images/77824_avant_1.jpg
 [3]: http://www.heberger-image.fr/data/images/49565_transmission_2.jpg
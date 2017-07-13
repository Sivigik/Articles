# <span style="color: #ff6600">Introduction</span>

<p style="text-align: justify">
  La bobine de Tesla a �t� invent�e par un am�ricain, Nikola Tesla, dans les ann�es 1890. Le fonctionnement consiste � avoir deux bobines coupl�es et en r�sonance (on peut aussi le faire avec trois bobines). La r�sonance se calcule, mais elle peut aussi �tre r�gl�e lors de la mise sous tension de l�appareil : soit en utilisant un oscilloscope pour r�gler l'inductance de la bobine primaire par rapport � une fr�quence th�orique, ou alors avec " les moyens du pauvre " on r�gle le primaire en allongeant ou raccourcissant le bobine primaire pour savoir � quel endroit les arcs sont les plus longs. Il y a aussi la capacit� de l'�lectrode torique � calculer, ou bien il faut modifier ses dimensions en fonction d'une fois de plus de la taille de l'arc.
</p>

## <span style="color: #ff9900">Caract�ristiques</span>

**Attention Tr�s Haute Tension** 
*   **Alimentation:** Transformateur de mesure EDF: 100 V primaire => 20 KV secondaire, Puissance de 3500 VA.
*   **Condensateur:�**Condensateur fait maison (bouteille en verre): 20 nf, isolation max = 18 KV.
*   **Bobine primaire:** C�ble de cuivre: 12 mm�.
*   **Bobine secondaire:** Fils de cuivre �maill�: D = 0.4 mm, bobin� sur un tube PVC de 800 de haut et d'un diam�tre de 100mm.

# <span style="color: #ff6600">Puissance</span> Consommation de 19 A en 75 V soit une puissance de 1200 W. 

# <span style="color: #ff6600">Longueur des arcs</span> Leurs longueurs maximales est de 700 mm. Donc une tension approximative de 2 000 000 V soit 2 MV. 

# <span style="color: #ff6600">Fonctionnement</span>

<p style="text-align: justify">
  Le principe de fonctionnement est principalement bas� sur le chargement et d�chargement du condensateur dans la bobine primaire. La r�sonance entre les deux bobines est primordiale pour ce syst�me. La r�sonance est l'effet cr�� lorsque la premi�re impulsion de courant est envoy� dans le primaire, un fort champ �lectromagn�tique est g�n�r�, ce qui va �tre absorb� par la bobine secondaire par le principe d'un transformateur traditionnel qui a pour diff�rence de poss�der un noyau d'air au lieu d'�tre en un fer ferromagn�tique. Lorsque la bobine absorbe cette �nergie, de l'�lectricit� est g�n�r�, elle monte en haut de la bobine, puis elle redescend. Le principe de r�sonance r�side dans le fait que la deuxi�me d�charge du condensateur doit �tre envoy�e au moment pr�cis, o� le courant va redescendre, ce qui engendre une tr�s grande diff�rence de potentielle entre le bas et le haut de la bobine secondaire. Donc cette diff�rence de potentielle augmentant, la ionisation de l'air se produit, et on obtient un arc �lectrique. Cette r�sonance se r�gle par le biais de diff�rentes modifications du circuit :
</p>

*   La capacit� du condensateur puisque nous sommes dans un circuit LC (bobine condensateur).
*   L'inductance de la bobine primaire
*   L'inductance de la bobine secondaire

<p style="text-align: justify">
  La m�thode la plus simple est de faire varier l'inductance de la bobine primaire, d'une des mani�res expliqu�es dans l'introduction. La seconde m�thode est de modifier l'inductance de la bobine secondaire, cela est bien plus compliqu� puisqu'elle est g�n�ralement vernie, et est tr�s sensible puisque plusieurs centaines de milliers de volts la traversent. Mais il existe un moyen : toutes les bobines poss�dent une capacit�, qui est propre � leur inductance, donc en mettant un condensateur entre les bornes de la bobine nous faisons varier son inductance. On ne peut pas mettre de condensateur de cette mani�re puisque nous sommes face � des tensions de l'ordre du million de volts par exemple ma bobine que nous �tudions (la tore entre alors en jeu) cr�e une capacit� de quelques pico Faraday entre le sommet de la bobine et l'air ambiant qui repr�sente la masse, cela suffit pour faire varier l'inductance de la bobine et permettre l'accord.
</p>

# <span style="color: #ff6600">Sch�ma</span>

![image1][1] 
# <span style="color: #ff6600">�clateurs</span>

## <span style="color: #ff9900">�clateur statique</span>

<p style="text-align: justify">
  Le fonctionnement d'un �clateur statique est tr�s simple, il emploie seulement la propri�t� physique de l'air, qui est isolant � basse tension et qui est conducteur lorsque la tension est suffisamment �lev�e (l'air s'ionise). Donc lorsque le condensateur se charge, la tension augmente � ses bornes, puis il arrive le moment o� la tension est suffisante pour ioniser l'air qui est entre les �lectrode de l'�clateur. Le condensateur peut donc maintenant se vider dans la bobine primaire. Mais il a comme inconv�nient d'avoir la fr�quence de d�chargement des condensateur qui augmente, avec l��chauffement des �lectrodes, c'est pour cela qu'il faut les refroidir continuellement � l'aide d'un gros ventilateur pas exemple.
</p>

## <span style="color: #ff9900">�clateur rotatif</span>

<p style="text-align: justify">
  Ce type d'�clateur est le m�lange d'un �clateur statique et d'un relais de puissance. Il est g�n�ralement (j'ai utilis� cette m�thode l�, pour faire le mien) sous la forme d'un disque qui dispose d��lectrodes sur son p�rim�tre qui passent devant deux �lectrodes fixes (qui ne bougent pas par rapport au sol) ; � chaque passage les �lectrodes du disque vont faire contact avec les �lectrodes fixes ce qui va engendrer le d�chargement du condensateur. Pourquoi statique? Tous simplement par du fait que lorsque des �lectrodes se rapprochent l'une de l'autre, avant que le contact ne se fasse, un arc s'amorce entre elles. Cela a aussi l'avantage d'avoir une intensit� qui n'augmente pas directement mais plus lentement.
</p>

<p style="text-align: justify">
  Le principal atout de ce syst�me est que la fr�quence reste constante lors du fonctionnement, les �lectrodes du disque ne chauffent quasiment pas, par contre celles qui sont fixes chauffent et si on ne fait pas attention, elles peuvent entrer en fusion. Ce qui peut tr�s rapidement devenir tr�s dangereux, puisque de l'acier en fusion est projet� par le disque dans toutes les directions. Il faut faire attention aussi de r�aliser un disque parfaitement �quilibr� et aussi �vit� d'avoir les �lectrode fixes qui soit trop proches d'elles, puisque le disque peut se mettre � vibrer lorsque l'arc s'amorce. Cela m'est arriv�, avec un disque en plexiglas qui a �t� totalement d�truit, puis comme il tournait vite (10 000 tr/min) les �lectrodes ont �t� projet�es en l'air et ont laiss�s de gros impactes dans la planche du support.
</p>

# <span style="color: #ff6600">Image de la b�te</span> �clateur rotatif, fait � partir d'une disqueuse tournant � 11 000 tr/min: 

![image2][2] <p style="text-align: justify">
  � droite se trouve le transformateur haute tension, avec devant lui un transformateur de micro-onde rebobin�, qui sert d'inducteur pour diminuer la puissance du transformateur HT. Au milieu se trouve un transformateur d'isolement que j'ai aussi rebobin� pour avoir un primaire 230 V et un secondaire 75 V au lieu de 230 V primaire et de m�me en secondaire. Au fond � gauche se trouve le condensateur haute tension, c'est un sceau avec des bouteilles de verre, il est remplit d'eau sal�e, et d'huile pour isoler.
</p>

![image7][3] <p style="text-align: justify">
  Boitier de commande, il comporte deux variateurs de tension � base de triac, un pour la tension du transformateur, l'autre pour l��clateur rotatif, ce qui a pour effet de faire varier la vitesse de rotation du disque, donc faire varier aussi la fr�quence.
</p>

![image8][4] Vue de l'ensemble de la Bobine de Tesla: ![image3][5] 
# <span style="color: #ff6600">Monstres en fonctionnement</span>

![image4][6] ![image5][7] ![image6][8] 
# <span style="color: #ff6600">Vid�o</span> [youtube http://www.youtube.com/watch?v=JJTjoCbeFsI&w=720&h=460]

 [1]: http://www.heberger-image.fr/data/images/14936_Sch_ma_Bobine_de_Tesla.jpg
 [2]: http://www.heberger-image.fr/data/images/98676_DSC00483.jpg
 [3]: http://www.heberger-image.fr/data/images/56288_DSC03334.jpg
 [4]: http://www.heberger-image.fr/data/images/25812_Boitier_commande.jpg
 [5]: http://www.heberger-image.fr/data/images/64915_Tesla_enti_re.jpg
 [6]: http://www.heberger-image.fr/data/images/63743_Arc_3.jpg
 [7]: http://www.heberger-image.fr/data/images/75899_Arc_1.jpg
 [8]: http://www.heberger-image.fr/data/images/19964_Arc_2.jpg
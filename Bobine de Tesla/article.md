# <span style="color: #ff6600">Introduction</span>

<p style="text-align: justify">
  La bobine de Tesla a été inventée par un américain, Nikola Tesla, dans les années 1890. Le fonctionnement consiste à avoir deux bobines couplées et en résonance (on peut aussi le faire avec trois bobines). La résonance se calcule, mais elle peut aussi être réglée lors de la mise sous tension de l’appareil : soit en utilisant un oscilloscope pour régler l'inductance de la bobine primaire par rapport à une fréquence théorique, ou alors avec " les moyens du pauvre " on règle le primaire en allongeant ou raccourcissant le bobine primaire pour savoir à quel endroit les arcs sont les plus longs. Il y a aussi la capacité de l'électrode torique à calculer, ou bien il faut modifier ses dimensions en fonction d'une fois de plus de la taille de l'arc.
</p>

## <span style="color: #ff9900">Caractéristiques</span>

**Attention Très Haute Tension** 
*   **Alimentation:** Transformateur de mesure EDF: 100 V primaire => 20 KV secondaire, Puissance de 3500 VA.
*   **Condensateur: **Condensateur fait maison (bouteille en verre): 20 nf, isolation max = 18 KV.
*   **Bobine primaire:** Câble de cuivre: 12 mm².
*   **Bobine secondaire:** Fils de cuivre émaillé: D = 0.4 mm, bobiné sur un tube PVC de 800 de haut et d'un diamètre de 100mm.

# <span style="color: #ff6600">Puissance</span> Consommation de 19 A en 75 V soit une puissance de 1200 W. 

# <span style="color: #ff6600">Longueur des arcs</span> Leurs longueurs maximales est de 700 mm. Donc une tension approximative de 2 000 000 V soit 2 MV. 

# <span style="color: #ff6600">Fonctionnement</span>

<p style="text-align: justify">
  Le principe de fonctionnement est principalement basé sur le chargement et déchargement du condensateur dans la bobine primaire. La résonance entre les deux bobines est primordiale pour ce système. La résonance est l'effet créé lorsque la première impulsion de courant est envoyé dans le primaire, un fort champ électromagnétique est généré, ce qui va être absorbé par la bobine secondaire par le principe d'un transformateur traditionnel qui a pour différence de posséder un noyau d'air au lieu d'être en un fer ferromagnétique. Lorsque la bobine absorbe cette énergie, de l'électricité est généré, elle monte en haut de la bobine, puis elle redescend. Le principe de résonance réside dans le fait que la deuxième décharge du condensateur doit être envoyée au moment précis, où le courant va redescendre, ce qui engendre une très grande différence de potentielle entre le bas et le haut de la bobine secondaire. Donc cette différence de potentielle augmentant, la ionisation de l'air se produit, et on obtient un arc électrique. Cette résonance se règle par le biais de différentes modifications du circuit :
</p>

*   La capacité du condensateur puisque nous sommes dans un circuit LC (bobine condensateur).
*   L'inductance de la bobine primaire
*   L'inductance de la bobine secondaire

<p style="text-align: justify">
  La méthode la plus simple est de faire varier l'inductance de la bobine primaire, d'une des manières expliquées dans l'introduction. La seconde méthode est de modifier l'inductance de la bobine secondaire, cela est bien plus compliqué puisqu'elle est généralement vernie, et est très sensible puisque plusieurs centaines de milliers de volts la traversent. Mais il existe un moyen : toutes les bobines possèdent une capacité, qui est propre à leur inductance, donc en mettant un condensateur entre les bornes de la bobine nous faisons varier son inductance. On ne peut pas mettre de condensateur de cette manière puisque nous sommes face à des tensions de l'ordre du million de volts par exemple ma bobine que nous étudions (la tore entre alors en jeu) crée une capacité de quelques pico Faraday entre le sommet de la bobine et l'air ambiant qui représente la masse, cela suffit pour faire varier l'inductance de la bobine et permettre l'accord.
</p>

# <span style="color: #ff6600">Schéma</span>

![image1][1] 
# <span style="color: #ff6600">Éclateurs</span>

## <span style="color: #ff9900">Éclateur statique</span>

<p style="text-align: justify">
  Le fonctionnement d'un éclateur statique est très simple, il emploie seulement la propriété physique de l'air, qui est isolant à basse tension et qui est conducteur lorsque la tension est suffisamment élevée (l'air s'ionise). Donc lorsque le condensateur se charge, la tension augmente à ses bornes, puis il arrive le moment où la tension est suffisante pour ioniser l'air qui est entre les électrode de l'éclateur. Le condensateur peut donc maintenant se vider dans la bobine primaire. Mais il a comme inconvénient d'avoir la fréquence de déchargement des condensateur qui augmente, avec l’échauffement des électrodes, c'est pour cela qu'il faut les refroidir continuellement à l'aide d'un gros ventilateur pas exemple.
</p>

## <span style="color: #ff9900">Éclateur rotatif</span>

<p style="text-align: justify">
  Ce type d'éclateur est le mélange d'un éclateur statique et d'un relais de puissance. Il est généralement (j'ai utilisé cette méthode là, pour faire le mien) sous la forme d'un disque qui dispose d’électrodes sur son périmètre qui passent devant deux électrodes fixes (qui ne bougent pas par rapport au sol) ; à chaque passage les électrodes du disque vont faire contact avec les électrodes fixes ce qui va engendrer le déchargement du condensateur. Pourquoi statique? Tous simplement par du fait que lorsque des électrodes se rapprochent l'une de l'autre, avant que le contact ne se fasse, un arc s'amorce entre elles. Cela a aussi l'avantage d'avoir une intensité qui n'augmente pas directement mais plus lentement.
</p>

<p style="text-align: justify">
  Le principal atout de ce système est que la fréquence reste constante lors du fonctionnement, les électrodes du disque ne chauffent quasiment pas, par contre celles qui sont fixes chauffent et si on ne fait pas attention, elles peuvent entrer en fusion. Ce qui peut très rapidement devenir très dangereux, puisque de l'acier en fusion est projeté par le disque dans toutes les directions. Il faut faire attention aussi de réaliser un disque parfaitement équilibré et aussi évité d'avoir les électrode fixes qui soit trop proches d'elles, puisque le disque peut se mettre à vibrer lorsque l'arc s'amorce. Cela m'est arrivé, avec un disque en plexiglas qui a été totalement détruit, puis comme il tournait vite (10 000 tr/min) les électrodes ont été projetées en l'air et ont laissés de gros impactes dans la planche du support.
</p>

# <span style="color: #ff6600">Image de la bête</span> Éclateur rotatif, fait à partir d'une disqueuse tournant à 11 000 tr/min: 

![image2][2] <p style="text-align: justify">
  À droite se trouve le transformateur haute tension, avec devant lui un transformateur de micro-onde rebobiné, qui sert d'inducteur pour diminuer la puissance du transformateur HT. Au milieu se trouve un transformateur d'isolement que j'ai aussi rebobiné pour avoir un primaire 230 V et un secondaire 75 V au lieu de 230 V primaire et de même en secondaire. Au fond à gauche se trouve le condensateur haute tension, c'est un sceau avec des bouteilles de verre, il est remplit d'eau salée, et d'huile pour isoler.
</p>

![image7][3] <p style="text-align: justify">
  Boitier de commande, il comporte deux variateurs de tension à base de triac, un pour la tension du transformateur, l'autre pour l’éclateur rotatif, ce qui a pour effet de faire varier la vitesse de rotation du disque, donc faire varier aussi la fréquence.
</p>

![image8][4] Vue de l'ensemble de la Bobine de Tesla: ![image3][5] 
# <span style="color: #ff6600">Monstres en fonctionnement</span>

![image4][6] ![image5][7] ![image6][8] 
# <span style="color: #ff6600">Vidéo</span> [youtube http://www.youtube.com/watch?v=JJTjoCbeFsI&w=720&h=460]

 [1]: http://www.heberger-image.fr/data/images/14936_Sch_ma_Bobine_de_Tesla.jpg
 [2]: http://www.heberger-image.fr/data/images/98676_DSC00483.jpg
 [3]: http://www.heberger-image.fr/data/images/56288_DSC03334.jpg
 [4]: http://www.heberger-image.fr/data/images/25812_Boitier_commande.jpg
 [5]: http://www.heberger-image.fr/data/images/64915_Tesla_enti_re.jpg
 [6]: http://www.heberger-image.fr/data/images/63743_Arc_3.jpg
 [7]: http://www.heberger-image.fr/data/images/75899_Arc_1.jpg
 [8]: http://www.heberger-image.fr/data/images/19964_Arc_2.jpg
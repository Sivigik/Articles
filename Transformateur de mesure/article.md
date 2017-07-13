# <span style="color: #ff6600;">Introduction</span>

<p style="text-align: justify;">
  Les réseaux de distribution d’électricité acheminent l'énergie des centrales électriques aux particuliers. Ces centrales sont composées de plusieurs parties, qui s'adaptent à la quantité d'électricité qui les traversent.
</p>

<p style="text-align: justify;">
  Prenons l'exemple d'une centrale hydroélectrique qui génère une puissance de l'ordre de 20 MW. Si l'électricité était transportée sous une tension qui nous est familière, c'est-à-dire du monophasé 230 Vac (tension efficace) à 50 Hz ou du triphasé en 380 Vac (tension efficace) à 50Hz, nous aurions une intensité de 87 kA en 230 Vac, ou du 17 kA par phase en 380 Vac, pour le triphasé. Ce qui nécessiterait pour parcourir 100 km des câbles de section (attention les yeux) 29 580 000 mm² pour du 230 V et 5 780 000 mm² pour du triphasé (en admettant une chute de 10 Volts en fin de ligne). L'utilisation de telles tensions pour transporter notre précieuse énergie électrique aurait entraînée l'épuisement d'une grande partie de nos réserves mondiales de cuivre ou autre conducteur. Ainsi, au début du XX ème siècle, de grands ingénieurs (en particulier les fondateurs de <strong>General Electric</strong>) ont mis au point les premiers réseaux à Haute tension.
</p>

<p style="text-align: justify;">
  En reprenant l'exemple de la centrale hydroélectrique 20 MW, les génératrices de cette centrale produisent 20 kV en triphasé (en général). La tension étant trop élevée, des transformateurs de potentiel et de courant y sont présent pour diviser la tension et l'intensité par des constantes. Il est ainsi possible de vérifier la tension avec des composants fonctionnant en basse tension, ce qui a pour avantage d'améliorer la sécurité des techniciens et de réduire le coup du matériel. L'électricité après être passée par ces équipements pour être contrôlée (je passe tout ce qui concerne le redressement du cos f, les sécurités,...) est acheminée à un transformateur qui va l'élever de 20 kV à 400 kV.
</p>

<p style="text-align: justify;">
  Calculons maintenant les diamètres des câbles basse tension (soit ceux qui sortent des génératrices). Disons qu'il y a 100 m entre les génératrices et le transformateur, il y a une intensité de 277 A, donc la section est de 9 418 mm², pour une chute de 100 V, ce qui est réalisable, et pas trop coûteux par rapport à ce que nous avons vu plus tôt. Maintenant reprenons 100 km à parcourir mais cette fois en 400 kV. On a 17 A, avec une section de 11,56 mm² pour une chute de 5 000 V (cela n'influence pas grand chose à une tension aussi élevée).
</p>

<p style="text-align: justify;">
  Ceci montre l'importance des transformateurs Haute tension et des transformateurs de mesure dans ces domaines.
</p>   

# <span style="color: #ff6600;">Les transformateurs de potentiel</span>   

<p style="text-align: justify;">
  Ils sont utilisés pour faire des mesures sur les réseaux moyens, de hautes ou de très hautes tensions comme nous l'avons vu dans l'introduction.
</p>

<p style="text-align: justify;">
  Je vais maintenant traiter l'exemple d'un seul type de ces transformateurs de mesure, puisque j'en possède seulement de ce type. Il s'agit de ceux qui mesurent les lignes de 20 kV.
</p>

<p style="text-align: justify;">
  Ils possèdent un primaire extrêmement bien isolé pour cette tension, puisqu'ils doivent résister aux hausses de tension générées par exemples quand la foudre tombe sur les câbles (cela est de moins en moins fréquent, puisque une grande partie des réseaux 20 kV sont enterrés). En conséquence ils doivent résister aux fortes intensités qui sont générée par le même phénomène, pour cela ils ont un bobinage sur dimensionné.
</p>

![image1][1] ![image6][2] <p style="text-align: justify;">
  Sur les étiquettes de ces transformateurs, la puissance est divisée par 10, il y est écrit qu'elle est de 350 VA, elle est ainsi écrite pour respecter des normes, mais le transformateur fournit plus de 3 500 VA, car il est largement sur dimensionné, attention à ne pas dépasser cette puissance car il risquerait de chauffer sans que l'on puisse s'en rendre compte à cause de l'épaisse isolation.
</p>

<p style="text-align: justify;">
  Les transformateurs de potentiel sont les plus utiles dans mes expériences, ils permettent d'obtenir une grande puissance (vu au dessus), mais il ne faut jamais l'alimenter directement en 100 V (tension maximale conseillée, ce qui fournit 20kV au secondaire) si vous comptez faire des arcs électriques avec, car lors de la mise en court-circuit du secondaire, la consommation du primaire sera colossale, il peut tirer facilement plus de 100 A. Soit votre alimentation crame et le disjoncteur coupe le courant, soit, dans le pire des cas, le primaire du transformateur HT brûle, et cela est extrêmement compliqué à rembobiner à cause de l'isolant. Pour éviter cela il faut le mettre en série avec un ballast, ou un transformateur basse tension, qui limitera l'intensité à moins de 35 A. Le plus simple pour réaliser ce genre de "résistance" est de prendre un transformateur de micro-onde, auquel il faut enlever le secondaire (partie 2 000 V dans le micro-onde) pour le remplacer avec un bobinage en fils électriques de 2,5 mm² tout simplement. Si sa résistance est trop grande, court-circuiter le primaire (là où entrait le 230 V dans le micro-onde).
</p>

# <span style="color: #ff6600;">Les transformateurs d'intensité</span>

<p style="text-align: justify;">
  Les transformateurs d'intensité sont employés dans la mesure du courant qui passe sur les réseaux. Ils sont placés en série avec la ligne électrique. Ainsi, quand un courant passe dans le primaire, le flux magnétique est envoyé dans un secondaire à l'aide d'un tore (ici en fer puisque nous sommes sur des réseaux basse fréquence, 50 Hz), qui est isolé par rapport à la ligne où le courant est mesuré. Pour y mesurer l'intensité qui passe à n'importe quelle tension.
</p>

<p style="text-align: justify;">
  Le courant est généralement divisé par un facteur constant. Ce facteur, qui lie l'intensité qui passe dans le primaire et celle qui passe dans le secondaire, dépend du nombre de spires qu'il y a au primaire et au secondaire.
</p>

<p style="text-align: justify;">
  Pour un transformateur d'intensité sous la forme d'un tore placé directement sur le câble et avec un secondaire relié aux outils de mesure ou d'affichage (ampèremètre par exemple), la formule pour calculer le facteur est :
</p> [latex] {F = \frac {1} {N_s}} [/latex] La formule pour calculer l'intensité est : [latex]I_p = N_s \times I_s[/latex]           [latex]I_s = \frac {1} {N_s} \times I_p[/latex] 

<p style="text-align: justify;">
  Pour un transformateur d'intensité qui possède un primaire et un secondaire qui sont directement bobinés, le primaire est branché en série par rapport au réseau dont on veut mesurer l'intensité qui le traverse, et le secondaire est relié aux outils de mesure ou d'affichage. La formule est :
</p> [latex]F = \frac {N_p} {N_s}[/latex] La formule pour calculer l'intensité est : [latex]I_p = \frac {N_s} {N_p} \times I_s[/latex]            [latex]I_s = \frac {N_p} {N_s} \times I_p[/latex] [latex]F[/latex] est le facteur. [latex]I_p[/latex] est l'intensité qui traverse le primaire. [latex]I_s[/latex] est l'intensité qui est reçue dans le secondaire. [latex]N_p[/latex] est le nombre de spire dans le primaire du transformateur d'intensité. [latex]N_s[/latex] est le nombre de spire dans le secondaire du transformateur d'intensité. 

# <span style="color: #ff6600;">Où les trouver ?</span>

<p style="text-align: justify;">
  Ce genre de transformateurs est installé dans les centrales électriques, et les centres de redistribution. Des transformateurs de tension à deux phases sont présents sur certaines lignes haute tension isolées. En général, ils sont dans les zones rurales ou montagneuses. Pour s'en procurer il existe plusieurs moyens, mais cela reste très compliqué.
</p>

<p style="text-align: justify;">
  - La première est celle que j'ai utilisée deux fois, ce qui m'a permis d'avoir 6 transformateurs de potentiel et 6 transformateurs d'intensité (ainsi que des fusibles de 20 kV 40 A et 25 A). Cette méthode oblige à connaître une personne qui travaille dans ce milieu, ou à demander gentiment aux techniciens qui changent les équipements haute tension (pour la remise aux normes ou la destruction) s'ils peuvent vendre ou donner le matériel remplacé. Ou encore connaître le propriétaire de la centrale.
</p>

<p style="text-align: justify;">
  - la seconde méthode consiste à regarder de temps en temps sur <strong>Ebay</strong> si il y a des transformateurs à vendre, mais cela est très rare. Je n'en ai jamais vu pour l'instant, mais il y a des personnes qui s'en sont procurés de cette manière.
</p>

<p style="text-align: justify;">
  - La dernière méthode est la plus onéreuse. Il faut acheter le transformateur directement chez le fournisseur, mais il faut demander un devis, puis je doute qu'il vende des transformateurs de mesures haute tension à des particuliers, mais ça doit être faisable. Je pense que pour un transformateur aux normes européennes le prix doit être élevé, autour des 1250 €. Sinon, regardez sur des sites chinois mais le prix du transformateur y est ridicule par rapport aux frais de transport à mon avis, car en général les transformateurs de tension pèsent aux alentours de 35 kg.
</p>

# <span style="color: #ff6600;">Relations de calcul employées</span>
<p style="text-align: justify;">
 La puissance : [latex]P = U \times I[/latex] La section d'un câble en cuivre : [latex]S = 1,7 \times 10^{-2} \times L \times \frac {I} {CT}[/latex] [latex]S[/latex] : Section en [latex]mm^2[/latex]. [latex]1,7 \times 10^{-2}[/latex] est la résistance du cuivre par mètre. [latex]L[/latex] : longueur aller-retour du conducteur en m. [latex]I[/latex] : courant en ampère qui passe. [latex]CT[/latex] : chute de tension admise pour cette distance. 
</p>

# <span style="color: #ff6600;">Photos d'arc électrique</span>

![image2][3] ![image3][4] <p style="text-align: justify;">
  Deux transformateurs 20 kV mis en série pour avoir le neutre où à la masse des transformateurs. On met du 20 kV d'un coté et du - 20 kV de l'autre, pour avoir une différence de potentiel de 40 kV, ils sont alimentés en 100 V avec un transformateur en série pour limiter l'intensité à 26 A.
</p> Quelques images d'arc : 

![image4][5] ![image5][6]


# <span style="color: #ff6600;">Commentaire habile</span>

<p style="text-align: justify;">
Salut à toi !

Quand tu dit « Le plus simple pour réaliser ce genre de “résistance” est de prendre un transformateur de micro-onde, auquel il faut enlever le secondaire (partie 2 000 V dans le micro-onde) pour le remplacer avec un bobinage en fils électriques de 2,5 mm² tout simplement. Si sa résistance est trop grande, court-circuiter le primaire (là où entrait le 230 V dans le micro-onde). »

Je n’ai pas compris le raisonnement, ainsi que l’histoire de mise en CC du primaire ^^

Dans l’espoir d’une réponse.
lulrik
</p>

<p style="text-align: justify;">
Salut,

Le raisonnement est un peu tordu, mais le phénomène est simple, alors comme tu dois certainement le savoir, la caractéristique courant/tension d’une bobine est donnée par: [latex] u(t)=\frac{di(t)}{dt} \times L [/latex]
Donc au plus le courant qui circule est grand, au plus la tension au bornes de la bobine sera grande.
Alors la tension aux bornes du transformateur de mesure va diminuer, évidement la tension au secondaire diminuera en conséquence.
A première vu il est vrai que cela n’a pas vraiment d’intérêt, puisque cela rend la tension au secondaire très instable.
Mais dans le cas où l’on veut charger un banc de condensateur (par exemple pour une Bobine de Tesla) on calibre l’oscillateur LC de manière à ce que la puissance maximal soit inférieur à la limite que notre alimentation fournisse (alimentation secteur vers 100 V), on obtient ainsi le courant consommer au maximum par le primaire du transformateur de mesure, avec ceci on peut définie l’inductance de la bobine qui sera en série pour limiter le courant en cas de court-circuit.
En simplifiant les formules on peut faire une approximation comme ceci:
[latex] {u(t)=E \times \cos(\omega t) i(t)= I \times \sin(\omega t) \frac{di(t)}{dt} \times L} [/latex]
[latex] {\frac{u(t)}{\frac{di(t)}{dt}} = L} [/latex]
En prenant par exemple: [latex] \omega = 100 \pi, E = 100V , I = 35 A (courant max)[/latex]
[latex] {\frac{100 \ times \cos(\omega t)}{35 \times \omega \cos(\omega t)} = L} [/latex]
Donc: [latex] {L = 10 mH} [/latex]

Il faut donc un self de 10 mH, le plus simple pour en fabriquer un est d’employer la méthode décrite. La raison pour la quelle il faut court-circuiter le secondaire est que cela fait augmenter l’inductance, donc le courant maximal admissible.

vinvin-win
</p>


 [1]: http://www.heberger-image.fr/data/images/39362_TP_5.jpg
 [2]: http://www.heberger-image.fr/data/images/92287_TP_4.jpg
 [3]: http://www.heberger-image.fr/data/images/55187_TP_1.jpg
 [4]: http://www.heberger-image.fr/data/images/96909_inducteur_1.jpg
 [5]: http://www.heberger-image.fr/data/images/39991_arc_TP_2.png
 [6]: http://www.heberger-image.fr/data/images/50172_arc_TP_1.png
# Introduction


  Les r�seaux de distribution d��lectricit� acheminent l'�nergie des centrales �lectriques aux particuliers. Ces centrales sont compos�es de plusieurs parties, qui s'adaptent � la quantit� d'�lectricit� qui les traversent.



  Prenons l'exemple d'une centrale hydro�lectrique qui g�n�re une puissance de l'ordre de 20 MW. Si l'�lectricit� �tait transport�e sous une tension qui nous est famili�re, c'est-�-dire du monophas� 230 Vac (tension efficace) � 50 Hz ou du triphas� en 380 Vac (tension efficace) � 50Hz, nous aurions une intensit� de 87 kA en 230 Vac, ou du 17 kA par phase en 380 Vac, pour le triphas�. Ce qui n�cessiterait pour parcourir 100 km des c�bles de section (attention les yeux) 29 580 000 mm� pour du 230 V et 5 780 000 mm� pour du triphas� (en admettant une chute de 10 Volts en fin de ligne). L'utilisation de telles tensions pour transporter notre pr�cieuse �nergie �lectrique aurait entra�n�e l'�puisement d'une grande partie de nos r�serves mondiales de cuivre ou autre conducteur. Ainsi, au d�but du XX �me si�cle, de grands ing�nieurs (en particulier les fondateurs de <strong>General Electric</strong>) ont mis au point les premiers r�seaux � Haute tension.



  En reprenant l'exemple de la centrale hydro�lectrique 20 MW, les g�n�ratrices de cette centrale produisent 20 kV en triphas� (en g�n�ral). La tension �tant trop �lev�e, des transformateurs de potentiel et de courant y sont pr�sent pour diviser la tension et l'intensit� par des constantes. Il est ainsi possible de v�rifier la tension avec des composants fonctionnant en basse tension, ce qui a pour avantage d'am�liorer la s�curit� des techniciens et de r�duire le coup du mat�riel. L'�lectricit� apr�s �tre pass�e par ces �quipements�pour �tre contr�l�e (je passe tout ce qui concerne le redressement du cos f, les s�curit�s,...) est achemin�e � un transformateur qui va l'�lever de 20 kV � 400 kV.



  Calculons maintenant les diam�tres des c�bles basse tension (soit ceux qui sortent des g�n�ratrices). Disons qu'il y a 100 m entre les g�n�ratrices et le transformateur, il y a une intensit� de 277 A, donc la section est de 9 418 mm�, pour une chute de 100 V, ce qui est r�alisable, et pas trop co�teux par rapport � ce que nous avons vu plus t�t. Maintenant reprenons 100 km � parcourir mais cette fois en 400 kV. On a 17 A, avec une section de 11,56 mm� pour une chute de 5 000 V (cela n'influence pas grand chose � une tension aussi �lev�e).



  Ceci montre l'importance des transformateurs Haute tension et des transformateurs de mesure dans ces domaines.
 � 

# Les transformateurs de potentiel � 


  Ils sont utilis�s pour faire des mesures sur les r�seaux moyens, de hautes ou de tr�s hautes tensions comme nous l'avons vu dans l'introduction.



  Je vais maintenant traiter l'exemple d'un seul type de ces transformateurs de mesure, puisque j'en poss�de seulement de ce type. Il s'agit de ceux qui mesurent les lignes de 20 kV.



  Ils poss�dent un primaire extr�mement bien isol� pour cette tension, puisqu'ils doivent r�sister aux hausses de tension g�n�r�es par exemples quand la foudre tombe sur les c�bles (cela est de moins en moins fr�quent, puisque une grande partie des r�seaux 20 kV sont enterr�s). En cons�quence ils doivent r�sister aux fortes intensit�s qui sont g�n�r�e par le m�me ph�nom�ne, pour cela ils ont un bobinage sur dimensionn�.


![image1][1] ![image6][2] 
  Sur les �tiquettes de ces transformateurs, la puissance est divis�e par 10, il y est �crit qu'elle est de 350 VA, elle est ainsi �crite pour respecter des normes, mais le transformateur fournit plus de 3 500 VA, car il est largement sur dimensionn�, attention � ne pas d�passer cette puissance car il risquerait de chauffer sans que l'on puisse s'en rendre compte � cause de l'�paisse isolation.



  Les transformateurs de potentiel sont les plus utiles dans mes exp�riences, ils permettent d'obtenir une grande puissance (vu au dessus), mais il ne faut jamais l'alimenter directement en 100 V (tension maximale conseill�e, ce qui fournit 20kV au secondaire) si vous comptez faire des arcs �lectriques avec, car lors de la mise en court-circuit du secondaire, la consommation du primaire sera colossale, il peut tirer facilement plus de 100 A. Soit votre alimentation crame et le disjoncteur coupe le courant, soit, dans le pire des cas, le primaire du transformateur HT br�le, et cela est extr�mement compliqu� � rembobiner � cause de l'isolant. Pour �viter cela il faut le mettre en s�rie avec un ballast, ou un transformateur basse tension, qui limitera l'intensit� � moins de 35 A. Le plus simple pour r�aliser ce genre de "r�sistance" est de prendre un transformateur de micro-onde, auquel il faut enlever le secondaire (partie 2 000 V dans le micro-onde) pour le remplacer avec un bobinage en fils �lectriques de 2,5 mm� tout simplement. Si sa r�sistance est trop grande, court-circuiter le primaire (l� o� entrait le 230 V dans le micro-onde).


# Les transformateurs d'intensit�


  Les transformateurs d'intensit� sont employ�s dans la mesure du courant qui passe sur les r�seaux. Ils sont plac�s en s�rie avec la ligne �lectrique. Ainsi, quand un courant passe dans le primaire, le flux magn�tique est envoy� dans un secondaire � l'aide d'un tore (ici en fer puisque nous sommes sur des r�seaux basse fr�quence, 50 Hz), qui est isol� par rapport � la ligne o� le courant est mesur�. Pour y mesurer l'intensit� qui passe � n'importe quelle tension.



  Le courant est g�n�ralement divis� par un facteur constant. Ce facteur, qui lie l'intensit� qui passe dans le primaire et celle qui passe dans le secondaire, d�pend du nombre de spires qu'il y a au primaire et au secondaire.



  Pour un transformateur d'intensit� sous la forme d'un tore plac� directement sur le c�ble et avec un secondaire reli� aux outils de mesure ou d'affichage (amp�rem�tre par exemple), la formule pour calculer le facteur est :
 $$ F = \frac {1} {N_s} $$
 
 La formule pour calculer l'intensit� est : $$I_p = N_s \times I_s$$
 $$I_s = \frac {1} {N_s} \times I_p$$ 


  Pour un transformateur d'intensit� qui poss�de un primaire et un secondaire qui sont directement bobin�s, le primaire est branch� en s�rie par rapport au r�seau dont on veut mesurer l'intensit� qui le traverse, et le secondaire est reli� aux outils de mesure ou d'affichage. La formule est :
 $$F = \frac {N_p} {N_s}$$ La formule pour calculer l'intensit� est : $$I_p = \frac {N_s} {N_p} \times I_s$$
 $$I_s = \frac {N_p} {N_s} \times I_p$$ $$F$$ est le facteur. $$I_p$$ est l'intensit� qui traverse le primaire. $$I_s$$ est l'intensit� qui est re�ue dans le secondaire. $$N_p$$ est le nombre de spire dans le primaire du transformateur d'intensit�. $$N_s$$ est le nombre de spire dans le secondaire du transformateur d'intensit�. 

# O� les trouver ?


  Ce genre de transformateurs est install� dans les centrales �lectriques, et les centres de redistribution. Des transformateurs de tension � deux phases sont pr�sents sur certaines lignes haute tension isol�es. En g�n�ral, ils sont dans les zones rurales ou montagneuses. Pour s'en procurer il existe plusieurs moyens, mais cela reste tr�s compliqu�.



  - La premi�re est celle que j'ai utilis�e deux fois, ce qui m'a permis d'avoir 6 transformateurs de potentiel et 6 transformateurs d'intensit� (ainsi que des fusibles de 20 kV 40 A et 25 A). Cette m�thode oblige � conna�tre une personne qui travaille dans ce milieu, ou � demander gentiment aux techniciens qui changent les �quipements haute tension (pour la remise aux normes ou la destruction) s'ils peuvent vendre ou donner le mat�riel remplac�. Ou encore conna�tre le propri�taire de la centrale.



  - la seconde m�thode consiste � regarder de temps en temps sur <strong>Ebay</strong> si il y a des transformateurs � vendre, mais cela est tr�s rare. Je n'en ai jamais vu pour l'instant, mais il y a des personnes qui s'en sont procur�s de cette mani�re.



  - La derni�re m�thode est la plus on�reuse. Il faut acheter le transformateur directement chez le fournisseur, mais il faut demander un devis, puis je doute qu'il vende des transformateurs de mesures haute tension � des particuliers, mais �a doit �tre faisable. Je pense que pour un transformateur aux normes europ�ennes le prix doit �tre �lev�, autour des 1250 �. Sinon, regardez sur des sites chinois mais le prix du transformateur y est ridicule par rapport aux frais de transport � mon avis, car en g�n�ral les transformateurs de tension p�sent aux alentours de 35 kg.


# Relations de calcul employ�es

 La puissance : $$P = U \times I$$ La section d'un c�ble en cuivre : $$S = 1,7 \times 10^{-2} \times L \times \frac {I} {CT}$$ $$S$$ : Section en $$mm^2$$. $$1,7 \times 10^{-2}$$ est la r�sistance du cuivre par m�tre. $$L$$ : longueur aller-retour du conducteur en m. $$I$$ : courant en amp�re qui passe. $$CT$$ : chute de tension admise pour cette distance. 


# Photos d'arc �lectrique

![image2][3] ![image3][4] 
  Deux transformateurs 20 kV mis en s�rie pour avoir le neutre o� � la masse des transformateurs. On met du 20 kV d'un cot� et du - 20 kV de l'autre, pour avoir une diff�rence de potentiel de 40 kV, ils sont aliment�s en 100 V avec un transformateur en s�rie pour limiter l'intensit� � 26 A.
 Quelques images d'arc : 

![image4][5] ![image5][6]


# Commentaire habile


Salut � toi !

Quand tu dit � Le plus simple pour r�aliser ce genre de �r�sistance� est de prendre un transformateur de micro-onde, auquel il faut enlever le secondaire (partie 2 000 V dans le micro-onde) pour le remplacer avec un bobinage en fils �lectriques de 2,5 mm� tout simplement. Si sa r�sistance est trop grande, court-circuiter le primaire (l� o� entrait le 230 V dans le micro-onde). �

Je n�ai pas compris le raisonnement, ainsi que l�histoire de mise en CC du primaire ^^

Dans l�espoir d�une r�ponse.
lulrik



Salut,

Le raisonnement est un peu tordu, mais le ph�nom�ne est simple, alors comme tu dois certainement le savoir, la caract�ristique courant/tension d�une bobine est donn�e par: $$ u(t)=\frac{di(t)}{dt} \times L $$
Donc au plus le courant qui circule est grand, au plus la tension au bornes de la bobine sera grande.
Alors la tension aux bornes du transformateur de mesure va diminuer, �videment la tension au secondaire diminuera en cons�quence.
A premi�re vu il est vrai que cela n�a pas vraiment d�int�r�t, puisque cela rend la tension au secondaire tr�s instable.
Mais dans le cas o� l�on veut charger un banc de condensateur (par exemple pour une Bobine de Tesla) on calibre l�oscillateur LC de mani�re � ce que la puissance maximal soit inf�rieur � la limite que notre alimentation fournisse (alimentation secteur vers 100 V), on obtient ainsi le courant consommer au maximum par le primaire du transformateur de mesure, avec ceci on peut d�finie l�inductance de la bobine qui sera en s�rie pour limiter le courant en cas de court-circuit.
En simplifiant les formules on peut faire une approximation comme ceci:
$$ {u(t)=E \times \cos(\omega t) i(t)= I \times \sin(\omega t) \frac{di(t)}{dt} \times L} $$
$$ {\frac{u(t)}{\frac{di(t)}{dt}} = L} $$
En prenant par exemple: $$ \omega = 100 \pi, E = 100V , I = 35 A (courant max)$$
$$ {\frac{100 \ times \cos(\omega t)}{35 \times \omega \cos(\omega t)} = L} $$
Donc: $$ {L = 10 mH} $$

Il faut donc un self de 10 mH, le plus simple pour en fabriquer un est d�employer la m�thode d�crite. La raison pour la quelle il faut court-circuiter le secondaire est que cela fait augmenter l�inductance, donc le courant maximal admissible.

vinvin-win



 [1]: /media/article/7/attachments/39362_TP_5.jpg
 [2]: /media/article/7/attachments/92287_TP_4.jpg
 [3]: /media/article/7/attachments/55187_TP_1.jpg
 [4]: /media/article/7/attachments/96909_inducteur_1.jpg
 [5]: /media/article/7/attachments/39991_arc_TP_2.png
 [6]: /media/article/7/attachments/50172_arc_TP_1.png

# Pourquoi cet article ? 

Le NE555 est un composant pouvant être utilisé comme oscillateur astable ou monostable. Son domaine d'application est très très (très) étendu; il est donc probable que nous l'utilisions dans un prochain article. Afin de ne pas être forcé de le présenter à chaque fois, cet article s'en chargera. 

# Ok et plus précisément, c'est quoi ? 

Comme je l'ai déjà dit, le NE555 est un composant électronique qui peut-être utilisé comme un oscillateur astable ou monostable. Pour suivre cet article, il peut être intéressant de se référer à la documentation du composant. Vous la retrouverez [ici][1]. 

# Dissection 

Voici ce qui va nous occuper dans ce paragraphe.

![Schéma bloc du NE555][2]

On remarque tout d'abord que le NE555 possède 8 entrées/sorties : 

- L'alimentation (VCC) 
- La masse (GND) 
- Le seuil (THRESHOLD) 
- La gâchette (TRIGGER) 
- Une borne de ré-initialisation (RESET) 
- Une borne de contrôle (CONTROL VOLTAGE) 
- Une borne de décharge (DISCHARGE) 
- Une borne de sortie (OUT) 

Le NE555 est principalement utilisé pour contrôler un condensateur et agir en fonction de l'état de ce dernier. Concrètement, le fonctionnement du NE555 est relativement simple; il est composé de 3 blocs remarquables : 

- Le pont diviseur de tension 
- Le bloc set/reset 
- Les comparateurs 

![Schéma bloc du NE555 légendé.][3] 

Le pont diviseur assure à sa sortie une première tension à \(\frac{2}{3}\) de VCC et la deuxième à \(\frac{1}{3}\) de VCC. Il s'agit là d'une des plus grande forces du NE555 : son fonctionnement ne sera pas modifié par la tension d'alimentation. Les deux blocs comparateurs comparent les sorties du pont diviseur à la tension sur la broche de seuil et sur la broche de la gâchette. Si la tension de seuil est supérieure à \(\frac{2}{3}\) de VCC, on déclenche le reset du bloc R/S. Si la tension de la gâchette est inférieure à \(\frac{1}{3}\) de VCC, on déclenche le set du bloc R/S. Enfin la sortie est directement reliée à la sortie du bloc R/S. Un état haut du bloc R/S entraîne un état haut sur la sortie. Un état bas sur la sortie du R/S entraîne la mise à la masse de la borne de décharge ainsi qu'un état bas sur la sortie du NE555. Bien ! il est temps d'observer une première application du NE555. 

# Le montage astable 
Il s'agit sans doute du montage le plus utilisé du NE555. Il permet de générer un signal carré en sortie, avec un rapport cyclique calculable. Notez cependant qu'il existe des variantes qui permettent des réglages plus fins. Tout d'abord, voici à quoi ressemble le montage.

![astable][4]

Il nous permettra de générer des signaux de la sorte : 

![exemple][5]


Le condensateur se chargera par R1 et R2 et se déchargera par R2 uniquement. Le condensateur se chargera jusqu'à ce que la tension à ses bornes dépasse \(\frac{2}{3}\) de VCC. Le NE555 déclenchera alors la décharge du condensateur et passera sa sortie de l'état haut à l'état bas. Le condensateur se déchargera jusqu'à ce que la tension à ses bornes passe en dessous de \(\frac{1}{3}\) de VCC. Le NE555 arrêtera alors la décharge du condensateur et passera sa sortie à l'état haut. On souhaite connaître la fréquence du signal généré, le temps de charge et le temps de décharge du condensateur en fonction de R1 R2 et C1. 

## La charge 
On oublie le régime transitoire au moment où l'on met le circuit sous tension. Concrètement cela signifie que l'on considère que la tension aux bornes du condensateur est initialement de \(\frac{1}{3}\) de VCC. D'autre part, le NE555 n'intervient pas pendant la charge du condensateur. On peut donc simplifier le montage : 

![charge][6]

On écrit la loi des mailles : $$U_{\text{R1}} + U_{\text{R2}} + U_{\text{C1}} = \text{VCC}$$ On souhaite obtenir une équation de la tension aux bornes du condensateur. En notant \(i\) le courant dans la branche étudiée et \(C\) la capacité du condensateur C1, on a : $$i = \text{C} \times \dot{U}_{\text{C1}}$$ La loi d'Ohm nous assure également que la tension aux bornes d'une résistance vaut : $$U_{\text{R}} = \text{R} \times i$$ On a donc : $$ \text{C} \times (\text{R1} + \text{R2}) \times \dot{U}_{\text{C1}} + U_{\text{C1}} = \text{VCC} $$ Soit encore : $$\dot{U}_{\text{C1}} + \frac{1}{\text{C} \times (\text{R1} + \text{R2})} \times U_{\text{C1}} = \frac{\text{VCC}}{\text{C} \times (\text{R1} + \text{R2})}$$ On résout l'équation différentielle et on obtient : $$U_{\text{C1}}(t) = A * e^{\frac{-t}{\text{C} \times (\text{R1} + \text{R2})}} + \text{VCC}$$ On détermine la constante A à partir des conditions initiales : $$U_{\text{C1}}(0) = \frac{1}{3} \times VCC$$ On a donc : $$ A = - \frac{2}{3} \times VCC$$ Ainsi : $$U_{\text{C1}}(t) = (1 - \frac{2}{3} \times e^{\frac{-t}{\text{C} \times (\text{R1} + \text{R2})}}) \times \text{VCC}$$ Il ne reste plus qu'à résoudre l'équation \(U_{\text{C1}}(t) = \frac{2}{3} \times \text{VCC} \) pour connaître la durée de la charge du condensateur. $$\frac{2}{3} \times \text{VCC} = (1 - \frac{2}{3} \times e^{\frac{-t}{\text{C} \times (\text{R1} + \text{R2})}}) \times \text{VCC} $$ On a donc : $$t_{charge} = \ln (2) \times \text{C} \times (\text{R1} + \text{R2})$$ Cette formule est plutôt satisfaisante car non seulement elle nous donne le temps de charge du condensateur (ce qui était le but recherché :p ) mais elle nous montre également que ce temps de charge est totalement indépendant de la tension d'alimentation du montage ! 

## La décharge 
On va supposer que la tension aux bornes du condensateur est initialement de \(\frac{2}{3}\) de VCC. Le condensateur va se décharger jusqu'à ce que la tension à ses bornes soit de \(\frac{2}{3}\) de VCC. Le NE555 n'intervenant pas dans la décharge, on peut simplifier le montage de la sorte :

[<img class="size-full wp-image-653" src="http://sivigik.com/wp-content/uploads/2016/05/DechargeCondo.png" alt="Decharge du condensateur." width="102" height="210" />][7] Decharge du condensateur. 

On veut exprimer la tension aux bornes du condensateur en fonction de R2 et du temps. On écrit la loi des mailles : $$U_{\text{R2}} = U_{\text{C1}}$$ On applique comme précédemment la loi d'Ohm et l'équation du condensateur pour obtenir : $$\dot{U}_{\text{C1}} - \frac{1}{\text{R2} \times \text{C}} \times U_{\text{C1}} = 0$$ On résout l'équation différentielle en accord avec les conditions initiales : $$ U_{\text{C1}}(t) = \frac{2}{3} \times \text{VCC} \times e^{-\frac{t}{\text{R2}\times\text{C}}}$$ On veut maintenant connaître la durée de la décharge du condensateur. Pour cela on résout l'équation \(U_{\text{C1}}(t) = \frac{1}{3}\times \text{VCC}\). $$ \frac{1}{3}\times \text{VCC} = \frac{2}{3} \times \text{VCC} \times e^{-\frac{t}{\text{R2}\times\text{C}}}$$ On obtient : $$ t_{décharge} = \ln(2) \times \text{R2}\times\text{C}$$ Là encore on remarque que la formule est totalement indépendante de la tension d'alimentation du montage. 

## Caractéristiques du signal de sortie 

Nous sommes désormais capable d'exprimer le temps de charge et le temps de décharge du condensateur. On peut ainsi obtenir la fréquence de sortie du NE555 ainsi que le rapport cyclique En effet, la sortie est à l'état haut quand le condensateur se charge et à l'état bas quand il se décharge. 

![sortie][8]

Commençons par la fréquence du signal de sortie. On calcul d'abord sa période T. $$ T = t_{charge} + t_{décharge}$$ On remplace les temps de charge et de décharge par leurs expressions: $$ T = \ln (2) \times \text{C} \times (\text{R1} + \text{R2}) + \ln(2) \times \text{R1}\times\text{C}$$ Ce qui nous donne : $$ f = \frac{1}{T} = \frac{1}{\ln(2) \times \text{C} \times (2\times\text{R1}+\text{R2})}$$ Maintenant le rapport cyclique. Il s'agit du rapport entre la durée de l'état haut en sortie et la période du signal de sortie. On a : $$ \alpha = \frac{t_{charge}}{T} $$ On remplace le temps de charge et la période par leurs expressions respectives : $$ \alpha = \frac{\ln (2) \times \text{C} \times (\text{R1} + \text{R2})}{\ln(2) \times \text{C} \times (2\times\text{R1}+\text{R2})} $$ Soit encore : $$ \alpha = \frac{\text{R1}+\text{R2}}{2\times\text{R1}+\text{R2}}$$ Le rapport cyclique ne dépend donc que des deux résistances. On conçoit cependant que cette formule est "difficile à manier". C'est à dire que faire varier le rapport cyclique peut vite devenir pénible. Par exemple si l'on remplace R1 et R2 par un potentiomètre, de cette manière : 

![asatble][9]

On obtient la variation du rapport cyclique suivante (le "sens" de la courbe varie en fonction du branchement du potentiomètre): 

![][10] 

Comme on peut le voir, on ne peut pas faire descendre le rapport cyclique en dessous de 0.5, ce qui peut être problématique pour certaines applications, par exemple le pilotage de moteur à courant continu. Il existe des variantes du montage astable qui corrigent ce problème. Cet article est maintenant terminé ! Mais il reste beaucoup de choses à dire à propos du NE555. Dans de prochains articles j'aimerais vous parler du montage monostable du NE555 ainsi que d'autres montages astables. En attendant n'hésitez pas à partager cet article s'il vous a plu et bricolez bien. ;)

 [1]: http://pdf.datasheetcatalog.net/datasheet/WINGS/NE555.pdf
 [2]: /media/article/12/attachments/SchemaBloc.png
 [3]: /media/article/12/attachments/SchemaBloclegende.png
 [4]: /media/article/12/attachments/NE555Astable.png
 [5]: /media/article/12/attachments/Sortie-du-NE555.png
 [6]: /media/article/12/attachments/ChargeCondo.png
 [7]: /media/article/12/attachments/DechargeCondo.png
 [8]: /media/article/12/attachments/SortieNE555Condo-1.png
 [9]: /media/article/12/attachments/NE555AstablePotar.png
 [10]: /media/article/12/attachments/VariationRapportCyclique-1.png

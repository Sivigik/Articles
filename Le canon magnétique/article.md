# Petite présentation 

Plus connu sous le nom de *Coil Gun*, il utilise l'effet de <a href="https://fr.wikipedia.org/wiki/Canon_magn%C3%A9tique" target="_blank">répulsion magnétique</a> pour lancer un projectile ferromagnétique. Si cette arme est souvent perçue comme futuriste, il s'avère pourtant que des recherches militaires sont menées depuis la fin du XX ième siècle... mais le développement de telles armes est resté à l'état de prototype à cause d'un rendement très faible et d'une mise en place sur le terrain très difficile.  Grâce aux <a href="https://fr.wikipedia.org/wiki/Supraconductivit%C3%A9" target="_blank">supra- conducteurs</a> avec lesquels les bobines pourront être faites, de nombreux avantages vont apparaître : ce qui cachera ses défauts (pour l'instant très peu d'informations sur ces nouvelles recherches sont apparues). De nouvelles recherches voient le jour sur un autre type de canon qui utilise l'électricité comme moyen de propulsion : le *Ray Gun*. Un particulier en a réalisé un de puissance intéressante (par rapport à l'échelle du système) et qu'on peut retrouver sur <a href="http://www.powerlabs.org/railgun.htm" target="_blank">son site internet</a>.

# Fonctionnement 

Le fonctionnement est très simple, il suffit d'envoyer un fort courant électrique dans une bobine qui attirera le projectile, puis de stopper l'alimentation quand le projectile a franchi la moitié de son parcours dans la bobine. Le projectile est ainsi uniquement accéléré et non freiné par le même champ magnétique qui l'a mis en mouvement. Ainsi, pour avoir un fort courant durant un instant très bref, l'utilisation de condensateurs est la mieux adaptée. On stocke donc l'énergie électrique dans de gros condensateurs qui forment un "banc" (voir photos ci-dessous) et que l'on décharge dans la ou les bobines pour tirer. La puissance du canon dépend de 2 facteurs: 

*   Son architecture
*   La taille du banc de condensateurs 

Il existe différentes architectures. La plus commune sur internet, puisqu'elle est la plus simple à réaliser, est celle d'une simple bobine dans laquelle on décharge le banc de condensateurs. Cette architecture est très limitée et a un rendement presque nul (de l'ordre de 1%) car le projectile subit une violente accélération durant très peu de temps : une grande partie de l'énergie est donc perdue dans l'espace, et n'attire donc pas le projectile. Une autre architecture moins répandue, car plus difficile à mettre au point, mais beaucoup plus efficace, consiste à utiliser plusieurs bobines réparties le long du canon, qui vont successivement s'activer au passage du projectile par le biais de capteurs. Le projectile est sujet à un accélération bien moins violente, mais atteint une vitesse bien supérieure à celle que l'on obtient avec une simple bobine, pour une quantité d'énergie transmise bien plus importante. 

![allumage successif][1] Source : <a href="https://fr.wikipedia.org/wiki/Canon_magn%C3%A9tique" target="_blank">wikipedia.org</a> 

# Mes réalisations 

J'ai moi-même réalisé différents modèles, de puissance croissante. Mon premier modèle employait des condensateurs récupérés dans des télévisions à tube cathodique. La puissance était vraiment insignifiante, le banc de condensateurs ne pouvait stocker seulement que 60J : tout juste de quoi de transpercer du carton. Pour le second modèle, j'ai fait un banc de condensateurs un peu plus conséquent. J'ai acheté 16 condensateurs de 200V et 470µF en Russie, ce sont des anciens stocks qui datent des années 70, quand l'URSS produisait beaucoup de matériels électroniques pour ses projets militaires. De nos jours on retrouve sur **ebay** ces composants à des prix très faibles. Ce banc a une puissance de 250J. <a href="http://sivigik.com/wp-content/uploads/2015/12/IMG_3431.jpg" rel="attachment wp-att-255"><img class="aligncenter wp-image-255 size-large" src="http://sivigik.com/wp-content/uploads/2015/12/IMG_3431-1024x768.jpg" alt="IMG_3431" width="1024" height="768" /></a> <a href="http://sivigik.com/wp-content/uploads/2015/12/IMG_3433.jpg" rel="attachment wp-att-256"><img class="aligncenter wp-image-256 size-large" src="http://sivigik.com/wp-content/uploads/2015/12/IMG_3433-1024x768.jpg" alt="IMG_3433" width="1024" height="768" /></a> https://youtu.be/8Gp3BPVHADs Mon dernier modèle qui n'est pas terminé, mais dont j'ai fait quelques tests, a un banc de 8 condensateurs de 400V en 6 800µF, ce qui totalise une puissance de 4 320J. J'utilise 3 [thyristors][2] en parallèle de 1600 V et 200 A chacun, et pouvant résister à des pics de plusieurs milliers d'ampères ce qui permet de faire passer toute l'énergie dans la bobine avec très peu de pertes.  

<a href="http://sivigik.com/wp-content/uploads/2015/12/8-condensateur.jpg" rel="attachment wp-att-258"><img class="aligncenter wp-image-258 size-large" src="http://sivigik.com/wp-content/uploads/2015/12/8-condensateur-1024x768.jpg" alt="8 condensateur" width="1024" height="768" /></a> 

<video controls>
<source src="http://sivigik.com/wp-content/uploads/2016/05/0_Ohms.mp4" type="video/mp4">
</video>

[](http://sivigik.com/wp-content/uploads/2016/0nt/uploads/2015/12/IMG_4235.jpg)

<img class="aligncenter wp-image-260 size-large" src="http://sivigik.com/wp-content/uploads/2015/12/IMG_4235-1024x768.jpg" alt="IMG_4235" width="1024" height="768" /></a> 

<a href="http://sivigik.com/wp-content/uploads/2015/12/fil-cramé.png" rel="attachment wp-att-259"><img class="aligncenter wp-image-259 size-large" src="http://sivigik.com/wp-content/uploads/2015/12/fil-cramé-1024x576.png" alt="fil cramé" width="1024" height="576" /></a>

https://youtu.be/KWXVNlBQ4QE

 [1]: https://upload.wikimedia.org/wikipedia/commons/thumb/f/f7/Coilgun_animation.gif/435px-Coilgun_animation.gif
 [2]: https://fr.wikipedia.org/wiki/Thyristor 

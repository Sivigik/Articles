J'ai écrit il y a quelques temps une bibliothèque pour les modules à décalages de registres. Je vous propose ici de survoler son fonctionnement. 
# Comment marche le module ? 
Le fonctionnement est relativement simple. On envoie les données au module qui les stocke dans une mémoire tampon, puis on envoie un signal qui demande au module de basculer ses entrées et sorties en fonction de sa mémoire tampon. Cela nécessite trois voies : une première pour les données, une deuxième qui sert d'horloge et enfin une dernière qui déclenche le basculement. On peut noter que ces modules présentent l'avantage de pouvoir être couplés ensemble facilement sans pour autant nécessiter plus de voies. Un petit détour par la 

[datasheet du 74HC595][1] peut s'avérer très instructif. 
# Pourquoi faire une bibliothèque ? 
La bibliothèque standard d'Arduino offre déjà une fonction permettant de manipuler ce genre de modules. Mais cette fonction nécessite de recalculer à chaque appel l'adresse de la voie de sortie. On peut donc mieux faire. 

*ShiftRegister* garde en mémoire les voies utilisées. 
# Un gros exemple d'utilisation 
Plutôt que de vous détailler le fonctionnement de la bibliothèque (qui est assez basique) je vous propose une petite mise en pratique. Nous allons réaliser un compte à rebours paramétrable et qui déclenche un buzzer tout mimi à la fin. Petit schéma de montage : 

<a href="http://sivigik.com/wp-content/uploads/2016/02/compteur.png" rel="attachment wp-att-539"><img src="http://sivigik.com/wp-content/uploads/2016/02/compteur-300x207.png" alt="compteur" width="300" height="207" class="alignnone size-medium wp-image-539" /></a> La partie intéressante du code est la classe gérant l'affichage. Elle pilote les trois afficheurs 7 segments à travers le 74HC595. On utilise la persistance rétinienne: on allume un par un les afficheurs en modifiant les valeurs affichées avec le décodeur BCD. Pour envoyer des données au 74HC595 on passe un tableau d'octets à ShiftRegister. Chaque octet correspond à un module. Le bit 0 correspond à la sortie 0 du module. Et ça donne ça : <iframe width="560" height="315" src="https://www.youtube.com/embed/nDuBeRTyxB0" frameborder="0" allowfullscreen></iframe> 
# Et côté performances ? 
Une comparaison à l'oscilloscope réalisée par vinvin-win (poutous sur les fesses) a montré que la mise en cache permet d'économiser environ 90 µs par envois de données. Voici l'envoi d'une valeur avec ShiftRegister (DS en jaune STCP en bleu) 

<a href="http://sivigik.com/wp-content/uploads/2016/02/shiftregister.png" rel="attachment wp-att-536"><img src="http://sivigik.com/wp-content/uploads/2016/02/shiftregister-300x146.png" alt="shiftregister" width="300" height="146" class="alignnone size-medium wp-image-536" /></a> La même avec `shiftOut()` qui est fourni avec le logiciel Arduino. <a href="http://sivigik.com/wp-content/uploads/2016/02/shiftOut.png" rel="attachment wp-att-537"><img src="http://sivigik.com/wp-content/uploads/2016/02/shiftOut-300x146.png" alt="shiftOut" width="300" height="146" class="alignnone size-medium wp-image-537" /></a>

 [1]: http://www.nxp.com/documents/data_sheet/74HC_HCT595.pdf

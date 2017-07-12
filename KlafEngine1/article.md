Ça y est. Après quelques années de programmation, j'ai décidé de me lancer dans le grand bain, et de créer mon propre moteur de jeu. Cette série d'articles a pour but de décrire l'avancement du projet. Puisque je suis actuellement étudiant, les mises jour seront sans doute espacées dans le temps. 
# C'est quoi ? 
C'est vrai après tout : qu'est-ce que c'est qu'un moteur de jeu ? Pour nous ce sera une bibliothèque qui permettra de créer facilement un jeu vidéo (en 2D) pour un PC. 

# Un peu de spécifications 
Le but est d'avoir une lib' utilisable facilement. Elle sera codée en C++ et tentera d'utiliser les possibilité qu'offre la lib' standard. Pour l'affichage, mon choix s'est porté sur 

[SFML][1]. Pour la première fois de ma vie, j'ai décidé de me forcer à écrire une vrai documentation; pour cela j'utilise [doxygen][2]. L'architecture tentera de coller au modèle [ECS][3] (plus de détails dans un prochain article). Pour le moment, je prévois de découper la lib en plusieurs modules : - Core : L'implémentation de base de l'ECS. - Render : L'affichage. - Physics : La physique. - Interface : Gestion de l'interface utilisateur. - Logic : implémentation des logiques de jeu. Je prévois également de réaliser un système de sérialisation générique pour les objets gérés par le moteur, ainsi qu'un éditeur. J'aimerais aussi, dans un second temps, ajouter un module permettant de scripter les jeux, les niveaux etc. (sans doute en python). 
# Avancement actuel 
J'ai déjà implémenté une grande partie de l'ECS (comprendre : il est fonctionnel, mais certaines choses restent à perfectionner) ainsi qu'un embryon de module de rendu. Voici ce qu'est actuellement capable de faire le moteur : 

<iframe width="560" height="315" src="https://www.youtube.com/embed/MOCDAPl9PJo" frameborder="0" allowfullscreen></iframe> Vous pouvez retrouver des exemples sur [le github][4]. Si parmis-vous il y a des aventuriers, la documentation est [ici][5]. L'épisode 2 vous attend [ici][6] !

 [1]: http://sfml-dev.org/
 [2]: http://www.stack.nl/~dimitri/doxygen/
 [3]: https://en.wikipedia.org/wiki/Entity_component_system
 [4]: https://github.com/Klafyvel/KlafEngine
 [5]: http://klafyvel.github.io/KlafEngine/index.html
 [6]: http://sivigik.com/2016/06/chroniques-de-creation-dun-petit-moteur-de-jeu-episode-2/

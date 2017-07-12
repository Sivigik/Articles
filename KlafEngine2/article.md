Voici l'épisode n°2 de la création d'un petit moteur de jeu. Le premier épisode est disponible [ici][1]. Nous y parlerons du début de mise en place d'un [ECS][2], ce qui constitue le coeur du moteur, ainsi que d'une bibliothèque sympa que j'ai découverte récemment qui devrait me permettre d'implémenter simplement les interfaces utilitaires du moteur (création d'animations / de maps etc.). <!-- more -->

# Quel est le principe de l'ECS ? 
C'est relativement compliqué à expliquer. Si vous avez lu l'article wikipédia cité plus haut, il est probable que vous ne sachiez pas comment l'implémenter. Mes recherches m'ont menées vers 

[ceci][3], bien que j'ai pris beaucoup libertées vis à vis de l'implémentation originale. Je vous conseille fortement de lire le tutoriel, mais s'il n'y avait qu'une seule chose à retenir, c'est que l'ECS se distingue de l'implémentation traditionnelle, basée sur l'héritage, utilisée dans les jeux vidéos. Le but est de réduire l'arbre d'héritage pour rendre le tout plus souple d'utilisation. Cependant l'inconvénient majeur que je lui voit (pour l'instant !) est la difficulté de le mettre en place. j'ai actuellement quelque chose d'à peu près fonctionnel, mais qui mériterait encore des améliorations. 
# Au commencement, il y avait l'application. 
L'ECS est basé sur le concept d'entitées. Pour cela il me fallait une structure pour les stocker et les gérer. Ce sera la classe 

`Application`. Le nom n'est pas forcément bien choisi, car l'intégralité du programme ne sera pas géré par l'instance de la classe `Application`. En effet, puisque la SFML n'est pas spécialement pensée pour utiliser l'ECS, j'ai préféré ne pas tenter de l'y adapter pour l'instant. La classe `Application` n'est cependant pas un simple conteneur. Elle est capable de gérer plus ou moins intelligemment les entitées et de recycler les identifiants d'entitée inutilisés au moyen d'une file. L'application a également pour charge de stocker les composants, leurs *factory* et d'affecter les composants aux entitées. Il y a peu de choses notables à ce propos, si ce n'est qu'une entitée "sait" qu'elle possède un composant grâce à un masque binaire propre à chaque type de composant. Les entitées sont ainsi stockées dans un dictionnaire avec pour clé les entitées et pour valeur les masques binaires résultants des affectations de composants. Afin de limiter le temps de recherche d'une entitée par masque, on distingue la notion d'entitée *active* d'entitée *inactive*. L'application aura également a stocker les systèmes, mais la gestion de ces derniers n'étants pas encore satisfaisante, je ne la détaillerais pas aujourd'hui. 
# Les composants, la mémoire du jeu. 
Les composants sont, dans le tutoriel linké, de simples structures. Ici j'ai décidé de compliqué le tout, mais pas uniquement pour le plaisir ! :) En effet, KlafEngine sépare les composants en deux partie; la classe 

`Component` et la classe abstraite `ComponentData`. Cela permet de simplifier grandement la gestion des composants par la classe `Application`, car les composants ont toujours le même type `Component`. L'utilisateur quant à lui stocke ses données dans une classe dérivant de `ComponentData`. Les objets `Component` savent stocker les `ComponentData` *via* des pointeurs. C'est ici qu'intervient la notion de *factory*. En effet, l'application doit être capable de créer des instances de `Component` avec le bon `ComponentData`. Pour cela on utilise des fonction de *callback* appellées *factory*. Ce sont elles que l'application appelle lorsqu'on lui demande d'affecter un composant à une entitée. 
# Les systèmes. 
La dernière grosse partie du coeur de KlafEngine est constituée par les systèmes. Ils sont en charge de la gestion de la logique du jeu. Cependant il s'agit actuellement de la partie de KlafEngine qui a le plus de chance d'être modifiée. Je vais donc décrire uniquement les parties qui sont stables. Les systèmes ont pour mission de modifier les composants (entre autre). Pour cela il leur faut y avoir accès. C'est pourquoi la classe 

`System` est déclarée "amie" de la classe `Application`. Il implémente une méthode protégée qui permet à ses classes filles d'accéder aux composants de leurs applications. 
# Un exemple pour (essayer) de comprendre. 
Vous trouverez dans les fichiers d'exemples le fichier "coreExample.cpp". Il montre comment utiliser simplement le coeur de KlafEngine. Je vais ici le commenter. On va ici créer notre propre type de composants. Pour cela on le fait hériter de ComponentData et on crée la 

*factory* adaptée. <pre class="lang:c++ decode:true " >class MyCompData : public klf::ComponentData
{
public:
        MyCompData() : x(0), y(0) {}
        int x;
        int y;
};

std::unique_ptr&lt;klf::Component&gt; factory(unsigned int e)
{
        std::unique_ptr&lt;klf::Component&gt; c = klf::Component::createEmptyComponent(e);
        c-&gt;value = std::shared_ptr&lt;klf::ComponentData&gt;(new MyCompData());
        return c;
}</pre> Nous avons ensuite besoin d'un système pour manipuler le tout. 

<pre class="lang:c++ decode:true " >class MySystem : public klf::System
{
public:
        MySystem(klf::Application& app) : klf::System(app) {}
        void onUpdate()
        {
                std::cout &lt;&lt; "Update ! " &lt;&lt; std::endl;
                klf::Component& c = getComponent(1, 0);
                std::shared_ptr&lt;MyCompData&gt; d = std::dynamic_pointer_cast&lt;MyCompData&gt;(c.value);
                std::cout &lt;&lt; "Entity : " &lt;&lt; c.entity &lt;&lt; " " &lt;&lt; d-&gt;x &lt;&lt; " " &lt;&lt; d-&gt;y &lt;&lt; std::endl;
                d-&gt;x += 20;
        }
};</pre> Une petite implémentation de 

`range` plus tard, on a plus qu'à s'occuper de la fonction principale. <pre class="lang:c++ decode:true " >int main()
{
        sf::RenderWindow window(sf::VideoMode(800, 600), "KlafEngine");
        klf::Application app;

        app.registerComponentType(1, factory);

        std::cout &lt;&lt; "Let's create 100 entites with our MyCompData as component." &lt;&lt; std::endl;
        for(int i : range(0,100))
        {
                unsigned int entity = app.addEntity();
                app.addMask(entity, 1);
        }
        std::cout &lt;&lt; "Done." &lt;&lt; std::endl;
        std::cout &lt;&lt; "Let's remove entites 40 to 59 ." &lt;&lt; std::endl;
        for(int i : range(40,60))
        {
                app.removeEntity(i);
        }
        std::cout &lt;&lt; "Done." &lt;&lt; std::endl;
        std::cout &lt;&lt; "Let's create 60 entites with our MyCompData as component." &lt;&lt; std::endl;
        for(int i : range(0,60))
        {
                unsigned int e = app.addEntity();
                app.addMask(e, 1);
        }


        std::cout &lt;&lt; "Let's create a system and update it !" &lt;&lt; std::endl;

        MySystem s(app);
        s.onUpdate();
        s.onUpdate();

        return EXIT_SUCCESS;
}</pre> On retrouve la structure d'un programme classique de la SFML. On pourra noter 

`app.registerComponentType(1, factory);` qui permet d'enregistrer notre composant en tant que composant auprès de l'application avec le flag 1. Ensuite on joue avec l'API pour créer/supprimer des entitées et modifier leurs composants. On peut noter que l'utilisation des systèmes est relativement inélégante pour l'instant. Il faut que je trouve une solution. Pour information, voici ce qu'affiche cet exemple : <pre class="lang:sh decode:true " >$ ./coreExample 
Let's create 100 entites with our MyCompData as component.
Done.
Let's remove entites 40 to 59 .
Done.
Let's create 60 entites with our MyCompData as component.
Let's create a system and update it !
Update ! 
Entity : 0 0 0
Update ! 
Entity : 0 20 0</pre>

# La partie qui n'a rien à voir. 
Pour parler un peu moins de technique, j'ai découvert tout récemment 

**Dear ImGui** et son portage pour SFML. N'hésitez pas à jeter un coup d'oeuil [ici][4]. Voici ce que j'obtiens en compilant "simplement" l'exemple fourni : [video width="1376" height="770" mp4="http://sivigik.com/wp-content/uploads/2016/06/ImGui1.mp4"][/video] 

C'est tout pour aujourd'hui ! à la prochaine. :)

 [1]: http://sivigik.com/2016/05/chroniques-de-creation-dun-petit-moteur-de-jeu-episode-1/
 [2]: https://en.wikipedia.org/wiki/Entity_component_system
 [3]: http://www.gamedev.net/page/resources/_/technical/game-programming/understanding-component-entity-systems-r3013
 [4]: https://eliasdaler.wordpress.com/2016/05/31/imgui-sfml-tutorial-part-1/

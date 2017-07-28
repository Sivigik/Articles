Le langage Python est un outil incroyable. Parmi les multiples bibliothèques que fourni la communauté, on retrouve les incontournables Matplotlib et Numpy. Ces deux bibliothèques sont très puissantes et permettent la manipulation et la présentation de données aisément. Je vous proposerais régulièrement des petits tutoriels avec exemples pour réaliser des rendus de données avec matplotlib. Pour vous donner une idée de ce qu'on peut faire, voici une animation d'exemple que j'ai réalisée ainsi que le code qui l'a généré. 

<video controls>
<source src="/media/article/16/attachments/article.mp4" type="video/mp4">
</video>

Si la vidéo de charge pas, voir [ici](/media/article/16/attachments/article.mp4).

```python
import numpy as np
import matplotlib.pyplot as pl
from matplotlib import cm
from mpl_toolkits.mplot3d import axes3d

import matplotlib.animation as anim


f = lambda x,y,t: np.exp(-1/((1+y)*8)*(x+t/1000)**2 + 1)*np.sin(y)/((1+t/100*y))

X = np.linspace(-10,10)
Y = np.linspace(0, np.pi*2)
X,Y = np.meshgrid(X,Y)

n_image = 500

Z = f(X,Y,0)

pl.close('all')

fig = pl.figure()
ax = fig.gca(projection='3d')
ax.plot_surface(X, Y, Z, rstride=3, cstride=3, alpha=0.3)
cset = ax.contour(X, Y, Z, zdir='z', offset=-1, cmap=cm.coolwarm)
cset = ax.contour(X, Y, Z, zdir='x', offset=-10, cmap=cm.coolwarm)
cset = ax.contour(X, Y, Z, zdir='y', offset=6, cmap=cm.coolwarm)

ax.set_xlabel('X')
ax.set_ylabel('Y')
ax.set_zlabel('Z')

def update(i):
    Z = f(X,Y,i)
    print("Avancement: {}%".format(str(round(i/n_image*100,2))), end='\r')

    ax.clear()
    ax.plot_surface(X, Y, Z, rstride=3, cstride=3, alpha=0.3)
    cset = ax.contour(X, Y, Z, zdir='z', offset=-1, cmap=cm.coolwarm)
    cset = ax.contour(X, Y, Z, zdir='x', offset=-10, cmap=cm.coolwarm)
    cset = ax.contour(X, Y, Z, zdir='y', offset=6, cmap=cm.coolwarm)
    ax.set_zlim(-1, 1)
    ax.view_init(elev=np.sin(i/n_image*np.pi)*60, azim=i/n_image*360)


ani = anim.FuncAnimation(fig, update, n_image,interval=20)

ani.save('article.mp4', fps=48, bitrate=120, dpi=300)
print()

```

D'autres animations que j'ai pu réaliser: 

![Un développement limité][1] 

![Le même présenté différemment ][2] 

![le développement limité de cosinus à différents ordres][3]

 [1]: /media/article/16/attachments/animation.gif
 [2]: /media/article/16/attachments/Animation3D.gif
 [3]: /media/article/16/attachments/animationCos.gif

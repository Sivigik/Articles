Il est parfois utile de pouvoir convertir rapidement entre les bases. Ce petit programme est là pour ça, et il va de la base 2 à la base 36 :) . [Lien de téléchargement](/media/article/13/attachments/BASE.8Xp) 

```basic
:Lbl A
:"0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ"→Chaîne1
:0→P
:Input "DE BASE: ",A
:Input "VERS BASE: ",B
:If A≠10:Then 
:Input "NOMBRE: ",Chaîne2
:longueur(Chaîne2→L
:0→F
:0→I
:For(I,L,1,-1
:F+(carChaîne(Chaîne1,sous-Chaîne(Chaîne2,I,1))-1)*(A^(L-I))→F
:End
:F→N
:10→A
:1→P
:End
:If A=10:Then 
:If P=0:Input "NOMBRE: ",N
:0→R
:" "→Chaîne3
:While N≥B
:sous-Chaîne(Chaîne1,partDéc(N/B)*B+1,1
:Rep+Chaîne3→Chaîne3
:partEnt(N/B→N
:End
:sous-Chaîne(Chaîne1,N+1,1
:Rep+Chaîne3→Chaîne3
:End
:Disp Chaîne3
:Pause
:Goto A
```

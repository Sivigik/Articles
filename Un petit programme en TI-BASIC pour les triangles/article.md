Une question récurrente dans les QCMs du baccalauréat en math demande de qualifier 3 points. Forment-ils un triangle rectangle ? Sont ils alignés ? etc... Je vous propose ici un petit programme en TI-BASIC pour trouver rapidement la réponse. Il demande les coordonnées des trois points en entrée et qualifie la figure :) . 

```basic
:Input "XA",A
:Input "YA",B
:Input "ZA",C
:Input "XB",D
:Input "YB",E
:Input "ZB",F
:Input "XC",G
:Input "YC",H
:Input "ZC",I
:If (D-A)*(H-B)=(E-B)*(G-A) and (D-A)*(I-C)=(F-C)*(G-A) and (E-B)*(I-C)=(F-C)*(H-B):Disp "ALIGNEE"
:If (D-A)²+(E-B)²+(F-C)²=(G-A)²+(H-B)²+(I-C)²:Then 
:If (D-A)²+(E-B)²+(F-C)²=(G-D)²+(H-E)²+(I-F)²:Then :Disp "EQUILATERAL"
:Else :Disp "ISOCELE A"
:End
:End
:If (D-A)²+(E-B)²+(F-C)²=(G-D)²+(H-E)²+(I-F)²:Then 
:Disp "ISOCELE B"
:End
:If (D-G)²+(E-H)²+(F-I)²=(G-A)²+(H-B)²+(I-C)²:Then 
:Disp "ISOCELE C"
:End
:If (D-A)*(G-A)+(E-B)*(H-B)+(F-C)*(I-C)=0:Disp "RECTANGLE A"
:If (A-D)*(G-D)+(B-E)*(H-E)+(C-F)*(I-F)=0:Disp "RECTANGLE B"
:If (A-G)*(D-G)+(B-H)*(E-H)+(C-I)*(F-I)=0:Disp "RECTANGLE C"
```

Pour ceux qui peuvent l'envoyer directement depuis l'ordinateur sur la calculatrice vous pouvez [le télécharger](/media/article/3/attachments/TRIANGLE.8Xp) !

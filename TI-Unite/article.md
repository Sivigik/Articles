Pour ceux qui son sujets aux trous de mémoire quand il s'agit de convertir les unités, un petit programme fait par SL-Prog et moi-même : (vous pouvez également [le télécharger][1]) 
    :EffEcr
    :Input "NBR=",A
    :Menu("CONVERSION","MASSE",A,"VITESSE",B,"VOLUME",D,"ENERGIE",E,"ROTATION",F,"QUITTER",C
    :Lbl A
    :Menu("UNITES","G EN KG",7,"KG EN G",8,"G EN N",9,"KG EN N",10,"QUITTER",C
    :Lbl 7
    :A/1000
    :Disp Rep
    :Stop
    :Lbl 8
    :A*1000
    :Disp Rep
    :Stop
    :Lbl 9
    :A/100
    :Disp Rep
    :Stop
    :Lbl 10
    :A*10
    :Disp Rep
    :Stop
    :Lbl C
    :EffEcr
    :Stop
    :Lbl B
    :Menu("UNITES","M/S EN M/H",1,"M/H EN M/S",2,"M/H EN KM/H",3,"KM/H EN M/H",4,"M/S EN KM/H",5,"KM/H EN M/S",6,"QUITTER",C
    :Lbl 1
    :A*3600
    :Disp Rep
    :Stop
    :Lbl 2
    :A/3600
    :Disp Rep
    :Stop
    :Lbl 3
    :A/1000
    :Disp Rep
    :Stop
    :Lbl 4
    :A*1000
    :Disp Rep
    :Stop
    :Lbl 5
    :A*3.6
    :Disp Rep
    :Stop
    :Lbl 6
    :A/3.6
    :Disp Rep
    :Stop
    :Lbl D
    :Menu("UNITES:","L EN CL",15,"CL EN L",16,"L EN ML",17,"ML EN L",18,"QUITTER",C
    :Lbl 15
    :A/100
    :Disp Rep
    :Stop
    :Lbl 16
    :A*100
    :Disp Rep
    :Stop
    :Lbl 17
    :A*1000
    :Disp Rep
    :Stop
    :Lbl 18
    :A/1000
    :Disp Rep
    :Stop
    :Lbl E
    :Menu("ENERGIE","W/H VERS J",20,"KW/H VERS J",21,"J VERS W/H",22)
    :Lbl 20
    :A*3600
    :Disp Rep
    :Stop
    :Lbl 21
    :A*3.6
    :Disp Rep
    :Stop
    :Lbl 22
    :A/3600
    :Disp Rep
    :Stop
    :Lbl F
    :Menu("ROTATION","RD/S VERS TR/MIN",23,"TR/MIN VERS RD/S",24
    :Lbl 23
    :(A*60)/(2π)
    :Disp Rep
    :Stop
    :Lbl 24
    :(A*2π)/60
    :Disp Rep
    :Stop

 [1]: http://sivigik.com/prog/CONVERS.8Xp

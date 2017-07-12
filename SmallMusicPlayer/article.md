SmallMusicPlayer est une expérience que j'ai réalisée dans le but de manipuler le son avec python. Dans cet article, je vous propose de décrire son fonctionnement. 
# Les Bases L'idée m'est venu après avoir lu 

[ce post][1]. Pour des raisons de facilité, j'ai décidé de changer quelques règles pour obtenir les règles syntaxiques suivantes : **Écriture des notes :** 
    Do Re Mi Fa2 Re3#
    

**Écriture des silences (par ordre de longueur croissant):** 
    -
    --
    ---
    

**Changement de type de note (par défaut noire):** 
    Do croche Re Mi blanche Fa noire Sol Sol
    

**Changement de nuance (par défaut medium):** 
    Do piano Re Mi forte Fa Sol medium La
    

**Changement de tempo** 
    bpmSet 120 Do Re Mi bpmSet 180 Do Re Mi
    

# Le Début du code Avant même de pouvoir jouer du son, il faut pouvoir comprendre les instructions de l'utilisateur. Pour cela, nous allons créer quelques variables globales qui contiennent les instructions autorisées. 

    # Notes with Hz values
    NOTES={
        "Do":131,
        "Do#":139,
        "Re":147,
        "Re#":156,
        "Mi":165,
        "Fa":175,
        "Fa#":185,
        "Sol":196,
        "Sol#":208,
        "La":220,
        "La#":233,
        "Si":247,
        "Do2":262,
        "Do2#":277,
        "Re2":294,
        "Re2#":311,
        "Mi2":330,
        "Fa2":349,
        "Fa2#":370,
        "Sol2":392,
        "Sol2#":415,
        "La2":440,
        "La2#":466,
        "Si2":494,
        "Do3":523,
        "Do3#":554,
        "Re3":587,
        "Re3#":622,
        "Mi3":659,
        "Fa3":698,
        "Fa3#":740,
        "Sol3":784,
        "Sol3#":830,
        "La3":880,
        "La3#":932,
        "Si3":988,
        "Do4":1046,
    }
    DUREE={
        "croche":500,
        "noire":1000,
        "blanche":2000,
    }
    
    NUANCES={
        "piano":0.15,
        "medium":0.3,
        "forte":0.6,
    }
     Les durées sont en millisecondes. Pour les nuances, on considère que 1 est équivalent à mettre le son à fond. 

# La classe Note et les silences Une note est caractérisée par sa fréquence, sa durée et sa 'nuance'. 

    (freq, duree, nuance)
     On peut donc créer une classe 

`Note` 
    class Note:
        def __init__(self, note, duree, nuance=NUANCES['medium']):
            self.note = note
            self.duree = duree
            self.nuance = nuance
    
        def __str__(self):
            return '({}, {}, {})'.format(self.note, 
                                                self.duree, 
                                                self.nuance)
    
        def tuple(self):
            """Return the Note value into a tuple."""
            return (self.note, self.duree, self.nuance)
     La méthode 

`tuple` nous permettra de plus tard d'utiliser commodément les objets `Note` Passons maintenant aux silences. Comment faire un silence ? et bien en affectant un fréquence nulle par exemple ! On ajoute donc ceci au dictionnaire `NOTES`: 
    NOTES = {
        #...
        "Silence":0,
    }
     Ensuite, nous allons simplifier la création de notes silences. 

    silence = lambda duree: Note(NOTES["Silence"], duree)
     Il ne faut pas non-plus oublier de lier les silences aux caractères associés. On crée un dictionnaire global : 

    SILENCES = {
        '-': lambda:silence(DUREE['croche']),
        '--': lambda:silence(DUREE['noire']),
        '---': lambda:silence(DUREE['blanche']),
    }
     On peut d'ores et déjà tester ce code : 

    if __name__ == '__main__':
        print(Note(NOTES['Fa'], DUREE['croche']))
        print(Note(NOTES['Sol'], DUREE['blanche']))
        print(SILENCES['--']())
        print(Note(NOTES['Do#'], DUREE['noire']))
        print(Note(NOTES['Re3'], DUREE['croche']))
     On obtient : 

    $ python3 notes.py
    (175, 500, 0.3)
    (196, 2000, 0.3)
    (0, 1000, 0.3)
    (139, 1000, 0.3)
    (587, 500, 0.3)
    

# Parser les données Tout d'abord, il va nous falloir un conteneur, une partition en quelque sorte ! 

    class Partition(list):
        def __str__(self):
            s = str()
            for idx, n in enumerate(self):
                s += '{}:\t{}\n'.format(idx, n)
            return s
     Il s'agit d'une bête classe héritant de l'objet 

`list`. On se contente de surcharger la méthode `__str__()`. Il nous faut maintenant un parseur. Comme on sait que notre utilisateur (qu'on aime beaucoup) va faire des erreurs, on prépare une exception tout exprès. 
    class ParseError(Exception):
        pass
    
    class Parser:
        def __init__(self, partition, input_str):
            self.partition = partition
            self.input_str = input_str
            self.current_line = 1
    
        def is_allowed_instr(self, word):
            pass
    
        def get_instr_list(self):
            pass
    
        def parse(self):
            pass
     Le parseur nécessite une partition pour aller y écrire les notes. La méthode 

`get_instr_list` permet de transformer la chaîne de caractère reçue en liste d'instruction. `is_allowed_instr` détecte une instruction interdite. Enfin `parse`... parse le code ! Nous allons commencer par écrire la méthode de vérification. En effet il s'agit de la plus simple, puisqu'il suffit de vérifier que le mot est compris dans les instructions. 
    class Parser:
        #...
        def is_allowed_instr(self, word):
            allowed = False
            allowed = allowed or word in NOTES 
            allowed = allowed or word in DUREE 
            allowed = allowed or word in NUANCES 
            allowed = allowed or word in SILENCES
            if not allowed:
                raise ParseError("'{}' is not an allowed word at line {}"
                                .format(word, self.current_line))
            return True
    
    #...
     Si le mot ne correspond à aucune instruction, on lève une exception. Passons à l'écriture de 

`get_instr_list`. Chaque instruction est séparée des autres par un espace ou un retour à la ligne (`\n`). Ce qui donne : 
    class Parser:
        #...
        def get_instr_list(self):
            instr_list = []
            current_word = ''
            for c in self.input_str:
                if (c == ' ' or c== '\n') and not current_word == '':
                    self.is_allowed_instr(current_word)
                    instr_list.append(current_word)
                    current_word = ''
                    self.current_line += 1
                elif c != ' ':
                    current_word += c
            if not current_word == '': 
                self.is_allowed_instr(current_word)
                instr_list.append(current_word)
            return instr_list
        #...
     La méthode en profite également pour vérifier la validité des instructions. Il y a une toute petite subtilité ici. En effet, si le dernier mot n'est pas suivit d'un espace ou d'un retour à la ligne, il n'est pas ajouté à la liste. D'où la nécessité de récupérer le dernier mot si 

`current_word` n'est pas vide après avoir fini la boucle. Nous pouvons maintenant nous occuper de l'écriture de la méthode de *parsing*. Le fonctionnement est, là encore, assez simple. Après avoir récupéré la liste d'instructions, on la parcourt et on agit selon l'instruction. 
    class Parser:
        #...
        def parse(self):
            current_duree = DUREE['noire']
            current_nuance = NUANCES['medium']
    
            instr = self.get_instr_list()
    
            for i in instr:
                if i in DUREE:
                    current_duree = DUREE[i]
                elif i in NUANCES:
                    current_nuance = NUANCES[i]
                elif i in SILENCES:
                    self.partition.append(silence(current_duree))
                elif i in NOTES:
                    self.partition.append(Note(NOTES[i], current_duree, current_nuance))
    
             return self.partition
        #...
     Il manque une dernière fonctionnalité à notre classe 

`Parser`... Le changement de tempo ! J'ai gardé cette fonctionnalité pour plus tard car contrairement aux autres instruction, elle prend un argument : le tempo. Nous allons tout d'abord créer un nouveau dictionnaire global nommé `OTHER_OP` qui contiendra les instructions 'spéciales'. 
    OTHER_OP = {
       "bpmSet": lambda parser, val: Parser.set_bpm(parser, val),
    }
     Vous l'avez deviné, le code ci-dessus implique de modifier notre classe 

`Parser`. Ainsi : 
    class Parser:
        def __init__(self, partition, input_str):
            self.partition = partition
            self.input_str = input_str
            self.bpm = 180
            self.current_line = 1
    
        def set_bpm(self, val):
            self.bpm = int(val)
    #...
     Fini ? Pas vraiment. Il faut encore modifier la méthode de 

*parsing* pour prendre en compte le tempo. En musique, le tempo est donné en BattementParMinute (bpm). Nous stockons nos durées en millisecondes. Les valeurs données correspondent à un tempo de 60 bpm. Ainsi pour une noire, nous devrons faire : [latex] duree\_note = \frac{Duree['noire']}{\frac{bpm}{60}} [/latex] D'autre part, il nous faudra pouvoir interpréter l'argument de `bpmSet`. Pour réaliser cette opération, on vérifie si le mot courant est dans `OTHER_OP`. Si oui, lors du prochain passage de boucle, on exécute la fonction correspondante à l'instruction avec pour argument le mot courrant. En d'autres termes : 
    class Parser:
        #...
        def parse(self):
            current_duree = int(DUREE['noire']/(self.bpm/60))
            current_nuance = NUANCES['medium']
    
            instr = self.get_instr_list()
            operating_arg = False
            operation = ''
    
            for i in instr:
                if operating_arg:
                    OTHER_OP[operation](self, i)
                    operation = ''
                    operating_arg = False
                elif i in OTHER_OP:
                    operating_arg = True
                    operation = i
                elif i in DUREE:
                    current_duree = int(DUREE[i]/(self.bpm/60))
                elif i in NUANCES:
                    current_nuance = NUANCES[i]
                elif i in SILENCES:
                    self.partition.append(silence(current_duree))
                elif i in NOTES:
                    self.partition.append(Note(NOTES[i], current_duree, current_nuance))
    
            return self.partition
     Enfin, il ne faut pas oublier de modifier la méthode 

`is_allowed_instr` pour qu'elle accepte les nombres et les `OTHER_OP`. 
    class Parser:
        #...
        def is_allowed_instr(self, word):
            allowed = False
            allowed = allowed or word in NOTES 
            allowed = allowed or word in DUREE 
            allowed = allowed or word in NUANCES 
            allowed = allowed or word in SILENCES
            allowed = allowed or word in OTHER_OP
            try:
                allowed = allowed or isinstance(int(word), int)
            except ValueError:
                pass
            if not allowed:
                raise ParseError("'{}' is not an allowed word at line {}".format(word, self.current_line))
            return True
    #...
    

# Générer des sons wave Dans cette partie, nous allons utiliser le module 

`wave`, `math` et `os` de python. Vous pouvez donc ajouter 
    import wave, math, os, random
     Toute la magie va s'opérer autour de la classe partition. Nous souhaitons pouvoir réaliser deux actions: jouer la partition et la sauvegarder.

  
On ajoute donc deux méthodes à la classe: 
    class Partition(list):
        #...
        def save(self, filename='tmp.wav'):
            pass
        def play(self):
            pass
     La méthode 

`play` jouera le son. Si aucun son n'a encore été généré depuis que le morceau a été *parsé*, on créé un fichier temporaire. Il est donc nécessaire de savoir si un fichier a été généré. 
    class Partition(list):
        saved_file = ''
        #...
     Il faut également que le parseur modifie cette variable. 

    class Parser:
        #...
        def parse(self):
            self.partition.saved_file = ''
            #...
     Passons maintenant à l'écriture de la méthode 

`save`. Il s'agit de la plus intéressante pusique c'est elle qui va générer le signal. Le son sera codé sur 8 bits. Il existe donc 256 valeurs possible. Le spectre de notre son sera de forme sinusoïdal. En traçant la fonction sinus, on s'apperçoit qu'elle ne correspond pas à ce dont nous avons besoin. ![image sinus][2] Les valeurs de notre fonction doivent être sur [0, 255]. On peut donc commencer par 'centrer' notre fonction sur 128. Ainsi : [latex]f(x) = 128 + sin(x)[/latex] ![image sinus_centre][3] Nos nuances sont codées sur \[0, 1]. Nous voulons donc que pour un son de nuance 1, le signal oscille entre 0 et 255 inclus. On peut donc définir l'amplitude ainsi : [latex]amplitude = nuance * 127.5[/latex\] (on multiplie par 127.5 et non par 128 pour être sûr de ne pas 'déborder'). Notre fonction s'écrit désormais :[latex]f(x) = 128 + amplitude \cdot sin(x)[/latex].  
Ce qui donne pour une nuance de 0.5 : ![image sinus_amplitude][4] Il ne nous reste plus qu'à incorporer notre fréquence ! Pour cela, nous avons besoin de la fréquence de la note et de la fréquence d'échantillonage (le nombre de 'point' calculé par seconde; nous prendrons 44100Hz). On obtient ainsi : [latex]f(x) = 128 + amplitude \cdot sin(2 \cdot \pi \cdot x \cdot freq / freq_{ech})[/latex]. On obtient ainsi (avec une fréquence de 440Hz et une nuance de 0.5): ![image sinus_ok][5] L'implémentation est une simple application de la formule. 
    class Partition(list):
        #...
        def length(self):
            """Returns the duration of the partition in seconds."""
            duration = float()
            for n in self:
                duration += n.tuple()[1]
            duration = float(duration)/1000.0
            return duration
    
        def save(self, filename='tmp.wav'):
            self.saved_file = ''
            sound = wave.open(filename, 'w')
            canal_nb = 1
            octet_nb = 1
            fech = 44100
            ech_nb = int(self.length() * fech)
            params = (canal_nb, octet_nb, fech, ech_nb, 'NONE', 'not compressed')
            sound.setparams(params)
    
            for n in self:
                t = n.tuple()
                amplitude = 127.5*t[2]
                n_dur = int(float(t[1])/1000 *fech)
                for i in range(0, n_dur):
                    val = wave.struct.pack('B', int(128 + amplitude*math.sin(2.0*math.pi*t[0]*i/fech)))
                    sound.writeframes(val)
                sound.close()
                self.saved_file = filename
    
        #...
     Notez au passage l'ajout de la méthode 

`length` qui retourne la durée du morceau en secondes. On n'oublie pas de donner une valeur à `self.saved_file` pour éviter des compilations inutiles à la méthode `play`. Nous pouvons maintenant implémenter `play`. 
    class Partition(list):
        #...
        def play(self):
            if self.saved_file is '':
                sound_filename = 'tmp_{}.wav'.format(random.randint(0, 1000))
                print('Creating temporary file: {}'.format(sound_filename))
                self.save(filename=sound_filename)
                self.saved_file = ''
            else:
                sound_filename = self.saved_file
    
            print("Running VLC.")
            if self.saved_file is '':
                order ="vlc {0} &amp;&amp; rm -vf {0}".format(sound_filename)
                os.system(order)
            else:
                os.system("vlc {}".format(sound_filename))
     Je n'ai pas trouvé de fonctions dans la bibliothèque standard de python qui permette de jouer du son simplement (il existe un moyen via pygame). C'est pourquoi on utilise vlc. On peut noter également que l'on continue de réfléchir avec la variable 

`self.saved_file` pour éviter les double-compilations. ***Attention:*** cette méthode n'est absolument pas portable (elle ne fonctionne que sous GNU/Linux et avec vlc installé). Pour une utilisation sous windows, adaptez les commandes. Si nous testions notre programme ? Je vous conseille [docopt][6] pour parser les arguments de la ligne de commande. Ajoutez ceci au début du fichier: 
    """SmallMusicPlayer
    
    SmallMusicPlayer is available under the MIT License. See LICENSE.
    
    Usage: 
    SMP -f INPUTFILE (-t OUTPUTFILE | -p)
    SMP -s INPUTSTR (-t OUTPUTFILE | -p)
    """
     Il nous faut également importer docopt: 

    from docopt import docopt
     Et à la fin du fichier: 

    if __name__ == '__main__':
        args = docopt(__doc__)
    
        part = Partition()
        input_str = ""
    
        if args['-f']:
            with open(args['INPUTFILE'], 'r') as in_file:
                input_str = in_file.read()
        elif args['-s']:
            input_str = args['INPUTSTR']
    
            Parser(part, input_str).parse()
    
        if args['-t']:
            part.save(filename=args['OUTPUTFILE'])
        elif args['-p']:
            part.play()
     Voici un exemple de fichier à parser: 

    bpmSet 300 -- blanche Do3 noire Re3 Fa3 Mi3 Re3 Sol3 - Sol3 - Sol3
    La3 Mi3 Fa3 Re3 - Re3 - Re3 Fa3 Mi3 Re3 Do3 Do4 Si3 La3 Sol3 Fa3
    Mi3 Re3 blanche Do3
     Et avec un petit 

`python3 notes.py -f music -t article.wav` voici ce qu'on obtient: [audio mp3="http://sivigik.com/wp-content/uploads/2015/06/articleSmallMusicPlayer.mp3"][/audio] 
# Ajout d'une interface graphique

*Le code de l'interface est donné à titre indicatif, puisqu'il est sans réel rapport avec le traitement du son.* On crée une classe qui sera notre fenêtre. 
    from tkinter import *
    from tkinter import filedialog
    from notes import Partition, Parser, ParseError
    
    class MainWindow(Frame):
        def __init__(self, window, parser=None, **kwargs):
            Frame.__init__(self, window, width=800, height=600, **kwargs)
            self.pack(fill=BOTH)
    
            self.window = window
    
            self.parser = parser
            self.input_str = ''
            self.input_filename = ''
            self.output_file = ''
    
            self.create_widgets()
     On y ajoute une méthode pour construire tout les widgets. 

    class MainWindow(Frame):
        #...
       def create_widgets(self):
           # Menu
           self.menu_bar = Menu(self.window)
    
           self.file = Menu(self.menu_bar, tearoff=0)
           self.menu_bar.add_cascade(label='File', underline=0,
                                                   menu=self.file)
    
           self.file.add_command(label='Open File', underline=0, 
                                            command=self.open)
           self.file.add_command(label='Close File', underline=0, 
                                            command=self.close)
           self.file.add_command(label='Save File', underline=0, 
                                            command=self.save)
           self.file.add_separator()
           self.file.add_command(label="Quit", underline=0, 
                                            command=self.quit)
    
           self.window.config(menu=self.menu_bar)
    
           # Debug display
           self.out_frame= LabelFrame(self, width=800, 
                                                    height=100, 
                                                    borderwidth=1, 
                                                    text='Parser messages')
           self.out_frame.pack(side='bottom', fill=BOTH)
           self.out = Text(self.out_frame, height=10)
           self.out.config(bg='black', fg='orange', state=DISABLED)
           self.out.pack(fill=BOTH)
    
           #Code display
           self.edit_frame = LabelFrame(self, width=300, height=300, borderwidth=1, text='Notes')
           self.edit_frame.pack(side='left', fill=Y)
           self.edit = Text(self.edit_frame)
           self.edit.pack()
    
           #options
           self.options_frame = LabelFrame(self, width=100, height=400, borderwidth=1, text='Options')
           self.options_frame.pack(side="top", fill=X)
           self.var_output_file = StringVar()
           self.lbl_output_location = Label(self.options_frame,text='Output file name:' )
           self.lbl_output_location.pack()
           self.output_location = Entry(self.options_frame, textvariable=self.var_output_file, width =20)
           self.output_location.pack()
           self.output_location.delete(0, END)
           self.output_location.insert(0, "name")
    
           self.var_create_output_file = IntVar()
           self.var_play_sound_with_vlc = IntVar()
    
           self.case_output_file = Checkbutton(self.options_frame, text='Write output in a file', variable=self.var_create_output_file)
           self.case_output_file.pack()
           self.case_play_sound = Checkbutton(self.options_frame, text='Play generated sound with vlc', variable=self.var_play_sound_with_vlc)
           self.case_play_sound.pack()
    
           self.btn_run = Button(self.options_frame, text='Compile', command=self.run)
           self.btn_run.pack()
     On ajoute une gestion des entrées/sorties. 

    class MainWindow(Frame):
        #...
       def load_input_str(self):
           self.input_str = self.edit.get(1.0, END)
       def parser_print(self, output_str):
           self.out.config(state=NORMAL)
           self.out.insert(INSERT, output_str + '\n')
           self.out.config(state=DISABLED)
     On a également besoin de gérer les fichiers. 

    class MainWindow(Frame):
        #...
    
        def open(self):
            self.input_filename = filedialog.askopenfilename()
            with open(self.input_filename, 'r') as input_file:
                self.edit.insert(END, input_file.read()) 
    
        def close(self):
            self.edit.delete(0.0, END)
            self.input_filename = ''
    
        def save(self):
            with open(self.input_filename, 'w') as input_file:
                self.load_input_str()
                input_file.write(self.input_str)
     Enfin, on implémente de parseur et on lance le code. 

    class MainWindow(Frame):
        def run(self):
        self.out.delete(0.0, END)
        part = Partition()
        self.load_input_str()
        self.parser_print('Begin parsing...')
        try:
            Parser(part, str(self.input_str)).parse()
        except ParseError as e:
            self.parser_print(str(e))
        return
        else:
            self.parser_print('Parsed !')
    
        if self.var_create_output_file.get() == 1:
            self.parser_print('Writing output...')
            part.save(filename=self.var_output_file.get())
        if self.var_play_sound_with_vlc.get() == 1:
            self.parser_print('Playing output...')
            part.play()
        self.parser_print('Done')
    
    
    if __name__ == '__main__':
        f = Tk()
        m = MainWindow(f)
    
        m.mainloop()
        m.destroy()
     Et sous vos yeux ébahis ! 

![fenetre][7] 
# Sources et liens utiles

*   [les valeurs des notes][8]
*   [Un tutoriel qui parle de la librairie wave][9]
*   [Un super article sur la compilation][10]
*   [Le github du projet][11]

 [1]: http://http://pdp.microjoe.org/forums/sujet/606/algorithmie-python-interpreter-un-petit-langage#p10027
 [2]: http://www.heberger-image.fr/data/images/42137_sinus.png
 [3]: http://www.heberger-image.fr/data/images/30734_sinus_centre.png
 [4]: http://www.heberger-image.fr/data/images/79160_sinus_amplitude.png
 [5]: http://www.heberger-image.fr/data/images/70282_sinus_ok.png
 [6]: http://docopt.org/
 [7]: http://www.heberger-image.fr/data/images/48206_fen_r.png
 [8]: http://www.ordiecole.com/logo/hertz.html
 [9]: http://fsincere.free.fr/isn/python/cours_python_ch9.php
 [10]: http://progdupeu.pl/articles/68/introduction-a-la-compilation
 [11]: https://github.com/Klafyvel/SmallMusicPlayer

À la lecture du titre de cet article, vos yeux se posent sur votre carte Arduino, vous sentez un léger picotement dans votre nuque, vos poils se hérissent sur vos bras... Non décidément faire clignoter des LEDs à l'appuis sur un bouton, tourner un moteur pendant 3 secondes dans un sens puis pendant 6 secondes dans l'autre ne vous suffit plus ! Il est temps de passer à la vitesse supérieure ! Pourquoi ne pas faire communiquer votre ordinateur avec votre carte programmable préférée ? Certains d'entre vous me répondrons sans doute que rien n'est plus simple, il suffit pour cela d'ouvrir l'IDE Arduino et de taper |Ctrl| + |Maj| + |M| ! L'approche que je vous propose ici est légèrement différente. Pourquoi ne pas se passer de l'IDE Arduino ? Car après tout ça serait vachement chouette d'allumer une LED en appuyant sur le bouton d'une fenêtre à l'écran :) . 
# Le code de l'Arduino Il est ici très simple -ce n'est pas l'objet de cet article- et se contente de changer l'état de la sortie 2 selon l'entrée qu'il reçoit. Lorsque l'utilisateur envoie un 'a' on met la sortie à l'état haut. Sinon à l'état bas. 

    uint8_t LED = 2;
    
    void setup() {
      pinMode(LED, OUTPUT);
      Serial.begin(9600);
      digitalWrite(LED, LOW);
    }
    
    void loop() {
      if (Serial.available())
      {
        char received = Serial.read();
        if (received == 'a')
          digitalWrite(LED, HIGH);
        else
          digitalWrite(LED, LOW);
         Serial.flush();
      }
    }
     Vous pouvez d'ores et déjà essayer ce code via le moniteur série de l'arduino, je vous fais confiance ;) . 

![Notre objectif !][1] 
# Une première approche avec Python Avant de réaliser une belle interface graphique, il est nécessaire de comprendre comment envoyer des données sur la liaison série avec Python. Pour cela nous allons simplement demander à l'utilisateur d'entrer une lettre et nous allons l'envoyer à l'arduino avec le module 

`serial`. 
    import serial
    
    s = serial.Serial(port="/dev/ttyACM1")
    
    while True:
        s.write(bytes(input(">>> "), encoding="utf-8"))
     L'envoi de données est très simple. Il vous faudra sans doute changer le port (vous pouvez savoir le petit nom de celui que vous utilisez dans l'IDE Arduino). De manière générale, sous Windows les ports série sont de la forme 

`COMx`. Sous GNU/Linux vous les retrouverez dans le répertoire `/dev/` (il faut vérifier que vous ayez les droits d'accès). La seule subtilité est que la méthode `write` attend en paramètre un objet de type `bytes` alors que la fonction `input` renvoie un `str`. Il faut donc effectuer la conversion. Et si tout se passe bien vous obtenez cette magnifique CLI : ![La CLI][2] 
# Une petite interface graphique Si vous avez compris la première partie et si vous êtes à l'aise avec 

`tkinter`, cette partie ne devrait pas vous poser de problème. Nous allons simplement réaliser une interface graphique avec un bouton qui permettra d'allumer ou d'éteindre la LED. 
    import serial
    from tkinter import *
    
    class Window(Frame):
        def __init__(self, master, **kwargs):
            Frame.__init__(self, master, width=600, height=400, **kwargs)    
            self.master = master
    
            self.btn = Button(self, text="Appuis sur le bouton mon grand !", command=self.msg )
            self.btn.pack(side="bottom", fill=BOTH)   
    
            self.LED_state = True
            self.serial = serial.Serial(port="/dev/ttyACM1")
    
        def msg(self):
            if self.LED_state:
                self.serial.write(bytes('a', encoding="utf-8"))
            else:
                self.serial.write(bytes('z', encoding="utf-8"))
            self.LED_state = not self.LED_state
    
    if __name__ == '__main__':
        fen = Tk()
        w = Window(fen)
        w.pack()
        fen.mainloop()
     On se contente de venir envoyer la valeur inverse de la précédente à chaque appuis sur le bouton ('a' ou autre chose que 'a'). 

# *BONUS* Sélectionner le port série Les exemples précédents comportent un problème. En effet le port série utilisé est inscrit "en dur" dans le programme et il est impossible de le modifier. On pourrait imaginer demander à l'utilisateur d'écrire le nom du port série. Cependant durant mes pérégrinations sur le web, je suis tombé sur 

[cette solution][3] qui me plaît beaucoup, et je me permet donc de la partager. La fonction `serial_ports` renvoie la liste des ports série disponibles. On peut donc modifier le programme précédent pour permettre à l'utilisateur de choisir son port série. En modifiant le code précédent, on obtient donc : 
    import serial
    import sys
    import glob
    from tkinter import *
    from tkinter import messagebox
    
    def serial_ports():
        """Lists serial ports
    
        :raises EnvironmentError:
            On unsupported or unknown platforms
        :returns:
            A list of available serial ports
        """
        if sys.platform.startswith('win'):
            ports = ['COM' + str(i + 1) for i in range(256)]
    
        elif sys.platform.startswith('linux') or sys.platform.startswith('cygwin'):
            # this is to exclude your current terminal "/dev/tty"
            ports = glob.glob('/dev/tty[A-Za-z]*')
    
        elif sys.platform.startswith('darwin'):
            ports = glob.glob('/dev/tty.*')
    
        else:
            raise EnvironmentError('Unsupported platform')
    
        result = []
        for port in ports:
            try:
                s = serial.Serial(port)
                s.close()
                result.append(port)
            except (OSError, serial.SerialException):
                pass
        return result
    
    class Window(Frame):
        def __init__(self, master, **kwargs):
            Frame.__init__(self, master, width=600, height=400, **kwargs)
    
            self.master = master
    
    
            self.btn = Button(self, text="Appuis sur le bouton mon grand !", command=self.msg )
            self.btn.pack(side="bottom", fill=BOTH)
    
            self.list = Listbox(self)
            for element in serial_ports():
                self.list.insert(END, element)
    
            self.list.pack(side="bottom", fill=BOTH)
            self.list.bind('<Double-1>', self.clic)
    
    
            self.LED_state = True
            self.serial = serial.Serial()
    
        def msg(self):
            try:
                if self.LED_state:
                    self.serial.write(bytes('a', encoding="utf-8"))
                else:
                    self.serial.write(bytes('z', encoding="utf-8"))
                self.LED_state = not self.LED_state
            except:
                messagebox.showwarning("Serial port","Mauvais port série !")
    
        def clic(self, e):
            self.serial = serial.Serial(port=self.list.get(self.list.curselection()))
    
    if __name__ == '__main__':
        fen = Tk()
        w = Window(fen)
        w.pack()
        fen.mainloop()
     Et voilà le résultat ! 

![Le résultat][4] 
# Conclusion Cette petite introduction au module 

`serial` est terminée ! Restez curieux et n'hésitez pas à bidouiller de petits programmes. Vous pouvez par exemple vous intéresser à la réception de données via Python qui peut se faire avec le même module ! Pour cela référez-vous à sa documentation ;) . Vous pouvez la retrouver [ici][5] en ligne . Sinon un petit `python3 -c "import serial;help(serial)"` vous permettra d'accéder à la documentation du module hors ligne !

 [1]: http://sivigik.com/wp-content/uploads/2015/07/allume_led.jpg
 [2]: http://sivigik.com/wp-content/uploads/2015/07/CLI.png
 [3]: http://stackoverflow.com/questions/12090503/listing-available-com-ports-with-python
 [4]: http://sivigik.com/wp-content/uploads/2015/07/interface.png
 [5]: https://pyserial.readthedocs.org/en/latest/

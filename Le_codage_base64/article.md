# Introduction Dans cet article, nous allons nous intéresser au codage base64. Citation, 

*wikipedia* : 
> En informatique, base64 est un codage de l'information utilisant 64 caractères, choisis pour être disponibles sur la majorité des systèmes. Défini en tant qu'encodage MIME dans le RFC 2045, il est principalement utilisé pour la transmission de messages (courrier électronique et forums Usenet) sur l'Internet. Il est par ailleurs défini en propre dans le RFC 4648  Citation, *Comment ça marche* : 
> Les protocoles de courrier électronique ont en effet été prévus à l'origine pour transporter des messages en texte seulement. Or, étant donné la diversité des systèmes de courrier électronique, l'échange de données binaires se traduit la plupart du temps par des transformations du contenu rendant illisible le document original.  Citation, *wikipedia* : 
> L’intérêt de l'encodage base64 ne se trouve donc pas dans la représentation de données textuelles, mais surtout dans la représentation de données binaires. Lorsque l’on veut représenter des données binaires (une image, un exécutable) dans un document textuel, tel qu’un courriel, la simple transcription des 0 et des 1 utilise en ASCII un octet pour chaque bit : soit une augmentation de la taille d’un facteur 8. L'encodage en base64 permet en fait de limiter cette augmentation. ***Attendez ! Ne partez pas !*** L'intérêt du codage Base64 n'est pas l'objet de cet article. En effet, la réalisation d'un programme qui encode/décode est en réalité un prétexte à l'utilisation des masques et à la manipulation de données binaires !#Quelques règles Pour coder une information en base 64, on utilisera les caractères suivants: 
    'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/='
     La sortie de l'encodeur est donc une chaîne de caractères ne contenant que ces caractères. 

# L'algorithme de codage Pour encoder une chaîne, on va faire correspondre quatre caractères à chaque groupe de trois octets. Pour cela, on met 'bout à bout' la valeur de chacun des trois octets (on a donc un nombre codé sur 24 bits). Ensuite, on découpe ce nombre en quatre autres nombres codés sur 6 bits (donc compris entre 0 et 63 inclus). Enfin, on fait correspondre chacun de ces nombres à un caractère de notre table. Autrement dit, pour la chaîne d'entrée 'ABC' : 

![schémas_encodage][1] Cependant, on a un problème pour les chaînes qui n'ont pas un nombre de caractères (d'octets) multiple de 3. Dans ce cas, on complète avec des zéros et on ajoute un '=' à la fin de la sortie par octet manquant (1 ou 2). En entrée de notre fonction d'encodage, on aura une chaîne de caractères. Il va ensuite être nécessaire de 'combler' les caractères manquants si besoin. On va donc calculer le nombre de caractères manquants. Pour cela, récupère le reste de la division entière de la différence du nombre d'octets et de 3. Soit en python : 
    nb_of_null_bytes_needed = (3 - len(string))%3
     On ajoute ensuite le nombre d'octets nuls dont on a besoin, puis on découpe la chaîne en groupes de trois octets. Pour les mettre 'bout à bout', nous allons utiliser le décalage de bits et l'opérateur 

`OU`. Au début, on a : 
*   octet1 : `0100.0001` 
*   octet2 : `0100.0010` 
*   octet3 : `0100.0011`  Ensuite, on décale chaque octet en fonction de son rang : 

*   octet1 : `0100.0001 << 16 = 0100.0001.0000.0000.0000.0000` 
*   octet2 : `0100.0010 << 8 = 0000.0000.0100.0010.0000.0000` 
*   octet3 : `0100.0011 = 0000.0000.0000.0000.0100.0011`  Enfin, on applique l'opérateur OU: 

       0100.0001.0000.0000.0000.0000
    OU 0000.0000.0100.0010.0000.0000
    OU 0000.0000.0000.0000.0100.0011
    --------------------------------
       0100.0001.0100.0010.0100.0011
     Il faut maintenant découper ce nombre en paquets de six bits. Pour cela on va utiliser des masques.

  
Pour récupérer le premier groupe, on va donc utiliser `1111.1100.0000.0000.0000.0000` (`0xFC0000`). Pour le deuxième, `0000.0011.1111.0000.0000.0000` (`0x3F000`). Le troisième `0000.0000.0000.1111.1100.0000` (`0xFC0`). Enfin pour le quatrième `0000.0000.0000.0000.0011.1111` (`0x3F`). On utilisera également le décalage de bits à droite (18 pour le premier, 12 pour le second et 6 pour le troisième). Enfin, on fait correspondre chaque groupe à une valeur. 
# L'encodeur python Assez blablaté ! passons à l'action !

  
Tout d'abord, on va expliciter le jeu de caractères autorisés. 
    CHAR= 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/='
     Nous allons ensuite avoir besoin d'une fonction pour compléter avec des octets nuls : 

    def add_null_bytes(string, nb_of_null):
        working_string = string
        for i in range(0, nb_of_null):
            working_string += b'�'
        return working_string
     On peut ainsi attaquer sereinement notre fonction d'encodage.

  
On commence par mettre au propre notre chaîne de `bytes` d'entrée. 
    def to_base_64(string):
        output_string = ''
        nb_of_null_bytes_needed = (3 - len(string))%3 
        working_string = add_null_bytes(string, nb_of_null_bytes_needed)
     Puis on s'occupe de découper la chaîne en groupes de trois octets et de diviser ces groupes en nombres codés sur 6 bits. 

    def to_base_64(string):
        output_string = ''
        nb_of_null_bytes_needed = (3 - len(string))%3 
        working_string = add_null_bytes(string, nb_of_null_bytes_needed)
    
        while len(working_string) >= 3:
            cutted_string = working_string[:3]
            working_string = working_string[3:]
            num_val = cutted_string[0] << 16
            num_val |= cutted_string[1] << 8
            num_val |= cutted_string[2]
            output_string += CHAR[(num_val & 0xFC0000) >> 18]
            output_string += CHAR[(num_val & 0x3F000)>>12]
            output_string += CHAR[(num_val & 0xFC0)>>6]
            output_string += CHAR[num_val & 0x3F]
     Cependant, il ne faut pas oublier les '=' ! On doit en ajouter autant qu'on a ajouté d'octet nul (donc soit un, soit deux). Ce qui donne : 

    def to_base_64(string):
        output_string = ''
        nb_of_null_bytes_needed = (3 - len(string))%3 
        working_string = add_null_bytes(string, nb_of_null_bytes_needed)
    
         while len(working_string) >= 3:
             cutted_string = working_string[:3]
             working_string = working_string[3:]
    
             num_val = cutted_string[0] << 16
             num_val |= cutted_string[1] << 8
             num_val |= cutted_string[2]
    
             third_part_is_eq = len(working_string) < 3 and nb_of_null_bytes_needed is 2
             fourth_part_is_eq = len(working_string) < 3 and nb_of_null_bytes_needed in [1, 2]
    
             output_string += CHAR[(num_val & 0xFC0000) >> 18]
             output_string += CHAR[(num_val & 0x3F000)>>12]
             output_string += CHAR[(num_val & 0xFC0)>>6] if not third_part_is_eq else CHAR[-1]
             output_string += CHAR[num_val & 0x3F] if not fourth_part_is_eq else CHAR[-1]
    
        return output_string
     Il ne reste qu'à ajouter une fonction pour encoder une chaîne et une autre pour encoder un fichier. Pour l'encodage de fichier: 

    def encode_file(filename):
        string = []
        with open(filename, 'rb') as in_file:
            string = in_file.read()
        with open(filename + '.base64', 'w') as out_file:
            out_file.write(to_base_64(string))
     On peut noter ici tout l'intérêt d'attendre un 

`bytes` dans `to_base_64()` : cela permet la lecture binaire du fichier d'entrée et également d'avoir la certitude que tout octet soit géré (ce qui n'aurait pas été le cas avec une lecture 'classique' et un objet `str`). Enfin, pour l'encodage de chaîne de caractères, on s'assure juste de fournir un `bytes` à `to_base_64()`. 
    def encode_string(string):
        return to_base_64(string.encode('utf-8'))
    

# L'algorithme de décodage Il s'agit en réalité du même algorithme mais en commençant par la fin. On a en entrée 4 octets; on les raccourcit à 6 bits, puis on ré-assemble et on découpe en trois octets ! 

# Le décodeur python Il faut tout d'abord pouvoir vérifier que la chaîne de caractères fournie est valide (nombre de caractères multiple de 4 et finit par 2 '=' au maximum). 

    def is_valid_base_64(string):
        returned = True
        for c in string:
            returned &= c in CHAR
    
        returned &= len(string) % 4 is 0
    
        #A Base64 string should not end with '==='
        returned &= not(string[-1] is '=' and string[-2] is '=' and string[-3] is '=')
        return returned
     Ensuite, on veut pouvoir donner un 'poids' à chaque caractère. 

    def found_a_char_value(char):
        if char is '=':
            return 0
        else:
            return CHAR.find(char)
     Occupons-nous maintenant de la fonction de décodage. On commence par vérifier la chaîne. 

    def from_base_64(string):
        if not is_valid_base_64(string):
            raise ValueError('"{}" is not a valid base 64 string.'.format(string))
     Ensuite, on applique l'algorithme : 

    def from_base_64(string):
        if not is_valid_base_64(string):
            raise ValueError('"{}" is not a valid base 64 string.'.format(string))
    
        output_string = []
        working_string = string
    
        while len(working_string) >= 4:
            cutted_string = working_string[:4]
            working_string = working_string[4:]
    
            first_char_val = found_a_char_value(cutted_string[3])
            second_char_val = found_a_char_value(cutted_string[2])
            third_char_val = found_a_char_value(cutted_string[1])
            fourth_char_val = found_a_char_value(cutted_string[0])
    
            num_val =  first_char_val | (second_char_val << 6)
            num_val |= third_char_val << 12
            num_val |= fourth_char_val << 18
    
            output_string.append(num_val>>16)
            output_string.append((num_val & 0xFF00) >> 8)
            output_string.append((num_val & 0xFF))
    
        return bytes(output_string)
     Enfin, on s'occupe de la gestion des '=' (ils sont traités comme des 0, mais on ne veut pas se retrouver avec des 0 à la fin de la chaîne de sortie). 

    def from_base_64(string):
        if not is_valid_base_64(string):
            raise ValueError('"{}" is not a valid base 64 string.'.format(string))
    
        output_string = []
        working_string = string
    
        nb_eq = (1 if string[-1] is '=' else 0) + (1 if string[-2] is '=' else 0)
    
        while len(working_string) >= 4:
            cutted_string = working_string[:4]
            working_string = working_string[4:]
    
            first_char_val = found_a_char_value(cutted_string[3])
            second_char_val = found_a_char_value(cutted_string[2])
            third_char_val = found_a_char_value(cutted_string[1])
            fourth_char_val = found_a_char_value(cutted_string[0])
    
            num_val =  first_char_val | (second_char_val << 6)
            num_val |= third_char_val << 12
            num_val |= fourth_char_val << 18
    
            output_string.append(num_val>>16)
            if len(working_string) >= 4 or nb_eq <= 1:
                output_string.append((num_val & 0xFF00) >> 8)
            if len(working_string) >= 4 or nb_eq is 0: 
                output_string.append((num_val & 0xFF))
    
        return bytes(output_string)
     Pour finir, on ajoute une fonction de décodage de fichier et de chaîne. 

    def decode_file(filename):
        string = ''
        with open(filename, 'r') as in_file:
            string = in_file.read()
        string = from_base_64(string)
        with open(filename + '.dec', 'wb') as out_file:
            out_file.write(string)
    
    def decode_string(string):
        return from_base_64(string).decode('utf-8')
    

# Liens utiles

*   Le [github du projet][2]
*   [Wikipédia][3]
*   [Comment ça marche][4]

 [1]: http://www.heberger-image.fr/data/images/88702_Sch_ma_encodage.png
 [2]: https://github.com/Klafyvel/Base64Encoder
 [3]: http://fr.wikipedia.org/wiki/Base64
 [4]: http://www.commentcamarche.net/contents/94-codage-base64

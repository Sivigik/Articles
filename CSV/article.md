# Le format de fichier CSV 
Un problème courant en informatique est le stockage de l'information, et plus précisément sa représentation en mémoire. Si vous êtes déjà entré dans une salle de TP de physique-chimie, peut-être vous est-il arrivé de devoir noter sur votre compte rendu un certain nombre de valeurs expérimentales. Un moyen efficace de procéder consiste en la réalisation d'un tableau. C'est exactement le principe des fichiers CSV. Pourquoi CSV au fait ? pour 

*Comma-Separated Values*, littéralement : valeurs séparées par des virgules. Les données sont stockées au format texte (ce qui signifie que vous pouvez utiliser le bloc note par exemple pour éditer votre fichier). Il existe plusieurs variantes du format CSV, permettant de stocker des valeurs avec des virgules etc. L'objet de cet article et la création d'une petite bibliothèque pour lire ces fichiers en python. Il existe déjà des bibliothèques qui le font, il ne s'agit là que d'un prétexte pour s'entraîner. ;) Nous finirons cet article par une petite mise en pratique. 
# Comment kesk'on fait ?

## Où l'on discute stratégie 
Bon, vous vous en doutez bien, lire un fichier CSV n'a rien de bien sorcier. La première chose à laquelle on pense, c'est faire un petit script qui, à chaque fois qu'il rencontre un séparateur, ajoute une entrée dans une liste. Mais c'est sans compter sur notre langage préféré : <s>Le Brainfuck</s> Le Python ! Nous allons utiliser les générateurs pour éviter de surcharger la mémoire en lisant tout le fichier d'un coup. 

## Le coin tactique 
Nous découperons notre code en 3 fonctions : - une première, qui sera en réalité un générateur, chargée de découper le fichier en lignes et en colonnes, - une seconde chargée d'assembler un tableau à partir de ces cellules, - une dernière pour obtenir un tableau à partir d'un nom de fichier. 

## BANZAÏ ! 
Le générateur : 

```python
def csv_to_cell(s):
    c = ""
    for i in s:
        if i is ",":
            yield (c,'END_CELL')
            c=""
        elif i is "\n":
            yield (c,'END_LINE')
            c=""
        else:
            c+=i
   yield (c,'END_LINE')
```

On se contente ici de renvoyer le contenu des cellules une par une avec une information sur la nature de la transition. La partie assemblage de tableau : 

```python
def build_table(s):
    table = []
    row = []
    for i in csv_to_cell(s):
        row.append(i[0])
        if i[1] == "END_LINE":
            table.append(row[:])
            row = []
    return table
```
    
Rien de bien compliqué ici, je pense que le code se suffit à lui même. La lecture de fichier : 

```python
def table_from_file(filename):
    r=None
    with open(filename, "r") as f:
        r = build_table(f.read())
    return r
```
    
On peut difficilement faire plus simple ! 

## Retour vers la réalité

> Attends voir... tu nous avais dit que l'on allait éviter de stocker toutes les données dans une liste non ?

Bien vu ! Nous allons donc pouvoir coder une fonction qui renvoie des lignes à partir de chaînes de caractères reçues en entrée. Je vous propose d'essayer de la coder vous-même avant de regarder la correction. Petit indice, vous aurez besoin de `yield` ! C'est bon ? Voici ma version: 

```python
def csv_to_line(lines):
    for l in lines:
        yield [c[0] for c in csv_to_cell(l)]
```
        
L'intérêt de ce genre de structure est de pouvoir recevoir des données à la volée (d'une Arduino par exemple :-° ). Une petite application : 

```python
def reader():
    while True:
        yield input("> ")

def printer(it):
    for i in it:
        print(i)

if __name__ == '__main__':
    printer(csv_to_line(reader()))
```
        
Le résultat : 

```shell
> 1,2,3,4,5
['1', '2', '3', '4', '5']
>
```

## Garçon ? Plus de sucre s'il vous plaît. 
On peut encore améliorer tout ça ! 

### Permettre la conversion automatique lors de la lecture 

Bah oui, on va quand même pas se fatiguer à traiter nous-même les données quand on peut demander à notre lib' de le faire ! 

```python
def csv_to_cell(s, converter=str):
    c = ""
    for x,i in enumerate(s):
        if i is ",":
            yield (converter(c),'END_CELL')
            c=""
        elif i is "\n":
            yield (converter(c),'END_LINE')
            c=""
        else:
            c+=i
    try:
        yield (converter(c),'END_LINE')
    except ValueError:
        pass

def build_table(s, converter=str):
    table = []
    row = []
    for i in csv_to_cell(s,converter):
        row.append(i[0])
        if i[1] == "END_LINE":
            table.append(row[:])
            row = []
    return table

def table_from_file(filename,converter=str):
    r=None
    with open(filename, "r") as f:
        r = build_table(f.read())
    return r

def csv_to_line(lines, converter=str):
    for l in lines:
        yield [c[0] for c in csv_to_cell(l, converter)]

def reader():
    while True:
        yield input("> ")

def printer(it):
    for i in it:
        print(i)

if __name__ == '__main__':
    printer(csv_to_line(reader(), float))
```    

## Des titres à nos colonnes 

Tant qu'à stocker des données, autant savoir ce que c'est ! 

```python
def create_dict_from_columns(table):
    d = {}
    eq = {}
    for x,cell in enumerate(table[0]):
        d[cell] = []
        eq[cell] = x
    for key in d:
        for row in table[1:]:
            d[key].append(row[eq[key]])
    return d

def dict_from_file(filename, converter=float):
    r=None
    with open(filename, "r") as f:
        r = f.read()
    assert r

    table = []
    row = []
    r = r.split('\n')
    for c in csv_to_cell(r[0],str):
        row.append(c[0])
        table.append(row[:])
        row = []
    for c in csv_to_cell('\n'.join(r[1:]), converter):
        row.append(c[0])
        if c[1] == "END_LINE":
            table.append(row[:])
            row = []
    return create_dict_from_columns(table)
```
    
Ici l'implémentation montre un des défauts de notre conversion automatique de types : il est difficile de gérer le cas où plusieurs types de données différentes sont stockés. 

# Un bon gros exemple d'utilisation pour finir 

J'ai, pour illustrer cet article, réalisé un programme qui charge un fichier CSV pour l'afficher avec matplotlib. Le code est [ici](https://github.com/Klafyvel/ArticleSivigikCSV). 

![](http://sivigik.com/wp-content/uploads/2016/02/screencastCSV.gif)

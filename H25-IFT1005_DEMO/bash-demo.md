
# 1. Commandes

### Avec ``mkdir``, créez 11 répertoires, de ``exercice01`` à ``exercice12`` 

```bash
mkdir exercice{1..12}
```

### Avec ``touch``,  créez un fichier `completion.txt` et un fichier ``test.txt``

```bash
touch completion.txt test.txt
```

### Avec ``nano``, modifiez le contenu du fichier créé précédemment afin d'écrire le statut de complétion de chacun des exercices (exercice 1 : fait, exercice 2 : non fait)

```bash
nano completion.txt
"Exercice 1 : fait
...
"
ctrl+x
yes
ENTER
```

### Avec `mv`, déplacez le fichier `test.txt` dans le répertoire ``exercice12

```bash
mv test.txt exercice12
```

### Avec ``cd``, entrez dans le répertoire ``exercice12``, puis créez un fichier vide, ensuite sortez du répertoire avec ``cd ..

```bash
cd exercice12
touch obsolete.txt
cd ..
```

### Avec ``rm``, supprimez **récursivement** le répertoire `exercice12`

```bash
rm -r exercice12
```
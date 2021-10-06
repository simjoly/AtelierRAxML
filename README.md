# AtelierRAxML

Atelier d'initiation au logiciel d'analyse phylogénétique RAxML

Simon Joly, automne 2021

## Introduction

Ces dernières années, RAxML est devenu l’outil le plus robuste et le plus rapide pour faire des analyses phylogénétiques en maximum de vraissemblance (ML). C’est la référence pour ce type d’analyse et c’est pourquoi il est utilisé dans ce TP.

RAxML est souvent utilisé via un terminal en ligne de commande. Ce n’est pas particulièrement compliqué, mais il faut se familiariser avec les commandes. Certains outils avec interface graphique existent pour utiliser RAxML, mais il sont soient payants (e.g., CYPRES) ou soit moins flexibles que l'application en ligne de commande ([Swiss Institute for Bioinformatics](https://raxml-ng.vital-it.ch/)). Pour cette raison, cet atelier va introduire l'utilisation de RAxML en ligne de commande. Pour les intéressés, une section plus bas explique aussi comment l'utiliser sur le site de la [Swiss Institute for Bioinformatics](https://raxml-ng.vital-it.ch/).

> Cet atelier est une introduction à RAxML et n'explique pas toutes les options possible. Avant d'effectuer une analyse pour un travail ou une publication, vous devriez consulter le consulter le [manuel d’utilisation de RAxML](https://cme.h-its.org/exelixis/php/countManualNew.php). Pour plus d'informations, consultez le [site web de RAxML](https://cme.h-its.org/exelixis/web/software/raxml/).

## Préparation

### Logiciel

Comme RAxML est un logiciel en ligne de commande, il est généralement recommandé de compiler le programme sur chaque ordinateur pour s'assurer d'un bon fonctionnement. Comme c'est parfois compliqué de procéder ainsi rapidement dans les systèmes Windows et sur les macOS qui n'ont pas Xcode d'installé, je mets à la disposition des programmes déjà compilés pour ces environnements qui devraient fonctionner.

Si vous travaillez sur Linux ou si vous voulez recompiler le programme, veuillez visiter la [page Github de RAxML](https://github.com/stamatak/standard-RAxML) pour le code et les intructions de compilation.

Pour cet exercice, nous allons utiliser la version parallèle (pthreads) de RAxML.

Les exécutables sont dans le dossier `executables`. Je vous conseille de télécharger le programme approprié à votre système et de renommer le programme `raxml` pour faciliter l'utilisation pour l'atelier.

### Données

Il est possible d'utiliser vos propres données pour cet exercices, mais je mets aussi un alignements du gène chloroplastique rbcL de quelques arbres du Québec à votre disposition. Les données nécessaires pour les exercices sont dans le dossier `data`.

Notez que les données pour RAxML doivent idéalement être en format fasta.

## Une première analyse

### Premier test

D'abord, je vous suggère de créer un dossier sur votre ordinateur qui contiendra le logiciel raxml ainsi que les données du dossier `data` (ou vos données).

Pour utiliser RAxML, il faut ouvrir une fenêtre de terminal (DOS pour windows, terminal pour macOS). Il faut ensuite naviguer vers le dossier où se trouve le programme et les données (utilisez la commande `cd`).

Une fois dans le dossier, vous pouvez vous assurer que le logiciel fonctionne en tapant:

```
# Pour Windows:
$>raxml -h

# Pour MAC et linux:
$>./raxml -h
```

L'option `-h` demande à raxml de donner le fichier d'aide et vous devriez le voir à l'écran après avoir tapé la commande. Notez que le './' de la commande sur linux indique à l'ordinateur de chercher le programme dans le dossier actif. Il est possible de mettre le logiciel dans le PATH du système qui permettrait d'ommettre le './'. Pour le reste de l'atelier, je vais l'ommettre pour simplicité, mais n'oubliez pas de toujours l'ajouter au début de la commande pour les utilisateurs mac et linux.

### Première analyse

Il est maintenant possible de lancer la première analyse. Voici la commande à donner à raxml:

```
raxml -s rbcl.fasta -n test1 -m GTRGAMMA -T 2 -p 123 
```

Décorticons un peu cette commande par option.

1. L'option `-s` indique le fichier avec les séquences.
1. L'option `-n` donne un nom à l'analyse. Utilisez un nom différent à chaque nouvelle analyse.
1. L'option `-m` spécifie le modèle évolutif à utiliser. Plusieurs options sont possible (se référer au manuel).
1. L'option `-T` donne le nombre de coeurs de CPU à utiliser pour l'analyse. À modifier selon votre ordinateur. Je vous suggère d'utiliser un CPU de moins que le nombre de coeur de votre ordinateur pour vous permettre de continuer d'utiliser facilement l'ordinateur pendant les analyses.
1. L'option `-p` donne la graine pour le générateur de nombre aléatoire. Ça permet d'obtenir les même résultats à chaque fois lorsque l'on utilise le même numéro. C'est optionel.

Normalement, RAxML devrait procéder à l'analyse très rapidement puisque c'est un petit jeu de données. Il va alors écrire dans le dossier plusieurs fichiers dont les noms commencent par `RAxML_` et se terminent par `.test1` (le nom de l'analyse).

Le fichier `RAxML_bestTree.test1` contient le résultat (le meilleur arbre). Le fichier `RAxML_info.test1` contient les paramètres de l'analyse et la sortie. Il est utile de le vérifier si quelque chose n'a pas fonctionné. Le fichier `RAxML_log.test1` contient les logLikelihoods obtenus pendant l'analyse et le score final (dernière valeur du fichier).

### Changeons les arbres de départ



## Utiliser RAxML en ligne

Aller sur le site web du [Swiss Institute for Bioinformatics](https://raxml-ng.vital-it.ch/)

2. Data 
- Coller ou charger votre jeu de données en format fasta ou phylip
- Optionnel : Il est possible de charger un arbre phylogénétique « contrainte », c’est-à-dire que les branches présentes dans cet arbre phylogénétique devront obligatoirement se trouver dans l’arbre final. Cette approche peut être utile lorsque l’on est certain de certaines relations phylogénétiques (e.g., les souris son plus proche parentes des lapins que des koalas) ou si on veut tester des hypothèses phylogénétiques spécifiques.
3. Evolutionary Model 
- Ce block permet de choisir le modèle phylogénétique voulu et / ou de diviser le jeu de données en différents gènes si le jeu de données contient plusieurs gènes. Les valeurs données par défaut sont raisonnables, mais il est toujours mieux de déterminer le meilleur modèle évolutif pour nos données.
3. Analysis 
Ici, on doit choisir les paramètres de l’analyse.
ML tree search :  Il est toujours souhaitable de rechercher la topologie, les longueurs de branches et le modèle.
Starting trees : Il est possible de débuter l’analyse soit avec un arbre de parcimonie ou soit avec des arbres aléatoires, ou soit avec un arbre que l’on donne au programme. Les arbres aléatoires sont intéressants parce que les recherches vont débuter d’endroits vraiment différent et cela peut aider à l’assurer que la recherche d’arbres n’est pas coincé dans une région de l’espace des arbres qui est sous-optimale. Pour de petits jeux de données, cette option ne devrait pas avoir d’impact sur le résultat. 
-> Je vous recommande de cocher l’option « parsimonie » avec seulement un arbre de départ pour le labo.
Bootstrapping : Si vous voulez faire une analyse de bootstrap, je vous encourage à cliquer sur la case. Vous pouvez ensuite choisir « fixed » comme option et donner un nombre de réplicats de bootstrap à faire. Il est généralement recommandé de faire 1000 réplicats, mais ça peut être long avec certains jeux de données et vous pouvez choisir 100 dans le cadre du TP.
3. Submit 
Cliquez sur « submit » pour soumettre l’analyse. 
6. Preview and Download the Results 
7. Visualiser les résultats

- In your browser, add the suffix .tre to the RAxML_bipartitions.result file, and open it up in your favourite tree viewing program. Note: Unfortunately the widely used Figtree program does not read this specific file. One alternative is to use the demo version of Geneious (https://www.geneious.com). 


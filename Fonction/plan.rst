--------------------------------------------------------------------------------
Initiation à la progr - dummy title
--------------------------------------------------------------------------------

Objectifs du cours
================================================================================

- Découvrir les outils permettant le développement d'OrbisGIS
- Aller plus loin dans la connaissance des structures essentielles de GDMS
- Créer une nouvelle fonction d'analyse dans GDMSQL


Les outils de développement indispensables
--------------------------------------------------------------------------------

Être capable de développer en équipe.
================================================================================

OrbisGIS est développé et maintenu par des personnes distantes. 

Problèmes : 

- Comment gérer efficacement les modifications apportées dans le code source ?
- Comment savoir qui a fait une modification ?
- Comment assurer la mise en oeuvre de nouvelles fonctionnalités sans mettre
  en péril la base de code existante ?

Les systèmes de gestion de version
================================================================================

Pour résoudre ces problèmes, on peut s'appuyer sur un système de gestion de 
versions. La solution utilisée actuellement par l'équipe de développement
d'OrbisGIS s'appelle Subversion (SVN).

http://subversion.tigris.org

Les apports de SVN - la notion de commit
================================================================================

Pour mieux comprendre les modifications apportées par les développeurs, il est
intéressant de les gérer de façon incrémentale. On utilise pour cela la notion
de commit :

- Seules les lignes modifiées, ajoutées et supprimées sont communiquées.
- Chaque modification est accompagnée d'un commentaire la décrivant

Pour une personne suffisamment investie dans le projet, ces deux informations
sont généralement suffisantes pour :

- Comprendre la teneur du commit
- Apprécier la qualité du code produit
- Éventuellement, apporter des critiques à propos de la modification

Les apports de SVN - la notion de commit : exemple
================================================================================

.. image:: diff.png
  :width: 75%


Les apports de SVN - le suivi des modifications
================================================================================

Quand une modification est prête, le développeur peut la commiter. Cela revient
à publier les changements sur le dépôt SVN. Par conséquent :

- Le commit devient accesible à tous les développeurs du projet
- Le commit est associé par le serveur à son auteur

Les apports de SVN - la notion d'historique (1)
================================================================================

Une modification, une fois commitée, est ajoutée à l'historique du projet. Dans
SVN, l'historique est linéaire : tous les commits sont présentés les uns à la
suite des autres. À chaque commit est associé un numero de *révision*.

Il est possible d'interroger assez finement l'historique d'un dépôt SVN. Ainsi,
nous pouvons :

- Connaître toutes les modifications et tous les messages de chacune des 
  révisions
- Connaître précisément l'historique de chacune des lignes de chacun des 
  fichiers

Les apports de SVN - la notion d'historique (2)
================================================================================

Grâce à l'historique, nous pouvons donc connaître "exactement" :

- L'auteur d'une ligne défectueuse dans le code
- La justification première de l'écriture d'un code, les problèmes qu'il a 
  permis de résoudre.

Ces deux points sont bien sûr contraints :

- À la qualité des messages de commit
- À la qualité de la gestion du dépôt SVN.

SVN - quelques commandes de base
================================================================================

- svn checkout : Récupérer une copie locale d'un dépôt distant
- svn diff : Consulter les modifications apportées à la copie locale
- svn commit : Commiter les fichiers sur le serveur
- svn up : Récupérer les modifications poussées sur le serveur par les autres
  développeurs


SVN - conclusion
================================================================================

SVN est un outils qui permet de conserver une vision claire :

- Du travail effectué par tous les développeurs sur un projet
- De l'évolution d'un projet
- De la qualité ponctuelle des modifications apportées à un projet

Il s'agit également, au travers des messages de commit, d'un moyen de
communication au sein de l'équipe.

Maven - une gestion simplifiée du processus de build
================================================================================

Le second outil indispensable (notamment pour vous en TP) est Maven. Il s'agit
d'un outil permettant de gérer :

- Les dépendances d'un projet.
- Les différentes phases de la construction d'un projet.

Il réalise certaines tâches décrites parfois dans des Makefile

Maven - le paradigme Convention over Configuration (1)
================================================================================

Le principe fondateur de Maven est le suivant : les projets Java respectent
très souvent la même architecture et les même processus de construction. On va 
les définir comme convention pour éviter d'avoir à faire de la configuration 
qui serait :

- Dupliquée
- Fastidieuse

Il reste toutefois possible de personnaliser tous les paramètres de la 
construction du projet.

Maven - le paradigme Convention over Configuration (1)
================================================================================

L'architecture, en particulier, est très codifiée en Java :

- Fichier de configuration à la racine du projet
- Sources placées sous src/main
- Sources de tests placées sous src/test
- Fichiers compilés (.class, .jar...) placés sous target/

Maven - Configuration de l'outil
================================================================================

Maven est configuré au travers du fichier pom.xml, placé à la racine du projet.
On y définit les dépendances du projet, mais également tous les paramètres et
plugins nécessaires à la compilation du projet, à l'exécution des tests... 

Un projet ne vit (presque) jamais seul
================================================================================

Pour pouvoir construire un projet, on a souvent besoin de fonctionnalités
externes.

Exemple : Pour gérer les géométries, nous utilisons une bibliothèque (JTS) 
plutôt que de ré-écrire l'ensemble des codes. Pour construire le projet 
OrbisGIS, nous avons une dépendance envers JTS.

Maven permet de gérer ces dépendances : il va s'occuper de les transmettre
au compilateur, et même parfois à l'exécution. Il construit le "classpath"
nécessaire pour compiler et lancer le logiciel.

Maven - la notion de dépendance
================================================================================

.. image:: heritage.png
         :width: 100%

Maven : Récupération et gestion des dépendances
================================================================================

Pour récupérer et gérer les dépendances du projet, Maven a besoin : 

- De dépôts distants où il pourra chercher à les télécharger
- D'un dépôt local où il va les stocker. Ainsi, on évite les téléchargements 
  inutiles.

Quand on lance Maven la première fois, on "télécharge l'Internet"...

Maven - Exemple de dépendance
================================================================================

::

    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>3.8.1</version>
        <scope>test</scope>
    </dependency>

- Dépendance à junit
- junit.junit - version 3.8.1
- nécessaire seulement pendant la phase de test

Maven - La gestion des goals
================================================================================

On appelle goal, dans Maven, une phase de la vie d'un projet. Par défaut, 
Maven prévoit plusieurs de ces phases :

- compile : Compilation du projet
- test-compile : Compilation des test du projet
- test : exécution des tests du projet
- package : Packaging du projet (création du jar)
- install : Installation du package (jar+pom) dans le dépôt Maven local
- deploy : Installation du package (jar+pom) sur un serveur distant

Une phase peut dépendre d'autres phases. Ici, par exemple, chaque phase dépend
de toutes celles présentées avant elle dans la liste.

Maven - conclusion
================================================================================

Maven est un outil qui évite au développeur de perdre son temps sur des tâches
de configuration fastidieuses. Il permet d'aller à l'essentiel (gestion des 
dépendances, des plugins, des goals) et s'occupe de beaucoup de tâches 
chronophages.

Et d'autres outils encore...
================================================================================

Nous n'avons évoqué que deux des outils indispensables à la vie du projet de 
développement OrbisGIS. Il y en a d'autres :

- JUnit : Écriture de tests automatisés, protection contre les bugs
- Hudson/Jenkins : Vérification de l'intégrité du projet
- Sonar : Évaluation de la qualité des codes

GDMS et GDMSQL - de la table à la fonction
--------------------------------------------------------------------------------

Les DataSource dans GDMS
================================================================================

Les données sont gérées, grâce à GDMS, de façon transparente. On utilise le 
concept de *DataSource* quelle que soit la nature de la source de données. Les
*DataSource* présentent les données sous forme de table.

Afin de pouvoir manipuler une *DataSource*, il est nécessaire d'être
capable :

- De savoir quelle est la nature des données présentes dans la table.
- De savoir récupérer les données présentes dans la table.

La structure d'une DataSource
================================================================================

Une DataSource est composée de deux parties indépendantes. On trouve d'une part
les métadonnées réunissant :

- Les types des données, pour chacune des colonnes
- Les contraintes sur les types de données.

On trouve également (fort logiquement) les données dans une source de
données...

Les types de données
================================================================================

Au sein de GDMS, chaque valeur est associée à un type de données. Afin de 
forcer la cohérence entre la nature d'un colonne et son contenu, on associe 
également l'un de ces types aux colonnes, au sein des méta-données. Voyons 
comment sont gérés les types de données, avant de décrire les méta-données.

Dans GDMS, les types sont définis grâce à un champ entier (int), le typeCode. 
Deux valeurs du même type auront le même typeCode (ie leurs typeCode seront 
égaux).

Les types de données alphanumériques
================================================================================

GDMS comporte plusieurs types alpha-numériques selon les définitions suivantes :

::
	
  int BINARY = 1;
  int BOOLEAN = 2;
  int BYTE = 4;
  int DATE = 8;
  int DOUBLE = 16;
  int FLOAT = 32;
  int INT = 64;
  int LONG = 128;
  int SHORT = 256;
  int STRING = 512;
  int TIMESTAMP = 1024;
  int TIME = 2048;

Le type RASTER
================================================================================

Il y a un type dédié pour les données spatiales raster :

::

  int RASTER = 8192;


Les types de données géométriques
================================================================================

Les données géométriques sont gérées finement. Pour chaque type WKT, on a 
un type géométrique dédié :

::

  int GEOMETRY = 4096;
  int POINT = 32768 | Type.GEOMETRY;
  int LINESTRING = 65536| Type.GEOMETRY;
  int POLYGON = 131072 | Type.GEOMETRY;
  int MULTIPOLYGON = 262144 | Type.GEOMETRY;
  int MULTILINESTRING = 524288 | Type.GEOMETRYCOLLECTION;
  int MULTIPOINT = 1048576 | Type.GEOMETRYCOLLECTION;
  int GEOMETRYCOLLECTION = 2097152 | Type.GEOMETRY;

Les définitions de ces types sont un peu ésotériques... on utilise un opérateur
bit à bit sur les entiers pour en modifier la valeur...

Comment sont construits les types géométriques ?
================================================================================

L'opérateur "|" peut être considérer comme un "ou logique". Si on l'applique sur
deux entiers, il va mettre à 1 les bits de l'entier résultant pour lesquels le 
bit correspondant est mis à un dans au moins un des deux entiers d'entrée.

Concrètement...

- 0001100111
- |
- 1001010011
- -----------
- 1001110111

Pour une puissance de deux, nous sommes sûrs qu'il n'y a qu'un seul bit à 1.
On est sûr qu'il n'y aura pas de superposition entre les bits des puissances de 
deux. Par conséquent, tous les type géométriques héritent du bit de 4096. Les
collections de géométries possèdent également le bit de 2097152.

Comment tester les types géométriques ?
================================================================================

Comme il n'y a pas de superposition entre les bits lors de la construction des 
types, on ne perd pas d'informations, et on peut tester ces types.

Pour les types autres que GEOMETRY et GEOMETRYCOLLECTION, on fait un test
d'égalité (==).

Pour les types GEOMETRY et GEOMETRYCOLLECTION, on utilise l'opérateur bit à bit
&. Il s'agit du et logique sur les bits. Ainsi, pour tester qu'un type est 
bien compatible avec Type.GEOMETRY, on fera

::
  
  (monType.getTypeCode() & Type.GEOMETRY) != 0

Pour le type Type.GEOMETRYCOLLECTION :

::
  
  (monType.getTypeCode() & Type.GEOMETRYCOLLECTION) != 0


Le type NULL
================================================================================

Il existe un type NULL, dans GDMS, accessible grâce au champ 

::

  Type.NULL

Ce champ est compatible avec tous les autres types de données. On pourra donc 
mettre un valeur de Type Type.NULL dans n'importe quelle colonne (sauf
contrainte contraire). On ne pourra par contre pas mettre autre chose que 
des données de Type Type.NULL dans une colonne de Type Type.NULL.

Les contraintes sur les types de données
================================================================================



Comment placer une contrainte sur un type ? 
================================================================================

Les métadonnées
================================================================================

Créer une métadonnée
================================================================================

Les données - les Value
================================================================================

Les données - la classe ValueFactory
================================================================================

Récupérer une donnée dans une DataSource
================================================================================

Ajouter une donnée à une DataSource
================================================================================

Insérer une donnée dans une DataSource
================================================================================

Créer une DataSource
================================================================================

i























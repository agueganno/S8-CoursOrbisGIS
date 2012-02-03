================================================================================
Initiation à la progr - dummy title
================================================================================


OrbisGIS- Principes de fonctionnement
================================================================================

Objectifs du cours : 

- Présenter certains principes essentiels en informatique appliquée à la
  géographie
- Appliquer ces principes en développant au sein du logiciel SIG OrbsiGIS


OrbisGIS- Principes de fonctionnement
================================================================================

OrbisGIS est un logiciel SIG composé de plusieurs couches :

* La couche de gestion des données
* Le langage de manipulation des données
* La gestion des couches géographiques
* L'interface graphique

Les briques sont définies aussi indépendamment que possible, afin de simplifier
la maintenance du logiciel dans son ensemble

La couche de gestion des données : GDMS
================================================================================

Une gestion unifiée des sources de données (1)
--------------------------------------------------------------------------------

GDMS :i Generic Datasource Management System. C'est la couche de gestion des 
données dans OrbisGIS.

Objectif : Assurer la transparence des opérations de manipulation des données,
qu'elles soient géospatiales ou juste alpha-numériques.

Pour GDMS, tout est DataSource

Une gestion unifiée des sources de données (2)
--------------------------------------------------------------------------------

Utilisation de la notion de pilotes et d'importeurs (en construction) :

[insérer un schéma magnifique ici]

Concrètement, ça marche ?
--------------------------------------------------------------------------------

Plusieurs formats de données sont gérés par les pilotes :

* Des formats de fichiers : SHP, GDMS, MIF/MID, DXF...
* Les bases de données spatiales PostGIS

Des importeurs commencent à faire leur apparition (GPX)

Pourquoi ne pas faire que du PostGIS ?
--------------------------------------------------------------------------------

Les fichiers plats présentent certains avantages :

- Facilité d'échange
- Légèreté des manipulations
- Pas besoin d'accéder à une base de données

Les fichiers plats présentent des faiblesses :

- Pas de schéma
- Pas de relations entre les tables.
- Pas de vérification d'intégrité référentielle (clefs étrangères)
- Dispersion de la connaissance

Concrètement, une source de données, c'est quoi ?
--------------------------------------------------------------------------------

GDMS gère des tables de données. Une table est constituée :

- De métadonnées décrivant les types et contraintes sur les types qui 
  constituent la table
- De données, contenues dans les lignes de la table

Les métadonnées permettent :

* De vérifier qu'une opération peut être effectuée sur
  une table : on ne peut pas calculer l'aire d'une chaîne de caractères, 
  par exemple.
* De contrôler les données qui sont ajoutées à une table. On ne peut pas 
  insérer une géométrie dans un champ numérique.

Pourquoi un format de données spécifique à OrbisGIS ?
--------------------------------------------------------------------------------

Beaucoup de SIG libres ne proposent pas leur propre format de données. Ils 
manipulent plutôt des formats existants.

Le format GDMS natif présente des avantages :

* Rapidité d'accès aux données
* Gestion des données spatiales et alphanumériques dans un seul fichier
* Accès bufferisés aux données
* Gestion de fichiers de grande tailles 
* Format ouvert

La principale faiblesse du format GDMS : le manque de documentation... :-(

Gestion des données, gestion des indexes
--------------------------------------------------------------------------------

GDMS est capable de gérer des fichiers de plusieurs dizaines de Go.

Problème : Comment trouver une donnée rapidement ?

Plus précisément :

- Comment à trouver rapidement tous les enregistrements dont la valeur du
  champ "ALTITUDE" est 5 ?
- Comment trouver toutes les géométries présentes dans une zone données ?

Solution : Mettre en place des indexes

Les indexes alpha-numériques (1)
--------------------------------------------------------------------------------

Les types numériques et litéraux possèdent un point commun : on peut les 
ordonner "naturellement" :

- Pour les chaînes de caractères : Ordre lexicographique
- Pour les champs numériques : relation d'ordre pour les réel (ou les entiers
  selon les cas, mais la différence n'est pas fondamentale).

On est capable de trier les valeurs. Reste à les placer dans la structure de
données la plus adaptée.

Les indexes alpha-numériques (2)
--------------------------------------------------------------------------------

Quelle structure de données sur le disque ?

Simple table clé-valeur (valeur cherchée, position dans le fichier) et 
recherche par dichotomie : nombreuses opération d'entrée-sortie, coût élevé.

 
 [Insérer un schéma magnifique ici]

Les indexes alpha-numériques (3)
--------------------------------------------------------------------------------

Recherche dans un arbre équilibré (BTree) : Recherche dans une seule 
direction dans l'index.

[Insérer un schéma magnifique ici]

Avantages d'un arbre équilibré : 

- Profondeur constante -> On accède aux données dans le même temps quelle que 
  soit la donnée
- Recherche (sur disque) des données peut être faite en lisant toujours dans
  le même sens

[Insérer un schéma magnifique ici]

Les indexes spatiaux (1)
--------------------------------------------------------------------------------

Pour les données spatiales, on n'a pas de relation d'ordre simple. Mais on a 
tout de même besoin de trouver les données rapidement...

Stratégie : partitonnement de l'espace. On analyse la configuration spatiale des
données, et on construit un arbre reflétant l'organisation spatiale du jeu de 
données...

Les indexes spatiaux (2)
--------------------------------------------------------------------------------

[Construire un schéma magnifique à insérer ici]

Les indexes spatiaux (3)
--------------------------------------------------------------------------------

[Construire un schéma magnifique à insérer ici]

La couche de manipulation des données : GDMSQL
================================================================================

GDMS est la couche de manipulation des données. Elle permet de :

- Lire les données
- Écrire les données
- Gérer les sources de données
- Décrire les données

Les autres manipulations ne sont a priori pas prévues. C'est le rôle de GDMSQL.

GDMSQL : Une implémentation SQL avec fonctions spatiales.
--------------------------------------------------------------------------------

Le SQL est le langage de référence pour la manipulation des données dans 
OrbisGIS.

Avantages : 

- Langage connu des géomaticiens.
- Langage "proche" du langage naturel.

Inconvénients :

- Pas procédural
- Pas de variables

Concrètement...
--------------------------------------------------------------------------------

C'est (presque) ce que vous avez utilisé en TP. Il s'agit de la nouvelle version
du langage de manipulation des données inclus dans OrbisGIS.

[Insérer schéma magnifique]

Séparation de la gestion et de la manipulation-> possibilité de changer le 
langage de manipulation sans altérer la gestion des données.









Introduction à la programmation spatiale sous OrbisGIS
********************************************************************************

OrbisGIS - Principes de fonctionnement
================================================================================

OrbisGIS est un logiciel SIG composé de plusieurs couches :

 * La couche de gestion des données
 * Le langage de manipulation des données
 * La gestion des couches géographiques
 * L'interface graphique

Les briques sont définies aussi indépendamment que possible, afin de simplifier
la maintenance du logiciel dans son ensemble

La couche de gestion des données : Generic Datasource Management System
================================================================================

Une gestion unifiée des sources de données (1)
--------------------------------------------------------------------------------

GDMS : couche de gestion des données dans OrbisGIS.

Objectif : Assurer la transparence des opérations de manipulation des données,
qu'elles soient géospatiales ou juste alpha-numériques.

Pour GDMS, tout est DataSource

Une gestion unifiée des sources de données (2)
--------------------------------------------------------------------------------

Utilisation de la notion de pilotes et d'importeurs (en construction) :

[insérer un schéma magnifique ici]

Concrétement, ça marche ?
--------------------------------------------------------------------------------

Plusieurs formats de données sont gérés par les pilotes :

 * Des formats de fichiers : SHP, GDMS, MIF/MID, DXF...
 * Les bases de données spatiales PostGIS

Des importeurs commencent à faire leur apparition (GPX)




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

 * Simple table clé-valeur (valeur cherchée, position dans le fichier) et 
   recherche par dichotomie : nombreuses opération d'entrée-sortie, coût élevé.
 * Recherche dans un arbre équilibré (BTree) : Recherche dans une seule 
   direction dans l'index.

 Les indexes spatiaux (1)
--------------------------------------------------------------------------------

Pour les données spatiales, on n'a pas de relation d'ordre simple. Mais on a 
tout de même besoin de trouver les données rapidement...

Stratégie : partitonnement de l'espace. On analyse la configuration spatiale des
données, et on construit un arbre reflétant l'organisation spatiale du jeu de 
données...

 Les indexes spatiaux (1)
--------------------------------------------------------------------------------

[Construire un schéma magnifique à insérer ici]








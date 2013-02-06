Création d'une fonction table pour gdmsql
================================================================================

Pour gagner du temps...
--------------------------------------------------------------------------------

Afin de pallier aux déboires rencontrés la semaine dernière, vous allez 
récupérer les sources directement sur 

http://brehat.ec-nantes.fr/S8/S8Li.tar.gz

Cette archive contient les sources du logiciel, tronquée des sources et
ressources de test. Le tout représente un peu moins de 100Mo de données.

Étant donné qu'il s'agit du dernier TP, vous pouvez mettre vos travaux dans
un dossier temporaire (/tmp) pour être sûr d'avoir suffisamment d'espace.

Noter que, quoiqu'il arrive, entre 70 et 100 Mo seront nécessaires à Maven pour
récupérer ses modules et les dépendances d'OrbisGIS, et que cet espace sera pris
sur votre espace personnel. Vous ne pouvez pas (du moins pas simplement)
rediriger cette charge vers /tmp.

Une fois le téléchargement et l'extraction réalisées, vous pouvez l'ouvrir 
directement grâce à NetBeans. Et commencer à coder, enfin...

Pour gagner de l'espace
--------------------------------------------------------------------------------

Étant donné le checkout avorté du dernier TP, de l'espace disque est utilisé
inutilement dans votre espace utilisateur. Comme vous allez récupérer les
archivées, vous pouvez supprimer ces données devenues inutiles.

Par défaut, les codes sources récupérés avec SVN ont été placés dans votre
dossier personnel, dans un dossier qui s'appelle NetBeansProjects. Faites le
ménage dans ce dossier, et votre espace personnel respirera de nouveau...

Installation des sources d'OrbisGIS
--------------------------------------------------------------------------------

L'installation des sourcse du logiciel va se faire en deux parties :

- Nous allons utiliser l'environnement de développement intégré NetBeans. Pour
  le lancer, vous pouvez ouvrir une console et utiliser la commande (à 
  adapter) :

::

  /opt/netbeans-x/bin/netbeans

- La procédure d'installation des sources avec NetBeans peut être trouvée à
  l'adresse http://trac.orbisgis.org/t/wiki/devs/OrbisGIS_src_netbeans . Une
  fois au bout des instructions, vous serez en mesure de commencer à coder...

Objectif du TP
--------------------------------------------------------------------------------

Vous allez ajouter une fonction table à la grammaire de gdmsql. Vous pourrez 
vous appuyer sur le cours précédent (disponible sur le serveur pédagogique), 
ainsi que sur toutes les ressources disponibles sur Internet.

Définition de la fonction
--------------------------------------------------------------------------------

Nom de la fonction
********************************************************************************

La fonction s'appellera ST_BufferedMean.

Entrée de la fonction
********************************************************************************

- Une table contenant deux colonnes, dont l'une contient des objets de type 
  Point, et l'autre des valeurs numériques.
- Une valeur de type Double
- Le nom de la colonne numérique
- Un booléen optionnel

Sortie de la fonction
********************************************************************************

Une table contenant une colonne de type Point et deux colonnes de type
numérique.

Traitement
********************************************************************************

Pour chacun des points donnés en entrée, vous devrez :

- Trouver tous les autres points de la table dont la distance au point courant
  est inférieure au double passé en paramètre de la fonction
- Calculer la valeur moyenne du champ numérique associé à chacun de ces points
- Ajouter une ligne à la DataSource de sortie contenant le point, la valeur
  associée au point et la moyenne calculée précédemment

Le booléen passé en paramètre permettra de décider si la valeur numérique
associée au point courant doit être incluse dans le calcul de la moyenne.

Contraintes
--------------------------------------------------------------------------------

- La fonction sera placée dans un package dédié.
- La fonction devra s'exécuter avec succès en moins de cinq minutes sur les
  données de test.

Ressources
--------------------------------------------------------------------------------

Quelques javadoc intéressantes :

- Java http://docs.oracle.com/javase/6/docs/api/
- JTS http://tsusiatsoftware.net/jts/javadoc/index.html
- OrbisGIS (par module) : http://javadoc.orbisgis.org/

Ces documentations devraient répondre à la plupart des questions soulevées par
le sujet. Elles viennent en complément du cours précédent ce TP.

Pour la gestion des index :

- http://trac.orbisgis.org/t/wiki/devs/GDMS2/gdms_index

Données
--------------------------------------------------------------------------------

Les données de test peuvent être récupérées à l'adresse :

http://brehat.ec-nantes.fr/S8/

Le fichier est nommé receivers_dBA.gdms. Il contient toutes les informations
nécessaires à l'exécution de la fonction désirée...












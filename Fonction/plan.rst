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
versions. La solution utilisée par l'équipe de développement d'OrbisGIS 
s'appelle Subversion (SVN).

http://subversion.tigris.org

Les apports de SVN - la notion de commit
================================================================================



Les apports de SVN - le suivi des modifications
================================================================================



Les apports de SVN - le suivi des modifications
================================================================================

On 


Les apports de SVN - la notion d'historique
================================================================================


Les apports de SVN - le suivi des modifications
================================================================================


SVN - quelques commandes de base
================================================================================

SVN - conclusion
================================================================================

Maven - une gestion simplifiée du processus de build
================================================================================

Maven - le paradigme convention over Configuration
================================================================================

Maven - la notion de dépendance
================================================================================

Maven - La gestion des goals
================================================================================

Maven - conclusion
================================================================================

Et d'autres outils encore...
================================================================================

nous n'avons évoqué que deux des outils indispensables à la vie du projet de 
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

Les types de données alphanumériques
================================================================================

Les types de données géométriques
================================================================================

Comment tester les types géométriques ?
================================================================================

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

























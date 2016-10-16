.. _module_swrod:

##############
Module 'swrod'
##############

Le module 'swrod' (Single Window Read Only Documents) permet de d'afficher une liste de documents en lecture seule (à télécharger) provenant d'une source externe (GED, FTP, WS, ...) représentant les pièces déposées sur un dossier ADS au Guichet Unique de la collectivité.

Voir les apports de la fonctionnalité dans l'interface utilisateur :

- :ref:`Onglet "Documents Entrants" sur le dossier de coordination<dossiers_dc_onglet_documents_entrants_swrod>`
- :ref:`Onglet "Documents Entrants" sur le dossier d'instruction<dossiers_di_onglet_documents_entrants_swrod>`


Il est composé d'un abstracteur et d'un ensemble de connecteurs (aussi appelés plugins). Ces derniers respectent l'API de l'abstracteur.


Configuration d'un connecteur
#############################

La configuration du connecteur est définie dans `dyn/swrod.inc.php`.


Exemple :

.. code:: php

    $swrod = array(
        "type" => "swrodaria_example",
        "path" => "../plugins/swrod/swrodaria_example/swrodaria_example.class.php",
    );


Liste des paramètres obligatoires :

- **type** défini le type de connecteur 
- **path** défini le chemin du connecteur 


Dans cet exemple, le script swrodaria_example.class.php sera inclus et la classe swrodaria_example sera instanciée. Il n'exite aucun connecteur de base dans openARIA puisque dépendant de l'environnement.

Cette configuration n'est pas multi base de données. La configuration de ce module sera donc commune aux différentes configurations de base de données présentes dans le script `dyn/database.inc.php`.


Activation de l'option
######################

Pour que l'option soit activée, il est nécessaire de se rendre dans le menu 'Administration & Paramétrage > Paramètres' et d'ajouter/de modifier le paramètre **swrod** pour lui affecter la valeur 'true'.


Description de l'abstracteur et spécifications du connecteur
############################################################

Le script obj/swrod.class.php permet de définir les classes de base permettant de définir le fonctionnement du module.


Liste des classes définies dans le script :

* swrod
* swrod_base


*****
swrod
*****

La classe 'swrod' est une classe d'abstraction, spécifique à openARIA, permettant de gérer les interfaces avec des systèmes de stockage externes et ainsi proposer aux utilisateurs un accès aux documents du guichet unique. Cette classe est instanciée et utilisée par d'autres scripts pour gérer notamment la visualisation de ces documents dans l'onglet 'Documents entrants' du DC et du DI. Son objectif est d'instancier les classes spécifiques aux SIG aussi appelées
connecteurs correspondant au paramétrage de la collectivité.


**********
swrod_base
**********

Classe parente de tous les connecteurs SWROD.

    .. important:: Les classes des connecteurs SWROD doivent étendre de swrod_base.


* `$conf`_
* `get_list()`_
* `get_file()`_


$conf
*****

::

    $conf : null


*Paramètres du connecteur SWROD présent dans `dyn/swrod.inc.php`.*





get_list()
**********


::

    get_list(  $dossier) 


openARIA fournit la valeur positionnée dans le champ DA ADS ou DI ADS du dossier de coordination afin d'obtenir la liste des documents correspondant dans le stockage externe.


Parameters
``````````
(string) $dossier : Identifiant du dossier à rechercher.
Ex. : PC1305515J0045P0.

Returns
```````
(array) Tableau de résultats (un sous-tableau par document) qui contient les clés suivants :

- date_creation
- categorie
- nom_fichier
- type_document
- uid
- dossier

.. code:: php

    //
    return array(
        array(
            "date_creation" => "2016-12-01",
            "categorie" => "Arrêté",
            "nom_fichier" => "20161201ARR-01.pdf",
            "type_document" => "arrêté de conformité",
            "uid" => "12345",
            "dossier" => "AT0130551200001P0",
        ),
        array(
            "date_creation" => "2016-12-01",
            "categorie" => "Arrêté",
            "nom_fichier" => "20161201ARR-02.pdf",
            "type_document" => "arrêté de conformité",
            "uid" => "23465",
            "dossier" => "AT0130551200001P0",
        ),
        array(
            "date_creation" => "2013-12-01",
            "categorie" => "Arrêté",
            "nom_fichier" => "20131201ARR.pdf",
            "type_document" => "arrêté de conformité",
            "uid" => "46546",
            "dossier" => "AT0130551200001P0",
        ),
    );      

Si aucun résultat :

.. code:: php

    //
    return array();


En cas d'erreur :

.. code:: php

    //
    return false;


get_file()
**********


::

    get_file(  $id) 


openADS fournit une liste de parcelles et le numéro de dossier
correspondant. Le SIG renvoie un statut, spécifiant si le calcul été
effectué correctement ou non.



Parameters
``````````

(string) $id : Identifiant du document à télécharger dans le stockage externe.


Returns
```````
(array) Tableau contenant le fichier à télécharger.

.. code:: php

    //
    return array(
        'file_content' => "%PDF...%EOF",
        'metadata' => array(
            "filename" => "truc.pdf",
            "mimetype" => "application/pdf",
        ),
    );    


En cas d'erreur :

.. code:: php

    //
    return false;


.. _numerisation_automatique:

########################
Numérisation automatique
########################

L'emplacement des documents à numériser doit être spécifié dans le fichier *dyn/config.inc.php* via le paramètre *digitalization_folder* :

.. code-block:: php

    $config['digitalization_folder_path'] = '../var/digitalization/';


Ce répertoire devra obligatoirement contenir deux sous-répertoires *ACC* et *SI*.
Ces derniers devront également contenir les sous-répertoires *Todo* et *Done*.
Ils permettent respectivement de stocker/consulter les documents à traiter/traités.
L'opérateur qui numérise les documents devra donc déposer les documents dans le répertoire *SI/Todo* ou *ACC/Todo*.

.. note::

    La consultation n'est qu'informative étant donné que les documents traités sont créés dans le filestorage.
    Les fichiers traités sont déplacés dans le répertoire *Done* à des fins de vérfication du traitement de la reprise.
    Afin de limiter l'utilisation de l'espace disque ils peuvent être supprimés par un service automatique (cf. :ref:`Purge des documents numérisés<web_services_ressource_maintenance>`).

Exemple d'arborescence :

.. code-block:: bash

    var
    └── digitalization
        ├── ACC
        │   ├── Done
        │   └── Todo
        └── SI
            ├── Done
            │   └── 20160101AUTPCP.pdf
            └── Todo
                ├── T2ARRETE26-10-2016.pdf
                └── 20160206DGPA01.pdf

Un service automatique (*CRON*) se chargera de traiter ces documents afin les enregistrer dans le système de stockage prédéfini.

En fonction de sa nomenclature, le fichier pourra être rattaché à un établissement et un type de pièce.
Lors du processus de chargement automatique des fichiers, si le nom du fichier respecte la convention
de nommage alors les informations qui y sont contenues sont extraites et analysées.
Si l'une d'entre-elles est invalide alors la reprise de ce fichier est un échec.
Si le nom du fichier ne correspond pas à la nomenclature alors il est placé dans la bannette, destiné à être classifié manuellement par la suite.

La charte de nommage des fichiers est *TxxxxxType-de-doc-openARIAJJ-MM-AAAA.ext* :

- *Txxxxx* : caractère T suivi du numéro d'établissement sur 5 chiffres
- *Type-de-doc-openARIA* : le type de document correspond au champ 'Code' des types de fichiers depuis l'interface d'administration d'openARIA, ce type est passé en métadonnée lors du stockage du fichier.
- *JJ-MM-AAAA* : date au format jour-mois-année
- *.ext* : extension de fichier, **obligatoirement** *.pdf*

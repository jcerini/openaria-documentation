.. _document_numerise:

###########################################
Documents numérisés ou reprise de l'arriéré
###########################################

L'emplacement des documents peut être spécifié dans le fichier **dyn/config.inc.php** avec le paramètre **digitalization_folder**. Ce répertoire devra obligatoirement contenir deux sous-répertoires **ACC** et **SI**, ceux-ci devront aussi contenir les sous-répertoires **Todo** et **Done**, le premier permettant de stocker les documents à traiter et le second qui permet de consulter les documents traités.

.. code-block:: php

    $config['digitalization_folder_path'] = '../var/digitalization/';

L'opérateur qui numérise les documents devra donc déposer les documents dans le répertoire **Todo**.

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

Un service automatique (CRON) se chargera de traiter ces documents afin les enregistrer dans le système de stockage prédéfini.

En fonction de sa nomenclature le fichier pourra être lié à un établissement et un type de pièce.
Lors du processus de chargement automatique des fichiers, lorsque le nom de fichiers correspond à la convention
de nommage, les informations contenues dans le nom de fichier seront extraites et analysées afin d'éviter une
saisie supplémentaire par les utilisateurs.
Si le nom des fichiers ne correspond pas à cette nomenclature, ils seront placé dans la bannette et pour être classifié par la suite.

La charte de nommage des fichiers sera : TxxxxxType-de-doc-openARIAJJ-MM-AAAA.EXT :

- Txxxxx : caractère T suivi du numéro d'établissement sur 5 chiffres
- Type-de-doc-openARIA : le type de document correspond au champ 'Code' des types de fichiers depuis l'interface d'administration d'openARIA, ce type est passé en métadonnée lors du stockage du fichier.
- JJ-MM-AAAA : date au format jour-mois-année
- .EXT : extension de fichier '.pdf'


Les répertoires des documents traités sont ensuite déplacés dans le répertoire **Done** pour être supprimés par un autre service automatique.

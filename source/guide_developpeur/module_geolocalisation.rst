.. _module_geolocalisation:

######################
Module géolocalisation
######################

Le module de géolocalisation permet d'avoir des intéractions entre openARIA et un Système d'Information Géographique extérieur à l'application.

Ce module ajoute les fonctionnalités suivantes dans l'interface utilisateur :

- La possibilité de géolocaliser un établissement ou dossier de coordination sur le SIG
- Plusieurs liens de redirection vers l'élément sur le SIG, avec la carte centrée sur l'élément lorsqu'il est géolocalisé. Voir les listings
- Onglet "Contraintes" sur le dossier de coordination
- Onglet "Contraintes" sur l'établissement


Le module SIG est composé d'un abstracteur et d'un ensemble de connecteurs (aussi appelés plugins). Ces derniers respectent l'API de l'abstracteur.


Configuration d'un connecteur
#############################

La configuration du connecteur est définie dans `dyn/sig.inc.php`.


Exemple :

.. code:: php

    $conf["sig-default"] = array (
        "1" => array( // Identifiant de la collectivité
            'connector' => 'example',
            'path' => '../plugins/sig/geoaria_example/',
        ),
    );


Liste des paramètres obligatoires :

- **option_sig** doit être positionnée à la valeur "sig_externe"
- **connector** défini le type de connecteur (Dans cet exemple, le connecteur geoaria_generic.class.php contenu dans le dossier "obj" sera instancié.)
- **path** défini le chemin du connecteur
- **sig_treatment_mod** permet de définir le mode de synchronisation des contraintes :
    - "mono" : permet d'affecter les contraintes d'un SIG à chaque collectivité de l'application via le code insee fourni lors de l'appel au web service. Chaque commune n'accés qu'aux contraintes afféctées lors de la synchronisation.
    - "multi" : permet d'affecter toutes les contraintes du SIG à la collectivité correspondant à la communauté de commune. Ces contraintes seront disponible pour toutes les communes de la communauté.


Dans openARIA, le paramètre du menu Administration **option_sig** doit être positionné à la valeur "sig_externe".

Dans cet exemple, le script geoaria_example.class.php sera inclus et la classe geoaria_example sera instanciée. Il n'existe aucun connecteur de base dans openARIA puisque dépendant de l'environnement.

Il est possible d'avoir un paramétrage SIG par configuration de base de données. Pour cela, il faut ajouter dans le fichier de configuration `dyn/database.inc.php`, après les autres paramètres, un tableau nommé 'extras' :

.. code:: php

    "extras" => array (
        'sig' => 'sig-default', // Paramétrage de la configuration SIG à utiliser
    )




Description de l'abstracteur et spécifications du connecteur
############################################################

Le script obj/geoaria.class.php contient les classes de base qui définissent le fonctionnement du module.

Liste des classes définies dans le script :

* geoaria
* geoaria_base
* geoaria_exception
* geoaria_om_parameter_exception
* geoaria_argument_exception
* geoaria_bdd_exception
* geoaria_configuration_exception
* geoaria_connector_4XX_exception
* geoaria_connector_5XX_exception
* geoaria_connector_exception
* geoaria_connector_method_not_implemented_exception


*******
geoaria
*******

La classe 'geoaria' est une classe d'abstraction, spécifique à openARIA, permettant de gérer les interfaces avec des SIG externes et ainsi proposer aux utilisateurs de géolocaliser un élément sur le SIG, d'accéder directement au SIG avec la carte centrée sur l'élément, ou encore de récupérer en un clic les contraintes d'un élément. Cette classe est instanciée et utilisée par toutes les classes métier qui ont un besoin de géolocalisation, comme les dossiers, les établissements ou les contraintes. L'objectif de l'abstracteur est d'instancier les classes spécifiques aux SIG aussi appelées connecteurs correspondant au paramétrage de la collectivité.
Ces connecteurs héritent de la classe 'geoaria_base' qui leur sert de modèle.
Enfin la classe 'geoaria_exception' permet de gérer les erreurs.
Plusieurs classes en héritent afin de spécifier le type d'exception.

************
geoaria_base
************

Classe parente de tous les connecteurs geoaria.

    .. important:: Les classes des connecteurs geoaria doivent étendre de geoaria_base.



****************
geoaria_exception
****************

Classe gérant les erreurs (une exception est levée pour chacune).

******************************
geoaria_om_parameter_exception
******************************

Classe d'exceptions utilisée lors de la vérification des paramètres de l'application
utilisés par les méthodes de l'abstracteur.

**************************
geoaria_argument_exception
**************************

Classe d'exceptions utilisée lors de la vérification des arguments passés aux
méthodes de l'abstracteur.

********************
geoaria_bdd_exception
********************

Classe d'exceptions utilisée lors d'une erreur de base de données.

******************************
geoaria_configuration_exception
******************************

Classe d'exceptions utilisée lors d'une erreur dans le paramétrage du connecteur.


******************************
geoaria_connector_4XX_exception
******************************

Classe de gestion des exceptions retournée lors d'un code http 4XX.

    .. important:: Cette exception correspond à un problème inhérent à openARIA.


******************************
geoaria_connector_5XX_exception
******************************

Classe de gestion des exceptions retournée lors d'un code http 5XX.

    .. important:: Cette exception correspond à un problème inhérent au SIG.


**************************
geoaria_connector_exception
**************************

Classe de gestion des exceptions génériques remontées par le connecteur.


*************************************************
geoaria_connector_method_not_implemented_exception
*************************************************

Classe de gestion des exceptions sur les methodes du connecteur qui ne sont pas
implémentées.

Description de l'abstracteur
############################


*********
Attributs
*********

* `$sig`_ : Cet attribut permet de stocker l'instance du connecteur SIG utilisé.
* `$collectivite`_ : Paramètres de la collectivité fournie à l'abstracteur.

$sig
****

::

    $sig : null


*Cet attribut permet de stocker l'instance du connecteur SIG utilisé.*


$collectivite
*************

::

    $collectivite : array


*Paramètres de la collectivité fournie à l'abstracteur.*

*********************
Méthodes implémentées
*********************

* `__construct()`_
* `geocoder_objet()`_
* `synchro_contraintes()`_
* `recup_contraintes()`_
* `redirection_web()`_
* `redirection_web_emprise()`_
* `lister_etablissements_proches()`_
* `lister_proprietaires_parcelles()`_


__construct()
*************


::

    __construct(array $collectivite)


*Le constructeur instancie le connecteur SIG selon la configuration*


Parameters
``````````
- (array) $collectivite : Configuration du connecteur.


geocoder_objet()
****************


::

    geocoder_objet(string $obj, string $idx, array $params)


openARIA fournit le type d'objet, ainsi que toutes les informations utiles qui ont été renseignées qui peuvent permettre de géolocaliser l'établissement ou le dossier de coordination.


Parameters
``````````
- (string) $obj : Le type d'élément openARIA, "etablissement" ou "dossier".
- (string) $idx : Identifiant de l'objet.
- (array) $params Un tableau contenant un ou plusieurs des éléments suivants :


.. code:: php

    array (
        'parcelles' => array (
            array(
                'quartier' => string,
                'section' => string,
                'parcelle' => string
            ),
            array(
                'quartier' => string,
                'section' => string,
                'parcelle' => string,
            ),
        )
        'adresse' => string,
        'voie' => string,
        'dossier_ads' => string,
    ).


Returns
```````
(string) La précision de la géolocalisation en mètres.


En cas d'erreur :

.. code:: php

    //
    return false;


synchro_contraintes()
*********************


::

    synchro_contraintes(string $insee = null)


openARIA fournit au SIG externe le code INSEE d'une commune. Le SIG renvoie l'ensemble des contraintes applicables à cette commune. Ces contraintes sont ensuite enregistrées dans la base de données d'openARIA, afin d'être réutilisées lors de la récupération des contraintes applicables à un dossier de coordination ou un établissement.


Parameters
``````````

(string) $insee : Code INSEE de la commune.


Returns
```````
(array) Tableau de contraintes

.. code:: php

    //
    return array(
        array(
            array(
             "contrainte" => "22",
               "groupe_contrainte" => "Servitudes",
               "sous_groupe_contrainte" => "",
               "libelle" => "Exemple de servitude",
           ),
            array(
                "contrainte" => "27",
                "groupe_contrainte" => "ZONES DU PLU",
                "sous_groupe_contrainte" => "protection",
                "libelle" => "Une contrainte du PLU",
           ),
        ),
    );


S'il n'y a aucune parcelle :

.. code:: php

    //
    return array();


recup_contraintes()
*******************


::

    recup_contraintes(array $parcelle)


openARIA appelle le web service contrainte en lui fournissant la liste des parcelles dont on souhaite récupérer les contraintes. Le SIG renvoie une collection de contraintes qui s'y appliquent.


Parameters
``````````

(array) $parcelles : Un tableau contenant une ou plusieurs parcelles.


Returns
```````
(array) Tableau de contraintes

.. code:: php

    //
    return array(
            array(
                "contrainte" => "27",
                "groupe_contrainte" => "ZONES DU PLU",
                "sous_groupe_contrainte" => "protection",
                "libelle" => "Une contrainte du PLU",
           ),
        ),
    );


S'il n'y a aucune parcelle :

.. code:: php

    //
    return array();


redirection_web()
*****************

::

    redirection_web(string $obj = null, array $data = null) 

openARIA fournit le type d'objet et le ou les identifiant(s) de l'élement que l'utilisateur
souhaite consulter sur le SIG. Le connecteur renvoie un URL, qui permettra à l'utilisateur
d'accéder au SIG avec la vue centrée sur l'élément choisi.


Parameters
``````````

(string) $obj Le type d'objet à visualiser : parcelle/etablissement/dossier_coordination.
(array) $data Tableau contenant un ou plusieurs identifiants de l'objet, ex: une ou plusieurs parcelles, un ou plusieurs numéros d'établissements, un ou plusieurs numéros de dossiers de coordination. 

Format du tableau $data pour un objet établissement :

.. code:: php

    array(
        0 => 'T5',
        1 => 'T10',
        2 => 'T1111',
    )

Format du tableau $data pour un objet dossier_coordination :

.. code:: php

    array(
        0 => array(
            'id' => 'VPS-VISIT-000010',
            'type' => 'VPS',
            )
        1 => array(
            'id' => 'PC-PLAN-000001',
            'type' => 'PC',
            )
        )

Format du tableau $data pour un objet parcelle :

.. code:: php

    array (
        0 => array (
            'prefixe' => '201',
            'quartier' => '806',
            'section' => 'AB',
            'parcelle' => '0025',
            ),
        1 => array(
            'prefixe' => '208',
            'quartier' => 806,
            'section' => ' A',
            'parcelle' => '0050',
            ),
        )

Returns
```````
(String) L'URL du SIG centré sur le ou les éléments si l'objet a été précisé, sinon l'URL vers la vue par défaut du SIG.


redirection_web_emprise()
*************************

::

    redirection_web_emprise(string $obj, array $data) 

openARIA fournit le type d'objet et l'identifiant(s) de l'élement que l'utilisateur
souhaite dessiner manuellement sur le SIG. Le connecteur renvoie un URL, qui permettra à
l'utilisateur d'accéder au SIG en mode création d'établissement ou dossier de coordination.


Parameters
``````````

(string) $obj Le type d'objet à visualiser : parcelle/etablissement/dossier_coordination.
(array) $data L'identifiant de l'objet, son code ou numéro et l'identifiant de la voie.

Returns
```````
(String) L'url du SIG pour la création manuelle.


lister_etablissements_proches()
*******************************

::

    lister_etablissements_proches(array $params)

Récupération d'une liste d'établissements proches de l'objet passé en paramètre.


Parameters
``````````

- (array) $params Un tableau associatif contenant un ou plusieurs des paramètres suivant :

.. code:: php

    array(
        "idcentre" => array (
            "id" => string,
            "type" => string (etablissement/dossier_ads)
        )
        "listeparcelles" => array
        "limite" => string
        "distance" => string
    )

Returns
```````
(array) Tableau d'établissement(s), avec la distance en mètres de l'établissement par rapport à l'objet qui a été passé en paramètre.


lister_proprietaires_parcelles()
********************************


::

    lister_proprietaires_parcelles(array $parcelles)

Récupération des informations nominatives des propriétaires des parcelles passées en paramètres.
openARIA appelle le SIG en lui fournissant une ou plusieurs parcelles dont on souhaite obtenir les détails sur leur(s) propriétaire(s). Le résultat est un ensemble de propriétaires confondus (non identifiés par leur parcelle).


Parameters
``````````

- (array) $parcelles Tableau de parcelles.

Returns
```````
(array) Un tableau contenant les informations d'un ou plusieurs propriétaires d'une ou plusieurs parcelles. Le retour est par exemple :

.. code:: php

    array(
        "ident1" => "DUPONT",
        "ident2" => "CLAUDE",
        "adr1" => "4EME ETAGE DROITE",
        "adr2" => "42 AV ROGER SALENGRO",
        "adr3" => "QUARTIER EUROMED",
        "cp_ville_pays" => "13003 MARSEILLE",
        "code_pays" => ""
        )

Si la récupération a échoué, on retourne false

Redirection vers openARIA
#########################

OpenARIA permet la redirection depuis une application externe vers la fiche ou une sélection d'objet.
Pour cela il est nécessaire de passer par le script d'entrée à l'application *app/entry.php*.

*****************************
Accéder à la fiche d'un objet
*****************************

L'url doit être composée des pramètres suivant :

* **obj** objet de l'élément que l'on souhaite visualiser (*etablissement* ou *dc*) ;
* **action** type de redirection (*view* pour accéder à une fiche) ;
* **by** champ de l'objet sur lequel chercher les valeurs (*code* pour les établissements et *libelle* pour les dossiers de coordination) ;
* **id** valeur à chercher ;

Exemples d'url à composer :

* <lien_openaria>/app/entry.php?obj=etablissement&action=view&by=code&id=T3468
* <lien_openaria>/app/entry.php?obj=dc&action=view&by=libelle&id=VPS-VISIT-005018

**********************************
Accéder au listing d'une sélection
**********************************

L'url doit être composée des pramètres suivant :

* **obj** objet de l'élément que l'on souhaite visualiser (*etablissement* ou *dc*) ;
* **action** type de redirection (*list* pour accéder à une sélection d'objet) ;
* **by** champ de l'objet sur lequel chercher les valeurs (*code* pour les établissements et *libelle* pour les dossiers de coordination) ;
* **ids** valeurs à chercher séparées par des *,* ;

Exemples d'url à composer :

* <lien_openaria>/app/entry.php?obj=etablissement&action=list&by=code&ids=T3468,T3789,T4985
* <lien_openaria>/app/entry.php?obj=dc&action=list&by=libelle&id=VPS-VISIT-005018,AT-PLAN-009022,VPS-VISIT-005019

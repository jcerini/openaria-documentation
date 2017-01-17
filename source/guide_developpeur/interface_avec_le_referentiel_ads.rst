.. _module_interface_avec_le_referentiel_ads:

#################################
Interface avec le référentiel ADS
#################################


Interface avec le logiciel openADS : http://www.openmairie.org/catalogue/openads


Configuration du module
#######################

.. _configuration_echanges_sortants_referentiel_ads:

*Configuration des URLs des échanges sortants vers le référentiel ADS* :

dyn/services.inc.php ::

  $ADS_URL_MESSAGES = 'http://openads/services/rest_entry.php/messages/';
  $ADS_URL_DOSSIER_AUTORISATIONS = 'http://openads/services/rest_entry.php/dossier_autorisations/';
  $ADS_URL_DOSSIER_INSTRUCTIONS = 'http://openads/services/rest_entry.php/dossier_instructions/';
  $ADS_URL_CONSULTATIONS = 'http://openads/services/rest_entry.php/consultations/';
  $ADS_URL_VISUALISATION_DA = 'http://openads/app/web_entry.php?obj=dossier_autorisation&value=<ID_DA>';


*Configuration des paramètres des déclencheurs* :

- **ads__liste_services__si** : correspond à la liste des codes représentant le service ERP Sécurité Incendie tel qu'ils sont définis dans la colonne 'abrégé' du paramétrage des services d'openADS par exemple "Service Pr;ERPSI"
- **ads__liste_services__acc** : correspond à la liste des codes représentant le service ERP Accessibilité tel qu'ils sont définis dans la colonne 'abrégé' du paramétrage des services d'openADS par exemple "Division d;ERPACC"


Activation de l'option
######################

*Activation de l'option dans l'interface* :

om_parametre

- **option_referentiel_ads** -> true


Les échanges
############


.. _echange_ads_erp_101:

====================================================================
[101](Échange ADS → ERP) Dossier AT Information de qualification ADS
====================================================================

L'objectif principal de cet échange est de permettre à l'instructeur ADS de transmettre facilement les informations d'autorité compétente et de contraintes PLU (de compétence URBA) du dossier AT aux services ERP.


*Identifiant* : ADS_ERP__AT__INFORMATION_DE_QUALIFICATION_ADS


*Cas d'utilisation* :

• Suite à la qualification des informations d'autorité compétente et de contraintes PLU par l'instructeur ADS sur le dossier dans openADS, l'information est transmise à titre d'information sur le dossier dans openARIA.


*Déclencheur* :

• :ref:`Web Service exposé<web_services_ressource_messages_post>`


*Traitement* :

• Création de message : Un message de catégorie "entrant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 1.


*Contenu de l'échange* :

- **type** : Type de message
- **date** :  Date/heure d'envoi du message
- **emetteur** : Émetteur du message (Nom/Prénom/Login de l'utilisateur à l'origine du message)
- **dossier_instruction** : Identifiant du dossier d'instruction
- **contenu** :

  - **competence** : Compétence : texte : Qualification compétence : Mairie/Etat
  - **contraintes_plu** : Contraintes PLU : texte multilignes reprenant les contraintes PLU du dossier
  - **references_cadastrales** : 


*Exemple* :

.. sourcecode:: http
      
    POST /openaria/services/rest_entry.php/messages HTTP/1.1
    Host: localhost

    {
        "type" : "ADS_ERP__AT__INFORMATION_DE_QUALIFICATION_ADS",
        "date" : "31/12/2015 14:42",
        "emetteur" : "instr",
        "dossier_instruction" : "PC0130551600001P0",
        "contenu" : {
            "competence" : "",
            "contraintes_plu" : "",
            "references_cadastrales" : ""
        }
    }


.. _echange_ads_erp_102:

=====================================================================
[102](Échange ADS → ERP) Dossier PC/ERP Pré-demande de complétude ERP
=====================================================================

L'objectif principal de cet échange est de permettre à l'instructeur ADS de gagner du temps dans sa vérification de complétude et d'interroger rapidement les services ERP sur la complétude du dossier.


*Identifiant* : ADS_ERP__PC__PRE_DEMANDE_DE_COMPLETUDE_ERP


*Cas d'utilisation* :

• Un dossier PC qui concerne un ERP est identifié dans openADS, l'instructeur ADS souhaite obtenir avant la consultation officielle du service une pré-complétude par les services ERP. Une notification permet donc la création d'un dossier PLAN à qualifier dans openARIA.


*Déclencheur* :

• :ref:`Web Service exposé<web_services_ressource_messages_post>`


*Traitement* :

• Création de DC (PC-PLAN) possible : Si le message [103] n'est pas arrivé avant alors un dossier de coordination de type PC PLAN est créé.
• Récupération des informations sur le DI ADS : Via l'échange [212] récupération de la localisation des travaux (adresse, références cadastrales) et récupération du ou des demandeurs.
• Marquage du dossier DC (PC-PLAN) : Le marqueur « connecté avec le référentiel ADS » sur le dossier créé est positionnée à « OUI » afin de pouvoir identifier ce dossier à l'avenir.
• Création de message : Un message de catégorie "entrant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 0.


*Contenu de l'échange* :

- **type** : Type de message
- **date** :  Date/heure d'envoi du message
- **emetteur** : Émetteur du message (Nom/Prénom/Login de l'utilisateur à l'origine du message)
- **dossier_instruction** : Identifiant du dossier d'instruction


*Exemple* :

.. sourcecode:: http
      
    POST /openaria/services/rest_entry.php/messages HTTP/1.1
    Host: localhost

    {
        "type" : "ADS_ERP__PC__PRE_DEMANDE_DE_COMPLETUDE_ERP",
        "date" : "31/12/2015 14:42",
        "emetteur" : "instr",
        "dossier_instruction" : "PC0130551600001P0"
    }


.. _echange_ads_erp_103:

========================================================================
[103](Échange ADS → ERP) Dossier PC/ERP Pré-demande de qualification ERP
========================================================================

L'objectif principal de cet échange est de permettre à l'instructeur ADS de gagner du temps dans sa qualification de dossier et d'interroger rapidement les services ERP sur le caractère ERP du dossier.


*Identifiant* : ADS_ERP__PC__PRE_DEMANDE_DE_QUALIFICATION_ERP


*Cas d'utilisation* :

• Un dossier PC qui concerne un ERP est identifié dans openADS, l'instructeur ADS souhaite obtenir avant la consultation officielle du service une pré-qualification par les services ERP. Une notification permet donc la création d'un dossier PLAN à qualifier dans openARIA.


*Déclencheur* :

• :ref:`Web Service exposé<web_services_ressource_messages_post>`


*Traitement* :

• Création de DC (PC-PLAN) possible : Si le message [102] n'est pas arrivé avant, alors un dossier de coordination de type PC PLAN est créé.
• Récupération des informations sur le DI ADS : Via l'échange [212] récupération de la localisation des travaux (adresse, références cadastrales) et récupération du ou des demandeurs.
• Marquage du dossier DC (PC-PLAN) : Le marqueur « connecté avec le référentiel ADS » sur le dossier créé est positionnée à « OUI » afin de pouvoir identifier ce dossier à l'avenir.
• Création de message : Un message de catégorie "entrant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 0.

*Contenu de l'échange* :

- **type** : Type de message
- **date** :  Date/heure d'envoi du message
- **emetteur** : Émetteur du message (Nom/Prénom/Login de l'utilisateur à l'origine du message)
- **dossier_instruction** : Identifiant du dossier d'instruction


*Exemple* :

.. sourcecode:: http
      
    POST /openaria/services/rest_entry.php/messages HTTP/1.1
    Host: localhost

    {
        "type" : "ADS_ERP__PC__PRE_DEMANDE_DE_QUALIFICATION_ERP",
        "date" : "31/12/2015 14:42",
        "emetteur" : "instr",
        "dossier_instruction" : "PC0130551600001P0"
    }


.. _echange_ads_erp_104:

=========================================================================
[104](Échange ADS → ERP) Dossier PC/ERP Consultation officielle pour avis
=========================================================================

L'objectif principal de cet échange est de permettre à l'instructeur ADS d'émettre une consultation officielle pour avis des services ERP.


*Identifiant* : ADS_ERP__PC__CONSULTATION_OFFICIELLE_POUR_AVIS


*Cas d'utilisation* :

• Un dossier PC qui concerne un ERP est identifié dans openADS, l'instructeur ADS a lancé la consultation officielle du service. Une notification permet donc la création d'un dossier PLAN à qualifier dans openARIA ou le rattachement à un dossier existant si une pré-qualification a été réalisée.


*Déclencheur* :

• :ref:`Web Service exposé<web_services_ressource_messages_post>`


*Traitement* :

• Création de DC (PC-PLAN) possible : Si le message [102] ou le [103] n'est pas arrivé avant, alors un dossier de coordination de type PC PLAN est créé.
• Récupération des informations sur le DI ADS : Via l'échange [212] récupération de la localisation des travaux (adresse, références cadastrales) et récupération du ou des demandeurs.
• Marquage du dossier DC (PC-PLAN) : Le marqueur « connecté avec le référentiel ADS » sur le dossier créé est positionnée à « OUI » afin de pouvoir identifier ce dossier à l'avenir.
• Création de message : Un message de catégorie "entrant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 0.


*Contenu de l'échange* :

- **type** : Type de message
- **date** :  Date/heure d'envoi du message
- **emetteur** : Émetteur du message (Nom/Prénom/Login de l'utilisateur à l'origine du message)
- **dossier_instruction** : Identifiant du dossier d'instruction
- **contenu** :

  - **consultation** : Identifiant de la consultation
  - **service_abrege** : Code du service consulté
  - **service_libelle** : Libellé du service consulté
  - **date_envoi** : Date d'envoi de la consultation
  - **date_limite** : Date limite de réponse


*Exemple* :

.. sourcecode:: http
      
    POST /openaria/services/rest_entry.php/messages HTTP/1.1
    Host: localhost

    {
        "type" : "ADS_ERP__PC__CONSULTATION_OFFICIELLE_POUR_AVIS",
        "date" : "31/12/2015 14:42",
        "emetteur" : "instr",
        "dossier_instruction" : "PC0130551600001P0",
        "contenu" : {
            "consultation" : 2,
            "date_envoi" : "31/12/2015",
            "service_abrege" : "ACC",
            "service_libelle" : "Service Accessibilité",
            "date_limite" : "31/01/2016",
        }
    }


.. _echange_ads_erp_105:

===================================================================
[105](Échange ADS → ERP) Dossier PC/ERP Information de décision ADS
===================================================================

L'objectif principal de cet échange est de permettre d'informer les services ERP de certaines étapes importantes de la vie du dossier : arrêté effectué, retrait du dossier par le pétitionnaire, ...


*Identifiant* : ADS_ERP__PC__INFORMATION_DE_DECISION_ADS


*Cas d'utilisation* :

• Suite à un échange [102] et/ou [103] et/ou [104] (demande d'instruction d'un dossier PC par ADS), une étape importante survient sur le dossier (retrait par le pétitionnaire, arrêté de refus émis, ...) et les services ADS souhaitent en informer les services ERP. Lors de cette étape, un message d'information est envoyé aux services ERP.


*Déclencheur* :

• :ref:`Web Service exposé<web_services_ressource_messages_post>`


*Traitement* :

• Création de message : Un message de catégorie "entrant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 3.


*Contenu de l'échange* :

- **type** : Type de message
- **date** :  Date/heure d'envoi du message
- **emetteur** : Émetteur du message (Nom/Prénom/Login de l'utilisateur à l'origine du message)
- **dossier_instruction** : Identifiant du dossier d'instruction
- **contenu** :

  - **decision** : Décision : texte libre (Décision de l'arrêté)


*Exemple* :

.. sourcecode:: http
      
    POST /openaria/services/rest_entry.php/messages HTTP/1.1
    Host: localhost

    {
        "type" : "ADS_ERP__PC__INFORMATION_DE_DECISION_ADS",
        "date" : "31/12/2015 14:42",
        "emetteur" : "instr",
        "dossier_instruction" : "PC0130551600001P0",
        "contenu" : {
            "decision" : ""
        }
    }


.. _echange_ads_erp_106:

===============================================================================
[106](Échange ADS → ERP) Dossier PC/ERP Consultation officielle pour conformité
===============================================================================

L'objectif principal de cet échange est de permettre à l'instructeur ADS de gagner du temps dans sa consultation officielle pour conformité des services ERP.


*Identifiant* : ADS_ERP__PC__CONSULTATION_OFFICIELLE_POUR_CONFORMITE


*Cas d'utilisation* :

• Lorsqu'ADS interroge les services ERP sur la conformité (lors du dépôt d'une DAACT).


*Déclencheur* :

• :ref:`Web Service exposé<web_services_ressource_messages_post>`


*Traitement* :

• Création de message : Un message de catégorie "entrant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 0.
• Création d'un DC DAACT-PLAN : Il sera automatiquement qualifié en fonction de la qualification du plan (DC PC-PLAN) auquel il est rattaché.


*Contenu de l'échange* :

- **type** : Type de message "Consultation ERP pour conformité"
- **date** :  Date/heure d'envoi du message
- **emetteur** : Émetteur du message (Nom/Prénom/Login de l'utilisateur à l'origine du message)
- **dossier_instruction** : Identifiant du dossier d'instruction
- **contenu** :

  - **consultation** : Identifiant de la consultation
  - **service_abrege** : Code du service consulté
  - **service_libelle** : Libellé du service consulté
  - **date_envoi** : Date d'envoi de la consultation
  - **date_limite** : Date limite de réponse


*Exemple* :

.. sourcecode:: http
      
    POST /openaria/services/rest_entry.php/messages HTTP/1.1
    Host: localhost

    {
        "type" : "ADS_ERP__PC__CONSULTATION_OFFICIELLE_POUR_CONFORMITE",
        "date" : "31/12/2015 14:42",
        "emetteur" : "instr",
        "dossier_instruction" : "PC0130551600001P0",
        "contenu" : {
            "consultation" : 2,
            "date_envoi" : "31/12/2015",
            "service_abrege" : "SC",
            "service_libelle" : "Service Conformité",
            "date_limite": "31/01/2016"
        }
    }


.. _echange_ads_erp_107:

=====================================================================
[107](Échange ADS → ERP) Dossier PC/ERP Demande de visite d'ouverture
=====================================================================

Dans le contexte du guichet unique, l'objectif principal de cet échange est d'informer les services ERP qu'une demande de visite d'ouverture a été déposée.


*Identifiant* : ADS_ERP__PC__DEMANDE_DE_VISITE_D_OUVERTURE_ERP


*Cas d'utilisation* :

• Dans le cas où les demandes de visite d'ouverture des ERP sont saisies par le guichet unique dans openADS, alors lorsque le pétitionnaire vient déposer une demande de visite d'ouverture sur un PC qui concerne un ERP, une notification est transmise aux services ERP.


*Déclencheur* :

• :ref:`Web Service exposé<web_services_ressource_messages_post>`


*Traitement* :

• Création de message : Un message de catégorie "entrant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 0.
• Création de DC (VR-VISIT) possible
• Marquage du dossier DC (VR-VISIT)


*Contenu de l'échange* :

- **type** : Type de message
- **date** :  Date/heure d'envoi du message
- **emetteur** : Émetteur du message (Nom/Prénom/Login de l'utilisateur à l'origine du message)
- **dossier_instruction** : Identifiant du dossier d'instruction


*Exemple* :

.. sourcecode:: http
      
    POST /openaria/services/rest_entry.php/messages HTTP/1.1
    Host: localhost

    {
        "type" : "ADS_ERP__PC__DEMANDE_DE_VISITE_D_OUVERTURE_ERP",
        "date" : "31/12/2015 14:42",
        "emetteur" : "instr",
        "dossier_instruction" : "PC0130551600001P0"
    }


.. _echange_ads_erp_108:

=================================================
[108](Échange ADS → ERP) Dossier AT Dépôt initial
=================================================

Dans le contexte du guichet unique, l'objectif principal de cet échange est d'informer les services ERP qu'une demande d'autorisation de travaux a été déposée.


*Identifiant* : ADS_ERP__AT__DEPOT_INITIAL


*Cas d'utilisation* :

Un pétitionnaire est venu déposé une demande d'autorisation de travaux au guichet unique et la demande a été saisie dans openADS, un message est donc transmis à openARIA. L'arrivée de ce message entraîne dans openARIA la création d'un dossier de coordination de type AT PLAN dans l'état 'à qualifier' pour que le coordinateur ERP le voit apparaître dans son tableau de bord et puisse le prendre en charge.


*Déclencheur* :

• :ref:`Web Service exposé<web_services_ressource_messages_post>`


*Traitement* :

• Création de message : Un message de catégorie "entrant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 0.

*Traitement asynchrone* :

.. note::

    Un traitement asynchrone est nécessaire ici. En effet, nous sommes dans le contexte du guichet unique. L'échange est transmis par le référentiel ADS au référentiel ERP lors de la validation de la demande au guichet unique. Le dossier n'existe pas encore à ce moment là. Le formulaire de valaidation de la demande attend une confirmation de bonne réception de l'échange par le référentiel ERP afin de valider sa transaction et de créer effectivement le dossier rattaché à la demande. Il est donc impossible pour le référentiel ERP d'interroger le référentiel ADS sur un dossier pour obtenir ses informations alors qu'il n'a pas été encore effectivement créé dans celui-ci à ce moment là. L'objet du traitement asynchrone est donc de limiter le traitement synchrone à la création du message et d'avoir une méthode de traitement qui parcourt les messages non traités pour réaliser sur ces derniers les opérations nécessaires. Voir : :ref:`Web Service Maintenance de déclenchement des traitements de messages asynchrones<web_services_ressource_maintenance>`


• Création de DC (AT-PLAN) : Un dossier de coordination de type AT-PLAN est créé.
• Récupération des informations sur le DI ADS : Via l'échange [212] récupération de la localisation des travaux (adresse, références cadastrales) et récupération du ou des demandeurs.
• Marquage du dossier DC (AT-PLAN) : Le marqueur « connecté avec le référentiel ADS » sur le dossier créé est positionnée à « OUI » afin de pouvoir identifier ce dossier à l'avenir.


*Contenu de l'échange* :

- **type** : Type de message
- **date** :  Date/heure d'envoi du message
- **emetteur** : Émetteur du message (Nom/Prénom/Login de l'utilisateur à l'origine du message)
- **dossier_instruction** : Identifiant du dossier d'instruction


*Exemple* :

.. sourcecode:: http
      
    POST /openaria/services/rest_entry.php/messages HTTP/1.1
    Host: localhost

    {
        "type" : "ADS_ERP__AT__DEPOT_INITIAL",
        "date" : "31/12/2015 14:42",
        "emetteur" : "guichet",
        "dossier_instruction" : "AT0130551600001P0"
    }


.. _echange_ads_erp_109:

============================================================
[109](Échange ADS → ERP) Dossier AT Retrait du pétitionnaire
============================================================

Dans le contexte du guichet unique, l'objectif principal de cet échange est d'informer les services ERP qu'une demande de retrait d'autorisation de travaux a été déposée.


*Identifiant* : ADS_ERP__AT__RETRAIT_DU_PETITIONNAIRE


*Cas d'utilisation* :

• Le pétitionnaire dépose une demande de retrait au guichet unique sur un dossier connecté au référentiel ERP. Lors de la saisie de cette demande dans openADS, une notification est émise vers openARIA pour que les services ERP soient informés et puissent agir en conséquence.


*Déclencheur* :

• :ref:`Web Service exposé<web_services_ressource_messages_post>`


*Traitement* :

• Création de message : Un message de catégorie "entrant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 3.


*Contenu de l'échange* :

- **type** : Type de message
- **date** :  Date/heure d'envoi du message
- **emetteur** : Émetteur du message (Nom/Prénom/Login de l'utilisateur à l'origine du message)
- **dossier_instruction** : Identifiant du dossier d'instruction


*Exemple* :

.. sourcecode:: http
      
    POST /openaria/services/rest_entry.php/messages HTTP/1.1
    Host: localhost

    {
        "type" : "ADS_ERP__AT__RETRAIT_DU_PETITIONNAIRE",
        "date" : "31/12/2015 14:42",
        "emetteur" : "guichet",
        "dossier_instruction" : "AT0130551600001P0"
    }


.. _echange_ads_erp_110:

=================================================================
[110](Échange ADS → ERP) Dossier AT Demande de visite d'ouverture
=================================================================

Dans le contexte du guichet unique, l'objectif principal de cet échange est d'informer les services ERP qu'une demande de visite d'ouverture a été déposée.


*Identifiant* : ADS_ERP__AT__DEMANDE_DE_VISITE_D_OUVERTURE_ERP


*Cas d'utilisation* :

• Suite à une autorisation de travaux acceptée, le pétitionnaire dépose une demande de visite d'ouverture (de réception de travaux) au guichet unique en fournissant la référence de l'autorisation en question.


*Déclencheur* :

• :ref:`Web Service exposé<web_services_ressource_messages_post>`


*Traitement* :

• Création de message : Un message de catégorie "entrant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 0.
• Création de DC (VR-VISIT) possible : Lié (dossier parent) au DC (AT-PLAN) correspondant au dossier AT sur lequel la demande de visite a été déposée. Création automatique d'un DC de visite de réception lié (dossier parent) au DC AT correspondant au dossier AT sur lequel la visite de réception a été déposée. Un seul dossier VISIT peut être connecté au référentiel ADS sur le même dossier AT.
• Marquage du dossier DC (VR-VISIT)


*Contenu de l'échange* :

- **type** : Type de message
- **date** :  Date/heure d'envoi du message
- **emetteur** : Émetteur du message (Nom/Prénom/Login de l'utilisateur à l'origine du message)
- **dossier_instruction** : Identifiant du dossier d'instruction


*Exemple* :

.. sourcecode:: http
      
    POST /openaria/services/rest_entry.php/messages HTTP/1.1
    Host: localhost

    {
        "type" : "ADS_ERP__AT__DEMANDE_DE_VISITE_D_OUVERTURE_ERP",
        "date" : "31/12/2015 14:42",
        "emetteur" : "guichet",
        "dossier_instruction" : "AT0130551600001P0"
    }


.. _echange_ads_erp_111:

==========================================================================
[111](Échange ADS → ERP) Dossier PC/ERP Information de décision Conformité
==========================================================================

L'objectif principal de cet échange est de permettre d'informer les services ERP de certaines étapes importantes de la vie du dossier : arrêté effectué, retrait du dossier par le pétitionnaire, ...


*Identifiant* : ADS_ERP__PC__DECISION_DE_CONFORMITE_EFFECTUEE


L'échange [105] a été rendu plus générique et permet de réaliser l'objectif de cet échange. Celui-ci a donc été supprimé.


.. _echange_ads_erp_112:

=======================================================================
[112](Échange ADS → ERP) Dossier AT Dépôt de pièce par le pétitionnaire
=======================================================================

Dans le contexte du guichet unique, l'objectif principal de cet échange est d'informer les services ERP qu'un dépôt de pièces a été fait.


*Identifiant* : ADS_ERP__AT__DEPOT_DE_PIECE_PAR_LE_PETITIONNAIRE


*Cas d'utilisation* :

• Le pétitionnaire dépose des pièces complémentaires ou supplémentaires au guichet unique sur un dossier connecté au référentiel ERP. Lors de la saisie de cette demande dans openADS, une notification est émise vers openARIA pour que les services ERP soient informés et puissent agir en conséquence.


*Déclencheur* :

• :ref:`Web Service exposé<web_services_ressource_messages_post>`


*Traitement* :

• Création de message : Un message de catégorie "entrant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 3.


*Contenu du message* :

- **type** : Type de message
- **date** :  Date/heure d'envoi du message
- **emetteur** : Émetteur du message (Nom/Prénom/Login de l'utilisateur à l'origine du message)
- **dossier_instruction** : Identifiant du dossier d'instruction
- **contenu** :

  - **type_piece** : Si le Dossier d'instruction est ouvert, alors les pièces sont acceptées (si le dossier est « incomplet » les pièces sont classées « complémentaires », sinon les pièces sont classées « supplémentaires »). Dans les deux cas, openADS envoie automatiquement un message unique à openARIA signalant l'arrivée d'une pièce sur le dossier et son statut : pièce « complémentaire » ou « supplémentaire ».


*Exemple* :

.. sourcecode:: http
      
    POST /openaria/services/rest_entry.php/messages HTTP/1.1
    Host: localhost

    {
        "type" : "ADS_ERP__AT__DEPOT_DE_PIECE_PAR_LE_PETITIONNAIRE",
        "date" : "31/12/2015 14:42",
        "emetteur" : "admin",
        "dossier_instruction" : "AT0130551600001P0",
        "contenu": {
            "type_piece" : "complémentaire"
        }
    }


.. _echange_ads_erp_113:

=============================================================
[113](Échange ADS → ERP) Ajout d'une nouvelle pièce numérisée
=============================================================

L'objectif principal de cet échange est de permettre aux services ERP d'être informé de la numérisation d'une pièce sur un dossier sur lequel ils sont impliqués.


*Identifiant* : ADS_ERP__AJOUT_D_UNE_NOUVELLE_PIECE_NUMERISEE


*Cas d'utilisation* :

• Lorsque des documents numérisés concernant des dossiers qui concernent ERP, une notification permet d'informer les services ERP que les documents sont disponibles en ligne pour leur indiquer que la qualification est possible.


*Déclencheur* :

• :ref:`Web Service exposé<web_services_ressource_messages_post>`


*Traitement* :

• Création de message : Un message de catégorie "entrant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 0. (Cependant la création de ce message entraîne la création/mise à jour d'un autre message de catégorie "interne" qui lui est marqué comme non lu par défaut. L'objectif est de ne pas avoir 14 messages à lire lors de la numérisation de 14 pièces sur le même dossier.)
• Mise à jour du marqueur indiquant le dépôt des pièces


*Contenu de l'échange* :

- **type** : Type de message
- **date** :  Date/heure d'envoi du message
- **emetteur** : Émetteur du message (Nom/Prénom/Login de l'utilisateur à l'origine du message)
- **dossier_instruction** : Identifiant du dossier d'instruction
- **contenu** :

  - **date_creation** : Date de création
  - **nom_fichier** : Nom du fichier : texte
  - **type** : Type de document : texte
  - **categorie** : Catégorie du type de document


*Exemple* :

.. sourcecode:: http
      
    POST /openaria/services/rest_entry.php/messages HTTP/1.1
    Host: localhost

    {
        "type" : "ADS_ERP__AJOUT_D_UNE_NOUVELLE_PIECE_NUMERISEE",
        "date" : "31/12/2015 14:42",
        "emetteur" : "admin",
        "dossier_instruction" : "AT0130551600001P0",
        "contenu": {
            "date_creation" : "31/12/2015",
            "nom_fichier" : "DGIMPC.pdf",
            "type" : "Imprimé de demande de permis de construire",
            "categorie" : "Définition Générale"
        }
    }



.. _echange_ads_erp_114:

========================================================================
[114](Échange ADS → ERP) Dossier PC Notification de dossier à enjeux ADS
========================================================================

L'objectif principal de cet échange est de permettre aux services ADS de partager le caractère 'à enjeu' du dossier pour en informer le service ERP.


*Identifiant* : ADS_ERP__PC__ENJEU_ADS


*Cas d'utilisation* :

• Un instructeur peut qualifier le dossier comme Dossier à enjeux. Dans ce cas, un message « Dossier à enjeux ADS » est envoyé vers l'application ERP afin de mettre à jour le Dossier d'Instruction. La mise à jour est effectuée automatiquement et un message est présentés au service ERP qui est chargé de mettre à jour le dossier. 

*Déclencheur* :

• L'option ERP est activée
• Le formulaire de modification de dossier dossier d'instruction avec a enjeu ERP qui change de statut(dossier::triggermodifierapres())
• Le dossier est de type PC (paramètre 'erp__dossier_nature__PC')
• Le dossier est marqué comme « connecté au référentiel ERP »


*Traitement* :

• Création de message : Un message de catégorie "sortant" est ajouté dans openADS afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction. → Marqueur(s) de lecture du message : message marqué comme lu par défaut.
• Envoi de la requête à destination de la ressource 'messages' d'openARIA. :ref:`Configuration des échanges sortants<configuration_echanges_sortants_referentiel_erp>`.



*Contenu de l'échange* :

- **type** : Type de message
- **date** : Date/heure d’envoi du message
- **emetteur** : Émetteur du message (Nom/Prénom/Login de l’utilisateur à l’origine du message)
- **dossier_instruction** : Identifiant du dossier d’instruction
- **contenu** :

  • Dossier à enjeux ADS : Oui / Non


*Exemple* :

.. sourcecode:: http
      
    POST /openads/services/rest_entry.php/messages HTTP/1.1
    Host: localhost

    {
        "type": "ADS_ERP__PC__ENJEU_ADS",
        "date": "10/01/2017 12:52",
        "emetteur": "John Doe",
        "dossier_instruction": "PC0130551600001P0",
        "contenu": {
             "Dossier à enjeu ADS": "oui"
        }
    }



.. _echange_erp_ads_201:

=========================================================================================
[201](Échange ERP → ADS) Mise à jour du numéro de l'établissement dans le référentiel ADS
=========================================================================================

*Identifiant* : ERP_ADS__MAJ_NUMERO_ERP_DOSSIER_AUTORISATION


*Cas d'utilisation* :

• Un arrêté d'ouverture ERP est signé. Le numéro de l'établissement est transmis au logiciel ADS pour mise à jour du référentiel.


*Déclencheur* :

• L'option ADS est activée
• Mise à jour au moment de la notification de la décision (arrêté) d'ouverture uniquement.


*Traitement* :

• Création de message : Un message de catégorie "sortant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 0.
• Envoi de la requête à destination de la ressource 'dossier_autorisations' d'openADS. :ref:`Configuration des échanges sortants<configuration_echanges_sortants_referentiel_ads>`


*Contenu de l'échange* :

- **numero_erp** : c'est le code de l'établissement (exemple : 'T3498').


*Exemple* :

.. sourcecode:: http
      
    PUT /openads/services/rest_entry.php/dossier_autorisations/PC0130551601234 HTTP/1.1
    Host: localhost

    {
        "numero_erp":"T12345"
    }


.. _echange_erp_ads_202:

================================================================================================
[202](Échange ERP → ADS) Mise à jour du statut ouvert de l'établissement dans le référentiel ADS
================================================================================================

*Identifiant* : ERP_ADS__MAJ_STATUT_ERP_DOSSIER_AUTORISATION


*Cas d'utilisation* :

• Un arrêté d'ouverture ERP est signé. Cette information ainsi que la date sont transmis au logiciel ADS pour mise à jour du référentiel.


*Déclencheur* :

• L'option ADS est activée
• Mise à jour au moment de la notification de la décision (arrêté) d'ouverture uniquement.


*Traitement* :

• Création de message : Un message de catégorie "sortant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 0.
• Envoi de la requête à destination de la ressource 'dossier_autorisations' d'openADS. :ref:`Configuration des échanges sortants<configuration_echanges_sortants_referentiel_ads>`


*Contenu de l'échange* :

• **erp_ouvert** : Marqueur signifiant l'ouverture de l'établissement (booléen : 'oui' / 'non').
• **date_arrete** : Date de la décision d'ouverture (Format : 12/01/2015). 


*Exemple* :

.. sourcecode:: http
      
    PUT /openads/services/rest_entry.php/dossier_autorisations/PC0130551601234 HTTP/1.1
    Host: localhost

    {
        "erp_ouvert":"oui",
        "date_arrete":"12/01/2015"
    }


.. _echange_erp_ads_203:

================================================================================
[203](Échange ERP → ADS) Récupération des informations depuis le référentiel ADS
================================================================================

*Identifiant* : ERP_ADS__RECUPERATION_INFORMATIONS_DOSSIER_AUTORISATION


*Cas d'utilisation* :

• Lors de la saisie manuelle d'un DA ADS dans le formulaire du DC, on vérifie que ce dossier existe bien dans le référentiel ADS.
• Lors de la réception d'un message qui concerne un DA ADS, on récupère les informations qui le concerne pour éviter une resaisie dans openARIA.


*Traitement* :

• Envoi de la requête à destination de la ressource 'dossier_autorisations' d'openADS. :ref:`Configuration des échanges sortants<configuration_echanges_sortants_referentiel_ads>`


*Exemple* :

.. sourcecode:: http
      
    GET /openads/services/rest_entry.php/dossier_autorisations/PC0130551601234 HTTP/1.1
    Host: localhost


.. _echange_erp_ads_204:

=======================================================================================
[204](Échange ERP → ADS) Dossier PC/ERP Information sur la complétude ERP Accessibilité
=======================================================================================

L'objectif principal de cet échange est de permettre aux services ERP d'apporter une réponse à l'échange [102] et d'informer l'instructeur ADS sur la complétude ERP du dossier.


*Identifiant* : ERP_ADS__PC__INFORMATION_COMPLETUDE_ERP_ACCESSIBILITE


*Cas d'utilisation* :

• Cet échange ne concerne que le PC de type PLAN. Le service ERP Accessibilité indique au service ADS si le dossier est complet ou pas. Un délai de 15 jours est prévu, mais n'est pas géré coté ADS : tous les messages provenant du logiciel ERP sont acceptés dans openADS, y compris hors délais. Pour pouvoir effectuer cette réponse le service ERP a accès aux pièces nécessaires du dossier ADS via la GED.


*Déclencheur* :

• L'option ADS est activée
• Le dossier est marqué comme « connecté au référentiel ADS »
• Le DC est un PC-PLAN
• Le formulaire de complétude/incomplétude est validé sur le DI ACC


*Traitement* :

• Création de message : Un message de catégorie "sortant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 0.
• Envoi de la requête à destination de la ressource 'messages' d'openADS. :ref:`Configuration des échanges sortants<configuration_echanges_sortants_referentiel_ads>`


*Contenu de l'échange* :

- **contenu** :

  • libelle « Complétude ERP ACC » : valeur : « oui/non »
  • libelle « Motivation Complétude ERP ACC » : valeur : texte libre multi-lignes


*Exemple* :

.. sourcecode:: http
      
    POST /openads/services/rest_entry.php/messages HTTP/1.1
    Host: localhost

    {
        "type": "ERP_ADS__PC__INFORMATION_COMPLETUDE_ERP_ACCESSIBILITE",
        "date": "16/06/2014 14:12",
        "emetteur": "John Doe",
        "dossier_instruction": "PD12R0001",
        "contenu": {
            "Complétude ERP ACC": "non",
            "Motivation Complétude ERP ACC": "Lorem ipsum dolor sit amet..."
        }
    }


.. _echange_erp_ads_205:

==================================================================================
[205](Échange ERP → ADS) Dossier PC/ERP Information sur la complétude ERP Sécurité
==================================================================================

L'objectif principal de cet échange est de permettre aux services ERP d'apporter une réponse à l'échange [102] et d'informer l'instructeur ADS sur la complétude ERP du dossier.


*Identifiant* : ERP_ADS__PC__INFORMATION_COMPLETUDE_ERP_SECURITE


*Cas d'utilisation* :

• Cet échange ne concerne que le PC de type PLAN. Le service ERP Sécurité indique au service ADS si le dossier est complet ou pas. Un délai de 15 jours est prévu, mais n'est pas géré coté ADS : on accepte tous les messages y compris hors délais. Pour pouvoir effectuer cette réponse le service ERP a accès aux pièces nécessaires du dossier ADS via la GED.


*Déclencheur* :

• L'option ADS est activée
• Le dossier est marqué comme « connecté au référentiel ADS »
• Le DC est un PC-PLAN
• Le formulaire de complétude/incomplétude est validé sur le DI SI


*Traitement* :

• Création de message : Un message de catégorie "sortant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 0.
• Envoi de la requête à destination de la ressource 'messages' d'openADS. :ref:`Configuration des échanges sortants<configuration_echanges_sortants_referentiel_ads>`


*Contenu de l'échange* :

- **contenu** :

  • libelle « Complétude ERP SECU » : valeur : « oui/non »
  • libelle « Motivation Complétude ERP SECU » : valeur : texte libre multi-lignes


*Exemple* :

.. sourcecode:: http
      
    POST /openads/services/rest_entry.php/messages HTTP/1.1
    Host: localhost

    {
        "type": "ERP_ADS__PC__INFORMATION_COMPLETUDE_ERP_SECURITE",
        "date": "16/06/2014 14:12",
        "emetteur": "John Doe",
        "dossier_instruction": "PD12R0001",
        "contenu": {
            "Complétude ERP SECU": "oui",
            "Motivation Complétude ERP SECU": "Lorem ipsum dolor sit amet..."
        }
    }


.. _echange_erp_ads_206:

============================================================================
[206](Échange ERP → ADS) Dossier PC/ERP Information sur la qualification ERP
============================================================================

L'objectif principal de cet échange est de permettre aux services ERP d'apporter une réponse à l'échange [103] et d'informer l'instructeur ADS sur le caractère ERP du dossier.


*Identifiant* : ERP_ADS__PC__INFORMATION_QUALIFICATION_ERP


*Cas d'utilisation* :

• Cet échange ne concerne que le PC de type PLAN. 
• Le service ERP répond à une demande de qualification d'un dossier ADS. Il renseigne le type et la catégorie ERP. Ces informations enrichiront le Référentiel Autorisations lorsqu'elles seront actualisées dans le Dossier  d'Instruction par l'instructeur.


*Déclencheur* :

• L'option ADS est activée
• Le dossier est marqué comme « connecté au référentiel ADS »
• Le DC est un PC-PLAN
• Le formulaire de qualification est validé


*Traitement* :

• Création de message : Un message de catégorie "sortant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 0.
• Envoi de la requête à destination de la ressource 'messages' d'openADS. :ref:`Configuration des échanges sortants<configuration_echanges_sortants_referentiel_ads>`


*Contenu de l'échange* :

- **contenu** :

  • Confirmation ERP : oui/non (le Dossier est bien/n'est pas un ERP)
  • Type de dossier ERP : texte libre
  • Catégorie de dossier ERP : texte libre


*Exemple* :

.. sourcecode:: http
      
    POST /openads/services/rest_entry.php/messages HTTP/1.1
    Host: localhost

    {
        "type": "ERP_ADS__PC__INFORMATION_QUALIFICATION_ERP",
        "date": "16/06/2014 14:12",
        "emetteur": "John Doe",
        "dossier_instruction": "PD12R0001",
        "contenu": {
            "Confirmation ERP": "oui",
            "Type de dossier ERP": "Lorem ipsum dolor sit amet...",
            "Catégorie de dossier ERP": "Lorem ipsum dolor sit amet..."
        }
    }


.. _echange_erp_ads_207:

============================================================================
[207](Échange ERP → ADS) Dossier PC/ERP Notification de dossier à enjeux ERP
============================================================================

L'objectif principal de cet échange est de permettre aux services ERP de partager le caractère 'à enjeu' du dossier pour en informer l'instructeur ADS.


*Identifiant* : ERP_ADS__PC__NOTIFICATION_DOSSIER_A_ENJEUX_ERP


*Cas d'utilisation* :

• Cet échange ne concerne que le PC de type PLAN. 
• Le service ERP peut qualifier le dossier comme Dossier à enjeux. Dans ce cas, un message « Dossier à enjeux ERP » est envoyé vers l'application ADS. Ce message ne met pas directement à jour le référentiel mais il est pris en compte dans les messages présentés à l'instructeur qui est chargé de mettre à jour ses données, et par voie de conséquence le référentiel.


*Déclencheur* :

• L'option ADS est activée
• Le dossier est marqué comme « connecté au référentiel ADS »
• Le DC est un PC-PLAN
• Le DC est marqué comme à enjeu


*Traitement* :

• Création de message : Un message de catégorie "sortant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 0.
• Envoi de la requête à destination de la ressource 'messages' d'openADS. :ref:`Configuration des échanges sortants<configuration_echanges_sortants_referentiel_ads>`


*Contenu de l'échange* :

- **contenu** :

  • Dossier à enjeux ERP : Oui / Non


*Exemple* :

.. sourcecode:: http
      
    POST /openads/services/rest_entry.php/messages HTTP/1.1
    Host: localhost

    {
        "type": "ERP_ADS__PC__NOTIFICATION_DOSSIER_A_ENJEUX_ERP",
        "date": "16/06/2014 14:12",
        "emetteur": "John Doe",
        "dossier_instruction": "PD12R0001",
        "contenu": {
            "Dossier à enjeux ERP" : "oui"
        }
    }


.. _echange_erp_ads_208:

=================================================================================================
[208](Échange ERP → ADS) Dossier AT Mise à jour des informations arrêtées dans le référentiel ADS
=================================================================================================

*Identifiant* : ERP_ADS__AT__MAJ_ARRETE_ERP_DOSSIER_AUTORISATION


*Cas d'utilisation* :

• Cette information est envoyée par ERP à ADS suite à la signature de l'arrêté d'autorisation d'un dossier AT.


*Déclencheur* :

• L'option ADS est activée
• Mise à jour au moment de la notification de la décision (arrêté) d'autorisation uniquement.


*Traitement* :

• Création de message : Un message de catégorie "sortant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 0.
• Envoi de la requête à destination de la ressource 'dossier_autorisations' d'openADS. :ref:`Configuration des échanges sortants<configuration_echanges_sortants_referentiel_ads>`


*Contenu de l'échange* :

• « arrete_effectue » : Arrêté effectué. Format : booléen (oui/non)
• « date_arrete » : Date de l'arrêté. Format : date (JJ/MM/YYYY)


*Exemple* :

.. sourcecode:: http
      
    PUT /openads/services/rest_entry.php/dossier_autorisations/PC0130551601234 HTTP/1.1
    Host: localhost

    {
        "arrete_effectue":"some",
        "date_arrete":"04/06/2014"
    }


.. _echange_erp_ads_209:

==============================================================
[209](Échange ERP → ADS) Dossier PC/ERP Retour de consultation
==============================================================

L'objectif principal de cet échange est de permettre aux services ERP de répondre à une consultation d'un instructeur ADS directement depuis openARIA (sans nécessité de le faire depuis l'interface dédiée aux services consultés dans openADS).


*Identifiant* : ERP_ADS__PC__RETOUR_DE_CONSULTATION


*Cas d'utilisation* :

• Cet échange ne concerne que le DC de type PLAN (PC).
• L'instructeur ADS a consulté officiellement via l'échange [104] le service ACC ou SECU d'openARIA sur un dossier d'instruction ADS de type PC, lorsque le PV est généré sur le DI lié alors on envoi directement le PV avec l'avis à openADS.


*Déclencheur* :

• L'option ADS est activée
• Le dossier est marqué comme « connecté au référentiel ADS »
• Le DC est un PC-PLAN
• Émission du PV de plan.


*Traitement* :

• Création de message : Un message de catégorie "sortant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 0.
• Envoi de la requête à destination de la ressource 'consultations' d'openADS. :ref:`Configuration des échanges sortants<configuration_echanges_sortants_referentiel_ads>`


*Contenu de l'échange* :

• Date de retour d'avis (obligatoire) : {'date_retour': 'jj/mm/aaaa'} ;
• Avis (obligatoire) : {'avis' :'favorable|defavorable|favorable_reserve|...'} ;
• Motivation (facultatif) : {'motivation' :'Texte libre ...'} ;
• Nom du fichier de retour d'avis (facultatif) : {'nom_fichier' :'retour d'avis ABF.pdf'} ;
• Fichier encodé en base 64 (facultatif) : {'fichier_base64' :data}.


*Exemples* :

Retour d'avis d'une consultation sans fichier :

.. sourcecode:: http
      
    PUT /openads/services/rest_entry.php/consultations/12 HTTP/1.1
    Host: localhost

    {
        "date_retour": "14/01/2012",
        "avis": "Favorable"
    }

Retour d'avis d'une consultation avec fichier :

.. sourcecode:: http
      
    PUT /openads/services/rest_entry.php/consultations/12 HTTP/1.1
    Host: localhost

    {
        "date_retour": "14/01/2012",
        "avis": "Favorable",
        "fichier_base64": "JVBERi0xLjQKJcOkw7zDtsOfCjIgM",
        "nom_fichier": "plop.pdf"
    }


.. _echange_erp_ads_210:

===========================================================
[210](Échange ERP → ADS) Dossier AT Complétude Incomplétude
===========================================================

Dans le contexte du guichet unique, l'objectif principal de cet échange est de mettre à jour l'information de complétude d'un dossier AT dans openADS suite à sa complétude/incomplétude dans openARIA pour que les agents du guichet unique puisse accomplir leur mission d'enregistrement des demandes correctement.


*Identifiant* : ERP_ADS__AT__MAJ_COMPLETUDE_INCOMPLETUDE


*Cas d'utilisation* :

• Co complétude, vérifier que la complétude a été faite seulement sur l'un des deux services alors on envoi pas. Si les deux complétudes sont faites, alors on envoi un message de complétude. Le marqueur complet chez lez deux services envoi un message.


*Déclencheur* :

• L'option ADS est activée
• Le dossier est marqué comme « connecté au référentiel ADS »
• Le formulaire de complétude/incomplétude est validé sur un DI


*Traitement* :

• Création de message : Un message de catégorie "sortant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 0.
• Envoi de la requête à destination de la ressource 'dossier_instructionss' d'openADS. :ref:`Configuration des échanges sortants<configuration_echanges_sortants_referentiel_ads>`


*Contenu de l'échange* :

• « message » : « complet » ou « incomplet »
• « date » : Date de la mise à jour de l'information au format JJ/MM/AAAA


*Exemple* :

.. sourcecode:: http
      
    PUT /openads/services/rest_entry.php/dossier_instructions/PC0130551600001P0 HTTP/1.1
    Host: localhost

    {
        "message":"complet",
        "date":"27/10/2013"
    }


.. _echange_erp_ads_211:

===========================================
[211](Échange ERP → ADS) Dossier AT Clôture
===========================================

Dans le contexte du guichet unique, l'objectif principal de cet échange est de mettre à jour l'information de clôture d'un dossier AT dans openADS suite à sa clôture dans openARIA pour que les agents du guichet unique puisse accomplir leur mission d'enregistrement des demandes correctement.

*Identifiant* : ERP_ADS__AT__MAJ_CLOTURE


*Cas d'utilisation* :

• Ce message a vocation à permettre aux agents du Guichet unique de bien accomplir leur mission d'enregistrement face à l'arrivée d'une nouvelle pièce : si le dossier d'instruction DAT est ouvert, alors les pièces sont acceptées (si le dossier est « incomplet », les pièces sont classées « complémentaires », sinon les pièces sont « supplémentaires ») et si le dossier est clos, les pièces sont refusées.
• Tous les dossiers d'instruction d'AT ne donnent pas lieu à un arrêté, ni même à une instruction. Vus du guichet unique et d'openADS ils peuvent donc toujours paraître « en cours d'instruction ». Dès que le dossier est clos dans openARIA pour ccessibilité et Sécurité, un message doit partir vers openADS.
• Le message de clôture doit mettre à jour automatiquement dans openADS le dossier d'instruction avec un statut « clos » et cela doit se répercuter automatiquement sur le refus des nouvelles pièces arrivant au guichet unique.


*Déclencheur* :

• L'option ADS est activée
• Le dossier est marqué comme « connecté au référentiel ADS »
• Le dossier est noté comme clôturé


*Traitement* :

• Création de message : Un message de catégorie "sortant" est ajouté dans openARIA afin de consigner l'échange. Il est visible depuis l'onglet "Message(s)" du dossier d'instruction et du dossier de coordination. → Marqueur(s) de lecture du message : mode 0.
• Envoi de la requête à destination de la ressource 'dossier_instructionss' d'openADS. :ref:`Configuration des échanges sortants<configuration_echanges_sortants_referentiel_ads>`


*Contenu de l'échange* :

• « message » : « clos » ou « ouvert »
• « date » : Date de la mise à jour de l'information au format JJ/MM/AAAA


*Exemple* :

.. sourcecode:: http
      
    PUT /openads/services/rest_entry.php/dossier_instructions/PC0130551600001P0 HTTP/1.1
    Host: localhost

    {
        "message":"clos",
        "date":"27/10/2013"
    }


.. _echange_erp_ads_212:

================================================================================
[212](Échange ERP → ADS) Récupération des informations depuis le référentiel ADS
================================================================================

*Identifiant* : ERP_ADS__RECUPERATION_INFORMATIONS_DOSSIER_INSTRUCTION


*Cas d'utilisation* :

• Lors de la saisie manuelle d'un DI ADS dans le formulaire du DC, on vérifie que ce dossier existe bien dans le référentiel ADS.
• Lors de la réception d'un message qui concerne un DI ADS, on récupère les informations qui le concerne pour éviter une resaisie dans openARIA.


*Traitement* :

• Envoi de la requête à destination de la ressource 'dossier_instructions' d'openADS. :ref:`Configuration des échanges sortants<configuration_echanges_sortants_referentiel_ads>`


*Exemple* :

.. sourcecode:: http
      
    GET /openads/services/rest_entry.php/dossier_instructions/PC0130551601234P0 HTTP/1.1
    Host: localhost



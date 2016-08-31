###################
Rubrique "Dossiers"
###################

.. image:: menu-rubrik-dossiers.png

La rubrique "Dossiers" est divisée en catégories :

- DC (Coordination) : il est possible pour un technicien depuis le DI ou l'établissement d'accéder à des écrans de DC, il a donc été nécessaire d'ajouter une entrée de menu à cet effet, pour qu'elle soit disponible et sélectionnée sur cet écran afin de conserver une navigation cohérente.

- DI (Instruction) : catégorie principale dont les entrées sont sélectionnées lors d'accès aux écran de DI.

- Visites : catégorie nécessaire au listing du widget "mes visites à réaliser"

- Documents entrants : catégorie nécessaire au listing du widget "mes documents entrants non lus"

- Autorité de police : catégorie nécessaire au listing du widget "Autorités de police qui n'ont pas été notifiées ou exécutées"


DC (Dossiers de Coordination)
=============================

Les listing de DC
-----------------

Dossiers à qualifier
####################

(:menuselection:`Dossiers --> DC (Coordination) --> Dossiers à qualifier`)

Ce listing présente les dossiers de coordination à qualifier.


Tous les dossiers
#################

(:menuselection:`Dossiers --> DC (Coordination) --> Tous les dossiers`)

Ce listing présente tous les dossiers de coordination.

Lorsqu'un Système d'Information Géographique est paramétré, l'icône en forme de Terre au-dessus du tableau permet d'être redirigé vers le SIG et de consulter la sélection actuelle de dossiers de coordination. S'il n'y a pas eu de recherche avancée, le bouton redirige vers la couche des dossiers de coordination sur le SIG.

Les icônes en forme de Terre de chaque ligne du tableau permettent d'être redirigé sur le SIG avec la vue centrée sur le dossier de coordination correspondant à cette ligne.

.. image:: dossier_coordination-listing.png

Ajouter un nouveau DC
---------------------

(:menuselection:`Dossiers --> DC (Coordination) --> Nouveau dossier`)

Cette entrée de menu permet d'accéder directement au formulaire d'ajout d'un dossier de coordination.

.. image:: dossier_coordination-form-ajouter.png

Les types de dossier de coordination ont un paramétrage qui permet de remplir automatiquement certains champs du formulaire :

- la case à cocher de la qualification,
- la case à cocher du dossier d'instruction sécurité,
- la case à cocher du dossier d'instruction accessibilité.

La case à cocher "À qualifier" définit si un dossier doit être qualifié ou non.


La fiche du dossier de coordination (DC)
----------------------------------------

.. image:: dossier_coordination-fiche.png

Lorsqu'un Système d'Information Géographique est paramétré, les icônes en forme de Terre permettent d'être redirigé sur le SIG avec la vue centrée sur l'élément en question :

- si le dossier a été géolocalisé, l'icône dans le champ "Géolocalisé" permet d'être redirigé sur l'établissement sur le SIG.
- si l'établissement lié au dossier a été géolocalisé, on peut le visualiser sur le SIG en cliquant sur l'icône à côté du nom de l'établissement.
- si des références cadastrales ont été renseignées, l'icône dans le champ références cadastrales permet de visualiser ces parcelles sur le SIG.

Géolocaliser un dossier de coordination
#######################################

Si un SIG a été paramétré et que le dossier de coordination n'a pas déjà été géolocalisé, un bouton dans le portail d'actions contextuelles permet de le géolocaliser sur le SIG.

.. image:: dossier_coordination-action-geocoder-link.png

Cette géolocalisation se fait sur la base de l'adresse, des parcelles et du numéro de dossier ADS qui ont été renseignés. Si ces éléments ne permettent pas de géolocaliser automatiquement le dossier de coordination, un message sera affiché, qui contiendra un lien permettant à l'utilisateur de dessiner manuellement l'élément sur le SIG.

Une fois ce dessin manuel effectué sur le SIG, il faut une nouvelle fois lancer l'action de géolocalisation du portail d'actions contextuelles pour valider le dessin manuel. En cas de succès, un message de validation apparaît.

Onglet Contraintes
##################

La fonctionnalité est identique à l':ref:`application des contraintes aux établissements<etablissement_onglet_contraintes>`.

Onglet Contacts
###############

Onglet DC Parents
#################


.. _dossiers_dc_onglet_documents_entrants:

Onglet Documents Entrants
#########################

Listing standard (ou interne)
,,,,,,,,,,,,,,,,,,,,,,,,,,,,,

L'onglet "Document Entrants" sur la fiche d'un dossier de coordination affiche tous ses documents entrants liés (ainsi que ceux éventuellement liés aux dossiers d'instruction). Les informations présentées sont :

- le nom du document,
- le type du document (acte, courrier de l'explotant, ...),
- la date de création du document,
- la date de réception du document,
- la date d'émission du document,
- la date butoir du document,
- le statut du document (en cours, qualifié, ...).

.. image:: dc-onglet-documents-entrants-listing.png


.. _dossiers_dc_onglet_documents_entrants_swrod:

Listing guichet unique
,,,,,,,,,,,,,,,,,,,,,,

Dans le cas où le module :ref:`'swrod' (Documents du guichet unique en lecture seule)<module_swrod>` est activé, l'onglet peut posséder un affichage différent si le DC contient une référence vers un dossier ADS. Dans ce cas, l'onglet 'Interne' présente les mêmes informations et actions que l'onglet 'Documents Entrants' standard et l'onglet 'Guichet Unique' présente une vue en lecture seule des documents concernant le dossier ADS du DC.

.. image:: dc-onglet-documents-entrants-swrod-onglet-gu-view.png


Onglet Documents générés
########################


Onglet AP
#########



DI (Dossiers d'Instruction)
===========================

Les listing de DI
-----------------

Dossiers à qualifier
####################

(:menuselection:`Dossiers --> DI (Instruction) --> Dossiers à qualifier`)


Dossiers à affecter
###################

(:menuselection:`Dossiers --> DI (Instruction) --> Dossiers à affecter`)


Mes plans
#########

(:menuselection:`Dossiers --> DI (Instruction) --> Mes plans`)

Ce listing présente les dossiers d'instruction dont l'utilisateur connecté est noté comme instructeur et dont le type du dossier de coordination est de type PLAN.


Tous les plans
##############

(:menuselection:`Dossiers --> DI (Instruction) --> Tous les plans`)

Ce listing présente les dossiers d'instruction rattachés au service dont l'utilisateur connecté fait partie et dont le type du dossier de coordination est de type PLAN.


Mes visites
###########

(:menuselection:`Dossiers --> DI (Instruction) --> Mes visites`)

Ce listing présente les dossiers d'instruction dont l'utilisateur connecté est noté comme instructeur et dont le type du dossier de coordination est de type VISIT.


Toutes les visites
##################

(:menuselection:`Dossiers --> DI (Instruction) --> Toutes les visites`)

Ce listing présente les dossiers d'instruction rattachés au service dont l'utilisateur connecté fait partie et dont le type du dossier de coordination est de type VISIT.


Tous les dossiers
#################

(:menuselection:`Dossiers --> DI (Instruction) --> Tous les dossiers`)

Lorsqu'un Système d'Information Géographique est paramétré, les icônes en forme de Terre de chaque ligne du tableau permettent d'être redirigé sur le SIG avec la vue centrée sur le dossier de coordination lié à ce dossier d'instruction.

.. image:: dossier_instruction-listing.png

La fiche du dossier d'instruction (DI)
--------------------------------------

Lorsqu'un Système d'Information Géographique est paramétré et que le dossier de coordination lié à ce dossier d'instruction a été géolocalisé, l'icône en forme de Terre permet d'être redirigé sur le SIG avec la vue centrée sur le dossier de coordination lié.

.. image:: dossier_instruction-fiche.png

Actions
#######


+ Modifier
    - Disponible si le DI n'est pas clôturé.
    - Ouvre le formulaire de modification du dossier d'instruction.

+ Clôturer
    - Disponible si le DI n'est pas clôturé, n'est pas à qualifier et, dans le cas d'un dossier de coordination périodique, s'il possède une visite.
    - Clôture le dossier d'instruction.

+ Rouvrir
    - Disponible si le DI est clôturé, n'est pas à qualifier et, dans le cas d'un dossier de coordination périodique, si ce dernier n'est pas clôturé.
    - Rouvre le dossier d'instruction.

+ À poursuivre
    - Disponible si le DI n'est pas clôturé, si son statut est "à programmer" ou "programmé" et s'il y a au moins une visite planifiée.
    - Change le statut du dossier d'instruction en "à poursuivre".

+ À programmer
    - Disponible si le DI n'est pas clôturé, si son statut est "programmé" et s'il n'y a aucune visite ou qu'elles sont toutes annulées.
    - Change le statut du dossier d'instruction en "à programmer".

+ Programmer
    - Disponible si le DI n'est pas clôturé, si son statut est "à programmer" ou "à poursuivre" et s'il y a au moins une visite planifiée.
    - Change le statut du dossier d'instruction en "programmé".


Onglet Analyse
##############

Dans le coin haut gauche de la fiche d'analyse figure son état : en cours de
rédaction, terminée, validée ou actée.


Dans le coin haut droit sont disponibles les actions que l'on peut effectuer
dessus : changer son état et éditer un document (rapport, compte-rendu et
prévisualisation de procès-verbal).


Le corps de l'analyse est composé de plusieurs blocs de données qui ont chacun
un titre et éventuellement un bouton modifier (cela dépend de vos droits et de
l'état de l'analyse) :


+ Type de l'analyse
+ Objet
+ Descriptif de l'établissement
+ Classification de l'établissement
+ Données techniques
+ Réglementation applicable
+ Prescriptions
+ Documents présentés lors des visites et ceux fournis après ces dernières
+ Essais réalisés
+ Compte-rendu d'analyse
+ Observation
+ Avis proposé
+ Proposition de décision autorité de police


Onglet PV
#########

En plus de lister et de permettre d'accéder aux procès-verbaux rattachés au
dossier d'instruction, cet onglet permet d'en ajouter de trois manières :

+ en générant un PV, pour ce faire l'analyse du DI doit être validée

Le numéro est défini automatiquement selon l'année de la date de rédaction.
L'état de l'analyse devient "actée". On peut par la suite ajouter au PV généré
sa version signée.

+ en regénérant le dernier PV

Si l'analyse est rouverte puis revalidée, et qu'au moins un PV a déjà été généré,
alors il devient possible de regénérer le dernier. Pour le reste le comportement
est semblable à un PV généré.

+ en ajoutant directement un PV tiers.

Aucun numéro n'est défini. On peut modifier ce procès-verbal par la suite.

Dans tous les cas s'il s'agit d'un dossier d'instruction du service Sécurité
Incendie et que l'on ajoute un PV signé, tiers ou relatif au PV (re)généré, cela
met à jour les données techniques de l'établissement selon celles définies dans
l'analyse. De plus et ce quelque soit le service, toute action sur un PV
(création, modification) met à jour le couple de champs « proposition d'avis »
et « proposition de complément d'avis » de la demande de passage liée grâce au
couple de champs « proposition d'avis » et « proposition de complément d'avis »
de l'analyse du dossier d'instruction sur lequel on se trouve.


.. _dossiers_di_onglet_documents_entrants:

Onglet Documents Entrants
#########################

Listing standard (ou interne)
,,,,,,,,,,,,,,,,,,,,,,,,,,,,,

L'onglet "Document Entrants" sur la fiche d'un dossier d'instruction affiche tous ses documents entrants liés. Les informations présentées sont :

- le nom du document,
- l'établissement,
- le dossier de coordination,
- le dossier d'instruction,
- la date butoir du document,
- le statut du document (en cours, qualifié, ...).

.. image:: di-onglet-documents-entrants-listing.png


Listing guichet unique
,,,,,,,,,,,,,,,,,,,,,,

.. _dossiers_di_onglet_documents_entrants_swrod:

Dans le cas où le module :ref:`'swrod' (Documents du guichet unique en lecture seule)<module_swrod>` est activé, l'onglet peut posséder un affichage différent si le DC contient une référence vers un dossier ADS. Dans ce cas, l'onglet 'Interne' présente les mêmes informations et actions que l'onglet 'Documents Entrants' standard et l'onglet 'Guichet Unique' présente une vue en lecture seule des documents concernant le dossier ADS du DC.

.. image:: di-onglet-documents-entrants-swrod-onglet-gu-view.png


Onglet Documents générés
########################


Onglet Réunions
###############


Onglet Visites
##############




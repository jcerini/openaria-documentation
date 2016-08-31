#########################
Rubrique "Établissements"
#########################

.. image:: menu-rubrik-etablissements.png

La rubrique "Établissements" contient les accès aux établissements et unités d'accessibilité.

Les établissements
==================

Les listings des établissements
-------------------------------

Chacun des deux listings permet une recherche avancée complète sur plusieurs critères.

.. image:: etablissement-listing-search.png

Depuis le menu "Référentiel ERP"
################################

Liste tous les établissements qui constituent le référentiel officiel des ERP.

.. image:: etablissement_referentiel_erp-listing.png

Depuis le menu "Tous les établissements"
########################################

Liste tous les établissements ERP, les référentiels et les autres.

Lorsqu'un Système d'Information Géographique est paramétré, les icônes en forme de Terre de chaque ligne du tableau permettent d'être redirigé sur le SIG avec la vue centrée sur l'établissement correspondant à cette ligne.

L'icône en forme de Terre au-dessus du tableau permet d'être redirigé vers le SIG et de consulter la sélection actuelle d'établissements. S'il n'y a pas eu de recherche avancée, le bouton redirige vers la couche des établissements sur le SIG.

.. image:: etablissement_tous-listing.png

Ajouter un établissement
------------------------

Il est possible d'ajouter un établissement depuis les deux listings, soit depuis le formulaire d'ajout ou de modification d'un dossier de coordination. Dans chaque cas le formulaire est identique.

.. image:: etablissement-form-ajouter.png

Les établissements peuvent également être ajoutés depuis un fichier CSV. Un fichier CSV modèle est disponible sur le formulaire d'importation.

.. image:: etablissement-form-import.png

La fiche d'un établissement
---------------------------

.. image:: etablissement-fiche.png

Lorsqu'un Système d'Information Géographique est paramétré, les icônes en forme de Terre permettent d'être redirigé sur le SIG avec la vue centrée sur l'élément en question :

- si l'établissement a été géolocalisé, l'icône dans le champ "Géolocalisé" permet d'être redirigé sur l'établissement sur le SIG
- si des références cadastrales ont été renseignées, l'icône dans le champ références cadastrales permet de visualiser ces parcelles sur le SIG.

Les ERP référentiels
####################

Les ERP référentiel officiel font l'objet de visites périodiques obligatoire suivant leur type et catégorie (les ERP de type Plein Air n'ont pas de visite périodique).

La mise à jour des données des ERP référentiels se fait uniquement par une décision de procès-verbal.

Les ERP autres que référentiels
###############################

Les données des ERP autres que référentiel peuvent être mises à jour sans que cela se passe par une décision.

Ouverture / Fermeture d'un ERP
##############################

L'ouverture et la fermeture d'un ERP référentiel se fait depuis un arrêté. Pour les autres ERP il est possible de passer par le formulaire.

En cas d'extrême urgence, l'administrateur peut également modifier le statut d'ouverture d'un ERP référentiel.

Gestion de l'exploitant et des mandataires
------------------------------------------

L'exploitant est le responsable unique de l'établissement, de ce fait il peut être ajouté seulement depuis la fiche de l'établissement. La fiche de l'exploitant est visible depuis l'onglet "Contacts" de l'établissement, il est possible de le modifier de cet endroit. Une synchronisation se fera entre les données des deux enregistrements.

.. image:: etablissement_exploitant-form-ajouter.png

Il possible d'ajouter d'autres contacts, de type autre qu'exploitant. Ceux-ci seront visible au moyen de l'onglet des contacts de l'établissement.

.. image:: etablissement_contact-listing.png

Géolocaliser un établissement
-----------------------------

Si un SIG a été paramétré et que l'établissement n'a pas déjà été géolocalisé, une action dans le portail d'actions contextuelles permet de le géolocaliser sur le SIG.

.. image:: etablissement-action-geocoder-link.png

Cette géolocalisation se fait sur la base de l'adresse, des parcelles et du numéro de dossier ADS qui ont été renseignés. Si ces éléments ne permettent pas de géolocaliser automatiquement l'établissement, un message sera affiché, qui contiendra un lien permettant à l'utilisateur de dessiner manuellement l'élément sur le SIG.

.. image:: etablissement-action-geocoder-fail.png

Une fois ce dessin manuel effectué sur le SIG, il faut une nouvelle fois lancer l'action de géolocalisation du portail d'actions contextuelles pour valider le dessin manuel. En cas de succès, un message de validation apparaît.

.. image:: etablissement-action-geocoder-success.png

Archiver un établissement
-------------------------

Les établissements peuvent être archivés. Ils n'apparaitront plus dans le listing par défaut.

.. image:: etablissement-action-archiver-link.png

Un établissement archivé à la possiblité d'être désarchivé.

.. image:: etablissement-action-desarchiver-link.png

Lien avec le référentiel des voies
----------------------------------

Les voies sont récupérées automatiquement depuis le référentiel officiel grâce à  un processus quotidien qui récupérera le fichier de voies actualisées du référentiel et mettra à jour la table des voies dans OpenARIA.
Un champ de complétion automatique, avec un affichage des voies au fur et à mesure de la frappe, est utilisé pour la sélection de la voie. Les arrondissements seront alors filtrés par rapport à ces voies.

.. image:: etablissement-form-autocomplete.png

Les voies sont utilisées lors de la saisie des adresses, afin d'éviter toute erreur de saisie. Le changement de libellé de voie sera répercuté automatiquement sur les établissements. Les voies qui viennent du référentiel et n'existent plus seront désactivées et ne seront plus disponibles pour les nouvelles saisies.

Lien avec le référentiel patrimone
----------------------------------

La référence patrimoine ne sera affichée que si le statut juridique de l'établissement est "ville" et que l'option "option_referentiel_patrimoine" est activée.
Les références patrimoines sont obtenu à partir des références de parcelles.

Le fonctionnement est le suivant :

- suite à la saisie des références cadastrales, l'utilisateur disposera d'une action permettant de rechercher la référence patrimoine,
- cette action déclenchera un web service vers le référentiel patrimoine,
- le web service répondra avec une liste d’éléments de patrimoine,
- l'utilisateur sélectionnera les éléments qui sont pertinent,
- les références patrimoines seront stockées au sein de la fiche de l'établissement.

.. image:: etablissement-form-patrimoine.png


.. _etablissement_onglet_contraintes:

Onglet Contraintes
------------------

Liste
#####

Les contraintes affichées dans le tableau sont classées par groupe et sous-groupe, et éventuellement par le numéro d’ordre d’affichage si elles en possèdent un.
Chacune dispose de boutons permettant de la consulter, modifier et supprimer.
En sus du tableau deux liens permettent d'ajouter et récupérer des contraintes.

.. image:: etablissement-tab-contrainte.png

Formulaire
##########

Seul le texte complété est affiché et modifiable. Si la contrainte a été récupérée depuis le référentiel alors une action permet de la démarquer.

.. image:: etablissement-consulter-contrainte.png

Ajout
#####

On peut ajouter des contraintes du paramétrage d'openARIA. Seules les actives sont proposées (c'est à dire les archivées sont masquées).
Ajouter une contrainte synchronisée avec le référentiel SIG aura le même comportement qu'ajouter une contrainte créée manuellement :
elle ne sera pas marquée comme récupérée.

.. image:: etablissement-ajouter-contrainte.png

Récupération
############

L'option SIG doit être activée pour bénéficier de cette fonctionnalité. Selon les références cadastrales de l'établissement,
openARIA interroge le référentiel SIG pour récupérer les contraintes applicables à ces parcelles.
Si le logiciel ne dispose pas des dites contraintes, il proposera de les synchroniser.
Sinon, il ajoutera automatiquement ces contraintes à l'établissement (ou les mettra à jour si elles étaient déjà appliquées).
Le texte complété d'une contrainte récupérée est celui du référentiel SIG éventuellement concaténé au texte surchargé si ce dernier est défini dans le paramétrage.
Ce texte sera toujours écrasé lors d'une récupération : vous devez démarquer la contrainte si vous ne souhaitez pas que cela soit le cas.

.. image:: etablissement-recuperer-contrainte.png

Onglet UA
---------

Cet onglet présente un écran permettant d'accéder à trois listings :

• un listing des UA validées
• un listing des UA en projet
• un listing des UA archivées

Au clic sur l'onglet UA, on accède par défaut au listing des UA validées.

.. image:: etablissement_onglet-ua.png

Listing des UA validées
#######################

Une action d'ajout d'une UA est disponible depuis ce listing. Un lien représenté par un plus vert permet d'accéder au formulaire d'ajout d'une UA.

Un clic sur chaque ligne du listing permet d'accéder à la fiche de visualisation d'une UA.

Le tableau comporte les colonnes suivantes :

- « libellé » : c'est le libellé de l'UA qui permet de l'identifier parmi les autres UA de l'établissement.
- « acc. auditif » : information sur l'accessibilité au handicap auditif de l'UA. Les valeurs possibles sont : « Oui » / « Non » / « » (vide).
- « acc. mental » : information sur l'accessibilité au handicap mental de l'UA. Les valeurs possibles sont : « Oui » / « Non » / « » (vide).
- « acc. physique » : information sur l'accessibilité au handicap physique de l'UA. Les valeurs possibles sont : « Oui » / « Non » / « » (vide).
- « acc. visuel » : information sur l'accessibilité au handicap visuel de l'UA. Les valeurs possibles sont : « Oui » / « Non » / « » (vide).
- « dérogation » : information indiquant si l'UA possède une dérogation ou non. Les deux valeurs possibles sont : « Oui » et « » (vide).

.. image:: etablissement-onglet-ua-listing-ua-validees.png


Listing des UA en projet
########################

Aucune action d'ajout d'une UA n'est possible depuis ce listing.

Un clic sur chaque ligne du listing permet d'accéder à la fiche de visualisation d'une UA.

Le tableau comporte les colonnes suivantes :

- « libellé » : c'est le libellé de l'UA qui permet de l'identifier parmi les autres UA de l'établissement.
- « acc. auditif » : information sur l'accessibilité au handicap auditif de l'UA. Les valeurs possibles sont : « Oui » / « Non » / « » (vide).
- « acc. mental » : information sur l'accessibilité au handicap mental de l'UA. Les valeurs possibles sont : « Oui » / « Non » / « » (vide).
- « acc. physique » : information sur l'accessibilité au handicap physique de l'UA. Les valeurs possibles sont : « Oui » / « Non » / « » (vide).
- « acc. visuel » : information sur l'accessibilité au handicap visuel de l'UA. Les valeurs possibles sont : « Oui » / « Non » / « » (vide).
- « dérogation » : information indiquant si l'UA possède une dérogation ou non. Les deux valeurs possibles sont : « Oui » et « » (vide).

.. image:: etablissement-onglet-ua-listing-ua-en-projet.png


Listing des UA archivés
#######################

Aucune action d'ajout d'une UA n'est possible depuis ce listing.

Un clic sur chaque ligne du listing permet d'accéder à la fiche de visualisation d'une UA.

Le tableau comporte les colonnes suivantes :

- « libellé » : c'est le libellé de l'UA qui permet de l'identifier parmi les autres UA de l'établissement.
- « acc. auditif » : information sur l'accessibilité au handicap auditif de l'UA. Les valeurs possibles sont : « Oui » / « Non » / « » (vide).
- « acc. mental » : information sur l'accessibilité au handicap mental de l'UA. Les valeurs possibles sont : « Oui » / « Non » / « » (vide).
- « acc. physique » : information sur l'accessibilité au handicap physique de l'UA. Les valeurs possibles sont : « Oui » / « Non » / « » (vide).
- « acc. visuel » : information sur l'accessibilité au handicap visuel de l'UA. Les valeurs possibles sont : « Oui » / « Non » / « » (vide).
- « dérogation » : information indiquant si l'UA possède une dérogation ou non. Les deux valeurs possibles sont : « Oui » et « » (vide).
- « état » : c'est l'état de l'UA. Les deux valeurs possibles sont : « en projet » et « validé ».

.. image:: etablissement-onglet-ua-listing-ua-archives.png


.. _etablissements_etablissement_onglet_documents_entrants:

Onglet Documents Entrants
-------------------------

L'onglet "Document Entrants" sur la fiche d'un établissement affiche tous ses documents entrants liés (ainsi que ceux éventuellement liés aux dossiers d'instruction et aux dossiers d'instruction rattachés à l'établissement). Les informations présentées sont :

- le nom du document,
- le type du document (acte, courrier de l'explotant, ...),
- la date de création du document,
- la date de réception du document,
- la date d'émission du document,
- la date butoir du document,
- le statut du document (en cours, qualifié, ...).

.. image:: etablissement-onglet-documents-entrants-listing.png


Les unités d'accessibilité (UA)
===============================

Les unités d'accessibilité (UA) permettent de découper les établissements en plus petites unités au sens de l'accessibilité. Ces unités ont vocation à stocker les données techniques particulières à cette unité au sein de l'établissement.


Le listing des UA
-----------------

.. image:: etablissement-ua-listing.png

Ce listing est un tableau qui fait apparaître toutes les UA qui ne sont pas archivées. Une recherche avancée permet de filtrer les UA qui apparaissent dans le listing. 

Aucune action d'ajout d'une UA n'est possible depuis ce listing.

Un clic sur chaque ligne du listing permet d'accéder à la fiche de visualisation d'une UA.

Le tableau comporte les colonnes suivantes :

- « libellé » : c'est le libellé de l'UA qui permet de l'identifier parmi les autres UA de l'établissement
- « établissement » : même chose que pour le reste des listings
- « adresse » : même chose que pour le reste des listings
- « accessible » : les quatre informations sur l'accessibilité de l'UA sont concaténées dans la même cellule du tableau (auditif : « Oui » / « Non » / « » (vide), mental : « Oui » / « Non » / « » (vide), physique : « Oui » / « Non » / « » (vide), visuel : « Oui » / « Non » / « » (vide))
- « état » : c'est l'état de l'UA. Les deux valeurs possibles sont : « en projet » et « validé »

Lorsqu'un Système d'Information Géographique est paramétré, les icônes en forme de Terre de chaque ligne du tableau permettent d'être redirigé sur le SIG avec la vue centrée sur l'établissement lié à cette UA.

La recherche avancée des UA
---------------------------

.. image:: etablissement-ua-search.png

La recherche avancée permet de filtrer les UA qui apparaissent dans le listing sur les critères suivants :

- « Libellé » : texte libre sur le libellé de l'UA.
- « Établissement » : texte libre sur le code et le libellé de l'établissement. Identique au critère de recherche du même nom dans les recherches avancées des écrans de listing de dossiers.
- « Numéro » : texte libre. Identique au critère de recherche du même nom dans les recherches avancées des écrans de listing de dossiers.
- « Voie » : texte libre. Identique au critère de recherche du même nom dans les recherches avancées des écrans de listing de dossiers.
- « Arrondissement » : liste à choix sur l'arrondissement de l'établissement (valeurs : « 1er », « 2ème », ... Ce sont les valeurs disponibles dans le paramétrage des arrondissements ). Identique au critère de recherche du même nom dans les recherches avancées des écrans de listing de dossiers. Si aucune sélection « Choisir », ce critère n'applique aucun filtre sur le listing.
- « État » : liste à choix sur l'état de l'UA (valeurs : « en projet », « validé »). Si aucune sélection « Choisir », ce critère n'applique aucun filtre sur le listing.
- « Accessible auditif » : liste à choix sur l'information sur l'accessibilité au handicap auditif de l'UA (valeurs : « Oui », « Non »). Si aucune sélection « Choisir », ce critère n'applique aucun filtre sur le listing.
- « Accessible mental » : liste à choix sur l'information sur l'accessibilité au handicap mental de l'UA (valeurs : « Oui », « Non »). Si aucune sélection « Choisir », ce critère n'applique aucun filtre sur le listing.
- « Accessible physique » : liste à choix sur l'information sur l'accessibilité au handicap physique de l'UA (valeurs : « Oui », « Non »). Si aucune sélection « Choisir », ce critère n'applique aucun filtre sur le listing.
- « Accessible visuel » : liste à choix sur l'information sur l'accessibilité au handicap visuel de l'UA (valeurs : « Oui », « Non »). Si aucune sélection « Choisir », ce critère n'applique aucun filtre sur le listing.

La recherche avancée affiche les champs de recherche les uns à la suite des autres sans possibilité de regroupement.


La fiche d'une UA
-----------------

Lorsqu'un Système d'Information Géographique est paramétré et que l'établissement lié à cette UA a été géolocalisé, l'icône en forme de Terre permet d'être redirigé sur le SIG avec la vue centrée sur l'établissement lié.

.. image:: etablissement-ua-view.png


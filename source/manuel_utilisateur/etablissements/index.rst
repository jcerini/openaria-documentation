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


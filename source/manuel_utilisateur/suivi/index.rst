################
Rubrique "Suivi"
################

.. image:: menu-rubrik-suivi.png

La rubrique "Suivi" est divisée en catégories :

- Documents entrants

- Documents générés

- Programmations

- Réunions

- Pilotage


Les réunions
============

Le listing des réunions
-----------------------

Ce listing présente les réunions spécifiques au service de l'utilisateur connecté. 


Ajouter une réunion
-------------------

Le listing des réunions présente un bouton "Ajouter" qui permet d'accéder au formulaire d'ajout d'une nouvelle réunion.

Le code de la réunion est composé automatiquement du code du type de réunion sélectionné concaténé avec la date de la réunion (Exemple : CCS-2014-06-22). Le libellé de la réunion est composé du libellé du type de réunion sélectionné concaténé avec la date de la réunion (Exemple : Réunion Plénière CCS du 24/06/2014). Lors de la création de la réunion, les données présentes dans le paramétrage du type de réunion sont récupérées automatiquement dans le formulaire de création (heure, lieu, ...).


Gérer l'ordre du jour de la réunion
-----------------------------------

L'ordre du jour est composé de la liste des dossiers dont les instances présentes vont discuter pendant la réunion. Il y a un unique ordre du jour par réunion. Si le type de réunion contient plusieurs catégories, alors cette liste est groupée par catégorie. Depuis l'écran de gestion de la réunion, plusieurs actions sont disponibles pour la composition de l'ordre du jour.


Réunion
#######

Cet écran présente un listing de toutes les demandes de passage qui ont été planifiées à la réunion sur laquelle on se trouve, groupées par catégorie.


Planifier
#########

Cet écran présente un listing des dossiers pressentis, ce sont toutes les demandes de passage qui n'ont été planifiées à aucune réunion mais dont le type correspond au type de la réunion sur laquelle on se trouve. Des cases à cocher permettent de sélectionner les demandes de passage que l'on souhaite planifier/ajouter à l'ordre du jour. En cliquant sur le bouton de validation, le traitement est effectué sauf si la demande de passage n'est plus disponible. Dans les deux cas un message indique à l'utilisateur le résultat du traitement.

Pour aider à la saisie des dossiers à planifier, une action permet de sélectionner tous les éléments du listing (cocher toutes les cases à cocher) en un seul clic et un formulaire de recherche permet de filtrer le listing sur :

- une période pour la date souhaitée (du ... au ...),
- la catégorie.


Déplanifier
###########

Cet écran présente un listing des demandes de passage qui ont été planifiées pour la réunion sur laquelle on se trouve. Des cases à cocher permettent de sélectionner les demandes de passage que l'on souhaite retirer de l'ordre du jour. En cliquant sur le bouton de validation, le traitement est effectué sauf si un retour d'avis est déjà saisi dans la demande de passage. Dans les deux cas un message indique à l'utilisateur le résultat du traitement. Pour aider à la saisie des dossiers à déplanifier, une action permet de sélectionner tous les éléments du listing (cocher toutes les cases à cocher) en un seul clic.


Planifier nouveau
#################

Cet écran permet de planifier directement un ou des dossiers d'instruction à la réunion sur laquelle on se trouve sans créer manuellement au préalable une demande de passage sur le ou les dossiers d'instruction concernés. Trois choix de planification directe sont possibles : 

- programmation : planifie tous les dossiers d'instruction correspondant aux visites présente dans une programmation. Il suffit de sélectionner : la programmation (parmi la liste des programmations passées qui n'ont pas déjà été planifiées pour une autre réunion) et la catégorie (dans laquelle on souhaite insérer ces demandes de passage).

- réunion : planifie tous les dossiers d'instruction présents dans une réunion. Il suffit de sélectionner : la réunion (parmi la liste des réunions clôturées qui ne sont pas des réunions de commission et qui n'ont pas déjà été planifiées pour une autre réunion) et la catégorie (dans laquelle on souhaite insérer ces demandes de passage).

- dossier : planifie le dossier d'instruction correspondant au code du dossier de coordination ou du dossier d'instruction saisi. Il suffit de saisir le code du dossier de de sélectionner la catégorie (dans laquelle on souhaite insérer cette demande de passage).


Numéroter
#########

Cette action permet de déclencher la numérotation de l'ordre du jour, c'est-à-dire numéroter la liste des demandes de passage planifiées à partir de 1. Une fois que la numérotation a été déclenchée, tout nouveau dossier prendra le numéro suivant. Un dossier retiré de l'ordre du jour laissera un vide dans la numérotation. La numérotation initiale se fait par catégorie selon l'ordre défini dans le paramétrage du type de réunion.



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


Tous les dossiers
#################

(:menuselection:`Dossiers --> DC (Coordination) --> Tous les dossiers`)

Ce listing présente tous les dossiers de coordination.


Ajouter un nouveau DC
---------------------

(:menuselection:`Dossiers --> DC (Coordination) --> Nouveau dossier`)


La fiche du dossier de coordination (DC)
----------------------------------------

Onglet DC Parents
#################


Onglet Documents entrants
#########################


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


La fiche du dossier d'instruction (DI)
--------------------------------------


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


Onglet PV
#########


Onglet Documents entrants
#########################


Onglet Documents générés
########################


Onglet Réunions
###############


Onglet Visites
##############




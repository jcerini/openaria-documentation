.. _module_filestorage:

####################
Module 'filestorage' 
####################

Dans l'application openARIA, lorsqu'un document a vocation à être consulté ultérieurement, il doit être stocké de manière pérenne. Par défaut, c'est un système de stockage unique qui est un répertoire présent à la racine de l'application sur le système de fichiers du serveur.

C'est le module 'filestorage' qui est en charge de réaliser cette opération. Il est composé d'un abstracteur et d'un ensemble de connecteurs (aussi appelés plugins). Ces derniers respectent l'API de l'abstracteur. Le connecteur par défaut est 'filestorage_filesystem' présent dans le framework openMairie.

http://openmairie.readthedocs.io/projects/omframework/fr/latest/reference/filestorage.html

Le stockage du document est composé du fichier en lui-même mais aussi d'un ensemble d'informations permettant éventuellement d'utiliser le fichier en consultation depuis une autre application qu'openARIA (par exemple dans une GED). On appelle ces informations les métadonnées.


Les fichiers stockés
####################


- Logo [om_logo.fichier]

  - Titre : Logo <LIBELLE>
  - Description : logo
  - Origine : téléversé
  - Stockage à l'ajout du fichier
  - Mise à jour à chaque mise à jour du champ fichier

- Document généré finalisé [courrier.om_fichier_finalise_courrier]

  - Titre : Établissement <CODE> - Dossier <CODE DC ou CODE DI> - <MODELE>
  - Description : document généré finalisé
  - Origine : généré
  - Stockage à la finalisation de l'édition
  - Mise à jour à chaque refinalisation de l'édition
  - Mise à jour des métadonnées à chaque modification de l'enregistrement (triggermodifierapres)

- Document généré numérisé signé [courrier.om_fichier_signe_courrier]

  - Titre :  Établissement <CODE> - Dossier <CODE DC ou CODE DI> - <MODELE> (signé)
  - Description : document généré numérisé signé
  - Origine : téléversé
  - Stockage à l'ajout du fichier
  - Mise à jour à chaque mise à jour du champ fichier
  - Mise à jour des métadonnées à chaque modification de l'enregistrement (triggermodifierapres)

- Document entrant numérisé [piece.uid]

  - Titre :  Établissement <CODE> - Dossier <CODE DC ou CODE DI> - <TYPE>
  - Description : document entrant numérisé
  - Origine : téléversé
  - Stockage à l'ajout du fichier
  - Mise à jour à chaque mise à jour du champ fichier
  - Mise à jour des métadonnées à chaque modification de l'enregistrement (triggermodifierapres)

- Procès verbal numérisé ajouté [proces_verbal.om_fichier_signe]

  - Titre :  Établissement <CODE> - Dossier <CODE DC ou CODE DI> - procès verbal
  - Description : procès verbal numérisé ajouté
  - Origine : téléversé
  - Stockage à l'ajout du fichier
  - Mise à jour à chaque mise à jour du champ fichier

- Ordre du jour finalisé [reunion.om_fichier_reunion_odj]

  - Titre : (<CODE>) <TYPE> du <DATE> - ordre du jour
  - Description : ordre du jour de réunion finalisé
  - Origine : généré
  - Stockage à la finalisation de l'édition
  - Mise à jour à chaque refinalisation de l'édition

- Compte rendu global finalisé [reunion.om_fichier_reunion_cr_global]

  - Titre : (<CODE>) <TYPE> du <DATE> - compte rendu global
  - Description : compte rendu global de réunion finalisé
  - Origine : généré
  - Stockage à la finalisation de l'édition
  - Mise à jour à chaque refinalisation de l'édition

- Compte rendu global numérisé signé [reunion.om_fichier_reunion_cr_global_signe]

  - Titre : (<CODE>) <TYPE> du <DATE> - compte rendu global (signé)
  - Description : compte rendu global de réunion numérisé signé
  - Origine : téléversé
  - Stockage à l'ajout du fichier
  - Mise à jour à chaque mise à jour du champ fichier

- Ensemble des comptes rendus individuels numérisés signés [reunion.om_fichier_reunion_cr_par_dossier_signe]

  - Titre : (<CODE>) <TYPE> du <DATE> - compte rendu par dossier (signé)
  - Description : ensemble des comptes rendus de réunion individuels numérisés signés
  - Origine : téléversé
  - Stockage à l'ajout du fichier
  - Mise à jour à chaque mise à jour du champ fichier

- Documents numérisése [piece.uid]

    - Titre : Nom du fichier
    - Stockage à l'ajout du fichier

Les métadonnées
###############


+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Clé                                  | Description                                                                                                                                                                |
+======================================+============================================================================================================================================================================+
| filename                             | Nom du fichier. Exemple : "nomdufichier.pdf" ou "nomdufichier.png".                                                                                                        |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| size                                 | Taille du fichier en octets. Exemple : "3254" ou "15124".                                                                                                                  |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| mimetype                             | Type MIME du fichier. Exemple : "application/pdf" ou "image/png".                                                                                                          |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| application                          | Nom de l'application. La valeur est "openARIA".                                                                                                                            |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| titre                                | Titre permettant d'identifier le document (spécifique à chaque champ fichier). Exemple : "Établissement T1234 - Dossier VPS-VISIT-13211-SI - Courrier simple".             |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| description                          | Description générique du document. Exemple : "ordre du jour de réunion finalisé".                                                                                          |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| origine                              | Origine du document. La valeur est "généré" si le document est généré par openARIA et la valeur est "téléversé" si le document est téléversé par l'utilisateur.            |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| code_reunion                         | Code de la réunion. Exemple : "CCS-PLEN-2016-07-20".                                                                                                                       |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| date_reunion                         | Date de la réunion au format AAAA-MM-JJ. Exemple : "2015-12-31".                                                                                                           |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| type_reunion                         | Libellé du type de réunion. Exemple : "Commisson Communale de Sécurité".                                                                                                   |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| commission                           | Marqueur indiquant si la réunion est une commission ou non. La valeur est "true" si c'est le cas et "false" si ce n'est pas le cas.                                        |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| etablissement_code                   | Code de l'établissement. Exemple : "T3556".                                                                                                                                |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| etablissement_libelle                | Libellé de l'établissement. Exemple : "MATERNELLE LES CANTARELLES".                                                                                                        |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| etablissement_siret                  | Numéro de SIRET de l'établissement au format "sans espace". Exemple : "00011122233333".                                                                                    |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| etablissement_referentiel            | Marqueur indiquant si l'établissement est référentiel ou non. La valeur est "true" si c'est le cas et "false" si ce n'est pas le cas.                                      |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| etablissement_exploitant             | Prénom et nom de l'exploitant. Exemple : "Paul DURAND".                                                                                                                    |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| etablissement_adresse_numero         | Numéro de l'adresse de l'établissement.                                                                                                                                    |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| etablissement_adresse_mention        | Mention de l'adresse de l'établissement.                                                                                                                                   |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| etablissement_adresse_voie           | Libellé de la voie de l'adresse de l'établissement.                                                                                                                        |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| etablissement_adresse_cp             | Code postal de l'adresse de l'établissement.                                                                                                                               |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| etablissement_adresse_ville          | Ville de l'adresse de l'établissement.                                                                                                                                     |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| etablissement_adresse_arrondissement | Arrondissement de l'adresse de l'arrondissement. Exemple : "6ème".                                                                                                         |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| etablissement_ref_patrimoine         | Références patrimoines de l'établissement. Exemple : "120;90".                                                                                                             |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| dossier_coordination                 | Libellé du dossier de coordination. Exemple : "VPS-VISIT-13211".                                                                                                           |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| dossier_instruction                  | Libellé du dossier d'instruction. Exemple : "VPS-VISIT-13211-SI".                                                                                                          |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| signataire                           | Prénom et nom du signataire. Exemple : "Jacques DURAND".                                                                                                                   |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| signataire_qualite                   | Qualité du signataire. Exemple : "Adjoint délégué au Maire aux ERP".                                                                                                       |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| date_signature                       | Date de signature. Exemple : "2015-12-31".                                                                                                                                 |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| arrete_numero                        | Numéro de l'arrêté. Exemple : "2016_01234_ERP".                                                                                                                            |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| arrete_reglementaire                 | Marqueur indiquant si l'arrêté est réglementaire ou non. La valeur est "true" si c'est le cas et "false" si ce n'est pas le cas.                                           |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| arrete_notification                  | Marqueur indiquant si l'arrêté est soumis à notification individuelle ou non. La valeur est "true" si c'est le cas et "false" si ce n'est pas le cas.                      |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| arrete_date_notification             | Date de notification de l'arrêté (retour de l'AR du document). Exemple : "2015-12-31".                                                                                     |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| arrete_publication                   | Marqueur indiquant si l'arrêté est soumi à publication au recueil des actes administratifs ou non. La valeur est "true" si c'est le cas et "false" si ce n'est pas le cas. |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| arrete_date_publication              | Non renseigné.                                                                                                                                                             |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| arrete_temporaire                    | Marqueur indiquant si l'arrêté prévoit explicitement une date d'expiration ou non. La valeur est "true" si c'est le cas et "false" si ce n'est pas le cas.                 |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| arrete_expiration                    | Date d'expiration (date de notification + délai de la décision). Exemple : "2015-12-31".                                                                                   |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| arrete_date_controle_legalite        | Date de retour du contrôle de légalité. Exemple : "2015-12-31".                                                                                                            |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| arrete_nature_acte                   | Nature juridique de l'arrêté. La valeur est soit "Arrêtés Réglementaires" sinon "Arrêtés Individuels".                                                                     |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| arrete_nature_acte_niv1              | Code du texte de premier niveau du domaine juridique de l'arrêté. Exemple : "9 Autres domaines de competences".                                                            |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| arrete_nature_acte_niv2              | Code du texte de second niveau du domaine juridique de l'arrêté. Exemple : "9.1 Autres domaines de competences des communes".                                              |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| pv_erp_numero                        | Numéro du procès verbal. Exemple : "SI-2016/00001".                                                                                                                        |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| pv_erp_nature_analyse                | Nature de l'analyse. Exemple : "Visite de réception sécurité".                                                                                                             |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| pv_erp_reference_urbanisme           | Code du dossier d'autorisation urbanisme. Exemple : "PC0130551600001".                                                                                                     |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| pv_erp_avis_rendu                    | Avis rendu. Exemple : "FAVORABLE".                                                                                                                                         |
+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+




.. _web_services_rest:

############
Web Services
############

Les web services d'openADS sont RESTful. Les retours sont au format JSON, encodés en UTF-8.

.. _web_services_ressource_maintenance:

Ressource "maintenance"
#######################


==========================================================
Importation des documents numérisés
==========================================================

.. http:post:: /openads/services/rest_entry.php/maintenance

   **Exemple de requête** :

   .. sourcecode:: http
      
      POST /openads/services/rest_entry.php/maintenance HTTP/1.1
      Host: localhost

      {
        "module": "import",
        "data": {
          "service": "ACC"
          // Ces deux paramètres sont facultatifs
          "Todo" : "chemin_dossier_source", // ou "" pour utiliser le chemin dans la configuration
          "Done" : "chemin_dossier_destination" // ou "" pour utiliser le chemin dans la configuration   
        }
      }


==========================================================
Purge des documents numérisés
==========================================================

.. http:post:: /openads/services/rest_entry.php/maintenance

   **Exemple de requête** :

   .. sourcecode:: http
      
      POST /openads/services/rest_entry.php/maintenance HTTP/1.1
      Host: localhost

      {
        "module": "purge",
        "data": {
          // Ces trois paramètres sont facultatifs
          "dossier": "chemin_dossier", // ou "" pour utiliser le chemin dans la configuration
          "nombre_de_jour": nombre_de_jour, // ou "" pour n'imposer aucunes limites,
          "dossier_vide" : true // ou false pour supprimer le répertoire si celui-ci est vide.
        }
      }

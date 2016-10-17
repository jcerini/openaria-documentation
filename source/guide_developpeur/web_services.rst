.. _web_services_rest:

############
Web Services
############

Les web services d'openARIA sont RESTful. Les retours sont au format JSON, encodés en UTF-8.


.. _web_services_ressource_maintenance:

Ressource "maintenance"
#######################

================================================
Synchronisation des utilisateurs via un annuaire
================================================

.. http:post:: /openaria/services/rest_entry.php/maintenance

   **Exemple de requête** :

   .. sourcecode:: http
      
      POST /openaria/services/rest_entry.php/maintenance HTTP/1.1
      Host: localhost

      {
        "module": "user"
      }

   **Exemple de réponse** :

   .. sourcecode:: http

      HTTP/1.1 500 Internal Server Error
      Content-Type: text/javascript

      {
        "http_code": 500,
        "http_code_message": "500 Internal Server Error",
        "message": "Erreur interne"
      }

   :statuscode 200: Tout s'est déroulé correctement.
   :statuscode 500: Erreur interne.


=========================
Synchronisation des voies
=========================

.. http:post:: /openaria/services/rest_entry.php/maintenance

   **Exemple de requête** :

   .. sourcecode:: http
      
      POST /openaria/services/rest_entry.php/maintenance HTTP/1.1
      Host: localhost

      {
        "module": "voies",
        "data" : {
            "file_name" : "/tmp/synchronsization_voies.csv"
        }
      }


========================
Numérisation automatique
========================

.. http:post:: /openaria/services/rest_entry.php/maintenance

   **Exemple de requête** :

   .. sourcecode:: http
      
      POST /openaria/services/rest_entry.php/maintenance HTTP/1.1
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


===============================
Synchronisation des contraintes
===============================

.. http:post:: /openaria/services/rest_entry.php/maintenance

   **Exemple de requête** :

   .. sourcecode:: http
      
      POST /openaria/services/rest_entry.php/maintenance HTTP/1.1
      Host: localhost

      {
        "module": "contraintes"
      }


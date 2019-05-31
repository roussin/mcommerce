# Mcommerce

- L'application Mcommerce est composée de 3 Microservices :
  * Microservice-produits -> gestion des produits
  * Microservice-commandes -> gestion des commandes
  * Microservice-paiement -> gestion des achats
  
 - Les Edges Microservices :
   * Les Edges Microservices s'occupent principalement de l'orchestration des Microservices métier contenant la logique de 
     l'application.
   * Les Edge Microservices les plus populaires sont ceux publiés et utilisés par Netflix pour sa plateforme. 
   * Ils sont en grande partie regoupés sous Spring Cloud et disposent de fonctionnalités pour fonctionner ensemble.
     
 - Faire communiquer les Microservices grâce à Feigne :
   * Feign est un outil permettant de faire communiquer les Microservices très simplement entre eux, en générant 
     automatiquement les requêtes HTTP adéquates à partir de classes appelées "proxis".
     
 - Externaliser la configuration des Microservices :
   * Les fichiers de configuration des Microservices peuvent être externalisés vers un dépot GIT, par exemple grâce à SpringBoot Config. 
   * Cet Edge Microservice va alors récupérer la dernière version de chaque fichier de configuration et la servir au Microservice correspondant.
   * Pour forcer l'actualisation des données d'un fichier de configuration dans un Microservice, il suffit d'envoyer une requête POST
     vers l'endpoint/refresh exposé par Actuator.
   
  - Rendez les Microservices découbvrable grâce à Eureka :
    * Eureka est un autre Edge Microservice qui permet de garder un registre de toutes les instances disponibles des Microservices.
    * Chaque Microservice qui intègre Eureka ira s'enregistrer à chaque démarrage ou lancement d'une nouvelle instance.
    * Eureka vérifie ensuite régulièrement que les Microservices sont toujours disponibles afin de mettre à jour son registre.
      
 - Equilibrer la charge de l'application grâce à Ribbon :
   * Ribbon est un équilibreur de charge côté client. Une fois intégré dans un Microservice, il est capable de communiquer
     automatiquement avec Eureka afin de choisir l'instance à appeler d'un Microservice donné. Un algorythme s'occupe ainsi de
     répartir les requêtes sur toutes les instances disponible.
     
 - Créer une API Gateway pour l'application ZUUL :
   * ZUUL va se positionner comme point d'entré unique de notre application. Ainsi quand ClientUi, par exemple, voudra
     appeler les Microservices, il passera par ZUUL (dispatch, modifie, et applique des filtres, des règles à ces requêtes)
   * ZUUL permet de réaliser des opérations communes à tous les Microservices (Sécurisation de l'accès, mise en place d'un
     nombre d'appels limite à l'API, transformation des requêtes afin de les enrichir avant qu'elles n'atteignent les 
     Microservices cibles, etc.

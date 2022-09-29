# Nous allons découper le traitement en trois lots :

  1-Récupération des données Alpha Vantage.
  
  2-Découpage des données et envoi vers un broker Kafka.
  
  3-Récupération des données et stockage dans une base de données MongoDB.
  
# Réalisation UI 1ère Etape:	
- Connecter vous à l'interface graphique de NiFi. Allez sur :

   https://ipadresse:port/nifi
   
-Vous serez dirigé vers la page de Login de NiFi:

![nifi](https://user-images.githubusercontent.com/78825764/193147697-1b9ee848-c8c9-42da-88b6-98e83ab4e6e4.PNG)

  Entrer votre nom d'utilisateur et mot de passe

- Une fois connecté à votre interface vous devez créer 3 différents process group

-Insérez l'icône du Process Group et faites-la glisser pour créer un nouveau Process Group:

![process_group](https://user-images.githubusercontent.com/78825764/193155523-9dc14871-1799-4aaf-8bef-cc0463eaefb7.PNG)

-Donner pour chaque Process Group un nom (1-AlphaVantage Download ; 2-push to kafka ; 3-kafka Consumer to MongoDb)

![add_process](https://user-images.githubusercontent.com/78825764/193156172-2f58be31-51cb-4ac9-b4e5-35dda96a5ae6.PNG)

![process](https://user-images.githubusercontent.com/78825764/193156594-d4cfa7cd-a5fb-48b1-9735-e3cd128a266e.PNG)

-Maintenant on va travailler sur le Process Groupe AlphaVantage Download , accédez au process group avec un double clique . 

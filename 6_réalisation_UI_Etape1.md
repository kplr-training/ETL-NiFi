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

- Maintenant on va travailler sur le Process Groupe AlphaVantage Download , accédez au process group avec un double clique .

![p](https://user-images.githubusercontent.com/78825764/193159163-7456956c-e1f9-40c4-9e5b-5f7698cfea60.PNG)
- Ajouter le Truststore filename /home/ec2-user/cacerts.jks 

- Entrez le password changeit dans le Truststore Password 

-Ensuite on va glisser l'icone de processor 


![b](https://user-images.githubusercontent.com/78825764/193159262-452364ad-5ba5-4667-a881-cf14bee04724.png)

-et on va créer le premier prossecor nommé Getthttp : Apple Stock

![addproc](https://user-images.githubusercontent.com/78825764/193159722-154b95e1-5aef-4853-af32-28c80fea1f32.PNG)

  -Filtrez en entrant GetHttp
  
  ![F](https://user-images.githubusercontent.com/78825764/193159995-fb9b8ac9-36a3-47b7-b5c0-9d8b5bb595f5.png)
    
 puis cliquez sur le bouton add



![GetHTTP](https://user-images.githubusercontent.com/78825764/193209167-4b3a769c-12d3-4a2d-a1b8-7eec98cdfbca.PNG)
 
 -Ensuite nous allons réalisé quelques configurations en faisant double clique le processor GetHTTP 
 
        
  - Vous pouvez renomer votre processor en GetHTTP: IBM Stock en cliquant sur settings
 



![z](https://user-images.githubusercontent.com/78825764/193210264-7d894d2a-afeb-427c-bd36-1365cc40525b.PNG)

  - Ensuite , cliquez sur properties
  
  ![pro](https://user-images.githubusercontent.com/78825764/193211015-aef65fa6-6263-4d95-850c-82a2b581e4b1.PNG)
  
  ![p](https://user-images.githubusercontent.com/78825764/193217500-8fc0cfb8-4659-4653-9940-651a84974b75.PNG)

  - On va chercher notre URL pour pouvoir accéder au données de AlghaVantage .Allez sur https://www.alphavantage.co/ et Appuyez sur GET YOUR FREE API KEY FOR FREE
  - Entrez vos données et appuyez sur GET FREE API KEY et vous allez avoir votre API KEY
     
![API](https://user-images.githubusercontent.com/78825764/193216923-e11b27d0-7776-4b8b-9220-c7573484c878.PNG)
  - Maintenant que you avez votre API on va entrer l'URL https://www.alphavantage.co/query?function=TIME_SERIES_INTRADAY&symbol=AAPL&interval=1min&apikey=YOURAOIKEY&datatype=csv  et le filename intraday_5min_AAPL.csv
  
  ![F](https://user-images.githubusercontent.com/78825764/193219225-22b86fad-ebda-47cf-a017-e7cee90e2ed5.png)

  - Ensuite appuyez sur SSL Context Service > Create new service > Compatible Controller Services >StandardSSLContextService 1.17.0 > create
   
  
  
  ![F](https://user-images.githubusercontent.com/78825764/193219872-f93ceaf9-8da9-469b-bf03-432bf080930d.png)
  

![F](https://user-images.githubusercontent.com/78825764/193220732-7bf0b551-4d37-4d08-a35e-42a033027401.png)


![F](https://user-images.githubusercontent.com/78825764/193221722-7db7bd8a-62f9-4b28-ba75-6ae2edc1ee2c.png)

- Cliquez sur la flèche 



![F](https://user-images.githubusercontent.com/78825764/193222554-4e0832ae-d38f-4ad3-9c00-e689a9cd8fbd.png)

- Cliquez sur Yes


![F](https://user-images.githubusercontent.com/78825764/193222725-2399018b-c7a1-479a-83b2-daf188b4e588.png)

- Cliquez sur l'icone de paramètre 


![F](https://user-images.githubusercontent.com/78825764/193223530-b779f5db-592e-47c4-96d8-02d80917ad7b.png)

![F](https://user-images.githubusercontent.com/78825764/193225234-8acbfe0c-5dd1-40b6-88f5-8d6f20bff3e8.png)

- Modifiez le paramètre Truststore type no value > LKS

![F](https://user-images.githubusercontent.com/78825764/193225694-63f370de-8023-4ad0-a68f-d8fc7f1499fd.png)

- Ajouter le Truststore Filename /home/ec2-user/cacerts.jks
- Ajouter le Truststore Password changeit 
![F](https://user-images.githubusercontent.com/78825764/193227831-105915ce-cc31-4c35-b2fe-fbbacba48f72.png)

![F](https://user-images.githubusercontent.com/78825764/193228993-dfc8f1ee-31bc-407e-9b28-5a9dcba3ab21.png)

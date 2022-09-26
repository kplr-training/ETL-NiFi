# Réalisation dans l'UI
- dans le  navigateur, ouvrir l'addresse http://votre.adresse.ip.linux:8443/nifi , l'interface NiFi s'ouvre
- se connecter : login :            password : 
- Une  interface pour créer les flux  s'affiche :
![68747470733a2f2f692e6962622e636f2f7853584e4735762f53637265656e73686f742d323032312d30322d31382d4e692d46692d466c6f772e706e67](https://user-images.githubusercontent.com/73080397/192320163-16bbd029-f290-4d57-be99-35143d0100c4.png)




Nous allons découper le traitement en trois lots :
1. Récupération des données Alpha Vantage.
2. Découpage des données et envoi vers un broker Kafka.
3. Récupération des données et stockage dans une base de données MongoDB.

![Nifi workshop](https://i.ibb.co/6H11VgZ/Screenshot-2021-02-18-Ni-Fi-Flow-00.png)


## Etape 1 : Récupération des données Alpha Vantage.
A  la fin de cette étape nous devons obtenir le process groupe de l'image dessus :
![Nifi workshop](https://i.ibb.co/k9J8kdz/Screenshot-2021-02-18-Ni-Fi-Flow-01.png)
- glisser l'icône "process group" vers le milieu de l'écran
- process group name : AlphaVantage Download
- double-cliquer dessus, la page du process group à construire apparait
1. Appeler le service Alpha Vantage.</br>

- glisser l'icône "processor" 
- ajouter le process "GetHTTP"
- double cliquer dessus et aller dans "properties"
- mettre les champs suivants :
      
      
      

Prévoir un écart de 30 secondes entre deux appels. Faut pas oublier que le compte est gratuit et ne permet pas plus de 5 appels par minute.

![Nifi workshop](https://i.ibb.co/4gkR7Qx/Screenshot-2021-02-18-Ni-Fi-Flow-02.png)

2. Mettre à jour le nom du fichier en sortie avec un nom unique basé sur le current time :

![Nifi workshop](https://i.ibb.co/vwJkJq3/Screenshot-2021-02-18-Ni-Fi-Flow-03.png)

3. Stocker les fichiers csv dans le dossier de sortie :

![Nifi workshop](https://i.ibb.co/tcjxJRz/Screenshot-2021-02-18-Ni-Fi-Flow-04.png)

On voit que les fichiers sont déposés dans le dossier défini dans le processor :

![Nifi workshop](https://i.ibb.co/ZhRgrdx/Screenshot-from-2021-02-18-14-28-00.png)
- glisser l'icone "Process group" 

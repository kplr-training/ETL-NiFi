# Préparation du certificat Alpha Vantage:	
- télécharger le certificat de Alpha Vantage : 

    - se rendre sur le site de [Alpha Vantage ](https://www.alphavantage.co/),  remarquer que celui-ci est protégé par le protocole HTTPS
    - cliquer sur le bouton du cadenas "afficher les informations à propoos  du site"
    - la  connexion est sécurisée > certificat valide > détails > exporter le certificat selectionné.
    - enregistrer le certificat sur votre machine windows/mac, maintenant il faut le copier dans la machine Amazon Linux !
- copier le fichier du certificat à partir de votre machine vers la machine Amazon Linux : 
    - se rendre sur windows cmd/ macOS terminal
    - se rendre sur le repertoire où vous avez mis le certificat par exemple `cd downloads`
    - copier en utilisant la commande scp `scp -i [clé de connexion] [chemin source] [chemin destination]`
    - par exemple : ```scp -i NIFI-2022.pem alphavantage.co.cer ec2-user@ec2-15-236-215-61.eu-west-3.compute.amazonaws.com:/home/ec2-user ```
    - vérifier que le fichier à bien été copié : `ls` vous devriez voir le nom du fichier dans la liste.
- charger le certificat dans un Keystore : mot de passe par défaut du keystore : "changeit"
```
keytool -import -v -trustcacerts -file sni.cloudflaressl.com -alias alphaca -keystore cacerts.jks
```

# Introduction
# Se connecter à l'instance Amazon Linux

- Utiliser l'invite de commande directement si vous êtes sur Windows10
<img src=https://user-images.githubusercontent.com/73080397/182381175-0a91c49a-c047-4d97-9470-6b3f424d2e67.png width="500">
- Ouvrir le terminal si vous êtes sur MacOS

![open-folder-application-terminal](https://user-images.githubusercontent.com/73080397/182381582-8eb3bccb-c9bd-4c4d-acf5-f0e510b748a3.png)

- Vos Credentials et IP respectives vous seront envoyés sur le chat
- Une clé SSH .pem vous sera transmise sur le chat
- username : `ec2-user`
- adresse ip : `adresse ip fournie`
- options de connection : clé ssh ppk
- Se rendre dans le repertoire où vous  avez mis votre fichier pem
  Par exemple, si vous êtes sur windows et que vous l'avez mis dans le dossier téléchargements :
```
cd downloads
```
- et puis connectez-vous à l'instance EC2 :
 ```
ssh -i "cle-ssh.pem" ec2-user@ec2-addresse_ip.compute-1.amazonaws.com
```

![ter](https://user-images.githubusercontent.com/73080397/182382478-19512c71-e9e7-4367-8ed8-8d48ea4063f4.png)

- Si la connexion ne s'établit toujours pas sur Windows, installer [mobaXterm](https://download.mobatek.net/2022020030522248/MobaXterm_Portable_v20.2.zip)
- si vous passez par MobaXterm ou Putty, vous devez convertir la clé du format .pem au format .ppk 
  voir ce mini [tuto](https://stackoverflow.com/questions/3190667/convert-pem-to-ppk-file-format)). 
  (**attention**, cette operation est souvent très hasardeuse au vu des différentes versions compatibles). 

Pour vérifier votre version de Linux (Centos, Debian ou Amazon Linux):
 ```
cat /etc/os-release
```

# Télécharger et installer Java 11.0.6
- se connecter à l'instance Amazon Linux
- installer java-openjdk11 :
```
sudo amazon-linux-extras install java-openjdk11
```
- trouver et copier le chemin d'installation direct de java
```
readlink -f $(which java)
```
- définir la variable d'environnement JAVA_HOME dans le fichier .bashrc
    - ouvrir le fichier .bashrc
    - éditer
- vérifier l'installation de java :
```
java -version
```
- vérifier la variable JAVA_HOME:
```
echo $JAVA_HOME
```


# APACHE ZOOKEEPER:
- lancer zookeeper :  
```
sudo su
./bin/zookeeper-server-start.sh config/zookeeper.properties > zk.log &
```


# APACHE NIFI 1.17.0:
- se rendre dans [la page de télécchargement de NiFi](https://nifi.apache.org/download.html)
- sources > Binaries >  copier  le premier lien apparu dans la page, celui-ci ressemble à https://dlcdn.apache.org/nifi/1.17.0/nifi-1.17.0-bin.zip
- télécharger le fichier zip : 
```
wget https://dlcdn.apache.org/nifi/1.17.0/nifi-1.17.0-bin.zip
```
- dézipper le fichier
```
tar -xvf nifi-1.17.0-bin.zip
```
- se rendre dans le  repertoire nifi-1.17.0
```
cd nifi-1.17.0
```
- définir les propriétés dans le fichier nifi.properties 
    - ouvrir le fichier nifi.properties avec l'éditeur de texte : 
    ```
    vi /home/ec2-user/nifi-1.17.0/conf/nifi.properties
    ```
    - insérer les éléments suivants: (i pour insérer/ :wq pour enregistrer et quitter)
    ```
    nifi.web.https.host=0.0.0.0
    nifi.web.https.port=8443
    nifi.web.https.network.interface.default=
    nifi.web.https.application.protocols=http/1.1
    nifi.web.jetty.working.directory=./work/jetty
    nifi.web.jetty.threads=200
    nifi.web.max.header.size=16 KB
    nifi.web.proxy.context.path=
    nifi.web.proxy.host=15.236.215.61:8443
    ```
    
- lancer NiFi
```
bin/nifi.sh start
```


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

# Réalisation dans l'UI
- dans le  navigateur, ouvrir l'addresse http://votre.adresse.ip.linux:8443/nifi , l'interface NiFi s'ouvre
- se connecter : login :            password : 
- Une  interface pour créer les flux  s'affiche


- glisser l'icone "Process group" 


# Préparation de la base de données MongoDB 





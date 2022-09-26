
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

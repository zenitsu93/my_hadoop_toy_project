# Instructions pour configurer votre environnement Hadoop avec Docker
## Télécharger et configurer Hadoop avec Docker

### Télécharger l'image Docker

Depuis un terminal, téléchargez l’image Docker que j’ai stockée sur Docker Hub :

```sh
docker pull zenitsu93/spark-hadoop:v1
```

### Créer les conteneurs

#### Créer un réseau Docker

Créez un réseau qui permettra de relier les trois conteneurs :

```sh 
docker network create --driver=bridge hadoop
```

#### Démarrer les conteneurs

Démarrez les conteneurs à partir de l’image téléchargée :

```sh
docker run -itd --net=hadoop -p 50070:50070 -p 8088:8088 -p 8080:8080 -p 7077:7077 -p 16010:16010 --name hadoop-master --hostname hadoop-master zenitsu93/spark-hadoop:v1

docker run -itd -p 8042:8042 --net=hadoop --name hadoop-slave1 --hostname hadoop-slave1 zenitsu93/spark-hadoop:v1

docker run -itd -p 8043:8042 --net=hadoop --name hadoop-slave2 --hostname hadoop-slave2 zenitsu93/spark-hadoop:v1
```

### Utiliser le conteneur hadoop-master

Entrez dans le conteneur `hadoop-master` pour commencer à l’utiliser :

```sh
docker exec -it hadoop-master bash
```


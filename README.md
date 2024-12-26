# Instructions pour configurer votre environnement Hadoop avec Docker

## Étape 1: Télécharger l'image Docker

Depuis un terminal, téléchargez l’image Docker que j’ai stockée sur Docker Hub :

```sh
docker pull zenitsu93/spark-hadoop:v1
```

## Étape 2: Créer les conteneurs

### Créer un réseau Docker

Créez un réseau qui permettra de relier les trois conteneurs :

```sh 
docker network create --driver=bridge hadoop
```

### Démarrer les conteneurs

Démarrez les conteneurs à partir de l’image téléchargée :

```sh
docker run -itd --net=hadoop -p 9870:9870 -p 8088:8088 -p 7077:7077 -p 16010:16010 -p 9999:9999 --name hadoop-master --hostname hadoop-master zenitsu93/spark-hadoop:v1

docker run -itd -p 8040:8042 --net=hadoop --name hadoop-slave1 --hostname hadoop-slave1 zenitsu93/spark-hadoop:v1

docker run -itd -p 8041:8042 --net=hadoop --name hadoop-slave2 --hostname hadoop-slave2 zenitsu93/spark-hadoop:v1
```

## Étape 3: Utiliser le conteneur hadoop-master

Entrez dans le conteneur `hadoop-master` pour commencer à l’utiliser :

```sh
docker exec -it hadoop-master bash
```
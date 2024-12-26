# Depuis un Terminal, téléchargez l’image docker que j’ai stocké sous dockerhub

```sh
docker pull zenitsu93/spark-hadoop:v1
```

# Créez les 3 contenaires à partir de l’image téléchargée. Pour cela:

## Créez un réseau qui permettra de relier les trois contenaires:

```sh 
docker network create --driver=bridge hadoop
```

## Démarrez les conteneurs:

```sh
docker run -itd --net=hadoop -p 9870:9870 -p 8088:8088 -p 7077:7077 -p 16010:16010 -p 9999:9999 --name hadoop-master --hostname hadoop-master zenitsu93/spark-hadoop:v1

docker run -itd -p 8040:8042 --net=hadoop --name hadoop-slave1 --hostname hadoop-slave1 zenitsu93/spark-hadoop:v1

docker run -itd -p 8041:8042 --net=hadoop --name hadoop-slave2 --hostname hadoop-slave2 zenitsu93/spark-hadoop:v1
```

## Entrez dans le contenaire hadoop-master pour commencer à l’utiliser
```sh
docker exec -it hadoop-master bash
```
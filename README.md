# Documentation Docker – FEUILLE DE TRICHE

## Introduction

**Docker** permet d'exécuter des applications dans des conteneurs, ce qui garantit un environnement cohérent entre le développement, les tests et la production.

##  Prérequis

- Avoir Docker installé : [Installer Docker](https://docs.docker.com/get-docker/)
- Connaissances de base en ligne de commande
- Compte GitHub

## Structure du projet
mon-projet-docker/
├── Dockerfile
├── .dockerignore
├── docker-compose.yml # facultatif
├── README.md
├── requirements.txt # dépendances Python
└── app/
├── main.py # fichier principal Python
└── autres fichiers éventuels


##  Le fichier Dockerfile

Un **Dockerfile** décrit comment construire une image Docker personnalisée.

dockerfile
# Image de base officielle
FROM python:3.11

# Répertoire de travail dans le conteneur
WORKDIR /app

# Copier les fichiers dans le conteneur
COPY . /app

# Installer les dépendances (exigées par requirements.txt)
RUN pip install --no-cache-dir -r requirements.txt

# Démarrer le script principal
CMD ["python", "main.py"]

Explication ligne par ligne :

FROM: démarre à partir d'une image existante (ici Python).

WORKDIR: définit le répertoire de travail dans le conteneur.

COPY: copie les fichiers de ton PC vers le conteneur.

RUN: exécute une commande pendant la construction de l'image.

CMD: commande à exécuter quand le conteneur démarre.



## .dockerignore

__pycache__/
*.pyc
.env
.git

## Commandes Docker de base
# Construction de l'image
docker build -t mon-app .

# Exécution du conteneur
docker run -p 8000:8000 mon-app

# Lister les conteneurs
docker ps

# Arrêter un conteneur
docker stop <container_id>

# Supprimer un conteneur
docker rm <container_id>

# Supprimer une image
docker rmi <image_id>

## docker-compose.yml
version: '3'
services:
  web:
    build: .
    ports:
      - "8000:8000"
    volumes:
      - .:/app
Lancer avec : docker-compose up

##  Nettoyage
docker system prune

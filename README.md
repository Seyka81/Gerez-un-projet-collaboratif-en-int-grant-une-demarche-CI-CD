
# BobApp

**BobApp** est une application web composée d’un front-end en Angular et d’un back-end en Java Spring Boot.  
Le projet est entièrement dockerisé et intègre une pipeline CI/CD avec **GitHub Actions**.

---

## Structure du projet


```
bobapp/
├── front/                # Application Front-end (Angular)
├── back/                 # Application Back-end (Spring Boot)
└── workflows/
  ├── frontend.yml  # CI/CD pour le front
  └── backend.yml   # CI/CD pour le back
```
---

## Démarrage rapide

### Prérequis

- Node.js & npm
- Java 11 & Maven
- Docker
- Git

### Cloner le projet

```bash
git clone https://github.com/Seyka81/Gerez-un-projet-collaboratif-en-int-grant-une-demarche-CI-CD.git
cd bobapp
````

---

## Front-end (Angular)

### Lancer en local

```bash
cd front
npm install
ng s
```

### Lancer les tests

```bash
ng test
```

### Docker

```bash
# Construire l'image ou vous pouvez la pull depuis le docker hub
docker build -t bobapp-front .
docker pull acros05/gerez-un-projet-collaboratif-en-int-grant-une-demarche-ci-cd-frontend:latest

# Lancer le conteneur
docker run -p 8080:8080 --name bobapp-front -d bobapp-front
docker run -p 8080:8080 --name bobapp-front -d acros05/gerez-un-projet-collaboratif-en-int-grant-une-demarche-ci-cd-frontend:latest
```

---

## Back-end (Spring Boot)

### Lancer en local

```bash
cd back
mvn clean install
Puis vous pouvez lancer le projet depuis la class BobappApplication
```

### Lancer les tests

```bash
mvn test
```

### Docker

```bash
# Construire l'image ou vous pouvez la pull depuis le docker hub
docker build -t bobapp-back .
docker pull acros05/gerez-un-projet-collaboratif-en-int-grant-une-demarche-ci-cd-backend:latest

# Lancer le conteneur
docker run -p 8080:8080 --name bobapp-back -d bobapp-back
docker run -p 8080:8080 --name bobapp-front -d acros05/gerez-un-projet-collaboratif-en-int-grant-une-demarche-ci-cd-backend:latest
```

---

## Workflows CI/CD – GitHub Actions

Deux workflows sont définis dans `.github/workflows/` :

### `frontend.yml`

* Installation des dépendances Angular
* Exécution des tests
* Analyse SonarQube (qualité de code & couverture)
* Création & push de l’image Docker vers Docker Hub

### `backend.yml`

* Installation des dépendances maven
* Exécution des tests
* Analyse SonarQube (qualité de code & couverture)
* Création & push de l’image Docker vers Docker Hub

> Le déploiement est conditionné à la réussite de toutes les étapes.

---

## Déploiement

Les images Docker sont automatiquement **buildées et poussées sur Docker Hub** via GitHub Actions, dès que les tests et les analyses qualité sont validés.

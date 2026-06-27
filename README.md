# Nextcloud — Infrastructure Cloud Privé sous Docker

![Dashboard Nextcloud](https://github.com/user-attachments/assets/183eccd7-87ed-4c21-ac53-2adf4295ecf2)

> Déploiement d'une infrastructure cloud privée et souveraine avec **Nextcloud Hub** et **MariaDB**, orchestrée via **Docker Compose** sur Ubuntu Server.

---

## Table des matières

- [Introduction](#introduction)
- [Prérequis & Installation de l'OS](#prérequis--installation-de-los)
- [Installation de Nextcloud](#installation-de-nextcloud)
- [Connexion SSH depuis la machine locale](#connexion-ssh-depuis-la-machine-locale)
- [Installation de Docker](#installation-de-docker)
- [Accès à l'interface Nextcloud](#accès-à-linterface-nextcloud)
- [Conclusion](#conclusion)

---

## Introduction

Nextcloud est une plateforme open-source de productivité et de collaboration **on-premise**, conçue comme alternative souveraine aux solutions cloud grand public (Google Drive, Microsoft 365, Dropbox).

### Avantages

| Critère | Détail |
|---|---|
| **Souveraineté & RGPD** | Contrôle total des données sur infrastructure propre, sans dépendance aux GAFAM |
| **Rentabilité** | Aucun coût de licence par utilisateur ; stockage limité uniquement par le matériel |
| **Flexibilité Docker** | Déploiement conteneurisé isolant les services (Nextcloud / MariaDB), facilitant les mises à jour et la portabilité |
| **Évolutivité** | Écosystème d'applications riche (Talk, suite Office, gestion de tâches) activable en un clic |

### Inconvénients

| Critère | Détail |
|---|---|
| **Maintenance** | Gestion interne obligatoire de la sécurité et des sauvegardes ; risque de perte de données en cas de crash |
| **Contrainte matérielle** | Performances et vitesses de synchronisation directement liées à la bande passante et à la puissance de la machine hôte |

---

## Prérequis & Installation de l'OS

Il vous faut une **machine dédiée** : une VM (Machine Virtuelle) ou un PC inutilisé. Installez ensuite **Ubuntu Desktop** sur cette machine.

- 📖 Guide de création de VM et installation d'Ubuntu Desktop : [yacinehrc/Ubuntu-Desktop](https://github.com/yacinehrc/Ubuntu-Desktop)

---

## Installation de Nextcloud

### 1. Accéder au Terminal

Une fois Ubuntu démarré, ouvrez le menu des applications via l'icône en bas à droite, puis lancez **Terminal**.

![Bureau Ubuntu](https://github.com/user-attachments/assets/1046e6fb-94f2-4d5b-a9e8-e4da200d9b17)

![Ouverture du Terminal](https://github.com/user-attachments/assets/1e685b39-c04b-4cb9-bcf4-e4f4ade73a40)

### 2. Mettre à jour les paquets système

```bash
sudo apt update && sudo apt upgrade -y
```

Saisissez votre mot de passe utilisateur lorsqu'il est demandé.

![Mise à jour des paquets](https://github.com/user-attachments/assets/2f0dc452-cf7c-43dc-b6f2-2fa29739d07e)

![Téléchargement en cours](https://github.com/user-attachments/assets/2fb0f0a4-fbf0-4418-874d-f1e73b344b4a)

### 3. Installer le serveur SSH

SSH n'étant pas installé par défaut sur Ubuntu Desktop, exécutez :

```bash
sudo apt install ssh -y
```

![Installation SSH](https://github.com/user-attachments/assets/c5dea647-0bb7-40f2-a23b-bfee02229e7d)

### 4. Récupérer l'adresse IP de la machine

```bash
clear
ip a
```

Repérez l'entrée `2: ens33`, puis la valeur `inet` — c'est votre adresse IP locale *(ignorez le suffixe `/xx` correspondant au masque de sous-réseau)*.

![Adresse IP](https://github.com/user-attachments/assets/536e8dee-6e41-4b0c-8550-abe6b66c4898)

> **Exemple :** `192.168.35.138`

---

## Connexion SSH depuis la machine locale

Depuis un terminal **PowerShell (Windows)** ou **Bash (Linux/macOS)**, connectez-vous à distance :

```bash
ssh utilisateur@adresse_ip
```

> Remplacez `utilisateur` par votre nom d'utilisateur Ubuntu et `adresse_ip` par l'adresse récupérée à l'étape précédente.

![Commande SSH](https://github.com/user-attachments/assets/aecdf8e8-ef01-4c12-8a4d-eeb3b781e924)

À la première connexion, confirmez l'empreinte de l'hôte en répondant `yes`.

![Confirmation SSH](https://github.com/user-attachments/assets/726d5cc8-f603-4608-b7c2-7242d56cba80)

La connexion est établie lorsque le prompt affiche le même utilisateur que sur la machine Ubuntu.

| Machine | Prompt |
|---|---|
| Ubuntu | ![Prompt Ubuntu](https://github.com/user-attachments/assets/0bd8fd09-c5b4-456f-9cf1-2ccb535cd63c) |
| Machine locale | ![Prompt local](https://github.com/user-attachments/assets/704d6322-e27d-410f-8ced-72eae7908a99) |

---

## Installation de Docker

**Docker** permet d'empaqueter une application et toutes ses dépendances (code, runtime, bibliothèques) dans un conteneur isolé et portable.

### 1. Installer Docker et Docker Compose

```bash
sudo apt install docker.io docker-compose -y
```

### 2. Créer le répertoire de projet

```bash
mkdir mes-data && cd mes-data
```

> Remplacez `mes-data` par le nom de votre choix.

![Création du dossier](https://github.com/user-attachments/assets/9ee3b5ab-3271-427c-b565-489aac9877f3)

### 3. Créer le fichier de configuration Docker Compose

```bash
nano docker-compose.yml
```

![Éditeur nano](https://github.com/user-attachments/assets/df01cbc0-6676-425c-9352-c46850678673)

Copiez-collez la configuration suivante :

```yaml
version: '3'
services:
  db:
    image: mariadb:10.11
    command: --transaction-isolation=READ-COMMITTED --log-bin=binlog --binlog-format=ROW
    restart: always
    volumes:
      - db_data:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=mot_de_passe_secure
      - MYSQL_PASSWORD=nextcloud_pass
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud

  app:
    image: nextcloud:latest
    restart: always
    ports:
      - 8080:80
    volumes:
      - nextcloud_data:/var/www/html
    environment:
      - MYSQL_PASSWORD=nextcloud_pass
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_HOST=db

volumes:
  db_data:
  nextcloud_data:
```

Enregistrez et quittez l'éditeur : **Ctrl+X**, puis **Y**, puis **Entrée**.

![Configuration docker-compose.yml](https://github.com/user-attachments/assets/5421e84d-a194-482f-b2e7-ac29087e560b)

### 4. Démarrer les conteneurs

```bash
sudo docker-compose up -d
```

![Lancement Docker](https://github.com/user-attachments/assets/87f3b0bf-e408-4122-a0a1-5db2a68dbe05)

---

## Accès à l'interface Nextcloud

Ouvrez un navigateur et accédez à l'URL suivante en remplaçant l'IP par la vôtre :

```
http://192.168.35.138:8080
```

![Barre d'adresse](https://github.com/user-attachments/assets/4a36b2e5-8716-46c5-8564-d1c799ab7025)

La page d'initialisation de Nextcloud s'affiche. Renseignez un nom d'utilisateur administrateur et un mot de passe.

![Page d'initialisation](https://github.com/user-attachments/assets/94791be2-e3e5-4cd6-8acf-f0524688af8e)

![Création du compte admin](https://github.com/user-attachments/assets/0b5a3c99-7e32-4fc6-a5bc-5de39f38a0e0)

> **Cas particulier :** Si vous êtes redirigé vers une page d'erreur contenant `/index.php/core/apps/recommended` dans l'URL, supprimez cette partie et rechargez la page.
>
> ![Erreur de redirection](https://github.com/user-attachments/assets/4ec451bc-41ec-4aac-a5a2-69b4c8a37f32)
> ![URL corrigée](https://github.com/user-attachments/assets/224b96be-72fa-4e0c-ba6a-51c3608be6f6)

Vous accédez désormais au **tableau de bord Nextcloud**.

![Tableau de bord Nextcloud](https://github.com/user-attachments/assets/8a32b311-dd57-4bbf-ac2d-0d9d8d3fdd30)

### Fonctionnalités disponibles

| Fonctionnalité | Description |
|---|---|
| **Stockage & Synchronisation** | Centralisation des fichiers avec synchronisation automatique entre PC, smartphone et serveur |
| **Partage sécurisé** | Partage de documents via des liens protégés par mot de passe et date d'expiration |
| **Travail collaboratif** | Édition de documents (type Word/Excel) à plusieurs et en temps réel depuis le navigateur |
| **Communication** | Chat, visioconférence (Talk), gestion d'agendas et de contacts partagés |

---

## Conclusion

Ce projet illustre la mise en œuvre d'une infrastructure cloud privée, moderne et entièrement conteneurisée. En associant **Docker Compose** pour l'orchestration des services et **Nextcloud Hub** pour la productivité, cette architecture répond concrètement aux enjeux actuels de **souveraineté numérique** et de **conformité RGPD**, tout en restant accessible et reproductible.

---

*Réalisé par [Yacine Harrache](https://github.com/yacinehrc) — BTS SIO SLAM | EPSI Lille*

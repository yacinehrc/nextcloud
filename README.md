### NEXTCLOUD
<img width="1912" height="909" alt="Capture d&#39;écran 2026-06-27 063808" src="https://github.com/user-attachments/assets/183eccd7-87ed-4c21-ac53-2adf4295ecf2" />


---
## INTRODUCTION
Nextcloud est une plateforme open-source de productivité et de collaboration sur site (on-premise), conçue pour offrir une alternative souveraine aux solutions de stockage cloud grand public (Google Drive, Microsoft 365, Dropbox).

<strong>Avantages</strong> :
- Souveraineté & RGPD : Contrôle total des données sur infrastructure propre, sans dépendance vis-à-vis des GAFAM.

- Rentabilité (Open-Source) : Aucun coût de licence par utilisateur et stockage limité uniquement par le matériel informatique.

- Flexibilité Docker : Déploiement conteneurisé isolant les services (Nextcloud/MariaDB), facilitant les mises à jour et la portabilité.

- Évolutivité : Écosystème d'applications riche (visioconférence Talk, suite Office, gestion de tâches) activable en un clic.

<strong>Inconvénients</strong> :
- Maintenance critique : Gestion interne obligatoire de la sécurité et des sauvegardes (backups) ; risque de perte de données en cas de crash.

- Contrainte matérielle : Performances et vitesses de synchronisation directement liées à la bande passante et à la puissance de la machine hôte.
---

## INSTALLATION D'OS
Tout d'abord, il vous faut soit une VM (Machine Virtuelle), soit un PC qui ne sert plus à rien. Ensuite, vous devez donc installer Ubuntu (pour ici, le modèle "Desktop" suffit largement). Voici le lien de téléchargement de l'OS : https://ubuntu.com/download/desktop
Pour l'explication de création de VM, voici mon repository explicatif sur ce sujet : <strong>(pour l'installation d'Ubuntu Desktop, il suffit d'aller sur ce repository et de descendre jusque la section "Installation")<strong>
---

## INSTALLATION DE NEXTCLOUD
Une fois l'installation d'Ubuntu terminée, nous arrivons sur ce bureau.
<img width="1919" height="1034" alt="Capture d&#39;écran 2026-06-26 135323" src="https://github.com/user-attachments/assets/1046e6fb-94f2-4d5b-a9e8-e4da200d9b17" />


Il faut donc appuyer sur l'icône des 9 boutons en bas à droite.
<img width="1919" height="1032" alt="Capture d&#39;écran 2026-06-26 135340" src="https://github.com/user-attachments/assets/819e47f7-2253-49c9-85a6-7fd20de90791" />


Il faut maintenant ouvrir l'application "Terminal".
<img width="1919" height="1032" alt="Capture d&#39;écran 2026-06-26 135340" src="https://github.com/user-attachments/assets/1e685b39-c04b-4cb9-bcf4-e4f4ade73a40" />


Nous arrivons donc sur un terminal, où nous allons en installer quelques paquets pour se connecter en SSH (Secure Shell est un protocole informatique qui permet de se connecter à distance et de manière sécurisée à une autre machine via un terminal) depuis notre machine local.
<img width="1919" height="1032" alt="Capture d&#39;écran 2026-06-26 135401" src="https://github.com/user-attachments/assets/010ea0c8-fd5e-4be3-8912-999872be02ce" />


Pour commencer, nous allons taper la commande suivante afin de s'assurer que les derniers paquets sont mit à jour : sudo apt update && sudo apt upgrade -y
<img width="1919" height="1032" alt="Capture d&#39;écran 2026-06-26 135541" src="https://github.com/user-attachments/assets/2f0dc452-cf7c-43dc-b6f2-2fa29739d07e" />


Cela nous demande votre mot de passe d'utilisateur. Puis, le téléchargement s'effectuera.
<img width="1919" height="1036" alt="Capture d&#39;écran 2026-06-26 135559" src="https://github.com/user-attachments/assets/2fb0f0a4-fbf0-4418-874d-f1e73b344b4a" />


Une fois la mise à jour effectuée, nous allons installer SSH car il n'est pas installé de base sur Ubuntu (mais sur d'autres distributions, il peut être demandé de l'installer à la configuration d'installation). Donc, nous tapons cette commande : sudo apt install ssh -y
<img width="1919" height="1032" alt="Capture d&#39;écran 2026-06-26 140023" src="https://github.com/user-attachments/assets/c5dea647-0bb7-40f2-a23b-bfee02229e7d" />


Ensuite, pour y voir plus clair, nous pouvons effacer notre terminal avec la commande : clear
<img width="1919" height="1032" alt="Capture d&#39;écran 2026-06-26 140121" src="https://github.com/user-attachments/assets/7c635af2-b599-43c5-993b-8f6d97712e6e" />


Puis, nous allons donc trouver notre adresse IP qui est cruciale pour se connecter en SSH. Elle se trouve en "2: ens33" et il faut descendre et trouver "inet" et à droite se trouvera l'adresse IP <strong>(Il ne faut pas prendre en compte l'adresse de sous-réseau qui est le / avec une valeur après).</strong> Dans mon cas, mon adresse IP est 192.168.35.138
<img width="1919" height="1036" alt="Capture d&#39;écran 2026-06-27 061918" src="https://github.com/user-attachments/assets/536e8dee-6e41-4b0c-8550-abe6b66c4898" />

---

## SE CONNECTER EN SSH
À présent, nous pouvons ouvrir un PowerShell sur Windows (ou un terminal sur une distribution Linux) et nous allons nous connecter en SSH en tapant la commande : ssh user@ip <strong>→ en remplacant "user" par votre nom d'utilisateur sur votre Ubuntu, et "ip" par l'adresse IP s'affichant sur votre terminal Ubuntu</strong>.
<img width="1919" height="1034" alt="Capture d&#39;écran 2026-06-27 062045" src="https://github.com/user-attachments/assets/aecdf8e8-ef01-4c12-8a4d-eeb3b781e924" />


Cela nous demande une autorisation, où nous répondons "yes".
<img width="1919" height="1036" alt="Capture d&#39;écran 2026-06-27 062110" src="https://github.com/user-attachments/assets/726d5cc8-f603-4608-b7c2-7242d56cba80" />


Et une fois connecté, nous avons donc le même utilisateur que sur le terminal Ubuntu.
Ubuntu : <img width="240" height="21" alt="Capture d&#39;écran 2026-06-27 071853" src="https://github.com/user-attachments/assets/0bd8fd09-c5b4-456f-9cf1-2ccb535cd63c" />
Machine Locale : <img width="206" height="13" alt="Capture d&#39;écran 2026-06-27 071924" src="https://github.com/user-attachments/assets/704d6322-e27d-410f-8ced-72eae7908a99" />


---
## INSTALLATION DE DOCKER
Docker sert à empaqueter une application et tout ce dont elle a besoin pour fonctionner (code, runtime, outils système, bibliothèques) dans un bloc unique appelé un conteneur.

Pour l'installer, nous allons taper la commande suivante : sudo apt install docker.io docker-compose -y
Cela va à nouveau demander notre mot de passe utilisateur, puis s'installer.

Une fois cette étape faite, nous allons créer un dossier pour regrouper tous les fichiers du projet au même endroit. Il faut donc taper cette commande : mkdir nom && cd nom <strong>→ en remplacant "nom" par le nom de fichier que vous voulez donner, personnellement, ce sera mes-data</strong>.
<img width="1913" height="1003" alt="Capture d&#39;écran 2026-06-27 062720" src="https://github.com/user-attachments/assets/9ee3b5ab-3271-427c-b565-489aac9877f3" />


Puis, nous serons donc dans ce dossier. Nous allons modifier le fichier de configuration du projet, voici la commande : nano docker-compose.yml
<img width="1919" height="1029" alt="Capture d&#39;écran 2026-06-27 062745" src="https://github.com/user-attachments/assets/df01cbc0-6676-425c-9352-c46850678673" />


Une fois arrivé, nous sommes dans un fichier d'écriture vierge, il faudra donc rentrer le bloc de configuration suivant :

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


Ainsi, cela ressemble à ceci : 
<img width="1919" height="1036" alt="Capture d&#39;écran 2026-06-27 062808" src="https://github.com/user-attachments/assets/5421e84d-a194-482f-b2e7-ac29087e560b" />


Puis, pour sortir du fichier, il suffit d'appuer sur les touches Ctrl + x, Y et Entrée.

Et maintenant, nous pouvons lancer Docker via la commande : sudo docker-compose up -d
<img width="1919" height="1036" alt="Capture d&#39;écran 2026-06-27 062902" src="https://github.com/user-attachments/assets/87f3b0bf-e408-4122-a0a1-5db2a68dbe05" />


## ACCÉDER À NEXTCLOUD
Nous arrivons dans les dernières étapes, nous allons maintenant pouvoir accéder à l'interface de Nextcloud.
Pour cela, nous ouvrons un navigateur, et nous allons taper dans l'URL notre IP dans le port 8080 : http://ip.ip.ip.ip:8080 (pour moi, ce sera http://192.168.35.138:8080)
<img width="1130" height="42" alt="Capture d&#39;écran 2026-06-27 063144" src="https://github.com/user-attachments/assets/4a36b2e5-8716-46c5-8564-d1c799ab7025" />


Et nous accédons à l"interface de Nextcloud.
<img width="1909" height="908" alt="Capture d&#39;écran 2026-06-27 063159" src="https://github.com/user-attachments/assets/94791be2-e3e5-4cd6-8acf-f0524688af8e" />


Il faut maintenant y mettre un nom d'utilisateur de votre choix, et un mot de passe.
<img width="1916" height="906" alt="Capture d&#39;écran 2026-06-27 063339" src="https://github.com/user-attachments/assets/0b5a3c99-7e32-4fc6-a5bc-5de39f38a0e0" />


CAS EXCEPTIONNEL :
Normalement, vous devriez arriver sur le tableau de bord de Nextcloud, si ce n'est pas le cas et que vous avez l'image suivante, il faudra juste supprimer "/index.php/core/apps/recommented" de l'URL.
<img width="1915" height="909" alt="Capture d&#39;écran 2026-06-27 063716" src="https://github.com/user-attachments/assets/4ec451bc-41ec-4aac-a5a2-69b4c8a37f32" />
<img width="1131" height="37" alt="Capture d&#39;écran 2026-06-27 063735" src="https://github.com/user-attachments/assets/224b96be-72fa-4e0c-ba6a-51c3608be6f6" />


Maintenant, vous êtes sur le tableau de bord de Nextcloud.
<img width="1912" height="909" alt="Capture d&#39;écran 2026-06-27 063808" src="https://github.com/user-attachments/assets/8a32b311-dd57-4bbf-ac2d-0d9d8d3fdd30" />


Plusieurs choix s'offrent à vous à présent :
- Stockage & Synchronisation : Centraliser tes fichiers et les synchroniser automatiquement entre ton PC, ton smartphone et ton serveur.

- Partage Sécurisé : Partager des documents ou des dossiers via des liens protégés par mot de passe et date d'expiration.

- Travail Collaboratif : Éditer des documents de type Word/Excel à plusieurs et en temps réel directement sur le web.

- Outils de Communication : Discuter par chat, passer des appels vidéo (visioconférence) et gérer des agendas ou contacts partagés.


## CONCLUSION
Ce projet démontre la mise en œuvre d'une infrastructure cloud moderne, sécurisée et entièrement conteneurisée. En associant la puissance de Docker Compose pour l'orchestration et de Nextcloud Hub pour la productivité, cette architecture répond concrètement aux problématiques actuelles de souveraineté numérique et de conformité RGPD.

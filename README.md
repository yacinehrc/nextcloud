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


À présent, nous pouvons ouvrir un PowerShell sur Windows (ou un terminal sur une distribution Linux) et nous allons nous connecter en SSH en tapant la commande : ssh user@ip <strong>→ en remplacant "user" par votre nom d'utilisateur sur votre Ubuntu, et "ip" par l'adresse IP s'affichant sur votre terminal Ubuntu</strong>.
<img width="1919" height="1034" alt="Capture d&#39;écran 2026-06-27 062045" src="https://github.com/user-attachments/assets/aecdf8e8-ef01-4c12-8a4d-eeb3b781e924" />
































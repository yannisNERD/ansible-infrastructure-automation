# Automatisation de la Sécurité des Serveurs 🛡️ (Debian/Ubuntu)

Ce projet utilise Ansible pour automatiser la sécurisation des serveurs Debian/Ubuntu, en intégrant des tâches liées à l'accès SSH et en réalisant une analyse de vulnérabilité avec OpenSCAP. L'objectif est d'améliorer la sécurité des systèmes en appliquant les meilleures pratiques et en effectuant des vérifications automatiques de sécurité. 🚀

Note : Ce projet est initialement conçu pour les systèmes RedHat, mais a été adapté pour fonctionner également avec Debian et Ubuntu grâce à des ajustements spécifiques pour ces environnements. 🔄

## Structure du projet 🗂️

Le projet est organisé autour d'un **playbook Ansible** et plusieurs fichiers de tâches qui sont inclus dans le playbook principal. Voici une brève description des fichiers présents :

### Playbook principal (`playbook.yml`) 📜

Le fichier principal qui orchestre l'exécution des tâches sur les serveurs cibles. Ce playbook fait appel à trois fichiers de tâches différents :
1. **Tâches d'accès SSH** : Gestion de l'accès SSH sécurisé, incluant la création d'un utilisateur dédié (secadmin) et la désactivation de l'accès root.
2. **Installation des paquets nécessaires** : Installation de **OpenSCAP** et autres outils nécessaires pour l'analyse de vulnérabilités.
3. **Scan de vulnérabilités** : Exécution d'un scan de vulnérabilités avec **OpenSCAP** et génération d'un rapport d'analyse.

### Tâches d'accès SSH (`tasks_ssh_access.yml`) 🔐

Ce fichier contient des tâches pour sécuriser l'accès SSH :
- Vérification de l'existence de l'utilisateur `secadmin`.
- Création de l'utilisateur `secadmin` s'il n'existe pas, avec ajout au groupe `sudo`.
- Copie de la clé SSH publique pour l'utilisateur `secadmin`.
- Désactivation de l'accès SSH pour l'utilisateur `root`.
- Limitation de l'accès SSH uniquement à l'utilisateur `secadmin`.

### Installation des paquets nécessaires (`tasks_install_openscap.yml`) 📦

Cette tâche installe les paquets nécessaires pour effectuer un scan de vulnérabilités avec **OpenSCAP**, y compris :
- **libopenscap8** : Librairie nécessaire pour exécuter les scans.
- **wget** et **bzip2** : Utilitaires pour télécharger et décompresser les fichiers OVAL nécessaires à l'analyse.

### Scan de vulnérabilités avec OpenSCAP (`tasks_vulnerability_scan_with_secadmin.yml`) 🧐

Ce fichier exécute le processus complet pour effectuer un scan de vulnérabilités :
- Création d'un répertoire pour stocker les fichiers OVAL et les rapports.
- Téléchargement et décompression des fichiers OVAL pour Ubuntu/Debian.
- Exécution d'un scan avec **OpenSCAP** pour générer un rapport d'analyse détaillé.
- Affichage du chemin où le rapport est généré.

## Prérequis 🔧

Avant d'exécuter ce projet, assurez-vous d'avoir les éléments suivants :
- **Ansible** installé sur votre machine de gestion.
- Un accès SSH fonctionnel à vos serveurs **Debian/Ubuntu** cibles.
- La clé SSH publique disponible pour l'utilisateur `secadmin`.

## Installation 🏗️

Clonez ce projet et exécutez le playbook Ansible avec la commande suivante :

```bash
git https://github.com/yannisNERD/ansible-infrastructure-automation.git
cd ansible-infrastructure-automation
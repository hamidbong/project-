# Déploiement d'Application Web avec Ansible, NGINX et Bind9
Ce projet automatise le déploiement d'une application web répartie sur plusieurs serveurs pour assurer la haute disponibilité. L'architecture utilise deux serveurs web, un load balancer NGINX, et un serveur DNS Bind9 pour fournir une solution d'accès via un nom de domaine unique.
## Table des Matières
- [Aperçu](#aperçu)
- [Architecture](#architecture)
- [Prérequis](#prérequis)
- [Configuration de l'inventaire](#configuration-de-l'inventaire)
- [Installation](#installation)
- [Utilisation](#utilisation)
- [Rôles Ansible](#rôles-Ansible)
- [Contribution](#contribution)
- [Licence](#licence)
## Aperçu
Ce projet utilise Ansible pour déployer une application web sur deux serveurs distincts, un load balancer NGINX, et un serveur DNS Bind9. La configuration NGINX répartit la charge entre les deux serveurs web pour assurer la haute disponibilité, tandis que Bind9 fournit la résolution DNS pour le domaine mywebsite.com.
## Architecture
1. Serveurs web : Deux serveurs (web1 et web2) hébergeant l'application.
2. Load Balancer : Un serveur utilisant NGINX pour répartir la charge entre web1 et web2.
3. Serveur DNS : Un serveur Bind9 configuré pour résoudre example.com vers le load balancer.
## Prérequis
- Ansible installé sur la machine de contrôle.
* Accès SSH configuré vers tous les serveurs.
+ Ansible 2.9+.
- Système d'exploitation ubuntu
## Configuration de l'inventaire
Définissez les adresses IP de chaque serveur dans `inventory.ini` :
```
[webservers]
web1 ansible_host=192.168.1.10
web2 ansible_host=192.168.1.11

[loadbalancer]
loadbalancer ansible_host=192.168.1.20

[dns]
dnsserver ansible_host=192.168.1.30
```
## Installation
1. Clonez le dépôt :
```bash
  git clone https://github.com/votre-utilisateur/deploiement-web-ansible.git
  cd deploiement-web-ansible
```
2. Assurez-vous que tous les serveurs sont accessibles via SSH et que vous disposez des privilèges sudo.
## utilisation
Lancez le playbook principal pour déployer toute l'architecture :
```bash
  ansible-playbook -i inventory.ini playbook.yml
```
### Verification
* Accédez à `http://example.com` (ou à l'IP du load balancer) pour vérifier que l'application est accessible.
- Utilisez des commandes DNS, comme dig, pour vérifier que le DNS résout example.com vers l'IP du load balancer.


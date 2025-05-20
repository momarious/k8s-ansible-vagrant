# k8s-ansible-vagrant

# Provisionnement de cluster Kubernetes local

Ce repo permet de provisionner automatiquement un cluster Kubernetes local à l'aide de :
- Vagrant pour la virtualisation
- Ansible pour l'automatisation de la configuration

## Prérequis
- Ubuntu 22.04
- VirtualBox
- Vagrant
- Ansible

## Fonctionnement
- **VirtualBox** permet de créer des machines virtuelles
- **Vagrant** permet de créer des machines virtuelles de VirtualBox grâce à un script
- **Ansible** permet d'automatiser le provisionning des machines virtuelles

## Mise en place
1. Démarrer le cluster :
   ```bash
   vagrant up

2. Vérifier le master :

    ```bash
    vagrant ssh master
    kubectl cluster-info

3. Redémarrer les workers  :

    ```bash
    vagrant ssh worker-1
    sudo reboot

    ```bash
    vagrant ssh worker-2
    sudo reboot
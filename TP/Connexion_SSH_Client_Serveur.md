## TP 1 : Configuration SSH entre un client et un serveur

### Objectifs

Créer et évaluer une connexion sécurisée via le protocole SSH entre une machine cliente/attaquante (Kali Linux) et un serveur ou une machine vulnérable (Metasploitable), dans le but de comprendre les mécanismes d'accès distant et d'authentification.

### Activités
1. Verifier la connectivité entre les deux machines :
*  Identification des adresses IP de chaque machine : `ipconfig`
 
*  Effectuer des tests de `ping` entre les machines : 
   
  
2. Installer ou vérifier le focntionnement de ssh sur la machine serveur/vulnérable :
   ```
   sudo apt update
   sudo apt install openssh-server -y
   sudo systemctl status ssh
   sudo systemctl start ssh
   sudo systemctl enable ssh
   ```
   >  Si erreur: Verifier que le port écoute :
   `sudo ss -tlnp | grep :22  ==> (reusltat attendu)  LISTEN 0 128 0.0.0.0:22 `
   Sinon 
*      Verifier le statut : `sudo ufw status`
*      Autoriser le port sur le pare-feu: `sudo ufw allow 22/tcp`
3. Géneration de la paire de clé sur la machine cliente: 
   `ssh-keygen -t rsa -b 4096` ou `ssh-keygen`

4. Copie de la clé publique vers le serveur:
   `ssh-copy-id utilisateur@adresse_du_serveur` ou
   `cat ~/.ssh/id_rsa.pub | ssh utilisateur@adresse_du_serveur "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"`
   
5. Connexion au serveur à partir de la machine cliente
     `ssh utilisateur@adresse_du_serveur` ou 
     `ssh -i ~/.ssh/id_rsa utilisateur@adresse_du_serveur`
     

6. Modifier le fichier de configuration pour changer le port et interdire l'authentification par mot de passe
*    `sudo nano /etc/ssh/sshd_config`
*    Rechercher et changer/ajouter ces lignes
     ```
     PermitRootLogin no
     PasswordAuthentication no
     Port numero_port_souhaite  // ex: 2222
     ```
* Redémarrer le service : `sudo systemctl restart ssh` 
* Tester la connexion avec le nouveau port: `ssh utilisateur@adresse_du_serveur -p nouveau_port`

6. Configuration d'un alias de connexion
   ```
   nano ~/.ssh/config
   Host myserver
   HostName adresse_ip
   User nom_utilisateur
   IdentityFile ~/.ssh/ma_cle_privée
   Port numero_port_configure
   ```
* Se connecter: `ssh myserver`

7. Exécution de commandes à l'interieur du serveur
*    Créer un dossier `my_repo`
*    Créer un fichier `file_repo` à l'interieur de ce fichier et y ajouter le contenu `Mon premier fichier sur un serveur distant`

8. Copier le dossier créer sur le serveur sur la machine cliente

   `scp -r user@adresse_serveur:/chemin/dossier /chemin/local/`

### Conclusion
Ce TP a permis de mettre en œuvre une connexion sécurisée à distance via le protocole SSH entre une machine cliente et un serveur. Le processus a consisté en la vérification de la connectivité entre les machines, la génération de clés, l'accès à la machine cible et l'exécution de commandes à l'intérieur de celle-ci.
   
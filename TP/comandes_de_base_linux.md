## TP 2 : Commandes de base de Linux

### Objectifs

- [x] Se familiariser avec l'environnement Linux et explorer le système.
- [x] Utilisation du terminal, manipulation des fichiers et répertoires (se déplacer, lire, etc.)
- [x] Comprendre et gerer les utilisateurs et les permissions
- [x] Compression, archivage et téléchargement de fichier

### Activités

####  ** 1 : Naviguer dans les répertoires et explorer la structure**
- **Objectif** : Explorer la structure du système de fichiers avec les commandes `cd`, `pwd` et `ls`.
- **Instructions** : 
  1. Utilisez `pwd` pour afficher votre répertoire actuel.
  2. Changez de répertoire avec `cd /etc` et utilisez `ls` puis `ls -l` et `ls -la` pour afficher son contenu (fichiers cachés y compris).
  3. Revenez au répertoire précédent avec `cd -`.
  4. Montez de deux niveaux dans l'arborescence avec `cd ../..`.

---

#### ** 2 : Créer une arborescence de répertoires imbriqués**
- **Objectif** : Utiliser `mkdir` pour créer des répertoires imbriqués.
- **Instructions** : 
  1. Créez une arborescence de répertoires avec `mkdir -p ~/Documents/Projets/Exercice1`.
  2. Vérifiez la création avec `ls -R ~/Documents`.

---

#### ** 3 : Copier et déplacer des dossiers et des fichiers**
- **Objectif** : Manipuler des fichiers et des répertoires avec `cp` et `mv`.
- **Instructions** : 
  1. Créez un fichier avec `touch ~/Documents/Projets/Exercice1/fichier.txt`.
  2. Copiez ce fichier dans un nouveau répertoire avec `cp ~/Documents/Projets/Exercice1/fichier.txt ~/Documents/Backup/`.
  3. Déplacez ce fichier dans un autre répertoire avec `mv ~/Documents/Backup/fichier.txt ~/Documents/Projets/Exercice2/`.

---

#### ** 4 : Créer, vider et supprimer des fichiers**
- **Objectif** : Utiliser `touch`, `truncate`, `rm` pour créer, vider et supprimer des fichiers.
- **Instructions** : 
  1. Créez un fichier vide avec `touch ~/Documents/Projets/fichier_vide.txt`.
  2. Ajoutez du contenu à ce fichier avec `echo "Contenu de test" >> ~/Documents/Projets/fichier_vide.txt`.
  3. Videz le fichier avec `truncate -s 0 ~/Documents/Projets/fichier_vide.txt`.
  4. Supprimez le fichier avec `rm ~/Documents/Projets/fichier_vide.txt`.

---   

#### ** 5 : Supprimer des répertoires vides et non vides**
- **Objectif** : Utiliser `rmdir` et `rm -rf` pour supprimer des répertoires.
- **Instructions** : 
  1. Créez un répertoire vide avec `mkdir ~/Documents/Vide`.
  2. Supprimez-le avec `rmdir ~/Documents/Vide`.
  3. Créez un répertoire avec des fichiers avec `mkdir -p ~/Documents/NonVide && touch ~/Documents/NonVide/fichier.txt`.
  4. Supprimez-le avec `rm -rf ~/Documents/NonVide`.

---

#### ** 6 : Afficher le contenu d'un fichier avec `cat`, `head`, et `tail`**
- **Objectif** : Manipuler l'affichage des fichiers avec `cat`, `head`, et `tail`.
- **Instructions** : 
  1. Créez un fichier avec plusieurs lignes :  
     ```bash
     for i in {1..20}; do echo "ligne $i" >> fichier.txt; done
     ```
  2. Affichez tout le contenu du fichier avec `cat fichier.txt`.
  3. Affichez les 5 premières lignes avec `head -n 5 fichier.txt`.
  4. Affichez les 5 dernières lignes avec `tail -n 5 fichier.txt`.
  5. Utilisez `tail -f fichier.txt` pour suivre en direct les nouvelles lignes ajoutées.

---

#### ** 7 : Zipper et dézipper des fichiers**
- **Objectif** : Utiliser `zip` et `unzip` pour compresser et décompresser des fichiers.
- **Instructions** : 
  1. Créez quelques fichiers avec `touch fichier1.txt fichier2.txt fichier3.txt`.
  2. Compressez-les dans une archive zip avec `zip fichiers.zip fichier1.txt fichier2.txt fichier3.txt`.
  3. Décompressez l'archive avec `unzip fichiers.zip`.

---

#### ** 8 : Utiliser `tar` pour créer et extraire une archive**
- **Objectif** : Utiliser `tar` pour créer et extraire une archive.
- **Instructions** : 
  1. Créez un répertoire avec des fichiers :  
     ```bash
     mkdir MonProjet && touch MonProjet/{fichier1.txt,fichier2.txt}
     ```
  2. Compressez ce répertoire avec `tar cvf mon_projet.tar MonProjet/`.
  3. Extrayez l'archive avec `tar xvf mon_projet.tar`.

---

#### ** 9 : Télécharger des fichiers avec `wget`**
- **Objectif** : Utiliser `wget` pour télécharger un fichier depuis Internet.
- **Instructions** : 
  1. Utilisez la commande `wget` pour télécharger un fichier :  
     ```bash
     wget https://siteauchoix.com/fichier.zip 
     ```
  2. Vérifiez le téléchargement avec `ls`.

---

#### ** 10 : Trouver l'emplacement d'une commande avec `whereis`**
- **Objectif** : Utiliser `whereis` pour localiser un fichier binaire, source, ou manuel.
- **Instructions** : 
  1. Utilisez `whereis` pour trouver l'emplacement de la commande **bash** :
     ```bash
     whereis bash
     ```

---

#### ** 11 : Créer une sauvegarde avec `cp -r`**
- **Objectif** : Copier un répertoire avec `cp -r` pour créer une sauvegarde.
- **Instructions** : 
  1. Créez un répertoire avec du contenu :  
     ```bash
     mkdir MonDossier && touch MonDossier/fichier{1..3}.txt
     ```
  2. Copiez-le de manière récursive avec `cp -r MonDossier/ Sauvegarde_MonDossier/`.

---

#### ** 12 : Supprimer plusieurs fichiers avec un seul `rm`**
- **Objectif** : Supprimer plusieurs fichiers à la fois avec `rm`.
- **Instructions** : 
  1. Créez plusieurs fichiers avec :  
     ```bash
     touch fichier1.txt fichier2.txt fichier3.txt
     ```
  2. Supprimez-les tous d'un coup avec `rm fichier1.txt fichier2.txt fichier3.txt`.

---

#### ** 13 : Raccourci pour exécuter la dernière commande**
- **Objectif** : Utiliser `!!` pour exécuter la dernière commande.
- **Instructions** : 
  1. Exécutez une commande simple, par exemple `ls`.
  2. Ré-exécutez la dernière commande avec `!!`.

---

#### ** 14 : Afficher et suivre un fichier log en temps réel avec `tail -f`**
- **Objectif** : Utiliser `tail -f` pour suivre un fichier log en temps réel.
- **Instructions** : 
  1. Utilisez `tail -f` sur un fichier journal, par exemple :  
     ```bash
     tail -f /var/log/syslog
     ```

---

#### ** 15 : Renommer plusieurs fichiers avec `mv`**
- **Objectif** : Renommer des fichiers en utilisant des commandes combinées avec `mv`.
- **Instructions** : 
  1. Créez trois fichiers :  
     ```bash
     touch fichierA.txt fichierB.txt fichierC.txt
     ```
  2. Renommez-les avec :  
     ```bash
     mv fichierA.txt nouveauFichierA.txt
     ```

---

#### ** 16 : Afficher des fichiers compressés avec `zcat`**
- **Objectif** : Afficher le contenu d'un fichier compressé sans le décompresser avec `zcat`.
- **Instructions** : 
  1. Compressez un fichier texte avec `gzip fichier.txt`.
  2. Affichez son contenu avec `zcat fichier.txt.gz`.

---

#### ** 17 : Supprimer un fichier de manière forcée avec `rm -rf`**
- **Objectif** : Utiliser `rm -rf` pour forcer la suppression d'un répertoire non vide.
- **Instructions** : 
  1. Créez un répertoire avec des fichiers :  
     ```bash
     mkdir TestDir && touch TestDir/file{1..3}.txt
     ```
  2. Supprimez-le avec la commande :  
     ```bash
     rm -rf TestDir
     ```
---
#### ** 18 : Rediriger l'entrée et la sortie avec `>` et `>>`**
- **Objectif** : Utiliser les redirections pour capturer la sortie d'une commande dans un fichier.
- **Instructions** :
  1. Exécutez une commande et redirigez sa sortie vers un fichier :
     ```bash
     echo "Ceci est une sortie redirigée" > sortie.txt
     ```
  2. Ajoutez du contenu à ce fichier avec `>>` :
     ```bash
     echo "Ligne supplémentaire" >> sortie.txt
     ```

---

#### ** 19 : Utiliser `df` et `du` pour surveiller l'espace disque**
- **Objectif** : Utiliser `df` et `du` pour surveiller l'espace disque.
- **Instructions** :
  1. Affichez l'utilisation de l'espace disque de votre système :
     ```bash
     df -h
     ```
  2. Affichez l'utilisation de l'espace disque d'un répertoire spécifique :
     ```bash
     du -sh /var/log
     ```

---
#### ** 20: Gérer les permissions avec `chmod` et `chown`**
- **Objectif** : Modifier les permissions et le propriétaire d'un fichier.
- **Instructions** :
  1. Créez un fichier avec `touch fichier_securise.txt`.
  2. Utilisez `chmod` pour accorder uniquement les droits de lecture et d'exécution au propriétaire :
     ```bash
     chmod 500 fichier_securise.txt
     ```
  3. Changez le propriétaire du fichier avec `chown` :
     ```bash
     sudo chown utilisateur1:utilisateur1 fichier_securise.txt
     ```
---
#### ** 21: Intégration d’un nouvel employé

Un nouvel employé `yao` rejoint l’équipe. Il doit :
1. Être ajouté au système,
2. Faire partie du groupe `dev`,
3. Avoir un mot de passe initial.

```bash
sudo adduser yao
sudo groupadd dev
sudo usermod -aG dev yao
sudo passwd yao
```
---
#### ** 22: Changement d’équipe
`yao` passe du groupe `dev` à `Système`.

```bash
sudo groupadd Système
sudo gpasswd -d yao dev
sudo usermod -aG Système yao
```
---
#### ** 23 Modifier les permissions d'un fichier pour un groupe**
   - Créer un fichier `project.txt`.
   - Assigner le groupe `dev` au fichier et donner les droits de lecture.
   - Commandes : 
     - `chown :dev project.txt`
     - `chmod g+r project.txt`
     - 
#### ** 24 Contrôler les permissions d'accès sur un répertoire**
   - Créer un répertoire `projects/`.
   - Assigner le groupe `dev` avec des droits de lecture et d'écriture.
   - Commandes : 
     - `chown :dev projects/`
     - `chmod 770 projects/`
     
### Conclusion

Ce travail TP a permis de découvrir les commandes de base du système Linux. Plusieurs activités permettent de naviguer dans l’arborescence des fichiers, de gérer les répertoires et fichiers, ainsi que d'exécuter des commandes essentielles comme ls, cd, cp, mv, et rm.  Ce TP offre donc la possibilité de développer des compétences pratiques essentielles pour l'utilisation efficace d'un environnement Linux et la réalisation de tests d'intrusion.
## TP 3 : Reconnaissance

### Objectifs

Ce TP vise à découvrir des outils permettant de comprendre et de maîtriser la phase de reconnaissance dans un test d'intrusion, dans le but de collecter un maximum d'informations sur une cible de manière passive ou active.

### Activités

####  ** 1 : Collecter des informations (adresse IP, emails,  numéros téléphoe, technologies, etc)**
- **Objectif** : Rechercher des adresses Ip, decouvrir les informations et meta données de nom de domaine, etc.
- **Instructions** : 
  1. Utilisez `ping example.com` et `nslookup example.com` pour connaitre l'adresse IP.
  2. Saisir `whois example.com` pour avoir des informations sur la date de création, expiration, serveur DNS, registar, etc.
  3. Lancer dans un navigateur [https://www.iplocation.net/](https://www.iplocation.net/) pour visualiser son adresse IP, sa localisation, etc.
---

#### ** 2 : Analyse discrète avec What Web **
- **Objectif** : collecter et scanner des sites web à partir de sa machine Kali Linux.
- **Instructions** : 
  1. Consulter les options de What Web avec `whatweb --help`.
  2. Ananlyser un site web en mode furtif `whatweb example.com`.
  3. Ananlyser un site web en mode furtif et verbeux `whatweb example.com -v`.
  4. Analyser une plage d'adresse en mode agressif: `wahtweb adresse_initiale-adresse_finale --agression 3 -v`
  5.  Analyser sans afficher les messages d'erreur (adresse IP non disponible dans la plage)  `wahtweb adresse_initiale-adresse_finale --agression 3 -v --no-errors`
  6. Enregistrer le resultat de l'analyse dans un fichier  `wahtweb adresse_initiale-adresse_finale --agression 3 -v --log-verbose=resultat`. Faire `ls -l` puis `cat resultat` pour voir le contenu du fichier créer
---

#### ** 3 : Collecter des emails  **
- **Objectif** : Collecter  des adresses mails avec TheHarvester et hunter.io.
- **Instructions** : 
1. Cloner le projet: 
   ```bash
     git clone https://github.com/laramies/theHarvester
     cd theHarvester
     ```
1. Consulter la documentation  de theHarvester avec `theHarvester --help`

2. Rechercher des adresses emails liés à un domaine: `theHarvester -d nom_domaine -b all`. Utiliser l'option `-d` définis le sous-domaine, `-b` la base de recherche et `-l` pour limiter le nombre maximal d'occurence à récupérer par  exemple `theHarvester -d domaine.com -l 100 -b google`
3. Rechercher des adresses e-mail sur la plateforme Hunter. Créer un compte sur [hunter.io](https://hunter.io/). Utiliser la barre de recherche pour obtenir des adresses e-mails d'un domaine.
---

#### ** 4 : Collecter des informations sur une cible avec RED_HAWK **
- **Objectif** : Collecter des informations sur un site web ou nom de domaine avant une attaque ou un audit
- **Instructions** : 
  1. Cloner le projet sur github `git clone https://github.com/Tuhinshubhra/RED_HAWK`.
  2. Ensuite `cd RED_HAWK` puis lancer avec `php rhawk.php` .
  3. Voir les options avec  `help`.
  4. Suivre les instructions pour lancer le type d'analyse souhaité.

---   

#### ** 5 : Rechercher des noms d’utilisateur avec Sherlock **
- **Objectif** : Rechercher des noms d’utilisateur (usernames) sur différentes plateformes (site web, réseaux sociaux, etc.).
- **Instructions** : 
  1. Cloner le projet  `git clone https://github.com/sherlock-project/sherlock`.
  2. lancer la recherche d'un nom d'utilisateur spécifique
      ```
      cd sherlock
      python3 sherlock nom_utilisateur
     ```
---
  
### Conclusion

Ce TP a permis de découvrir  différents outils dans la collecte et l'analyse des informations de façon légale et sur des sources ouvertes (OSINT – Open Source Intelligence). Outre les outils explorés dans ce TP, plusieurs autres outils tels que [Maltego](https://www.maltego.com/), [reon-ng](https://github.com/lanmaster53/recon-ng), [Sublist3r](https://github.com/aboul3la/sublist3r), etc. et peuvent testés dans le même contexte. Il souligne les défis liés à la protection des données personnelles. Les données accessibles publiquement peuvent parfois être utilisées à des fins malveillantes, ce qui met en évidence l'importance d'une gestion prudente de notre présence en ligne. Il faut également garder à l'esprit que ce TP doit être réalisé uniquement dans un laboratoire personnel, sur des plateformes légales ([TryHackMe](https://tryhackme.com/), [HTB](https://www.hackthebox.com/), etc.) ou avec autorisation écrite.
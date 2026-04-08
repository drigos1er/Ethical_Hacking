## TP 4 : Scanning

### Objectifs

L'objectif de ce TP est de saisir le rôle de la phase de scanning dans un test d'intrusion, de se familiariser avec les outils et techniques employés afin d'identifier des hôtes actifs, des vulnérabilités potentielles et de repérer des ports et services exposés.

### Activités

####  ** 1 : Découverte d'hôtes avec Netdiscover et Netstat **
- **Objectif** : Identifier les hôtes connectés (machine, équipements réseaux, etc.) sur un réseau
- **Instructions** : 
  1. Installer netdiscover sur Kali Linux `sudo apt install netdiscover`
  2. Concultation des options: `sudo netdiscover --help` 
  3. Scanne en mode passif sur le réseau courant `sudo netdiscover`
  4. Scanne d'un réseau spécifique `sudo netdiscover -r nmap <adresse_IP>/<masque_réseau>` (`ex:192.168.10/24`)
  5. Scanne d'une interface spécifique `sudo netdiscover -i eth0` (eth0= interface, peut être remplacé par votre interface)
  6. Analyser les ports ouverts avec `netstat -tuln`
---

#### ** 2 : Scanner un réseau avec Network Mapper (Nmap) **
- **Objectif** : Scanner un réseau pour découvrir des hôtes, ports, services, etc.
- **Instructions** : 
  1. Ping Scan (Scan basique, rapide et discret) sur une adresse `nmap -sP <adresse_IP> ou <nom_domaine>` et sur une plage d'adresse `nmap -sP <adresse_IP>/<masque_réseau>`.
  2. Scan TCP SYN (plus furtif) pour scanner les ports sans établir une connexion TCP complète:  `nmap -sS <adresse_IP> ou <nom_domaine>`.
  3. Scan avec une connexion TCP complète:  `nmap -sT <adresse_IP> ou <nom_domaine>`.
  4. Identifier les services UDP:  `nmap -sU <adresse_IP> ou <nom_domaine>`
  5. Analyser les ports ouverts et versions de services  sur une adresse IP `nmap -sV <adresse_IP> ou <nom_domaine>` ou sur une plage d'adresse `nmap -sV <adresse_IP>/<masque_réseau>`
  6. Scan d'un port spécifique  `nmap -p <num_port> <adresse_IP> ou <nom_domaine>`.
  7. Enregistrer la sortie d’un scan dans un fichier  `nmap  -sV -p <num_port> <adresse_IP> ou <nom_domaine> > scan.txt`.
  8. Scan d'une plage de port  `nmap -p <plage_port> <adresse_IP> ou <nom_domaine>`.
  9. Identifier le système d'exploitation `nmap -O  <plage_port> <adresse_IP> ou <nom_domaine>`.
  10. Scanner en mode verbeux `nmap -v  <plage_port> <adresse_IP> ou <nom_domaine>`.
  11. Scanner en mode agressif `nmap -A  <plage_port> <adresse_IP> ou <nom_domaine>`.
  12. Identifier la version de OpenSSh sur [scanme.nmap.org](http://scanme.nmap.org/)
---

#### ** 3 : Recherche de vulnérabilités avec [Nikto](https://cirt.net/nikto/)  **
- **Objectif** : Analyser les serveurs/sites web pour repérer des vulnérabilités, des configurations incorrectes et des fichiers potentiellement dangereux.
- **Instructions** : 
1. Cloner le projet: 
   ```bash
     git clone https://github.com/sullo/nikto
     cd nikto
    ```
1. Consulter la documentation  de theHarvester avec `nikto --help`

2. Scanner un site web `nikto -h http://example.com`
3. Exporter le rapport dans un fichier html `nikto -h https://example.com -o rapport.html -Format html` 
---

#### ** 4 : détecter les failles de sécurité d’un site ou application Web **
- **Objectif** : Analyser de façon automatisée et manipuler les requêtes HTTP/HTTPS gràce à l'outil OWASP ZAP (Zed Attack Proxy)
- **Instructions** : 
  1. Télécharger et installer [zapproxy](https://www.zaproxy.org/).
  2. Lancer `zapproxy` et cliquez sur l'onglet  `Quick Start (Démarrage rapide)` .
  3. Cliquez sur   `Manual Explore (Explorer manuellement)`.
  4. Dans le champ `Url to explore (URL à explorer)`, saisissez l'URL complète de l'application web que vous souhaitez explorer.
  5. Sélectionnez le navigateur que vous souhaitez utiliser.
  6. Cliquez sur `Launch Browser (Lancer le navigateur)`.

---   
  
### Conclusion

Ce travail pratique, effectué à l'aide d'outils tels que Nmap et Netdiscover, a permis d'identifier les ports ouverts, les services exposés ainsi que plusieurs vulnérabilités potentielles sur une cible déterminée.
Cette phase de scanning confirme son rôle critique dans un test d’intrusion, en fournissant les informations nécessaires à l’exploitation. Les résultats mettent en évidence des surfaces d’attaque exploitables, soulignant la nécessité de réduire l’exposition des services, de filtrer les ports et d’appliquer des correctifs de sécurité.
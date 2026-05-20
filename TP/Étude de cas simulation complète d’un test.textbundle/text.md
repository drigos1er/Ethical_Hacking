## Le contexte de la mission : une PME exposée
Imaginons une mission confiée par une entreprise de taille moyenne, spécialisée dans la gestion de ressources humaines. Elle héberge une application web permettant à ses clients de consulter des documents RH, de gérer des plannings et d’échanger avec des consultants. L’infrastructure est hébergée sur un cloud public (type AWS), et l’accès à l’application s’effectue via un portail web externe. L’entreprise souhaite tester la robustesse de sa sécurité face à une attaque réaliste, initiée depuis Internet, sans fournir d’informations préalables. Le périmètre inclut le portail web, les API exposées, ainsi que les services de messagerie associés au domaine principal.

Le contrat signé définit un test en boîte noire, externe et non intrusif, soit sans perturbation de production ou d’intégration de code à risque, sur la partie production. Aucune attaque par déni de service n’est autorisée, et l’exploitation de failles doit se limiter à la preuve d’impact, sans exécution de code distant en production. L’objectif est de démontrer l’existence d’un scénario d’attaque crédible menant à la compromission d’un compte client ou d’un accès au système d’information interne.

## Reconnaissance : ouverture de la surface d’attaque
La mission commence par une phase de reconnaissance passive. À l’aide d’outils comme whois, Amass, DNSDumpster et Shodan, le pentester collecte des informations sur les domaines associés à l’entreprise, les adresses IP exposées, et les services accessibles publiquement. Il identifie rapidement un domaine secondaire utilisé pour les environnements de test : dev.rh-consulting.fr, ainsi qu’un sous-domaine api.rh-consulting.fr utilisé pour des appels REST.

Une recherche via des moteurs OSINT (Open Source Intelligence) révèle plusieurs documents PDF contenant des métadonnées indiquant le nom de l’outil utilisé pour générer l’interface web (Angular 11), ainsi que des noms de développeurs internes. Sur LinkedIn, un employé affiche fièrement qu’il « administre le backend Node.js et l’environnement Docker de prod ». Ces détails, bien qu’anodins, permettent déjà de cibler les technologies et de préparer les scans.


## Scan et énumération : détection des portes entrouvertes
Un scan discret via Nmap sur l’IP de l’API révèle que plusieurs ports non standard sont ouverts. Un port 3000 affiche une bannière Node.js en mode debug. L’énumération via des outils comme Dirsearch et FFUF sur les chemins accessibles permet de découvrir un endpoint non documenté : /admin/test-login. Ce dernier retourne un message JSON d’erreur avec une stacktrace complète, ce qui indique que l’environnement n’est pas correctement configuré en production.

Le testeur identifie également, via Burp Suite, une API exposant un endpoint GET permettant de récupérer des données utilisateurs sans authentification, grâce à un paramètre mal validé. Une injection dans l’ID de l’utilisateur renvoie des informations d’un autre client, confirmant une faille d’IDOR (Insecure Direct Object Reference). Cela constitue déjà un premier vecteur exploitable.

## Exploitation : preuve de compromission ciblée
Plutôt que de poursuivre une exploitation hasardeuse, le pentester choisit une attaque contrôlée et ciblée. Il modifie la requête API pour interroger les 100 premiers ID utilisateurs et découvre que certains d’entre eux renvoient des adresses e-mail, des noms complets, et des noms de fichiers PDF liés à des documents RH. Il parvient à obtenir l’URL complète de ces documents, hébergés sur un bucket S3 (Amazon Simple Storage Service) public mais mal configuré. La lecture directe de ces documents est possible depuis un simple navigateur.

Plutôt que de télécharger l’ensemble des fichiers, il en sélectionne un seul, anodin, et notifie dans le rapport que plus de 10 000 fichiers confidentiels sont potentiellement exposés à tout internaute. Il n’est pas nécessaire d’aller plus loin : la démonstration est suffisante pour alerter l’entreprise.

## Post-exploitation : observation sans perturbation
Dans ce scénario, la post-exploitation reste volontairement limitée. Le testeur aurait pu chercher à utiliser l’accès API pour tester une élévation de privilèges ou injecter des scripts, mais cela aurait impliqué un risque de perturbation. En accord avec le contrat, il s’arrête à la preuve d’accès non autorisé et à la démonstration du contournement des droits d’accès. Il documente scrupuleusement les endpoints utilisés, les requêtes exactes, les en-têtes, les réponses et les captures.

## Nettoyage : traçabilité et discrétion
Toutes les requêtes ont été envoyées via un proxy dédié, les enregistrements DNS n’ont pas été modifiés, et aucun fichier n’a été écrit sur les serveurs. Le pentester vérifie néanmoins que l’adresse IP utilisée ne reste pas active, qu’aucun cookie de session persistante n’a été créé, et que les journaux de son côté ne contiennent pas de données sensibles. Il chiffre les preuves collectées et détruit les fichiers temporaires.

## Extrait de rapport final - Mission RH Consulting (simulation)
Titre du document : rapport de test d’intrusion externe - Portail RH Consulting

Client : RH Consulting

Date du test : du 6 au 10 mai 2025

Type de test : boîte noire, externe, non destructif

Prestataire : SecureTest Partners

Auteur : Kenan B. - Pentester certifié CEH

1. Résumé exécutif

L’objectif de ce test d’intrusion était d’évaluer la résistance du portail web externe de RH Consulting à une attaque réaliste simulée par un acteur malveillant n’ayant aucun accès initial. La mission s’est déroulée sur cinq jours, dans les conditions prévues contractuellement (test en boîte noire, sans perturbation de la production).

Les résultats du test révèlent plusieurs vulnérabilités critiques et moyennes, dont l’exploitation combinée permettrait à un attaquant d’accéder à des documents RH confidentiels appartenant à des clients de l’entreprise, sans authentification préalable.

Les risques identifiés concernent :

une mauvaise isolation des environnements de test et de production ;

un endpoint d’API exposé permettant des accès non autorisés à des données personnelles ;

une configuration incorrecte d’un bucket S3, exposant de nombreux fichiers sensibles.

Ces failles présentent un risque juridique, réglementaire (RGPD), et réputationnel majeur. Une série de recommandations détaillées a été formulée afin de corriger ces vulnérabilités et renforcer la posture de sécurité globale.

2. Vulnérabilité critique n°1 - IDOR sur l’API /user/profile

Description

L’endpoint GET /api/v1/user/profile?id=XXX permet de consulter le profil utilisateur en modifiant simplement l’ID en paramètre. Aucune authentification n’est exigée, et aucun contrôle d’accès côté serveur n’est mis en place.

Impact

Un attaquant peut itérer les identifiants et récupérer massivement des données personnelles (nom, prénom, e-mail, documents associés), ce qui constitue une violation directe du RGPD.

Preuve

Une requête GET sur l’ID 142 a retourné les informations d’un autre utilisateur que celui initialement connecté. Les captures d’écran et les réponses brutes sont jointes en annexe.

Recommandation

Implémenter une logique d’authentification systématique via jeton JWT ou session sécurisée, et vérifier côté serveur que l’utilisateur authentifié a le droit de consulter l’ID demandé.

3. Vulnérabilité critique n°2 - Bucket S3 accessible publiquement

Description

Un bucket Amazon S3 nommé rh-prod-client-docs est accessible en lecture sans authentification via des URL publiques. Ces documents sont exposés sans chiffrement ni expiration.

Impact

Plus de 10 000 fichiers PDF contenant des documents RH confidentiels (contrats, fiches de paie, relevés d’heures) sont accessibles à toute personne connaissant l’URL.

Preuve

Une liste d’URL obtenue via l’API permet d’accéder librement à ces fichiers, sans authentification. Une seule preuve est incluse dans ce rapport à titre démonstratif.

Recommandation

Désactiver l’accès public au bucket via la console AWS, appliquer une stratégie IAM restrictive, et activer les logs d’accès pour identifier les consultations non autorisées passées.

4. Vulnérabilité moyenne n°1 - Endpoint de debug Node.js exposé

Description

Le port 3000 sur le sous-domaine dev.rh-consulting.fr expose une interface de debug Node.js, en environnement de préproduction, sans contrôle d’accès.

Impact

Un attaquant peut provoquer des erreurs serveur retournant des informations internes : versions, dépendances, chemins systèmes, et identifiants en clair dans certains cas.

Preuve

Une requête POST malformée sur /admin/test-login retourne une stacktrace complète exposant le nom du fichier de configuration.

Recommandation

Interdire l’accès public aux environnements de développement et désactiver toute trace de debug ou de logging verbeux en production.

1. Résumé des vulnérabilités 


## Recommandations générales

Auditer l’ensemble des API exposées et mettre en place une authentification systématique.

Mettre en œuvre un WAF en amont du portail web, avec inspection des requêtes et détection d’anomalies. 

Désactiver tous les accès de développement sur les domaines publics, via filtrage IP ou proxy inverse. 

Réviser les permissions AWS S3 à l’aide d’outils comme AWS Config ou ScoutSuite.

Planifier des revues de code régulières pour détecter les comportements d’accès directs non contrôlés.

## Annexes

Captures d’écran des réponses API IDOR (anonymisées).

Requêtes HTTP précises utilisées (fichiers .txt fournis séparément).

Extrait des métadonnées PDF contenant des informations internes.

Journal d’actions techniques horodatées (Netcat, Burp Suite, Nmap).
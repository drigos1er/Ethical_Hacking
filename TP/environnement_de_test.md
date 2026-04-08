## TP 1 : Mise en place d’un laboratoire de tests

### Objectifs

- [x] Expérimenter sans encourir de risques : Travailler dans un environne-
ment isolé (VM, sandbox, etc.)
- [x] Passer de la théorie à la mise en pratique dans un cadre sécurisé : Explorez des outils tels que Kali Linux, Metasploit, etc.
- [x] Effectuer des simulations d’attaques authentiques sur des systèmes présentant des vulnérabilités.

### Activités
1. Télécharger et installer un environnement de virtualisation (virtualbox,
VMware Workstation, etc.) :
* Liens installation virtualBox : 
   [Téléchargement](https://www.virtualbox.org/wiki/Downloads)
   [Documentation](https://www.virtualbox.org/manual)
* Liens installation VMware : 
   [Lien](https://www.vmware.com/products/desktop-hypervisor)
  
2. Télécharger et installer Kali Linux  sur une machine virtuelle :
   [Télécharment](https://www.kali.org/get-kali/#kali-platforms)
   [Documentation](https://www.kali.org/docs/)
   
3. Télécharger et installer Metasploitable: 
   [Lien 1](https://www.metasploit.com/download)
   [Lien 2](https://docs.rapid7.com/metasploit/metasploitable-2/)
   [Lien 3](https://sourceforge.net/projects/metasploitable/)

4. Mise en réseau des différentes machines virtuelles (Kali et Metasploitable: 
   [Lien 1](https://www.virtualbox.org/manual/ch06.html)
   [Lien 2](https://www.it-connect.fr/comprendre-les-differents-types-de-reseaux-virtualbox/)
   [Lien 3](https://www.it-connect.fr/comprendre-les-differents-types-de-reseaux-de-vmware-workstation-pro)
   [Lien 4](https://mcflypartages.fr/blog/vmware_gestion_reseaux)
   
5. Identifier les adresses IP de chaque machine virtuelle et tester la connectivité:
*    > `ifconfig` // identifier les adresses IP des machines
*    > `ping  adresse_ip_machine_cible` // Test de la connectivité

### Conclusion
Ce TP permet de disposer d'environnement de test constitué de deux machines virtuelles. Une machine `Kali Linux` et une machine `Metaslpoitable` qui sont des hôtes du même réseau et dont la connectivité peut être vérifiée à travers des commandes `Ping`.    
   
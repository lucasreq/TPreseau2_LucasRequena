# TP reseau2_LucasRequena


## I. Exploration locale en solo

Wifi : Nom, Adresse mac, IP
= Carte reseau sans fil Wi-Fi, 30-24-32-A8-9B-2A, 10.33.2.49

Ethernet : Nom, Adresse mac,
IP = Carte Ethernet Ethernet , 0C-9D-92-34-61-A8, none

 

Adresse réseau (wifi) :
10.33.0.0

Adresse broadcast(wifi) :
10.33.3.255

 

Adresse
réseau (ethernet) : none

Adresse
broadcast(ethernet) : none

 

Afficher le
gateway :

Passerelle par
défaut : 10.33.3.253

Grace a Netstats -r j’ai obtenu
cela : 

Entouré en rouge l’adresse de la
passerelle

 
https://github.com/lucasreq/TPreseau2_LucasRequena/blob/master/Images/I.%20Exploration%20locale%20en%20solo/I.1.png
 

En graphique (sous Windows 10):


vous allez sur la barre de recherche et marquez « Modifier les paramètres
Wi-Fi », cliquez ensuite sur le nom du réseau et tout en bas de la page
vous pourrez trouver quelques infos.  

 

### 2. Modifications des informations

#### A. Modification d'adresse IP -
pt. 1

Je suis rentré sur la gestion de
partage et réseaux et j’ai accédé aux propriétés du réseau.

https://github.com/lucasreq/TPreseau2_LucasRequena/blob/master/Images/I.%20Exploration%20locale%20en%20solo/I.2.png

#### B. nmap

Grace a la commande nmap -sn -PE 

Nous obtenons cela :

https://github.com/lucasreq/TPreseau2_LucasRequena/blob/master/Images/I.%20Exploration%20locale%20en%20solo/I.3.png
 
#### C. Modification d'adresse IP

https://github.com/lucasreq/TPreseau2_LucasRequena/blob/master/Images/I.%20Exploration%20locale%20en%20solo/I.4.png

https://github.com/lucasreq/TPreseau2_LucasRequena/blob/master/Images/I.%20Exploration%20locale%20en%20solo/I.5.png

Après le changement de gateway je n'ai eu aucuns problemes pour aller sur internet

## II. Exploration locale en duo

### Firewall

1.Ouvrir le Pare-feu Windows, soit par la recherche intégrée, soit par le Menu Démarrer,
Outils d’administration Windows, **Pare-feu
Windows avec fonctions avancées de sécurité**.

2.Dans le menu de gauche, cliquer sur « **Règles de trafic entrant** » :

3. Dans le menu de gauche, cliquer sur « **Règles
de trafic entrant** » :

https://github.com/lucasreq/TPreseau2_LucasRequena/blob/master/Images/II.%20Firewall/II.1.png

4.Dans le menu de droite, cliquer sur « **Nouvelle règle** » .

5. Au premier écran Type de
règle, choisir « **Personnalisée** »
et faire **Suivant**.

https://github.com/lucasreq/TPreseau2_LucasRequena/blob/master/Images/II.%20Firewall/II.2.png


6.Laisser « **Tous les
programmes** » puis **Suivant**.

7. Ouvrir la liste « Type
de protocole » pour sélectionner « **ICMPv4** » qui correspond au ping
(Internet Control Message Protocol). Ne pas changer les autres options de cet
écran.

https://github.com/lucasreq/TPreseau2_LucasRequena/blob/master/Images/II.%20Firewall/II.3.png

8.Dans la partie Etendue, laisser « **Toute
adresse IP** » dans les deux champs s’il n’y a pas de
contrainte particulière. Sinon, indiquer les adresses IP précises, les plages
d’IP ou les sous-réseaux autorisés à pinguer la machine.

 

9. Quelle action entreprendre? « **Autoriser la
connexion** » pour répondre aux requêtes ping depuis un
autre poste.
 
https://github.com/lucasreq/TPreseau2_LucasRequena/blob/master/Images/II.%20Firewall/II.4.png

10. Définir sur quels réseaux cette nouvelle règle doit être
appliquée : **ne cocher que Domaine** pour éviter
que le ping soit autorisé sur une autre connexion que celle de l’entreprise (ce
qui ne devrait pas changer pour un serveur).

https://github.com/lucasreq/TPreseau2_LucasRequena/blob/master/Images/II.%20Firewall/II.5.png
 
11. Donner un **nom** à cette règle
firewall et cliquer sur **Terminer** pour la
valider.

12. Le ping est
immédiatement fonctionnel depuis un autre PC du réseau

https://github.com/lucasreq/TPreseau2_LucasRequena/blob/master/Images/II.%20Firewall/II.6.png

## III. Manipulations d'autres outils/protocoles côté client

### 1. DHCP
grâce a la commande netstat /all nous obtenons l'IP de l'adresse DHCP
https://github.com/lucasreq/TPreseau2_LucasRequena/blob/master/Images/III.Manipulation%20d'autres%20outils/DHCP-1.JPG

pour avoir une nouvelle adresse ip il faut procéder a plusieurs lignes de commandes dans le cmd:
* ```ipconfig /flushdns``` cette commande reinitialise le contenu du cache DNS
* ```ipconfig /release```  cette commande libere la configuration DHCP et libere la configuration d’adresse IP de toutes les cartes réseaux
* ```ipconfig /renew```  cette commande renouvelle la configuration DHCP de toutes les cartes…
C’est à dire qu’elle renouvelle sa connexion au serveur DHCP

### 2. DNS
En utilisant ```nslookup``` sur les deux exemples "google.com" et "ynov.com"
j'obtiens ceci:
https://github.com/lucasreq/TPreseau2_LucasRequena/blob/master/Images/III.Manipulation%20d'autres%20outils/DNS-%201.png

Ensuite pour faire un reverse lookup sur les exemples j'ai simplement réutiliser 
nmap car grâce a une adresse on peut trouver un nom de domaine et j'ai obtenu ceci:
https://github.com/lucasreq/TPreseau2_LucasRequena/blob/master/Images/III.Manipulation%20d'autres%20outils/DNS-2.png
 

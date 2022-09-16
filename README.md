# Keke_Voyage

## Dictionnaire de données

---

|NOM             |TYPE                           |DESIGNATION                  |
|----------------|-------------------------------|-----------------------------|
|ID_Client       |Alphanumérique                 |ID du client                 |
|Nom             |Alphanumérique                 |Nom du client                |
|Prénom          |Alphanumérique                 |Prénom du client             |
|DDN             |Date                           |Date de naissance du client  |
|Email           |Alphanumérique                 |Adresse mail du client       |
|Téléphone       |Alphanumérique                 |Numéro de téléphone du client|
|////////////////|///////////////////////////////|/////////////////////////////|
|ID_Compagnie    |Alphanumérique|ID de la compagnie aérienne|
|Nom             |Alphanumérique|Nom de la compagnie aérienne|
|////////////////|///////////////////////////////|/////////////////////////////|
|ID_vol          |Alphanumérique|ID du vol|
|Compagnie       |Alphanumérique|ID de la compagnie assurant le vol|
|Date de départ  |Datetime|Date et heure de départ du vol|
|Aéroport de départ|Alphanumérique|ID de l'aéroport de départ du vol|
|Aéroport d'arrivée|Alphanumérique|ID de l'aéroport d'arrivée du vol|
|Ouvrir_vol      |Boolean|Ouverture de la réservation par la compagnie|
|Fermer_vol      |Boolean|Fermeture de la réservation par la compagnie|
|Escale          |Alphanumérique|ID de l'aéroport de l'escale|
|////////////////|///////////////////////////////|/////////////////////////////|
|ID_Aéroport     |Alphanumérique|ID de l'aéroport|
|Villes desservies|Alphanumérique|Villes desservies par l'aéroport|
|Vols au départ  |Alphanumérique|ID des vols au départ de l'aéroport|
|Vols à l'arrivée|Alphanumérique|ID des vols à l'arrivée de l'aéroport|
|////////////////|///////////////////////////////|/////////////////////////////|
|ID_Escale       |Alphanumérique|ID de l'aéroport de l'escale du vol|
|Heure d'arrivée  |Time|Heure d'arrivée du vol|
|Heure de départ  |Time|Heure de départ du vol|

---

## Régles de gestion

### Client

* Afin que le client passe une commande, nous demandons son nom, son prénom, sa date de naissance, son adresse mail et son numéro de téléphone puis se créer automatique un id_client afin de l'identifier plus facilement par la suite.

* Lorsqu'un client éffectue une commande donc dans notre cas éffectue une reservation de vol, on lui confere le numéro de vol (ID_vol) le nom de la compagnie, la date de départ, l'heure de départ, le lieu qu'il aura choisi via la ville (ID_aeroport), les éventuelles escales (pas obligatoirement), destination. 

* Un client peut réserver plusieur billet ainsi un client n'est pas forcement un passager. Le client peut également réservé pour une personne tierce.


### Passager

* Le passager peut être un client, dans le sens ou c'est la même personne qui a commander un billet d'avion pour lui même. 

* Sans réservation, il n'y a pas de passager. Donc sans client pas de passager, passager dépend de client. 

* Un numéro de réservation par réservation, donc un numéro de réservation est un passager.

### Compagnie

* Si le client recoit bien le billet cela veut donc dire que la compagnie a créé le vol et qu'il est bien disponible (ouvrirVol = true). La compagnie peut toujours fermer le vol (fermerVol = true) dans ce cas le vol n'est plus disponible et le programme avertira automatique le client que son vol identifer grâce à son ID est annulé. 

* Les vols depende des compagnies, chaque compagnie possède ces propres vols.

### Vol

* Sans réservation donc sans client, aucun passager dans ce sens, aucune utilité à éffectuer le vol à vide.

* Vol dépend de la compagnie, il est créer par la compagnie et peut être aussi supprimer. 

* Un vol possède un point de départ et point d'arrivé (c'est mieux), donc un vol possède un aéroport de départ et un aéroport d'arrivé.

* Un vol possède une date et une heure de départ et également une date et une heure d'arrivé.

* Le vol possède donc une destination.

### Aéroport 

* Un aéroport peut avoir plusieurs vols. 

* Un aéroport dessert plusieurs villes (sinon peut de but de prendre l'avion).

### Escale 

*  Une escale est un héritage de l'aéroport étant donné que pour les passager cette escale (aéroport) n'est pas leur destination final, d'ou le nom escale.

* L'escale possède une heure d'arrivé, une heure de départ et un id (ID_escale).

---

## Ressource, lien 

* https://www.youtube.com/watch?v=0MwBeTq07JM

* https://www.devdesignbook.tiankod.fr/dynamique/use_case/

* https://www.devdesignbook.tiankod.fr/sgbd/merise/mpd/

* https://www.devdesignbook.tiankod.fr/sgbd/merise/mld/

* https://infocenter-archive.sybase.com/help/index.jsp?topic=/com.sybase.stf.poweramc.docs_12.0.0/html/mcgu/mcgup29.htm

* https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=fr

* 

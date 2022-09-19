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

# Requête SQL

```sql
CREATE TABLE Client(
   Id_Client COUNTER,
   Id_Passager VARCHAR(50),
   Nom VARCHAR(50),
   Prénom VARCHAR(50),
   Date_de_naissance DATE,
   Email VARCHAR(50),
   Numéro_de_téléphone VARCHAR(50),
   PRIMARY KEY(Id_Client, Id_Passager)
);

CREATE TABLE Vol(
   Id_Vol COUNTER,
   Compagnie VARCHAR(50),
   Aéroport_de_départ VARCHAR(50),
   Aéroport_d_arrivée VARCHAR(50),
   Escale VARCHAR(50),
   Date_de_départ DATETIME,
   Date_d_arrivée DATETIME,
   Destination VARCHAR(50),
   Ouvrir_Vol LOGICAL,
   Fermer_Vol LOGICAL,
   PRIMARY KEY(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale)
);

CREATE TABLE Compagnie(
   Id_Compagnie COUNTER,
   Nom VARCHAR(50),
   PRIMARY KEY(Id_Compagnie)
);

CREATE TABLE Aéroport(
   Id_Aéroport COUNTER,
   Vols_au_départ VARCHAR(50),
   Vols_à_l_arrivée VARCHAR(50),
   Villes_desservies VARCHAR(50),
   PRIMARY KEY(Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée)
);

CREATE TABLE Passager(
   Id_Passager COUNTER,
   Id_Vol COUNTER,
   Id_Client VARCHAR(50),
   Nom VARCHAR(50),
   Prenom VARCHAR(50),
   Numéro_de_passeport VARCHAR(50),
   PRIMARY KEY(Id_Passager, Id_Vol, Id_Client)
);

CREATE TABLE Escale(
   Id_Escale COUNTER,
   Heure_d_arrivé TIME,
   Heure_de_départ TIME,
   Id_Aéroport INT NOT NULL,
   Vols_au_départ VARCHAR(50) NOT NULL,
   Vols_à_l_arrivée VARCHAR(50) NOT NULL,
   PRIMARY KEY(Id_Escale),
   UNIQUE(Id_Aéroport),
   UNIQUE(Vols_au_départ),
   UNIQUE(Vols_à_l_arrivée),
   FOREIGN KEY(Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée) REFERENCES Aéroport(Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée)
);

CREATE TABLE Reserver(
   Id_Client INT,
   Id_Passager VARCHAR(50),
   Id_Vol INT,
   Compagnie VARCHAR(50),
   Aéroport_de_départ VARCHAR(50),
   Aéroport_d_arrivée VARCHAR(50),
   Escale VARCHAR(50),
   Id_Passager_1 INT,
   Id_Vol_1 INT,
   Id_Client_1 VARCHAR(50),
   PRIMARY KEY(Id_Client, Id_Passager, Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale, Id_Passager_1, Id_Vol_1, Id_Client_1),
   FOREIGN KEY(Id_Client, Id_Passager) REFERENCES Client(Id_Client, Id_Passager),
   FOREIGN KEY(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale) REFERENCES Vol(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale),
   FOREIGN KEY(Id_Passager_1, Id_Vol_1, Id_Client_1) REFERENCES Passager(Id_Passager, Id_Vol, Id_Client)
);

CREATE TABLE Assurer(
   Id_Vol INT,
   Compagnie VARCHAR(50),
   Aéroport_de_départ VARCHAR(50),
   Aéroport_d_arrivée VARCHAR(50),
   Escale VARCHAR(50),
   Id_Compagnie INT,
   PRIMARY KEY(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale, Id_Compagnie),
   FOREIGN KEY(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale) REFERENCES Vol(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale),
   FOREIGN KEY(Id_Compagnie) REFERENCES Compagnie(Id_Compagnie)
);

CREATE TABLE Atterrir(
   Id_Vol INT,
   Compagnie VARCHAR(50),
   Aéroport_de_départ VARCHAR(50),
   Aéroport_d_arrivée VARCHAR(50),
   Escale VARCHAR(50),
   Id_Aéroport INT,
   Vols_au_départ VARCHAR(50),
   Vols_à_l_arrivée VARCHAR(50),
   PRIMARY KEY(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale, Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée),
   FOREIGN KEY(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale) REFERENCES Vol(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale),
   FOREIGN KEY(Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée) REFERENCES Aéroport(Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée)
);

CREATE TABLE Decollage(
   Id_Vol INT,
   Compagnie VARCHAR(50),
   Aéroport_de_départ VARCHAR(50),
   Aéroport_d_arrivée VARCHAR(50),
   Escale VARCHAR(50),
   Id_Aéroport INT,
   Vols_au_départ VARCHAR(50),
   Vols_à_l_arrivée VARCHAR(50),
   PRIMARY KEY(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale, Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée),
   FOREIGN KEY(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale) REFERENCES Vol(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale),
   FOREIGN KEY(Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée) REFERENCES Aéroport(Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée)
);
```

## Ressource, lien 

* https://www.youtube.com/watch?v=0MwBeTq07JM

* https://www.devdesignbook.tiankod.fr/dynamique/use_case/

* https://www.devdesignbook.tiankod.fr/sgbd/merise/mpd/

* https://www.devdesignbook.tiankod.fr/sgbd/merise/mld/

* https://infocenter-archive.sybase.com/help/index.jsp?topic=/com.sybase.stf.poweramc.docs_12.0.0/html/mcgu/mcgup29.htm

* https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=fr

* 

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
|Date de départ  |Alphanumérique|Date et heure de départ du vol|
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
|Heure d'arrivée  |Alphanumérique|Heure d'arrivée du vol|
|Heure de départ  |Alphanumérique|Heure de départ du vol|

---

## Régles de gestion

### Client

* Afin que le client passe une commande, nous demandons son nom, son prénom, sa date de naissance, son adresse mail et son numéro de téléphone puis se créer automatique un id_client afin de l'identifier plus facilement par la suite.

* Lorsqu'un client éffectue une commande donc dans notre cas éffectue une reservation de vol, on lui confere le numéro de vol (ID_vol) le nom de la compagnie, la date de départ, l'heure de départ, le lieu qu'il aura choisi via la ville (ID_aeroport), les éventuelles escales (pas obligatoirement), destination. 

### Compagnie

* Si le client recoit bien le billet cela veut donc dire que la compagnie a créé le vol et qu'il est bien disponible (ouvrirVol = true). La compagnie peut toujours fermer le vol (fermerVol = true) dans ce cas le vol n'est plus disponible et le programme avertira automatique le client que son vol identifer grâce à son ID est annulé. 

### Vol

*  Une escale est un héritage de l'aéroport étant donné que pour les passager cette escale (aéroport) n'est pas leur destination final, d'ou le nom escale.

*  

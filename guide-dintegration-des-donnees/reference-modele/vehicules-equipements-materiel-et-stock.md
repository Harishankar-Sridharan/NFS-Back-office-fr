---
description: >-
  Référence du modèle d'échange : entités et champs du domaine Véhicules,
  équipements, matériel et stock.
---

# Véhicules, équipements, matériel et stock

## Véhicule (Vehicle)

Définition des véhicules

**Identifiant :** VEHICLEID · **Obligatoires :** VEHICLEID, VEHICLENAME

| Champ                                                             | Type        | Obl. | I/E | Réf.     | Description                                                                                                                                                          | Exemple / défaut                          |
| ----------------------------------------------------------------- | ----------- | ---- | --- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------- |
| VEHICLEID                                                         | Identifiant | Oui  | I/E |          | Identifiant du véhicule                                                                                                                                              |                                           |
| VEHICLENAME                                                       | Chaîne      | Oui  | I/E |          | Nom du véhicule tel qu'il apparaîtra à l'utilisateur                                                                                                                 |                                           |
| FLEETNAME                                                         | Chaîne      |      | I/E |          | Nom de la flotte à laquelle ce véhicule appartient                                                                                                                   |                                           |
| VEHICLETYPE                                                       | Entier      |      | I/E |          | Type de véhicule                                                                                                                                                     |                                           |
| DESCRIPTION                                                       | Chaîne      |      | I/E |          | Commentaire pour décrire ce véhicule                                                                                                                                 |                                           |
| AREAID                                                            | Réf.        |      | I/E | Area     | Région d'appartenance de ce véhicule                                                                                                                                 | REG\_001                                  |
| WORKSITEID                                                        | Réf.        |      | I/E | Worksite | Agence d'appartenance de ce véhicule                                                                                                                                 | WKS\_001                                  |
| QUANTITY1\_MAX … QUANTITY5\_MAX                                   | Entier      |      | I/E |          | Poids maximum transporté par le véhicule (série de 5 champs)                                                                                                         |                                           |
| QUANTITY1\_BEGIN … QUANTITY5\_BEGIN (synonyme : QUANTITY1\_START) | Entier      |      | I/E |          | Quota1 au départ supporté par le véhicule (série de 5 champs)                                                                                                        |                                           |
| QUANTITY1\_END … QUANTITY5\_END                                   | Entier      |      | I/E |          | Poids à l'arrivée transporté par le véhicule (série de 5 champs)                                                                                                     |                                           |
| CO2                                                               | Réel        |      | I/E |          | Quantité de CO2 rejeté par le véhicule aux 100 km                                                                                                                    |                                           |
| SPEEDMAX                                                          | Réel        |      | I/E |          | Vitesse maximale du véhicule                                                                                                                                         |                                           |
| COST\_BY\_KM                                                      | Réel        |      | I/E |          | Coût kilométrique du véhicule                                                                                                                                        |                                           |
| COST\_BY\_DAY                                                     | Réel        |      | I/E |          | Coût quotidien d'utilisation du véhicule                                                                                                                             |                                           |
| CONTROL\_DATE                                                     | Date        |      | I/E |          | Date du prochain contrôle technique du véhicule                                                                                                                      |                                           |
| MANUFACTURE\_DATE                                                 | Date        |      | I/E |          | Date de fabrication du véhicule                                                                                                                                      |                                           |
| LICENSE                                                           | Chaîne      |      | I/E |          | Immatriculation du véhicule                                                                                                                                          |                                           |
| ABBREVIATION                                                      | Chaîne      |      | I/E |          | Abréviation                                                                                                                                                          |                                           |
| GROUPNAME                                                         | Chaîne      |      | I/E |          | Nom du groupe                                                                                                                                                        |                                           |
| ROUTINGPROFILE                                                    | Chaîne      |      | I/E |          | Profile d'itinéraire (=Undefined;1=Car;3=Truck;5=Light delivery vehicle;7=Delivery truck;8=Bus;9=Emergency vehicle;10=Emergency truck;11=Taxi;13=Bike;14=Pedestrian) |                                           |
| LOADING1\_MAX                                                     | Entier      |      | I/E |          | Maximum weight carried by the vehicle                                                                                                                                |                                           |
| LOADING2\_MAX                                                     | Entier      |      | I/E |          | Maximum volume transported by the vehicle                                                                                                                            |                                           |
| LOADING1\_BEGIN                                                   | Entier      |      | I/E |          | Initial weight carried by the vehicle                                                                                                                                |                                           |
| LOADING2\_BEGIN                                                   | Entier      |      | I/E |          | Initial volume carried by the vehicle                                                                                                                                |                                           |
| LOADING1\_END                                                     | Entier      |      | I/E |          | Poids à l'arrivée transporté par le véhicule                                                                                                                         |                                           |
| LOADING2\_END                                                     | Entier      |      | I/E |          | Volume à l'arrivée transporté par le véhicule                                                                                                                        |                                           |
| MOTORIZATION                                                      | Chaîne      |      | I/E |          | Motorization                                                                                                                                                         | ELECTRIC,THERMIC,HYBRID                   |
| CHARGINGPLUGCOMPATIBILITY                                         | Chaîne      |      | I/E |          | Charging plug compatibility                                                                                                                                          | LEVEL0,LEVEL1,LEVEL2,LEVEL3,LEVEL4,LEVEL5 |
| POWERBYDISTANCE                                                   | Réel        |      | I/E |          | Power by distance                                                                                                                                                    |                                           |
| BATTERYCAPACITY                                                   | Réel        |      | I/E |          | Battery capacity(by Kwh)                                                                                                                                             |                                           |
| DISTANCEAUTONOMY                                                  | Entier      |      | I/E |          | Distance autonomy(by Km)                                                                                                                                             |                                           |
| BATTERYDATEBEGIN                                                  | Date        |      | I/E |          | Battery date begin                                                                                                                                                   |                                           |

## Équipement de suivi (Equipment)

Définition des équipements de suivi GPS (Tracking)

**Identifiant :** EQUIPMENTID · **Obligatoires :** EQUIPMENTID, EQUIPMENTNAME

| Champ         | Type        | Obl. | I/E | Réf. | Description                                                                 | Exemple / défaut |
| ------------- | ----------- | ---- | --- | ---- | --------------------------------------------------------------------------- | ---------------- |
| EQUIPMENTID   | Identifiant | Oui  | I/E |      | Identifiant de l'équipement de géolocalisation                              |                  |
| EQUIPMENTNAME | Chaîne      | Oui  | I/E |      | Nom de l'équipement de géolocalisation tel qu'il apparaitra à l'utilisateur |                  |
| EQUIPMENTTYPE | Chaîne      |      | I/E |      | Type de l'équipement de géolocalisation                                     |                  |
| DESCRIPTION   | Chaîne      |      | I/E |      | Commentaire pour décrire cet équipement de géolocalisation                  |                  |
| AREAID        | Réf.        |      | I/E | Area | Région d'appartenance de cet équipement de géolocalisation                  | REG\_001         |
| ACTIVE        | Booléen     |      | I/E |      | Activation (1,"O",true) / Désactivation du site/client (0,"N",false)        | 1 ; défaut : 1   |
| ABBREVIATION  | Chaîne      |      | I/E |      | Abréviation                                                                 |                  |

## Position de l'équipement de suivi (EquipmentPosition)

Position de l'équipement surveillé par GPS (suivi)

**Identifiant :** — · **Obligatoires :** EQUIPMENTID, POSITION\_DATETIME

| Champ              | Type       | Obl. | I/E | Réf.          | Description                                                                             | Exemple / défaut |
| ------------------ | ---------- | ---- | --- | ------------- | --------------------------------------------------------------------------------------- | ---------------- |
| EQUIPMENTID        | Réf.       | Oui  | I/E | Equipment     | Identifiant de l'équipement de géolocalisation                                          |                  |
| POSITION\_DATETIME | Date-heure | Oui  | I/E |               | Date et heure de la dernière position de l'équipememt                                   |                  |
| RESOURCEID         | Réf.       |      | E   | HumanResource | Identifiant d'intervenant affecté à l'équipement                                        |                  |
| VEHICLEID          | Réf.       |      | E   | Vehicle       | Identifiant de véhicule affecté à l'équipement                                          |                  |
| XGEO               | Longitude  |      | I/E |               | Commentaire pour décrire cet équipement de géolocalisation                              |                  |
| YGEO               | Latitude   |      | I/E |               | Région d'appartenance de cet équipement de géolocalisation                              |                  |
| SPEED              | Entier     |      | I/E |               | Vitesse de l'équipement mobile                                                          |                  |
| BEARING            | Entier     |      | I/E |               | Orientation de l'équipement mobile                                                      |                  |
| STATUS             | Entier     |      | I/E |               | État de l'équipement mobile                                                             |                  |
| FLAGS              | Entier     |      | I/E |               | Flags binaires décrivant l'état de l'équipement                                         |                  |
| POSITION\_METHOD   | Entier     |      | I/E |               | Méthode de positionnement                                                               |                  |
| ACCURACY           | Entier     |      | I/E |               | Précision de l'équipement mobile                                                        |                  |
| GPS\_STATUS        | Entier     |      | I/E |               | État du signal GPS de l'équipement mobile (0: aucun signal, 1: en ligne, 2: hors ligne) |                  |
| BATTERYLEVEL       | Entier     |      | I/E |               | Niveau de la batterie de l'équipement mobile (en %)                                     |                  |

## Hr-Vehicle-Equipment (HrVehicleEquipment)

Définition des affectations temporelles entre la ressource, l'équipement GPS et le véhicule

**Identifiant :** — · **Obligatoires :** RESOURCEID, VEHICLEID

| Champ                              | Type         | Obl. | I/E | Réf.          | Description                                                                                           | Exemple / défaut |
| ---------------------------------- | ------------ | ---- | --- | ------------- | ----------------------------------------------------------------------------------------------------- | ---------------- |
| RESOURCEID                         | Réf.         | Oui  | I/E | HumanResource | Identifiant de la ressource qui est à bord du véhicule                                                |                  |
| EQUIPMENTID                        | Réf.         |      | I/E | Equipment     | Identifiant de l'équipement de géolocalisation                                                        |                  |
| VEHICLEID                          | Réf.         | Oui  | I/E | Vehicle       | Identifiant du véhicule                                                                               |                  |
| STARTDATE (synonyme : START\_DATE) | Date (début) |      | I/E |               | Date de début de l'association entre la ressource, le véhicule et/ou l'équipement de géolocalisation  |                  |
| ENDDATE (synonyme : END\_DATE)     | Date (fin)   |      | I/E |               | Date de fin de l'association entre la ressource, le véhicule et/ou l'équipement de géolocalisation    |                  |
| STARTTIME (synonyme : START\_TIME) | Heure        |      | I/E |               | Heure de début de l'association entre la ressource, le véhicule et/ou l'équipement de géolocalisation |                  |
| ENDTIME (synonyme : END\_TIME)     | Heure        |      | I/E |               | Heure de fin de l'association entre la ressource, le véhicule et/ou l'équipement de géolocalisation   |                  |
| ACTION                             | Chaîne       |      | I/E |               | Verbe d'action pour supprimer l'enregistrement (DELETE)                                               |                  |

## Matériel (Supply)

Définition de l'entité matériel

**Identifiant :** — · **Obligatoires :** SUPPLYID, SUPPLYNAME

| Champ                  | Type       | Obl. | I/E | Réf.     | Description                                                                                   | Exemple / défaut |
| ---------------------- | ---------- | ---- | --- | -------- | --------------------------------------------------------------------------------------------- | ---------------- |
| SUPPLYID               | Chaîne     | Oui  | I/E |          | Identifiant du matériel                                                                       | SC001            |
| SUPPLYNAME             | Chaîne     | Oui  | I/E |          | Nom du matériel                                                                               |                  |
| DESCRIPTION            | Chaîne     |      | I/E |          | Description                                                                                   |                  |
| AREAID                 | Réf.       |      | I/E | Area     | Région à laquelle ce matériel appartient                                                      | REG\_001         |
| STOCK                  | Réel       |      | I/E |          | Stock                                                                                         | 10               |
| LOADING                | Réel       |      | I/E |          | Chargement (ex: poids)                                                                        | 10               |
| STOCK2                 | Réel       |      | I/E |          | Stock2                                                                                        | 10               |
| LOADING2               | Réel       |      | I/E |          | Chargement2 (ex: volume)                                                                      | 10               |
| DURATION               | Durée      |      | I/E |          | Durée                                                                                         | 30               |
| MANPOWER               | Entier     |      | I/E |          | Ressources humaines demandées                                                                 |                  |
| PRIORITY               | Entier     |      | I/E |          | Priorité                                                                                      |                  |
| ACTIVE                 | Booléen    |      | I/E |          | Activation (1,"O",true) / Désactivation du site/client (0,"N",false)                          | 1 ; défaut : 1   |
| ABBREVIATION           | Chaîne     |      | I/E |          | Abréviation                                                                                   |                  |
| FILLER1 … FILLER10     | Texte      |      | I/E |          | Champ de donnée libre de type texte (alphanumérique) (série de 10 champs)                     |                  |
| QUANTITY1 … QUANTITY10 | Réel       |      | I/E |          | Champ de donnée libre de type numérique (réel) (série de 10 champs)                           | -100.50          |
| LOGICAL1 … LOGICAL10   | Booléen    |      | I/E |          | Champ de donnée libre de type oui/non (booléen) 1/0 ou O/N ou true/false (série de 10 champs) | 1                |
| DATE1 … DATE10         | Date       |      | I/E |          | Champ de données libre de type Date (série de 10 champs)                                      | 16/01/2012       |
| DATETIME1 … DATETIME10 | Date-heure |      | I/E |          | Champ de données libre de type Date/Heure (même date que DATE1) (série de 10 champs)          | 2012/01/16 08:00 |
| WORKSITEID             | Réf.       |      | I/E | Worksite | Identifiant du site de travail                                                                | WS001            |

## Affectation de matériel (SupplyResource)

Affectation de matériel à un intervenant

**Identifiant :** — · **Obligatoires :** SUPPLYID, RESOURCEID

| Champ              | Type         | Obl. | I/E | Réf.          | Description                                                              | Exemple / défaut |
| ------------------ | ------------ | ---- | --- | ------------- | ------------------------------------------------------------------------ | ---------------- |
| SUPPLYASSIGNMENTID | Chaîne       |      | I/E |               | Identifant d'affectation de matériel                                     |                  |
| SUPPLYID           | Réf.         | Oui  | I/E | Supply        | Identifiant d'affectation d'intervenant / de matériel                    | SUP01            |
| RESOURCEID         | Réf.         | Oui  | I/E | HumanResource | Identifiant de l'intervenant                                             | HR001            |
| STARTDATE          | Date (début) |      | I/E |               | Date de fin de la période de travail de cette ressource pour ce matériel |                  |
| ENDDATE            | Date (début) |      | I/E |               | Date de fin de la période de travail de cette ressource pour ce matériel |                  |
| ACTION             | Chaîne       |      | I/E |               | Verbe d'action pour supprimer l'enregistrement (DELETE)                  |                  |

## Produit (Product)

Définition de l'entité produit

**Identifiant :** — · **Obligatoires :** PRODUCTID, PRODUCTNAME, PRODUCTFAMILYID

| Champ                  | Type       | Obl. | I/E | Réf.          | Description                                                                                   | Exemple / défaut |
| ---------------------- | ---------- | ---- | --- | ------------- | --------------------------------------------------------------------------------------------- | ---------------- |
| PRODUCTID              | Chaîne     | Oui  | I/E |               | Identifiant du produit                                                                        | PRD001           |
| PRODUCTNAME            | Chaîne     | Oui  | I/E |               | Nom du produit                                                                                |                  |
| PRODUCTFAMILYID        | Réf.       | Oui  | I/E | ProductFamily | Identifiant de la famille de produits                                                         | PRDFAM001        |
| AREAID                 | Réf.       |      | I/E | Area          | Région à laquelle ce produit appartient                                                       | REG\_001         |
| STOCK                  | Réel       |      | I/E |               | Stock                                                                                         | 10               |
| LOADING                | Réel       |      | I/E |               | Chargement (ex: poids)                                                                        | 10               |
| STOCK2                 | Réel       |      | I/E |               | Stock2                                                                                        | 10               |
| LOADING2               | Réel       |      | I/E |               | Chargement2 (ex: volume)                                                                      | 10               |
| DURATION               | Durée      |      | I/E |               | Durée                                                                                         | 30               |
| MANPOWER               | Entier     |      | I/E |               | Ressources humaines demandées                                                                 |                  |
| PRIORITY               | Entier     |      | I/E |               | Priorité                                                                                      |                  |
| ACTIVE                 | Booléen    |      | I/E |               | Activation (1,"O",true) / Désactivation du site/client (0,"N",false)                          | 1 ; défaut : 1   |
| ABBREVIATION           | Chaîne     |      | I/E |               | Abréviation                                                                                   |                  |
| FILLER1 … FILLER10     | Texte      |      | I/E |               | Champ de donnée libre de type texte (alphanumérique) (série de 10 champs)                     |                  |
| QUANTITY1 … QUANTITY10 | Réel       |      | I/E |               | Champ de donnée libre de type numérique (réel) (série de 10 champs)                           | -100.50          |
| LOGICAL1 … LOGICAL10   | Booléen    |      | I/E |               | Champ de donnée libre de type oui/non (booléen) 1/0 ou O/N ou true/false (série de 10 champs) | 1                |
| DATE1 … DATE10         | Date       |      | I/E |               | Champ de données libre de type Date (série de 10 champs)                                      | 16/01/2012       |
| DATETIME1 … DATETIME10 | Date-heure |      | I/E |               | Champ de données libre de type Date/Heure (même date que DATE1) (série de 10 champs)          | 2012/01/16 08:00 |
| DESCRIPTION            | Chaîne     |      | I/E |               | Description                                                                                   |                  |
| WORKSITEID             | Réf.       |      | I/E | Worksite      | Identifiant du site de travail                                                                |                  |
| UNITPRICE              | Réel       |      | I/E |               | Prix unitaire                                                                                 |                  |

## Famille de produits (ProductFamily)

Définition de l'entité famille de produits

**Identifiant :** — · **Obligatoires :** PRODUCTFAMILYID, PRODUCTFAMILYNAME

| Champ             | Type    | Obl. | I/E | Réf. | Description                                                          | Exemple / défaut |
| ----------------- | ------- | ---- | --- | ---- | -------------------------------------------------------------------- | ---------------- |
| PRODUCTFAMILYID   | Chaîne  | Oui  | I/E |      | Identifiant de la famille de produits                                | PRDFAM001        |
| PRODUCTFAMILYNAME | Chaîne  | Oui  | I/E |      | Nom de la famille de produits                                        |                  |
| DESCRIPTION       | Chaîne  |      | I/E |      | Description                                                          |                  |
| ABBREVIATION      | Chaîne  |      | I/E |      | Abréviation                                                          |                  |
| AREAID            | Réf.    |      | I/E | Area | Région à laquelle cette famille de produits appartient               | REG\_001         |
| ACTIVE            | Booléen |      | I/E |      | Activation (1,"O",true) / Désactivation du site/client (0,"N",false) | 1 ; défaut : 1   |

## Stock (Stock)

Définition de l'entité Stock

**Identifiant :** — · **Obligatoires :** STOCKAMOUNT, PRODUCTID

| Champ                   | Type   | Obl. | I/E | Réf.          | Description                                                      | Exemple / défaut |
| ----------------------- | ------ | ---- | --- | ------------- | ---------------------------------------------------------------- | ---------------- |
| STOCKAMOUNT             | Entier | Oui  | I/E |               | Quantité de stock                                                | 10               |
| THRESHOLD               | Entier |      | I/E |               | Seuil de stock                                                   | 2                |
| CAPACITY                | Entier |      | I/E |               | Capacité de stock                                                | 25               |
| DESCRIPTION             | Chaîne |      | I/E |               | Description du stock                                             |                  |
| WAREHOUSELOCATION       | Chaîne |      | I/E |               | Emplacement de l’entrepôt                                        |                  |
| WAREHOUSELOCATIONDETAIL | Chaîne |      | I/E |               | Détail de l’emplacement de l’entrepôt                            |                  |
| MAXOLDNESS              | Entier |      | I/E |               | Ancienneté maximale                                              |                  |
| LASTINVENTORYDATE       | Date   |      | I/E |               | Date du dernier inventaire                                       | 11/09/2023       |
| PRODUCTID               | Réf.   | Oui  | I/E | Product       | Identifiant du produit (se réfère à product.productid)           | PRD01            |
| WORKSITEID              | Réf.   |      | I/E | Worksite      | Identifiant du site de travail (se réfère à worksite.worksiteid) | WS01             |
| RESOURCEID              | Réf.   |      | I/E | HumanResource | Identifiant de la ressource (se réfère à resource.resourceid)    | HR01             |

## Mouvement de stock (StockMovement)

Définition de l'entité mouvement de stock

**Identifiant :** — · **Obligatoires :** MOVEPRODUCTID, SOURCESTOCKID, TARGETSTOCKID, MOVEMENTKIND, AMOUNT

| Champ         | Type   | Obl. | I/E | Réf.     | Description                                                  | Exemple / défaut                                                                       |
| ------------- | ------ | ---- | --- | -------- | ------------------------------------------------------------ | -------------------------------------------------------------------------------------- |
| MOVEPRODUCTID | Réf.   | Oui  | I/E | Product  | Identifiant du produit (se réfère à product.productid)       | PRD01                                                                                  |
| SOURCESTOCKID | Réf.   | Oui  | I/E |          | Identifiant du stock source (se réfère à stock)              | WS01                                                                                   |
| TARGETSTOCKID | Réf.   | Oui  | I/E |          | Identifiant du stock cible (se réfère à stock)               | WS02                                                                                   |
| MOVEMENTKIND  | Chaîne | Oui  | I/E |          | Type d’inventaire                                            | INVENTAIRE, LIQUIDATION, FROM\_SUPPLIER\_TO\_WS, FROM\_SUPPLIER\_TO\_HR, FROM\_WS\_TO… |
| AMOUNT        | Entier | Oui  | I/E |          | Montant                                                      |                                                                                        |
| DATEMOVEMENT  | Date   |      | I/E |          | Date de mouvement                                            | 11/09/2023                                                                             |
| SUPPLIERID    | Réf.   |      | I/E | Supplier | Identifiant du fournisseur (se réfère à supplier.supplierid) | Supp01                                                                                 |
| SUPPLIERNAME  | Chaîne |      | I/E |          | Nom du fournisseur                                           | ABC company                                                                            |
| CONSUMERKIND  | Chaîne |      | I/E |          | Type de consommateur                                         | CUSTOMER,PROJECT,APPOINTMENT                                                           |

## Fournisseur (Supplier)

Définition de l'entité Fournisseur

**Identifiant :** — · **Obligatoires :** SUPPLIERID, SUPPLIERNAME

| Champ        | Type    | Obl. | I/E | Réf.     | Description                                                      | Exemple / défaut |
| ------------ | ------- | ---- | --- | -------- | ---------------------------------------------------------------- | ---------------- |
| SUPPLIERID   | Chaîne  | Oui  | I/E |          | Identifiant du fournisseur                                       | SUP10            |
| SUPPLIERNAME | Chaîne  | Oui  | I/E |          | Nom du fournisseur                                               | ABC Co.,         |
| ABBREVIATION | Chaîne  |      | I/E |          | Abréviation du fournisseur                                       |                  |
| DESCRIPTION  | Chaîne  |      | I/E |          | Description                                                      |                  |
| ACTIVE       | Booléen |      | I/E |          | Actif                                                            |                  |
| AREAID       | Réf.    |      | I/E | Area     | Identifiant de la région (se réfère à area.areaid)               | REG01            |
| WORKSITEID   | Réf.    |      | I/E | Worksite | Identifiant du site de travail (se réfère à worksite.worksiteid) | WS01             |

---
description: >-
  Référence du modèle d'échange : entités et champs du domaine Sécurité et
  paramétrage.
---

# Sécurité et paramétrage

## Collection de droits (RightCollection)

Définition de la collection de droits

**Identifiant :** RIGHTCOLLECTIONNAME · **Obligatoires :** RIGHTCOLLECTIONNAME, RIGHTNAMES

| Champ               | Type        | Obl. | I/E | Réf. | Description                                                                                                                  | Exemple / défaut           |
| ------------------- | ----------- | ---- | --- | ---- | ---------------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| RIGHTCOLLECTIONNAME | Identifiant | Oui  | I/E |      | Nom de la collection de droits                                                                                               | Accès administrateur       |
| RIGHTNAMES          | Chaîne      | Oui  | I/E |      | Noms des droits                                                                                                              | ADMIN\_GUEST,ADMIN\_UPDATE |
| DESCRIPTION         | Chaîne      |      | I/E |      | Commentaire décrivant cette collection de droits                                                                             |                            |
| AREAID              | Réf.        |      | I/E | Area | Région à laquelle cette collection de droits appartient                                                                      | REG\_001                   |
| RIGHTCOLLECTIONID   | Chaîne      |      | I/E |      | Identifiant de la collection de droits (optionnel)                                                                           |                            |
| ABBREVIATION        | Chaîne      |      | I/E |      | Abréviation                                                                                                                  |                            |
| ACTION              | Chaîne      |      | I/E |      | Verbe d'action commandant certains comportements d'importation spécifiques (DELETE) pour retirer des droits de la collection |                            |

## Contenu de la collection de droits (RightCollectioncontent)

Définition de la collection de droits

**Identifiant :** — · **Obligatoires :** RIGHTCOLLECTIONNAME, RIGHTNAME

| Champ               | Type   | Obl. | I/E | Réf. | Description                                                                                                               | Exemple / défaut     |
| ------------------- | ------ | ---- | --- | ---- | ------------------------------------------------------------------------------------------------------------------------- | -------------------- |
| RIGHTCOLLECTIONNAME | Chaîne | Oui  | I/E |      | Nom de la collection de droits                                                                                            | Accès administrateur |
| RIGHTNAME           | Chaîne | Oui  | I/E |      | Nom du droit                                                                                                              | ADMIN\_GUEST         |
| DESCRIPTION         | Chaîne |      | I/E |      | Commentaire décrivant cette collection de droits                                                                          |                      |
| AREAID              | Réf.   |      | I/E | Area | Région à laquelle cette collection de droits appartient                                                                   | REG\_001             |
| RIGHTCOLLECTIONID   | Chaîne |      | I/E |      | Identifiant de la collection de droits (optionnel)                                                                        |                      |
| ABBREVIATION        | Chaîne |      | I/E |      | Abréviation                                                                                                               |                      |
| ACTION              | Chaîne |      | I/E |      | Verbe d'action commandant certains comportement spécifiques d'importation (DELETE) pour enlever un droit d'une collection |                      |

## Groupe (Group)

Définition du profil utilisateur

**Identifiant :** — · **Obligatoires :** GROUPNAME, COLLECTIONNAMES

| Champ                                             | Type          | Obl. | I/E | Réf.            | Description                                                                                                                          | Exemple / défaut                            |
| ------------------------------------------------- | ------------- | ---- | --- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------- |
| GROUPNAME (synonyme : USERGROUPNAME)              | Chaîne        | Oui  | I/E |                 | Nom du profil                                                                                                                        | Administrateur                              |
| COLLECTIONNAMES (synonyme : RIGHTCOLLECTIONNAMES) | Liste de réf. | Oui  | I/E | RightCollection | Noms des collections de droits                                                                                                       | Accès administrateur, Accès Centre d'appels |
| DESCRIPTION                                       | Chaîne        |      | I/E |                 | Commentaire décrivant ce profil utilisateur                                                                                          |                                             |
| AREAID                                            | Réf.          |      | I/E | Area            | Région à laquelle ce groupe appartient                                                                                               | REG\_001                                    |
| USERGROUPID                                       | Chaîne        |      | I/E |                 | Identifiant du groupe                                                                                                                |                                             |
| ABBREVIATION                                      | Chaîne        |      | I/E |                 | Abréviation                                                                                                                          |                                             |
| ACTION                                            | Chaîne        |      | I/E |                 | Verbe d'action commandant certains comportement spécifiques d'importation (DELETE) pour enlever une collection de droits d'un profil |                                             |

## Abonnement au journal d'application (ApplicationLogSubscription)

Souscrire aux détails de journalisation pour un profil utilisateur

**Identifiant :** — · **Obligatoires :** USERPROFILE, LOGTYPE, LOGLEVEL

| Champ               | Type   | Obl. | I/E | Réf. | Description                                                                                                                    | Exemple / défaut                                                                    |
| ------------------- | ------ | ---- | --- | ---- | ------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------- |
| USERPROFILE         | Chaîne | Oui  | I/E |      | Nom de profil utilisateur (non utilisé lorsque le champ RIGHTCOLLECTIONNAME est obligatoire)                                   | ADMIN                                                                               |
| LOGTYPE             | Chaîne | Oui  | I/E |      | Type de journal (peut être soit un code soit un nom)                                                                           | entity\_creation(100),entity\_update(150),entity\_disable(200),\<br/>import\_warn(… |
| LOGLEVEL            | Chaîne | Oui  | I/E |      | Niveau d'erreur (peut être un soit code soit un nom)                                                                           | DEBUG(10),INFO(20),ALERT(30),WARN(40),ERROR(50),SEVERE(60),FATAL(99);               |
| RIGHTCOLLECTIONNAME | Chaîne |      | I/E |      | Nom de collection de droits (il s'agit d'un champ optionnel utilisé avec le champ USERPROFILE, qui par défaut est obligatoire) | Accès administrateur                                                                |
| ACTION              | Chaîne |      | I/E |      | Verbe d'action pour supprimer l'enregistrement (DELETE)                                                                        |                                                                                     |

## Configuration personnalisée (CustomConfiguration)

Définition des propriétés de la configuration personnalisée

**Identifiant :** — · **Obligatoires :** CUSTOMCONFIGURATIONNAME, PROPERTYNAME

| Champ                   | Type    | Obl. | I/E | Réf. | Description                                                                              | Exemple / défaut |
| ----------------------- | ------- | ---- | --- | ---- | ---------------------------------------------------------------------------------------- | ---------------- |
| CUSTOMFAMILY            | Chaîne  |      | E   |      | Famille de la propriété                                                                  |                  |
| CUSTOMCATEGORY          | Chaîne  |      | E   |      | Catégorie de la propriété                                                                |                  |
| CUSTOMCONFIGURATIONNAME | Chaîne  | Oui  | I/E |      | Nom de la configuration personnalisée                                                    |                  |
| PROPERTYNAME            | Chaîne  | Oui  | I/E |      | Nom de la propriété                                                                      |                  |
| SUBSETNAME              | Chaîne  |      | I/E |      | Nom du sous-ensemble                                                                     |                  |
| DESCRIPTION             | Chaîne  |      | I/E |      | Description                                                                              |                  |
| PROPERTYVALUE           | Chaîne  |      | I/E |      | Valeur de la propriété                                                                   |                  |
| DEFAULTVALUE            | Chaîne  |      | E   |      | Valeur par défaut                                                                        |                  |
| ISOVERRIDDEN            | Booléen |      | I/E |      | Indique si la valeur par défaut a été écrasée par configuration (XML ou base de données) |                  |
| AREAID                  | Chaîne  |      | I/E |      | Région à laquelle cette configuration appartient                                         | REG\_001         |

## Apparence (Appearance)

Définition de l'apparence

**Identifiant :** APPEARANCEID · **Obligatoires :** APPEARANCEID

| Champ           | Type        | Obl. | I/E | Réf.     | Description                                             | Exemple / défaut                      |
| --------------- | ----------- | ---- | --- | -------- | ------------------------------------------------------- | ------------------------------------- |
| APPEARANCEID    | Identifiant | Oui  | I/E |          | Identifiant de l'apparence                              |                                       |
| APPEARANCENAME  | Chaîne      |      | I/E |          | Nom de l'apparence                                      |                                       |
| DESCRIPTION     | Chaîne      |      | I/E |          | Description                                             |                                       |
| CSSCLASS        | Chaîne      |      | I/E |          | Classe CSS                                              | gssevt.app.ttgAUTRE                   |
| HTMLCOLOR       | Chaîne      |      | I/E |          | Couleur HTML                                            | #ffd640                               |
| AREAID          | Réf.        |      | I/E | Area     | Région à laquelle cette apparence appartient            | REG\_001                              |
| ABBREVIATION    | Chaîne      |      | I/E |          | Abréviation                                             |                                       |
| OPACITY         | Entier      |      | I/E |          | Degré de transparence de l'apparence                    |                                       |
| THICKNESS       | Entier      |      | I/E |          | Épaisseur du style                                      |                                       |
| PHOTO           | Chaîne      |      | I/E |          | Chemin vers l'image                                     |                                       |
| WORKSITEID      | Réf.        |      | I/E | Worksite | Site de travail auquel cette apparence appartient       | WS001                                 |
| APPEARANCESTYLE | Texte       |      | I/E |          | Définition du style d'apparence                         | background-color: #d5a6bd !important; |
| ACTION          | Chaîne      |      | I/E |          | Verbe d'action pour supprimer l'enregistrement (DELETE) |                                       |

## Typologie (Typology)

Typologie

**Identifiant :** TYPOLOGYID · **Obligatoires :** TYPOLOGYID, TYPOLOGYNAME, ENTITY, FIELDNAME, GLOSSARYITEMID

| Champ                | Type        | Obl. | I/E | Réf.     | Description                                             | Exemple / défaut |
| -------------------- | ----------- | ---- | --- | -------- | ------------------------------------------------------- | ---------------- |
| TYPOLOGYID           | Identifiant | Oui  | I/E |          | Identifiant de la typologie                             | TYP01            |
| TYPOLOGYNAME         | Chaîne      | Oui  | I/E |          | Nom de la typologie                                     |                  |
| DESCRIPTION          | Chaîne      |      | I/E |          | Description                                             |                  |
| AREAID               | Réf.        |      | I/E | Area     | Région à laquelle cette typologie appartient            | REG\_001         |
| ENTITY               | Chaîne      | Oui  | I/E |          | _Description non renseignée dans le modèle._            |                  |
| FIELDNAME            | Chaîne      | Oui  | I/E |          | Nom du champ\r put("GROUP\_NAME","FILLER\_1")           | GROUP NAME       |
| GLOSSARYITEMID       | Identifiant | Oui  | I/E |          | Identifiant de l'élément du glossaire                   | G01              |
| RANK                 | Entier      |      | I/E |          | Rang                                                    |                  |
| LABEL                | Chaîne      |      | I/E |          | Nom de l'étiquette                                      |                  |
| CODE                 | Chaîne      |      | I/E |          | Code                                                    |                  |
| RESOURCEKEY          | Chaîne      |      | I/E |          | Clé de ressource                                        |                  |
| PARENTTYPOLOGYID     | Réf.        |      | I/E | Typology | Identifiant de la typologie parente                     | P01              |
| PARENTGLOSSARYITEMID | Identifiant |      | I/E |          | Identifiant de l'élément de glossaire parent            | PG01             |
| ACTION               | Chaîne      |      | I/E |          | Verbe d'action pour supprimer l'enregistrement (DELETE) |                  |

## Commun (Common)

Définition générale

**Identifiant :** — · **Obligatoires :** aucun

| Champ                                      | Type   | Obl. | I/E | Réf. | Description                                                                                                                                             | Exemple / défaut      |
| ------------------------------------------ | ------ | ---- | --- | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| AUTHOR                                     | Chaîne |      | I/E |      | Code permettant de signer l'enregistrement pour savoir quelle application a effectué la dernière modification                                           | Nomadia Field Service |
| CURRENT\_DATE (synonyme : OPERATION\_DATE) | Chaîne |      | I/E |      | Date/Heure à laquelle l'enregistrement a été modifié la dernière fois                                                                                   |                       |
| CONTEXT                                    | Chaîne |      | I/E |      | Indique dans quel contexte l'entité a été enregistrée: dans l'interface, en arrière-plan, via une importation, ou un service web                        |                       |
| OPERATORID                                 | Chaîne |      | I/E |      | Identifiant de l'utilisateur effectuant l'action                                                                                                        |                       |
| OPERATORKEY                                | Chaîne |      | I/E |      | ID interne de l'utilisateur effectuant l'action                                                                                                         |                       |
| CIRCULATIONLISTENERID                      | Chaîne |      | I/E |      | Lorsqu'une action d'exportation est le résultat d'un événement écouté par la circulation, indique le nom du listener impliqué                           |                       |
| CIRCULATIOMESSAGEINFOID                    | Chaîne |      | I/E |      | Lorsqu'une action d'exportation est le résultat d'un événement écouté par la circulation, indique le contenu du message d'information de la circulation |                       |

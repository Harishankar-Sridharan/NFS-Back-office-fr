---
description: >-
  Points d'entrée de l'export, types d'extraction, champs liés, formats de
  sortie et export global.
---

# Exporter des données

## Points d'entrée

| Point d'entrée                                             | Résultat                                                                                                                                                       |
| ---------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Administration > Fichiers CSV > Exporter un fichier CSV`  | Fichier export\<Entité>.csv pour une entité, avec choix des champs, des filtres, des séparateurs, des formats et de l'encodage. Option d'en-têtes en libellés. |
| `Administration > Fichiers CSV > Import/export CSV global` | Archive allExportFiles.zip : un fichier NN\_\<Entité>.csv par entité importable, numéroté selon l'ordre de dépendance.                                         |
| Service web exportEntities                                 | Opérations GetEntitiesProperties (SOAP/REST), getEntities (REST v2, JSON) et GetAppointmentsByResources.                                                       |
| Circulation                                                | Exports planifiés ou déclenchés par un événement (fichier, SQL, HTTP, webhook).                                                                                |

## Types d'extraction

Le type d'extraction (ExtractionKind) sélectionne les enregistrements ; son paramètre (ExtractionParam) le précise. Plusieurs types se combinent en les séparant par une virgule, avec les paramètres dans le même ordre.

| Type                           | Sélection                                                                                                               | Paramètre                                                            |
| ------------------------------ | ----------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| ALL                            | Tous les enregistrements (défaut).                                                                                      | —                                                                    |
| LASTUPDATED                    | Enregistrements modifiés récemment.                                                                                     | 1 : depuis hier 0 h ; 2 : depuis 7 jours ; n > 2 : depuis n minutes. |
| DATEINTERVAL                   | Période absolue.                                                                                                        | yyyy/MM/dd;yyyy/MM/dd                                                |
| DATEDIFFINTERVAL               | Période relative à aujourd'hui.                                                                                         | a;b : de J+a à J+a+b jours.                                          |
| AREA, WORKSITE, TEAM, RESOURCE | Filtre sur une région, un site, une équipe, une ressource.                                                              | Identifiant externe.                                                 |
| Types propres à une entité     | Par exemple pour le client : CUSTOMERPHONE, CONTACTWORKPHONE, PARENTWORKSITE, CUSTOMERTYPE, CUSTOMERKIND, DUTYCONTRACT. | Selon le type.                                                       |

## Champs liés

Une colonne de la forme ENTITE.CHAMP exporte un champ de l'entité référencée, par exemple Customer.CUSTOMERNAME dans un export d'interventions. Pour une liste de références, le suffixe (n) sélectionne le n-ième élément et () les exporte tous.

## Formats de sortie

Outre le CSV, le moteur d'export sait produire : JSON (liste d'objets ou tableau), tableau HTML, Excel (tableau HTML), XML d'enregistrements et script ECMAScript. Le format disponible dépend du point d'entrée.

## Export global

L'export global produit l'ensemble des entités importables, triées par niveau de dépendance. Le premier fichier contient uniquement RESOURCEID et RESOURCELASTNAME. L'archive obtenue est directement réimportable par l'import global (copie d'un environnement de recette vers un autre, par exemple).

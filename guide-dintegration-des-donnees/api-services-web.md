---
description: >-
  Familles de services web, services d'échange de données, services métier et
  codes d'erreur.
---

# API et services web d'intégration

## Familles de services

| Famille                   | URL                                                                         | Format                            | Usage                                                                                                      |
| ------------------------- | --------------------------------------------------------------------------- | --------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Services SOAP             | /ws/\<service>Service/ (WSDL : /ws/\[vN/]\<service>Service/\<service>.wsdl) | XML                               | Échange de données et services métier.                                                                     |
| Services REST historiques | /rest/\[vN/]\<service>/json/\<méthode> ou /xml/\<méthode>                   | JSON ou XML                       | Mêmes opérations que SOAP ; JSONP en GET (?data=).                                                         |
| API REST v1               | /ws-api/v1/\<service>/\<opération>                                          | JSON (XML pour certains services) | Services récents : disponibilité et réservation de créneaux, stock, zones restreintes, notifications, etc. |

La documentation en ligne de l'instance (pages d'aide de l'API) fournit, pour chaque service, la description des méthodes et des exemples de requêtes et de réponses JSON. Seules les versions n et n-1 de chaque service sont garanties.

## Services d'échange de données

| Service          | Opérations                                                               | Rôle                                                                |
| ---------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------- |
| entities         | SetEntitiesFromCsv, SetEntityFromProperties, setEntities (REST)          | Import d'enregistrements du modèle d'échange.                       |
| exportEntities   | GetEntitiesProperties, getEntities (REST v2), GetAppointmentsByResources | Export d'enregistrements.                                           |
| exchangeModel    | ListEntities, GetExchangeModel                                           | Découverte du modèle : entités, champs, types, champs obligatoires. |
| disabledEntities | RetrieveDisabledEntities, DisableEntities, RestoreDisabledEntities       | Désactivation et restauration d'objets.                             |
| extref           | IsExtrefAvailable, GetNewExtref, UpdateExtref                            | Gestion des identifiants externes.                                  |

### SetEntitiesFromCsv

Importe un contenu CSV transmis dans la requête. Comme pour l'import par fichier, l'entité est déduite de la ligne d'en-tête : la requête ne contient ni nom d'entité ni action.

| Élément                 | Défaut                  | Description                                                                               |
| ----------------------- | ----------------------- | ----------------------------------------------------------------------------------------- |
| CsvData                 | —                       | Contenu CSV : ligne d'en-tête puis lignes de données.                                     |
| DataSeparator           | ;                       | Séparateur de champs.                                                                     |
| TextDelimiter           | "                       | Délimiteur de texte.                                                                      |
| DateFormat              | dd/MM/yyyy              | Format des dates.                                                                         |
| SeparatorInListOfValues | ,                       | Séparateur de liste.                                                                      |
| GeocodingOptions        | AT\_STREET\_NUMBER, 0,8 | Tolérance (GeocodingType), score minimal (MinScore) et site de repli (DefaultWorkSiteId). |
| CommonInfo              | —                       | Authentification (voir [Authentification et sécurité](authentification-securite.md)).     |

La réponse contient IsSuccessful, NbSuccess, NbFailure, HtmlSummary (compte rendu ligne par ligne) et ErrorMessage.

### setEntities (REST)

Variante JSON : chaque enregistrement est un objet dont les clés sont les noms de champs. La réponse détaille les enregistrements en erreur (Errors\[] avec l'enregistrement et le message). L'option UseSingleTransaction est disponible.

### GetEntitiesProperties

Exporte une entité : EntityName, FieldNames (liste de champs séparés par des virgules), DateFormat, TimeFormat, ExtractionKind (défaut ALL), ExtractionParam, ExtractionAreaParam, EntityId/EntityIds, ValueListSeparator, DurationAsTimeFormat. La réponse contient des lignes (Rows) de propriétés nom/valeur.

### GetExchangeModel

Renvoie, pour une entité, la liste de ses champs avec description, exemple, valeur par défaut, caractère obligatoire, type, et restriction à l'import ou à l'export. ListEntities renvoie la liste des entités et leur description.

## Services métier

| Service                                                                           | Opérations principales                                                                                                                        |
| --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| scheduling                                                                        | GetResourcePlanning, ReserveAppointment, ConfirmAppointment, SuspendAppointment, ReactivateAppointment, RealizeAppointment, CancelAppointment |
| optimization, realTimeOptimization, manualOptimization, fillPlanning, routeSolver | Lancement et suivi d'optimisations ; recherche, validation et abandon de propositions de créneaux.                                            |
| geocode, route, searchAround                                                      | Géocodage, géocodage inverse, conversion de coordonnées, calcul d'itinéraire, recherche de proximité.                                         |
| otprocess                                                                         | Pilotage de traitements (démarrage, envoi de données, statut, résultat, arrêt).                                                               |
| messages, multimedia, tracking, mission, lock                                     | Messagerie, fichiers attachés, positions des ressources, missions, verrous.                                                                   |
| API REST v1 availableTime                                                         | Recherche de créneaux disponibles, réservation et annulation (search, reserve, cancel).                                                       |

## Résultat et codes d'erreur

Les réponses contiennent un bloc Result (Success, ErrorCode, Detail) et, le cas échéant, l'identifiant de session.

| Code     | Nom                               | Signification                                                                                           |
| -------- | --------------------------------- | ------------------------------------------------------------------------------------------------------- |
| 0        | UNKNOWN\_ERROR                    | Erreur non qualifiée ; voir Detail.                                                                     |
| 10       | SESSION\_NOT\_FOUND               | Session inconnue ou expirée.                                                                            |
| 11       | SESSION\_ALREADY\_RUNNING\_METHOD | Un appel concurrent est en cours sur la même session.                                                   |
| 20       | WRONG\_LOGIN\_PASSWORD            | Authentification refusée.                                                                               |
| 30       | IMPORT\_ERROR                     | Erreur d'import.                                                                                        |
| 40       | CONFIG\_ERROR                     | Erreur de configuration du serveur.                                                                     |
| 50       | WS\_SCHEMA\_ERROR                 | Requête non conforme au schéma.                                                                         |
| 500 et + | Codes propres au service          | Par exemple ENTITYNAME\_NOT\_FOUND (500) pour exchangeModel, EXTREF\_ALREADY\_EXISTS (501) pour extref. |

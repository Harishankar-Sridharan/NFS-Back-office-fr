---
description: >-
  Processeurs internes et externes de la circulation, paramètres dynamiques des
  requêtes SQL, options d'export CSV et destinataires des notifications.
---

# Processeurs

Un processeur (routeur de traitement) termine la chaîne. Les processeurs se déclarent dans la section `routers` / `processor-routers` d'un bloc.

## Processeurs internes (inside-processors)

Un processeur interne agit dans Nomadia Field Service.

| Balise                                | Rôle                                                                                                        | Paramètres principaux                                                                                                                                          |
| ------------------------------------- | ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `exchange-records-csv-processor`      | Lit un fichier CSV et importe chaque enregistrement ; produit un rapport global, les erreurs et les succès. | `separator`, `textDelimiter`, `valueListSeparator`, `dateFormat`, géocodage, `dictionary`, `report-router`, `error-router`, `success-router`                   |
| `exchange-records-xml-processor`      | Même rôle pour un document XML dont chaque nœud (`tagRecordName`, défaut `ROW`) est un enregistrement.      | idem                                                                                                                                                           |
| `csv-record-processor`                | Importe des enregistrements CSV transmis ligne à ligne ; le type d'entité est déduit des noms de colonnes.  | `separator`, `textDelimiter`, `mode-of-import` (`STANDARD`, `UPDATEONLY`, `INSERTONLY`), géocodage                                                             |
| `sql-importer-processor`              | Importe les enregistrements renvoyés par une requête sur une base externe (voir ci-dessous).                | `sql-connection`, `select-clause`, `mode-of-import`, `dictionary`, `error-router`, `report-router`, `ignore-area-lock`                                         |
| `sql-script-processor`                | Exécute un script SQL sur une base externe.                                                                 | `sql-connection`, `sql-script` ou `sql-script-file-path`, `command-delimiter`, `auto-commit` (défaut `false`), `stop-on-error` (défaut `true`), `error-router` |
| `batch-optim-processor`               | Lance une optimisation existante, désignée par son nom.                                                     | `optim-name`, `beginDate`/`endDate` (AAAA/MM/jj), `beginDateFromToday`, `endDateFromBeginDate`, `duration` (minutes), `isWaitingForEnd` (défaut `false`)       |
| `gss-services-processor`              | Appelle un service interne sur les données XML reçues et renvoie le résultat.                               | `service-name` : `geocoding`, `routing`, `mileage`, `itipdf`, `storepictrel` ; `service-param`                                                                 |
| `command-processor`                   | Exécute une commande système sur le serveur.                                                                | `full-path`, `argument`                                                                                                                                        |
| `periodic-customer-visit-generator` ◆ | Génère les visites périodiques des clients.                                                                 | `area-extref`, attributs `T0-weekDay`, `T0-fromToday`, `T1-fromT0`…                                                                                            |
| `mission-getter` ◆                    | Récupère les feuilles de route, missions ou opérations.                                                     | `kind` (`ROADMAP`, `MISSION`, `OPERATION`), `days-range`, `include-status`, `areaid`, `teamid`                                                                 |
| `route-corrector-processor` ◆         | Recalcule les distances des tournées.                                                                       | `beginDateFromToday`, `endDateFromBeginDate`                                                                                                                   |
| `locker` / `unlocker`                 | Pose / lève un verrou sur une ressource.                                                                    | `resource-type`, `selector`                                                                                                                                    |
| `custom-inside-processor`             | Traitement spécifique développé pour un projet.                                                             | `class-name`, `parameter`                                                                                                                                      |

{% hint style="info" %}
Les paramètres de géocodage communs aux processeurs d'import sont `geocoding-tolerance-type`, `geocoding-min-score` et `ungeocoded-default-worksite` (site de travail utilisé pour les adresses non géocodées). Ils suivent la même logique que l'[import CSV de l'administration](../../guide-dutilisation/imports-exports/importer-fichier-csv.md).
{% endhint %}

## Paramètres dynamiques des requêtes SQL

Les requêtes de `sql-importer-processor` et `sql-script-processor` peuvent contenir des paramètres remplacés à l'exécution par des valeurs du contexte de circulation.

| Écriture | Remplacement                                                                                             |
| -------- | -------------------------------------------------------------------------------------------------------- |
| `:nom`   | Remplacé par la valeur du paramètre `nom` du contexte, entre apostrophes. Forme recommandée.             |
| `nom=?`  | Remplacé par `nom='valeur'` si un paramètre `nom` existe dans le contexte. Le `?` n'est pas positionnel. |

| Paramètre                                         | Valeur                                                                                                            | Fourni par                                                                                |
| ------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| `:AREAID`                                         | Référence externe de la région.                                                                                   | Événement d'optimisation, ou paramètre de région transmis                                 |
| `:OPTIMIZATIONSTARTDATE` / `:OPTIMIZATIONENDDATE` | Début / fin de la période optimisée (AAAA-MM-JJ).                                                                 | Événement d'optimisation                                                                  |
| `:WORKSITEID` / `:WorkSites.ids`                  | Référence externe du site ou liste des sites (liste entre parenthèses).                                           | Événement d'optimisation ou paramètre transmis                                            |
| `:Resources.ids`                                  | Références externes des ressources optimisées (liste entre parenthèses).                                          | Événement d'optimisation                                                                  |
| `:LastImportedDate`                               | Date du dernier import réalisé par ce processeur (format `yyyy-MM-dd HH:mm:ss.sss`). Valeur initiale : la veille. | Mémorisée par Nomadia Field Service pour chaque processeur ; restaurée si l'import échoue |
| Tout autre `:nom`                                 | Valeur du paramètre de même nom.                                                                                  | Par exemple, paramètre d'une requête HTTP reçue                                           |

Exemple d'import incrémental : ne lire que les lignes modifiées depuis le dernier import (SQL Server).

```sql
select * from exch_APPOINTMENT
where DATEDIFF(SECOND, lastUpdate, CONVERT(datetime, :LastImportedDate, 121)) < 0
```

{% hint style="danger" %}
Les valeurs sont insérées telles quelles entre apostrophes dans la requête. N'alimentez pas une requête SQL avec des paramètres HTTP provenant d'une source non maîtrisée.
{% endhint %}

## Processeurs externes (outside-processors)

Un processeur externe produit une sortie (fichier, e-mail, appel web…).

| Balise                             | Rôle                                                                                                                     | Paramètres principaux                                                                                                                  |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------- |
| `simple-medium-sender`             | Écrit le message sur un médium de sortie. En cas d'échec d'écriture, nouvelles tentatives.                               | `output-medium`, `marshaller`, `number-reattempt` (défaut 10), `delay-reattempt` (défaut 500 ms)                                       |
| `csv-record-export-processor`      | Exporte des entités au format CSV vers un médium de sortie.                                                              | `listField`, `entity-name`, `dictionary`, `export-only-when-records`, `backup-medium`, options de format (voir ci-dessous)             |
| `sqlquery-to-csv-export-processor` | Exporte en CSV le résultat d'une requête SQL.                                                                            | `sql-query` ou `sql-query-file-name`, `export-only-when-records`, `output-medium`                                                      |
| `merging-records-medium-sender`    | Fusionne plusieurs fichiers CSV en un fichier CSV, un classeur Excel à plusieurs onglets ou une archive ZIP.             | `merge-mode` (`CSV`, `XLSX`, `ZIP`), `output-medium`, `charset-name`                                                                   |
| `sql-exporter-processor`           | Écrit des entités dans une table externe.                                                                                | `sql-connection`, `listField`, `table`, `action` (voir ci-dessous), `dictionary`                                                       |
| `sql-pinned-exporter-processor` ◆  | Exporte vers une table externe avec marquage des éléments exportés, puis notifie.                                        | `pin-table`, `router`, `notification-router`                                                                                           |
| `send-entities-processor`          | Construit une requête JSON, XML ou SOAP avec les champs d'une entité du contexte, généralement envoyée à un service web. | `listField`, `requestFormat` (`json`, `xml`, `soap`), `ws-key`, `ws-user`, `ws-password`, `output-medium`                              |
| `appointment-notifier`             | Compose un message (e-mail, invitation calendrier) à partir d'une intervention.                                          | `dest`, `msg` ou `msg-from-template-resource` ou `msg-from-report-template-id`, `msg-subject`, `ical-*`, `attachment`, `output-medium` |
| `unavailability-notifier`          | Même principe pour une indisponibilité (destinataire : ressources concernées).                                           | `dest` (`RESOURCE`), `msg`, `ical-*`, `output-medium`                                                                                  |
| `application-message-notifier`     | Même principe pour un message applicatif.                                                                                | `dest` (`SENDER`, `RECEIVER`, suffixes `_CC` / `_BCC`), `msg`                                                                          |
| `circulation-context-notifier` ◆   | Compose un message à partir du contexte de circulation.                                                                  | `dest`, `msg`, `output-medium`                                                                                                         |
| `mission-sender` ◆                 | Envoie leurs missions aux ressources.                                                                                    | `kind`, `operation` (`CREATE`, `UPDATE`, `DELETE`, `CLEARALL`), `days-range`, `include-status`                                         |

### Options de format des exports CSV

| Attribut                                         | Rôle                                                                                                                                               | Défaut                 |
| ------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| `separator`                                      | Séparateur de champs.                                                                                                                              | `,`                    |
| `textDelimiter`                                  | Encadrement des textes.                                                                                                                            | `"`                    |
| `valueListSeparator`                             | Séparateur des listes de valeurs dans un champ (différent de `separator`).                                                                         | `;`                    |
| `dateFormat` / `timeFormat`                      | Format des dates et des heures.                                                                                                                    | `yyyy/MM/dd` / `HH:mm` |
| `durationAsTimeFormat` / `durationAsHoursFormat` | Exporter les durées au format heure ou en heures (sinon en minutes).                                                                               | `false`                |
| `extractionKind`                                 | Périmètre exporté lorsque le processeur n'est pas déclenché par un écouteur d'entité : `ALL` (tout) ou `LASTUPDATED` (derniers créés ou modifiés). | `LASTUPDATED`          |
| `extractionParam`                                | Pour `LASTUPDATED` : nombre de jours inspectés.                                                                                                    | `1`                    |

### Actions de sql-exporter-processor

| `action`                 | Effet                                                            |
| ------------------------ | ---------------------------------------------------------------- |
| `UPDATE_INSERT` (défaut) | Met à jour la ligne de même identifiant externe, sinon l'insère. |
| `UPDATE`                 | Met à jour uniquement.                                           |
| `INSERT`                 | Insère uniquement.                                               |
| `DELETE`                 | Supprime les lignes des identifiants exportés.                   |
| `DELETEALL`              | Supprime toutes les lignes.                                      |

### Destinataires des notifications d'intervention (dest)

Plusieurs destinataires peuvent être séparés par des virgules ou répétés. Suffixe `_CC` : copie ; suffixe `_BCC` : copie cachée. Une adresse e-mail saisie telle quelle est un destinataire direct.

| Valeur                                                        | Destinataire                                                            |
| ------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `APP_RESOURCES`                                               | Ressources affectées à l'intervention.                                  |
| `APP_LEADER_RESOURCE`                                         | Ressource responsable affectée.                                         |
| `APP_REQUIRED_RESOURCES` / `APP_WISHED_RESOURCES`             | Ressources requises / souhaitées.                                       |
| `APP_VALIDATION_RESOURCE`                                     | Ressource ayant validé l'intervention.                                  |
| `APP_SUBCONTRACTOR`                                           | Contacts du sous-traitant.                                              |
| `APP_MAIN_CONTACT` / `APP_SECONDARY_CONTACT` / `APP_CONTACTS` | Contact principal / contacts secondaires / tous les contacts du client. |
| `APP_CUSTOMER_MAIN`                                           | Adresse principale du client.                                           |
| `APP_CUSTOMER_ORDERER`                                        | Donneurs d'ordre du client.                                             |

Les textes (`msg`, `msg-subject`…) sont des noms de ressources du fichier `notifier.properties`, qui peuvent contenir des champs du modèle d'échange entre crochets, par exemple `[DESCRIPTION]`.

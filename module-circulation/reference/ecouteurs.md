---
description: >-
  Écouteurs internes et externes de la circulation, filtre de transitions de
  statut et filtres de l'écouteur d'interventions.
---

# Écouteurs

Un écouteur est le point de départ d'une chaîne de traitement. Les écouteurs se déclarent dans la section `listeners` d'un bloc.

## Écouteurs internes (inside-listeners)

Un écouteur interne réagit à un événement de Nomadia Field Service.

| Balise                           | Réagit à                                                                            | Paramètres principaux                                                                                                                                                                                         |
| -------------------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `appointment-listener`           | Création, modification et suppression des interventions, une fois validées.         | `router`, `status-transition-filter`, `operation-mode`, `context`, `before-validation`, `allow-planning-updates-only`, `allow-detail-updates-only`, `notification-status-transition-filter` (voir ci-dessous) |
| `customer-listener`              | Création, modification et suppression des clients.                                  | `router`, `operation-mode`, `before-validation`                                                                                                                                                               |
| `unavailability-listener`        | Événements sur les indisponibilités.                                                | `router`, `operation-modes`, `status-transition-filter`, `unavailability-types`, `before-validation`                                                                                                          |
| `calendar-listener` ◆            | Événements de calendrier autres que les interventions et indisponibilités.          | `router`, `filter`                                                                                                                                                                                            |
| `reference-listener` ◆           | Événements sur les données de référence.                                            | `router`, `filter`, `before-validation`                                                                                                                                                                       |
| `optimization-listener`          | Événements du module d'optimisation (ex. début, fin).                               | `router`                                                                                                                                                                                                      |
| `instant-inside-listener`        | Heure programmée par un déclencheur ; lance un processeur autonome (export batch…). | `router`, `instant-trigger`                                                                                                                                                                                   |
| `application-event-log-listener` | Écritures du journal des événements de l'application.                               | `kinds` (codes de type d'événement séparés par « ; », ex. 330 = import\_error), `codes`, `send-counter-reinit-flag`                                                                                           |
| `web-service-listener`           | Appels aux services web de Nomadia Field Service.                                   | `event-name` (`BEFORE_WSMETHOD_START` ou `AFTER_WSMETHOD_END`), `wsPath`, `wsMethod` (POST, GET, PUT, PATCH, DELETE), `locale`                                                                                |
| `application-message-listener`   | Messages applicatifs.                                                               | `status-filter` (0 envoyé, 1 brouillon, 2 lu, 3 réponse, 4 acquitté), `emergency-filter`, `confidential-filter`, `expect-reply-filter`, `message-filter`, `senders-filter`, `receivers-filter`                |
| `application-start-listener`     | Démarrage et arrêt de l'application.                                                | `codes` (ex. 200 démarrage réussi, 201 échec), `format`                                                                                                                                                       |
| `agenda-marker-listener`         | Repères d'agenda.                                                                   | `kinds` (0 début de journée, 1 fin de journée, 6 en route, 7 sur site, 8 réalisé, 9/10 entrée/sortie de secteur…), `types`, `status`, `operation-modes`                                                       |

## Filtre de transitions de statut

La balise `status-transition-filter` d'un écouteur d'interventions limite les événements transmis selon le changement de statut. Elle contient une liste de règles séparées par des virgules. Chaque règle a la forme `statut_origine:statut_nouveau:décision` :

* `décision` vaut `1` (transmettre) ou `0` (ignorer) ;
* `*` désigne tous les statuts ;
* `#` (dans le statut nouveau) signifie « même statut que l'origine ».

Les règles sont évaluées dans l'ordre : la dernière règle qui correspond l'emporte. Si aucune règle ne correspond, l'événement est transmis.

| Filtre                | Effet                                                                                                             |
| --------------------- | ----------------------------------------------------------------------------------------------------------------- |
| `21:21:0,6:6:0`       | Transmet tout, sauf les modifications d'interventions Demandé (21) ou Suspendu (6) qui ne changent pas de statut. |
| `*:*:0,*:31:1`        | Ne transmet que les événements à l'issue desquels l'intervention est Confirmé (31).                               |
| `*:#:0`               | Ne transmet que les changements de statut.                                                                        |
| `*:*:0,*:31:1,31:*:1` | Transmet les passages vers et depuis Confirmé.                                                                    |

Les codes de statut d'intervention sont listés dans [Statuts d'intervention](../annexes/statuts-intervention.md).

## Autres filtres de l'écouteur d'interventions

| Balise                                    | Rôle                                                                                                  | Valeurs                                                                                                                                                                           |
| ----------------------------------------- | ----------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `operation-mode`                          | Limite aux types d'événements listés (séparés par « ; »).                                             | 0 général, 1 changement de statut, 2 création, 3 modification, 4 suppression                                                                                                      |
| `context`                                 | Limite aux contextes d'origine listés (nom ou code, séparés par « ; »).                               | 0 OtherUnknown, 10 OnUserAcknowledge, 20 OnBackground, 30 OnSchedulingBatch, 50 OnPeriodicRequestGeneration, 80 appel depuis l'application mobile, 400 OnImport, 500 OnWebService |
| `allow-planning-updates-only`             | Pour une modification, ne transmet que si elle change la planification.                               | `true` / `false`                                                                                                                                                                  |
| `allow-detail-updates-only`               | Pour une modification, ne transmet que si elle crée, supprime ou modifie un détail de l'intervention. | `true` / `false`                                                                                                                                                                  |
| `before-validation` ◆                     | Écoute les événements avant leur validation.                                                          | `true` / `false`                                                                                                                                                                  |
| `notification-status-transition-filter` ◆ | Filtre sur les transitions du statut de notification, même syntaxe que `status-transition-filter`.    | triplets                                                                                                                                                                          |

## Écouteurs externes (outside-listeners)

### outside-listener

Écoute les messages arrivant sur un médium d'entrée et les transmet à un routeur. Si le routeur renvoie FAUX, l'écouteur renvoie FAUX au médium, qui conserve le message pour un traitement ultérieur.

| Balise                         | Rôle                                                                                                                                                                                                         |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `input-medium`                 | Médium écouté.                                                                                                                                                                                               |
| `router`                       | Routeur qui reçoit le message.                                                                                                                                                                               |
| `default-unmarshaller`         | Transformateur qui décode le message (facultatif).                                                                                                                                                           |
| `timeout`                      | Âge maximal du message, en minutes. Active `timeout-router` et `diagnostic-router`.                                                                                                                          |
| `timeout-router`               | Appelé quand le routeur a échoué et que le message est plus ancien que `timeout` (date de création du fichier, horodatage JMS…).                                                                             |
| `success-if-timeout-successes` | Par défaut `true` : le message est considéré comme traité si `timeout-router` réussit. À `false`, seul le résultat du premier routeur compte.                                                                |
| `diagnostic-router`            | Appelé dans le même cas que `timeout-router`, après lui. Il reçoit un diagnostic de l'erreur (et non le message d'origine), par exemple pour l'écrire dans un journal. S'il échoue, l'écouteur renvoie FAUX. |

{% hint style="info" %}
`timeout-router` et `diagnostic-router` ne sont utilisés que si `timeout` est renseigné.
{% endhint %}

### bulk-outside-listener (déprécié)

Découpe un message en sous-messages (`cursor-factory`) et les transmet un à un, avec `report-router`, `error-router` et `success-router`. Cet écouteur est déprécié : pour importer un fichier CSV ou XML ligne à ligne, utilisez un `outside-listener` associé à `exchange-records-csv-processor` ou `exchange-records-xml-processor`, qui produisent eux-mêmes rapport, erreurs et succès.

## Écouteur de connexion JMS (connection-listeners)

`jms-connection-listener` surveille une connexion JMS (`jms-connection-to-listen`) et appelle `on-deconnection-router` à la déconnexion ou `on-reconnection-router` à la connexion et à chaque reconnexion. L'événement ne contient pas de message : utilisez `message-changer-router` pour en créer un.

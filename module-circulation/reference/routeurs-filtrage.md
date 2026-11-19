---
description: Routeurs de filtrage de la circulation, forward-router et routers-distributor.
---

# Routeurs de filtrage

Un routeur de filtrage filtre, aiguille ou complète le message, puis le transmet à un autre routeur. Les routeurs de filtrage se déclarent dans la section `routers` / `filter-routers` d'un bloc.

## Liste des routeurs de filtrage (filter-routers)

| Balise                                        | Rôle                                                                                                                                                      | Paramètres principaux                                                                                    |
| --------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| `forward-router`                              | Transmet à un routeur puis, selon le résultat, à un routeur de succès ou d'erreur ; transmet ensuite le bilan à un routeur de résultat (voir ci-dessous). | `router`, `success-router`, `error-router`, `result-router`                                              |
| `routers-distributor`                         | Distribue le message à plusieurs routeurs (voir ci-dessous).                                                                                              | `method`, liste de `router`                                                                              |
| `check-status-appointment-router`             | Ne transmet que les interventions dont le statut figure dans la liste ; les autres sont ignorées sans erreur.                                             | `router`, `include-status`/`status-id`                                                                   |
| `check-progression-step-appointment-router` ◆ | Filtre les interventions selon leur étape d'avancement.                                                                                                   | `include-progression-step`/`progression-step-id`                                                         |
| `check-task-type-appointment-router` ◆        | Filtre les interventions selon leur type de tâche.                                                                                                        | `include-entities` (`entity-id` ou `entity-extref`)                                                      |
| `check-task-type-group-appointment-router` ◆  | Filtre selon le groupe de types de tâche.                                                                                                                 | `task-type-group-id`, `task-type-group-extref`                                                           |
| `by-region-appointment-router`                | Aiguille selon la région de l'intervention.                                                                                                               | `region-router` (`region-id`, `router`), `default-router`                                                |
| `by-extapp-appointment-router`                | Aiguille selon l'application externe émettrice de l'intervention.                                                                                         | `extapp-router` (`extapp-name`, `router`), `default-router`                                              |
| `by-extref-appointment-router`                | Sépare les interventions avec ou sans référence externe.                                                                                                  | `router-if-extref`, `router-if-no-extref`                                                                |
| `by-entity-kind-router`                       | Aiguille selon le type d'entité du modèle d'échange.                                                                                                      | `entity-kind-router` (`entity-name`, `router`), `default-router`                                         |
| `by-entity-change-context-router`             | Aiguille selon le contexte de la modification (import, service web, batch…).                                                                              | `entity-change-context-code`, `default-router`                                                           |
| `by-entity-fields-conditional-router`         | Aiguille selon une condition JavaScript sur les champs de l'entité, ex. `'[APPOINTMENTID]'.startsWith('A')`.                                              | `entity-field-condition-router` (`field-condition` ou `field-condition-res`, `router`), `default-router` |
| `optimization-event-router` ◆                 | Filtre les événements d'optimisation.                                                                                                                     | `include-event` (`event-name`, `warn-level`), `filterName`                                               |
| `message-changer-router`                      | Remplace le message par un texte fixe.                                                                                                                    | `new-message`, `router`                                                                                  |
| `param-changer-router` ◆                      | Ajoute ou modifie des paramètres du contexte de circulation.                                                                                              | `param` (`name`, `value`), `router`                                                                      |
| `entity-iterator-router`                      | Parcourt une sélection d'interventions et transmet chaque élément.                                                                                        | `listField`, `region-id`, `router`, `extractionKind`, `extractionParam`                                  |
| `combined-appointment-router`                 | Ne transmet que la première intervention d'un client pour une journée.                                                                                    | `router`                                                                                                 |
| `worksite-filter`                             | Transmet le message pour chaque site de travail d'une liste ; l'identifiant du site est placé dans le contexte.                                           | `include-entities`, `sql-connection`, `selectExtrefQuery`                                                |
| `notification-appointment-filter-processor`   | Recherche des interventions, positionne ou bloque leur statut de notification et les place dans le contexte.                                              | `notification-status-to-set`, `notification-status-to-block`                                             |
| `superset-pinning-filter-router`              | Pour un lot de fichiers, transmet chaque fichier à `router` puis, après le dernier, appelle `nextRouter`.                                                 | `router`, `nextRouter`                                                                                   |
| `asynch-router`                               | Exécute le routeur de façon asynchrone.                                                                                                                   | `router`, `seconds-timeout`, `timeout-router`, `success-router`, `error-router`                          |
| `input-medium-trigger-router`                 | Déclenche le scan d'un médium d'entrée de type fichier.                                                                                                   | `input-medium`                                                                                           |
| `lock-router`                                 | Pose un verrou et transmet si la ressource n'est pas déjà verrouillée ; sinon appelle `error-router`.                                                     | `resource-type`, `selector`, `router`, `error-router`                                                    |
| `modulo-counter-filter-router` ◆              | Ne transmet qu'un message sur N.                                                                                                                          | `modulo-integer`, `initial-count`, `count-by-entity`                                                     |
| `backup-replay-filter`                        | Rejoue les enregistrements sauvegardés non envoyés vers les routeurs d'envoi.                                                                             | `replay-strategy`, `max-try-before-skip`, `application-filter`, `entity-kind-router`                     |
| `custom-filter-router`                        | Filtre spécifique développé pour un projet.                                                                                                               | `class-name`, `router`                                                                                   |

## forward-router

Le résultat final est VRAI dans trois cas :

* le routeur a réussi et il n'y a pas de `success-router` ;
* le routeur a réussi et `success-router` aussi ;
* le routeur a échoué mais `error-router` a réussi.

`result-router` reçoit le bilan des deux traitements et n'influence pas le résultat.

## routers-distributor

| Valeur de `method`   | Comportement                                                                                                                                           |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| (absente)            | Répartition : chaque message est envoyé à un seul routeur, à tour de rôle. Si ce routeur échoue, le suivant est essayé. Utile pour répartir la charge. |
| `COPY`               | Duplication : le message est envoyé à tous les routeurs. Le résultat est VRAI seulement si tous réussissent.                                           |
| `COPY_WHENFAIL`      | Envoi au premier routeur ; les suivants sont utilisés en cas d'échec.                                                                                  |
| `COPY_WHILE_SUCCESS` | Accepté par l'application ; comportement actuellement identique à `COPY`.                                                                              |

---
description: Journal d'application, abonnement au journal et exports de supervision.
---

# Journalisation et supervision

Les imports, exports et appels de services alimentent le journal d'application. Chaque événement a un type, un niveau, un code et l'utilisateur à l'origine de l'action.

| Type d'événement                                    | Code               | Usage pour l'intégration                                                |
| --------------------------------------------------- | ------------------ | ----------------------------------------------------------------------- |
| import\_warn / import\_error / import\_summary      | 300 / 330 / 360    | Avertissement, erreur ligne par ligne, résumé de fin d'import.          |
| export\_warn / export\_summary / export\_error      | 400 / 430 / 460    | Suivi des exports.                                                      |
| communication\_warn / \_success / \_error           | 500 / 530 / 550    | Échanges avec des systèmes externes.                                    |
| process\_start / process\_end                       | 600 / 650          | Début et fin de traitement.                                             |
| service\_call / service\_completed / service\_fail  | 700 / 730 / 760    | Appels de services.                                                     |
| webhook\_call / webhook\_completed / webhook\_fail  | 1200 / 1230 / 1260 | Envois vers un webhook (circulation).                                   |
| user\_api\_session                                  | 1001 / 1002        | Ouvertures de session API (1002 : session API de l'application mobile). |
| entity\_creation / entity\_update / entity\_disable | 100 / 150 / 200    | Cycle de vie des objets.                                                |

Codes émis par l'import pour import\_error : 1 (aucune entité ne correspond à l'en-tête), 2 (nombre de champs incorrect), 3 (erreur métier sur une ligne), 4 (erreur technique), 5 (erreur sur la première ligne). En fin d'import, un import\_warn de code 100 signale un import partiel, un import\_summary de code 200 un import complet ; tous deux indiquent la durée.

## Abonnement au journal

L'entité ApplicationLogSubscription abonne un profil utilisateur (USERPROFILE) ou une collection de droits (RIGHTCOLLECTIONNAME) à un type (LOGTYPE) et un niveau (LOGLEVEL) d'événements. Niveaux : DEBUG (10), INFO (20), ALERT (30), WARN (40), ERROR (50), SEVERE (60), FATAL (99).

## Exports de supervision

Les entités exportables ApplicationEvent et Journal permettent d'extraire le journal vers un outil de supervision. L'entité technique Common décrit les champs de traçabilité communs (AUTHOR, CURRENT\_DATE, CONTEXT, OPERATORID…).

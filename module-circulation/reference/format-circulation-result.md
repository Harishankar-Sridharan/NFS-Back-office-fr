---
description: >-
  Format XML circulation-result des réponses HTTP et des sorties de diagnostic
  de la circulation.
---

# Format de retour circulation-result

Les réponses aux appels HTTP de la circulation et les sorties des transformateurs XML de diagnostic et de résultat respectent le schéma `circulation-result.xsd`. Un document contient un élément `router-result` dont toutes les balises sont facultatives.

## Contenu de router-result

| Balise              | Contenu                                                                                                             |
| ------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `success`           | `true` ou `false` : le message a-t-il été traité ?                                                                  |
| `error-explanation` | Explication textuelle de l'erreur.                                                                                  |
| `error-code`        | Code d'erreur (voir tableau suivant).                                                                               |
| `message-info`      | Informations sur le message traité : identifiant, date de création, nom du médium, nom du support, numéro de ligne. |
| `briefs`            | Pour un traitement par lot : liste de comptes rendus de succès, d'avertissement ou d'erreur.                        |
| `message`           | Message libre.                                                                                                      |

## Codes d'erreur

| `error-code`   | Signification                                                    |
| -------------- | ---------------------------------------------------------------- |
| `ERROR`        | Erreur générale.                                                 |
| `PARSE_ERROR`  | Erreur de lecture du message reçu.                               |
| `IMPORT_ERROR` | Erreur lors de l'import du message.                              |
| `LOCK`         | Traitement impossible : écouteur interrompu par un verrouillage. |

## Exemple

```xml
<circulation-result>
  <router-result>
    <success>false</success>
    <error-explanation>importInterventions is stopped because : "lock …"</error-explanation>
    <error-code>LOCK</error-code>
  </router-result>
</circulation-result>
```

---
description: Transformateurs et connexions partagées de la circulation.
---

# Transformateurs et connexions

## Transformateurs (transformers)

Un transformateur convertit les données en texte (ou l'inverse), découpe un message ou traduit des noms de champs. Il est déclaré par le nom de la classe à utiliser (`by-class-appt-marshaller`, `by-class-appt-unmarshaller`). Les valeurs disponibles sont les suivantes (préfixe `com.geoconcept.schedule.logic.circulation.impl.`) :

| Valeur de `classname` (sans le préfixe)                                                     | Usage                                                                         |
| ------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| `PseudoMarshaller` / `PseudoUnmarshaller`                                                   | Transmettent le texte tel quel. À utiliser par défaut.                        |
| `appointment.AppointmentXMLMarshaller`                                                      | Intervention en XML, en fin de chaîne lancée par un écouteur d'interventions. |
| `appointment.ExtrefAppointmentXMLMarshaller`                                                | Intervention en XML par référence externe.                                    |
| `appointment.AnnouncedAppointmentXMLMarshaller` ◆                                           | Intervention annoncée en XML.                                                 |
| `DiagnosticDataMarshaller` / `DiagnosticDataXMLMarshaller` / `DiagnosticDataMailMarshaller` | En fin de chaîne d'un `diagnostic-router`.                                    |
| `ForwardResultDataMarshaller` / `ForwardResultDataXMLMarshaller`                            | En fin de chaîne d'un `result-router` de `forward-router`.                    |

Les versions XML produisent un document au format `circulation-result` (voir [Format de retour circulation-result](format-circulation-result.md)).

* `line-by-line-cursor-factory` découpe un texte en lignes ; `ignore-first-line` permet d'ignorer la ligne d'en-tête.
* `dictionaries`/`dictionary` définit une table de correspondance entre noms de champs externes (`outsideName`) et noms du modèle d'échange (`insideName`), utilisable par les processeurs d'import et d'export (`dictionary`).

## Connexions (connections)

| Balise                 | Rôle                                                                             | Paramètres principaux                                                                                                        |
| ---------------------- | -------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `sql-connection`       | Connexion à une base externe, requise par les processeurs SQL.                   | `driver`, `connectionString`, `user`, `password`, `synchronized` (défaut `true` : un seul processeur à la fois), `isolation` |
| `mail-session`         | Serveur de messagerie.                                                           | `host`, `user`, `login`, `password`, `from`, `store-protocol`, `transport-protocol`, `use-ssl`, `use-tls`                    |
| `http-connection`      | Connexion HTTP réutilisable, y compris pour obtenir un jeton d'accès.            | `verb`, `url`, `user`, `password`, `content-type`, `authorization`, `header`, `data`, `custom-class-name`                    |
| `root-path-connection` | Chemin racine commun : les chemins relatifs des médiums fichiers y sont ajoutés. | `path`                                                                                                                       |
| `jms-connection`       | Connexion JMS.                                                                   | `factory-jndi-name`, `reconnection-delay`                                                                                    |

{% hint style="success" %}
Référencez les comptes, mots de passe, chaînes de connexion et URL de ces connexions dans le coffre-fort (voir [Sécuriser les identifiants avec le coffre-fort](../coffre-fort.md)).
{% endhint %}

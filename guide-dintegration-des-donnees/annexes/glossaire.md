---
description: Définitions des termes utilisés dans le guide d'intégration des données.
---

# Glossaire

| Terme                    | Définition                                                                                                                    |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------- |
| Entité                   | Type d'objet échangé (client, ressource, intervention…), décrit par une liste de champs.                                      |
| Modèle d'échange         | Ensemble des entités et champs utilisables pour importer et exporter des données Nomadia Field Service.                       |
| Identifiant externe      | Identifiant d'un objet dans le SI du client (champ …ID), utilisé par Nomadia Field Service pour retrouver l'objet.            |
| Référence                | Champ qui contient l'identifiant externe d'un objet d'une autre entité (type ID\_FOREIGN ou IDS\_LIST).                       |
| En-tête                  | Première ligne d'un fichier CSV, contenant les noms des champs.                                                               |
| Séparateur de liste      | Caractère qui sépare plusieurs valeurs dans un même champ.                                                                    |
| Délimiteur de texte      | Caractère qui entoure une valeur (généralement ").                                                                            |
| BOM                      | Marque d'ordre d'octets placée en tête de certains fichiers UTF-8.                                                            |
| Géocodage                | Calcul des coordonnées géographiques à partir d'une adresse.                                                                  |
| Région                   | Entité Area : périmètre de données planifiées ensemble (territoire ou activité).                                              |
| Site de travail / agence | Entité Worksite : lieu de rattachement des ressources et des clients.                                                         |
| Intervention             | Entité Appointment : travail à réaliser chez un client (« rendez-vous » dans l'ancienne terminologie).                        |
| Macro-statut             | Regroupement des statuts d'intervention : Candidate, Scheduled, Achieved, Cancelled, Aside.                                   |
| Circulation              | Moteur de flux automatisés de Nomadia Field Service (fichiers, SFTP, HTTP, SQL, JMS).                                         |
| Webhook                  | URL d'un système externe appelée par Nomadia Field Service pour lui transmettre des données.                                  |
| Session                  | Contexte d'authentification d'un client de service web, identifié par un SessionId.                                           |
| Jeton porteur (bearer)   | Jeton d'accès transmis dans l'en-tête HTTP Authorization.                                                                     |
| SOAP / REST              | Styles de services web : SOAP échange des messages XML décrits par un WSDL ; REST utilise des URL et des formats JSON ou XML. |
| Typologie                | Liste de codes et de libellés associée à un champ personnalisé.                                                               |

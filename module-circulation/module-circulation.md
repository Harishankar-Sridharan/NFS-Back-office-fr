---
description: >-
  Présentation du module Circulation de Nomadia Field Service, qui fait circuler
  les données entre l'application et les systèmes externes.
---

# Présentation

La circulation est un moteur d'échanges intégré à Nomadia Field Service. Elle fait circuler les données entre Nomadia Field Service et les systèmes externes (fichiers, serveurs SFTP, bases de données, services web, messagerie…) et automatise certains traitements internes.

La circulation ne propose pas d'écran de saisie : son comportement est décrit dans un fichier XML, `circulation_config.xml`, chargé au démarrage du serveur et remplaçable depuis l'administration. Ce fichier décrit des chaînes de traitement : un événement ou un message entrant est capté, éventuellement filtré, puis traité dans Nomadia Field Service ou transmis vers l'extérieur.

{% hint style="info" %}
Cette documentation décrit la version 2027.1.1 de Nomadia Field Service. Certains écrans ou objets peuvent être absents des versions antérieures.
{% endhint %}

## À qui s'adresse cette documentation ?

* Administrateurs fonctionnels de Nomadia Field Service.
* Consultants et intégrateurs chargés de mettre en place les échanges avec le système d'information du client.
* Équipes support et projet.

La configuration se fait dans un fichier XML : une connaissance de base de ce format est nécessaire.

## Exemples d'usage

| Besoin                                                                             | Composants utilisés (exemples)                                                             |
| ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| Importer chaque nuit les clients, indisponibilités et interventions déposés en CSV | `directory-input-medium`, `exchange-records-csv-processor`                                 |
| Récupérer des fichiers sur un serveur SFTP ou y déposer des exports                | `url-input-medium`, `url-output-medium`                                                    |
| Lancer une optimisation batch après un import ou à heure fixe                      | `batch-optim-processor`, `instant-trigger`                                                 |
| Exporter en CSV les interventions qui changent de statut                           | `appointment-listener`, `csv-record-export-processor`                                      |
| Alimenter une base de données externe ou importer depuis celle-ci                  | `sql-exporter-processor`, `sql-importer-processor`                                         |
| Envoyer un e-mail, un SMS ou un message applicatif                                 | `appointment-notifier`, `mail-output-medium`, `sms-output-medium`, `message-output-medium` |
| Appeler un service web REST ou HTTP                                                | `rest-output-medium`, `http-output-medium`, `send-entities-processor`                      |
| Recevoir des messages par HTTP (URL de la circulation)                             | `http-input-medium`                                                                        |

## Conventions utilisées

* `outside-listener` : nom d'une balise ou d'une valeur à saisir telle quelle dans le fichier de circulation.
* **Fichier de circulation** : libellé d'un menu, d'un écran ou d'un bouton de l'application.
* `Administration > Fichiers XML` : chemin de navigation dans le module d'administration.
* **Intervention** : rendez-vous planifiable dans Nomadia Field Service (balises `appointment` dans le fichier).

## Dans cette section

| Page                                                                         | Contenu                                                                                |
| ---------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| [Comprendre le fonctionnement de la circulation](principe-fonctionnement.md) | Notions clés, chaîne de traitement, structure du fichier                               |
| [Prérequis et accès aux écrans](prerequis-acces.md)                          | Droits nécessaires et écrans d'administration                                          |
| [Charger un fichier de circulation](charger-fichier-circulation.md)          | Chargement au démarrage, import d'un nouveau fichier, messages du rapport              |
| [Suivre et piloter la circulation](suivre-piloter-circulation.md)            | Configuration en cours, écouteurs, exemples livrés, listeners HTTP, liens d'export     |
| [Sécuriser les identifiants avec le coffre-fort](coffre-fort.md)             | Coffre-fort, références et migration                                                   |
| [Exemples de configuration](exemples/)                                       | Trois cas complets commentés                                                           |
| [Référence du fichier de circulation](reference/)                            | Tous les objets et leurs paramètres                                                    |
| [Annexes](annexes/)                                                          | Expressions cron, statuts d'intervention, correspondance avec l'ancienne documentation |

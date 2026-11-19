---
description: >-
  Guide d'intégration des données de Nomadia Field Service (NFS) : modèle
  d'échange, imports et exports, services web, cycle de vie des interventions.
---

# Présentation

Ce guide explique comment alimenter Nomadia Field Service (NFS) avec les données d'un client et comment en extraire les résultats. Il décrit les canaux d'échange, le modèle d'échange (entités et champs), les règles de format et de validation, l'ordre d'intégration, la gestion des erreurs et les services web disponibles.

Le paramétrage de l'application (profils et droits, tâches d'optimisation, vocabulaire, logo) relève de l'administration fonctionnelle : il n'est pas traité ici. Consultez le [Guide d'utilisation](../guide-dutilisation/guide-utilisation.md).

## À qui s'adresse ce guide ?

* Consultants Intégration et chefs de projet qui préparent une reprise de données ou un flux récurrent.
* Équipes Support qui diagnostiquent un import ou un export en erreur.
* Partenaires techniques et équipes informatiques des clients qui développent un connecteur.
* Équipes R\&D qui ont besoin d'une référence fonctionnelle du modèle d'échange.

Le lecteur doit savoir manipuler un fichier CSV et lire un document JSON ou XML. Les termes techniques sont repris dans le [glossaire](annexes/glossaire.md).

## Périmètre

| Inclus dans ce guide                                                                     | Hors périmètre                                                                                                     |
| ---------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| Modèle d'échange : 109 entités importables ou exportables, champs, types, références     | Paramétrage fonctionnel (profils, collections de droits, optimisation, vocabulaire)                                |
| Import et export CSV depuis l'interface d'administration, import et export globaux (ZIP) | Configuration détaillée de la circulation (voir [Module Circulation](../module-circulation/module-circulation.md)) |
| Services web d'échange de données (SOAP et REST) et services de prise de rendez-vous     | Application mobile, mobilité et formulaires terrain                                                                |
| Statuts et cycle de vie des interventions, règles de validation, erreurs, journalisation | Exploitation, hébergement, sauvegarde et sécurité de l'infrastructure                                              |

## Dans cette section

| Page                                                                   | Contenu                                                                                                                              |
| ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| [Vue d'ensemble de l'intégration](vue-ensemble.md)                     | Principe, canaux d'échange, architecture et séquence type                                                                            |
| [Prérequis](prerequis.md)                                              | Données à préparer, identifiants externes, accès                                                                                     |
| [Authentification et sécurité](authentification-securite.md)           | Modes d'authentification des services web, bonnes pratiques                                                                          |
| [Concepts et modèle d'échange](modele-echange.md)                      | Entités, types de données, colonnes d'import et d'export, synonymes                                                                  |
| [Référentiels et ordre d'intégration](integrer-donnees/)               | Ordre de chargement, puis intégration de chaque domaine : organisation, ressources, calendriers, compétences, clients, interventions |
| [Importer des données](imports.md)                                     | Points d'entrée, format CSV, création, mise à jour, suppression, géocodage, import global                                            |
| [Exporter des données](exports.md)                                     | Points d'entrée, types d'extraction, formats, export global                                                                          |
| [API et services web d'intégration](api-services-web.md)               | Services d'échange de données, services métier, codes d'erreur                                                                       |
| [Champs personnalisés](champs-personnalises.md)                        | Champs libres, typologies, libellés                                                                                                  |
| [Validation des données et gestion des erreurs](validation-erreurs.md) | Contrôles, codes d'erreur, compte rendu d'import                                                                                     |
| [Journalisation et supervision](journalisation-supervision.md)         | Journal d'application, abonnements, exports de supervision                                                                           |
| [Exemples d'intégration](exemples.md)                                  | Jeu de données fictif complet et appels de services web                                                                              |
| [Bonnes pratiques](bonnes-pratiques.md)                                | Préparation, chargement, performances                                                                                                |
| [Diagnostic et résolution des problèmes](diagnostic.md)                | Erreurs courantes et démarche de diagnostic                                                                                          |
| [Référence du modèle d'échange](reference-modele/)                     | Toutes les entités et tous les champs, par domaine                                                                                   |
| [Annexes](annexes/)                                                    | Ordre d'intégration détaillé, correspondance avec l'ancien guide, glossaire                                                          |

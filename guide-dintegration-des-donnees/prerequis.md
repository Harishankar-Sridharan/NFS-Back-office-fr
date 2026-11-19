---
description: >-
  Données à préparer, identifiants externes et accès nécessaires avant un projet
  d'intégration.
---

# Prérequis

## Données à préparer

| Donnée                 | Exigence minimale                                                                                               | Entités Nomadia Field Service            |
| ---------------------- | --------------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| Organisation           | Au moins une région ; un site de travail (agence) pour rattacher ressources et clients                          | Area, Worksite                           |
| Référentiel d'activité | Groupes et types d'intervention avec une durée par défaut                                                       | TaskTypeGroup, TaskType                  |
| Ressources             | Identifiant unique et nom pour chaque ressource ; adresse de départ et de retour pour les ressources optimisées | HumanResource                            |
| Clients et sites       | Identifiant unique et nom ; adresse géocodable ou coordonnées                                                   | Customer                                 |
| Interventions          | Identifiant unique, client, type d'intervention, période de réalisation                                         | Appointment                              |
| Calendriers            | Modèles de journée et de semaine, jours fériés                                                                  | WorkdayType, WorkWeekType, PublicHoliday |

## Identifiants externes

Chaque entité est identifiée par un identifiant externe : la valeur du champ d'identifiant (par exemple CUSTOMERID) fournie par le système d'information du client. Nomadia Field Service s'en sert pour retrouver un objet existant et pour résoudre les références entre entités. Cet identifiant doit être unique et stable dans le temps.

{% hint style="warning" %}
Ne réutilisez jamais un identifiant pour un autre objet. Un import qui retrouve un identifiant existant met à jour l'objet existant au lieu d'en créer un nouveau.
{% endhint %}

## Accès et environnement

* Un compte utilisateur Nomadia Field Service autorisé à accéder au module d'administration pour les imports et exports manuels.
* Pour les services web : l'URL de l'instance, la clé de protection de l'API si elle est activée, et un compte utilisateur dédié à l'intégration (voir [Authentification et sécurité](authentification-securite.md)).
* Un environnement de recette alimenté avant toute reprise en production.

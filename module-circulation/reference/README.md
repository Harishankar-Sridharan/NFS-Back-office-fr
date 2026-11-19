---
description: Référence complète du fichier de circulation et règles générales d'écriture.
---

# Référence du fichier de circulation

Cette section décrit tous les objets disponibles dans le fichier de circulation et leurs paramètres principaux.

## Règles générales

* Le format est défini par le schéma `circulation-config.xsd`, livré avec l'application. Validez vos fichiers avec un éditeur XML qui l'utilise.
* L'ordre des balises imposé par le schéma doit être respecté.
* Balises communes à la plupart des objets : `id` (obligatoire, unique), `description` (facultative), `alert-application-log-enabled` (facultative, `true` pour tracer le début et la fin des traitements dans le journal des événements de l'application).
* Les valeurs booléennes s'écrivent `true` ou `false`.

{% hint style="info" %}
Les tableaux de cette section présentent tous les objets disponibles dans la version documentée. Les objets signalés par ◆ sont décrits à partir du schéma de configuration uniquement : validez leur comportement sur un environnement de recette avant toute mise en production.
{% endhint %}

## Dans cette section

| Page                                                                | Objets décrits                                                                                          |
| ------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| [Écouteurs](ecouteurs.md)                                           | Écouteurs internes et externes, filtres de statut, écouteur de connexion JMS                            |
| [Routeurs de filtrage](routeurs-filtrage.md)                        | `filter-routers`, `forward-router`, `routers-distributor`                                               |
| [Processeurs](processeurs.md)                                       | Processeurs internes et externes, paramètres SQL, options d'export CSV, destinataires des notifications |
| [Médiums](mediums.md)                                               | Médiums d'entrée et de sortie, nom des fichiers produits                                                |
| [Transformateurs et connexions](transformateurs-connexions.md)      | `transformers`, `connections`                                                                           |
| [Déclencheurs et interrupteurs](declencheurs-interrupteurs.md)      | `triggers`, `interruptors`                                                                              |
| [Format de retour circulation-result](format-circulation-result.md) | Réponses HTTP et sorties XML de diagnostic                                                              |

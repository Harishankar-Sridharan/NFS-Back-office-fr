---
description: >-
  Codes des statuts d'intervention utilisables dans les filtres de statut de la
  circulation.
---

# Statuts d'intervention

Codes utilisables dans les filtres de statut (`status-transition-filter`, `include-status`).

| Code | Libellé dans Nomadia Field Service | Signification                                                             |
| ---- | ---------------------------------- | ------------------------------------------------------------------------- |
| 0    | Inconnu                            | Statut inconnu.                                                           |
| 21   | Demandé                            | Demande non planifiée, à planifier (batch, temps réel ou manuel).         |
| 2    | Planifié                           | Planifiée ; peut être déplacée et réaffectée.                             |
| 28   | Accepté                            | Planifiée ; peut être déplacée mais pas réaffectée à une autre ressource. |
| 30   | Réservé                            | Planifiée ; ne peut plus être déplacée mais peut être réaffectée.         |
| 31   | Confirmé                           | Planifiée ; ne peut plus être ni déplacée ni réaffectée.                  |
| 32   | Sous-traité                        | Confiée à un sous-traitant.                                               |
| 3    | Réalisé                            | Intervention réalisée.                                                    |
| 6    | Suspendu                           | À replanifier manuellement ; ignorée par l'optimisation.                  |
| 10   | Abandonné                          | Intervention annulée.                                                     |
| 40   | Journalisé                         | Copie conservant un état antérieur de l'intervention.                     |

Pour la signification des états dans l'application, consultez [Comprendre les états des rendez-vous](../../guide-dutilisation/introduction/statuts-rendez-vous.md).

---
description: Déclencheurs et interrupteurs de la circulation.
---

# Déclencheurs et interrupteurs

## Déclencheurs (triggers)

* `directory-trigger` et `url-trigger` scannent toutes les `scan-time-interval` millisecondes les répertoires (ou URL) des médiums qui les référencent. Un seul déclencheur peut piloter plusieurs médiums.
* `instant-trigger` génère des événements à des dates programmées, soit par une expression cron (attribut `cron-periodicity`, voir [Expressions cron](../annexes/expressions-cron.md)), soit par un délai initial (`startMinute`) et une période (`period` : 0 minute, 1 jour, 2 semaine ; `periodLength`).
* Avec `synchronized` à `true` (défaut), un déclenchement est annulé si le précédent n'est pas terminé. Recommandé pour les imports fréquents.

## Interrupteurs (interruptors)

Un `business-lock-interruptor` arrête un écouteur (et son médium) pendant le verrouillage des interventions d'une région, puis le redémarre au déverrouillage.

| Balise                  | Valeur                                                 |
| ----------------------- | ------------------------------------------------------ |
| `resource-type`         | `LOCK_APPOINTMENTS_ON_REGION` (seule valeur acceptée). |
| `selector`              | Référence externe de la région.                        |
| `listener-to-interrupt` | Identifiant de l'écouteur à interrompre.               |

```xml
<interruptors>
  <business-lock-interruptor>
    <id>verrou-region-sud</id>
    <resource-type>LOCK_APPOINTMENTS_ON_REGION</resource-type>
    <selector>REG-SUD</selector>
    <listener-to-interrupt>import-csv-ecouteur</listener-to-interrupt>
  </business-lock-interruptor>
</interruptors>
```

Pendant l'interruption, un appel HTTP à l'écouteur reçoit une réponse en échec avec le code d'erreur `LOCK`.

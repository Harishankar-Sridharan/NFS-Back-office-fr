---
description: Syntaxe et exemples des expressions cron utilisées par la circulation.
---

# Expressions cron

Les expressions cron (`cron-periodicity`) suivent la syntaxe de la bibliothèque Quartz : 6 champs obligatoires et 1 facultatif, séparés par des espaces.

## Champs d'une expression cron

| Champ              | Valeurs                       | Caractères spéciaux |
| ------------------ | ----------------------------- | ------------------- |
| Secondes           | 0-59                          | `, - * /`           |
| Minutes            | 0-59                          | `, - * /`           |
| Heures             | 0-23                          | `, - * /`           |
| Jour du mois       | 1-31                          | `, - * ? / L W`     |
| Mois               | 1-12 ou JAN-DEC               | `, - * /`           |
| Jour de la semaine | 1-7 ou SUN-SAT (1 = dimanche) | `, - * ? / L #`     |
| Année (facultatif) | 1970-2099                     | `, - * /`           |

## Caractères spéciaux

| Caractère | Signification                                                                               |
| --------- | ------------------------------------------------------------------------------------------- |
| `*`       | Toutes les valeurs.                                                                         |
| `?`       | Aucune valeur précise (jour du mois ou jour de la semaine : l'un des deux doit valoir `?`). |
| `-`       | Intervalle : `10-12` = 10, 11 et 12.                                                        |
| `,`       | Liste : `MON,WED,FRI`.                                                                      |
| `/`       | Pas : `0/15` dans les secondes = 0, 15, 30, 45.                                             |
| `L`       | Dernier : dernier jour du mois, ou `6L` = dernier vendredi du mois.                         |
| `W`       | Jour ouvré le plus proche : `15W`.                                                          |
| `#`       | N-ième jour du mois : `6#3` = troisième vendredi.                                           |

## Exemples

| Expression                | Déclenchement                                                |
| ------------------------- | ------------------------------------------------------------ |
| `0/10 * * * * ?`          | Toutes les 10 secondes                                       |
| `0 0/5 * * * ?`           | Toutes les 5 minutes                                         |
| `0 0 12 * * ?`            | Tous les jours à midi                                        |
| `0 30 21 ? * *`           | Tous les jours à 21 h 30                                     |
| `0 15 10 ? * MON-FRI`     | Du lundi au vendredi à 10 h 15                               |
| `0 0/30 8-18 ? * MON-FRI` | Toutes les 30 minutes de 8 h à 18 h 30, du lundi au vendredi |
| `0 0 6 L * ?`             | Le dernier jour de chaque mois à 6 h                         |
| `0 15 10 ? * 6#3`         | Le troisième vendredi du mois à 10 h 15                      |

{% hint style="warning" %}
Évitez de programmer des traitements entre minuit et 1 h du matin : le changement d'heure peut les sauter ou les répéter.
{% endhint %}

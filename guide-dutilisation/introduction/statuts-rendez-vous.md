---
description: Comprendre les états des rendez-vous et les actions qui les modifient.
---

# Comprendre les états des rendez-vous

Chaque rendez-vous possède un état. L'état indique où en est le rendez-vous : en attente de planification, programmé, effectué ou annulé. Il permet de rechercher, de compter et de filtrer les rendez-vous, et il détermine ce qui peut encore être modifié.

Par exemple, un rendez-vous confirmé par téléphone avec le client engage votre organisation : passez-le à l'état **Confirmé**. Il reste dans le planning et ni l'intervenant, ni la date, ni l'heure ne peuvent plus changer.

## États disponibles

Les états sont regroupés par famille. Ce regroupement est visible notamment dans le champ **État** de la recherche de rendez-vous.

| Famille         | États                       |
| --------------- | --------------------------- |
| **Candidat**    | Demandé, Suspendu           |
| **Programmé**   | Planifié, Réservé, Confirmé |
| **Effectué**    | Réalisé, Déplacé, Imprévu   |
| **Annulé**      | Abandonné, Déprogrammé      |
| **Sous-traité** | Sous-traité                 |

Pendant la prise de rendez-vous, l'état **Planification en cours** s'affiche tant que le créneau choisi n'a pas été validé.

### Ce que permet chaque état

| État            | Dans le planning ? | Ce qui peut encore changer                                                                                                                     |
| --------------- | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **Demandé**     | Non                | Tout : le rendez-vous peut être placé par tous les moyens, y compris l'optimisation globale.                                                   |
| **Suspendu**    | Non                | Le rendez-vous peut être replanifié, mais pas par l'optimisation globale. Il attend une action de votre part, par exemple un rappel du client. |
| **Planifié**    | Oui                | L'intervenant, la date et l'heure.                                                                                                             |
| **Réservé**     | Oui                | L'intervenant. La date et l'heure sont figées.                                                                                                 |
| **Confirmé**    | Oui                | Rien : l'intervenant, la date et l'heure sont figés.                                                                                           |
| **Réalisé**     | —                  | Réalisé à la date prévue, par l'intervenant affecté.                                                                                           |
| **Déplacé**     | —                  | Réalisé, mais pas à la date prévue ou pas par l'intervenant affecté.                                                                           |
| **Imprévu**     | —                  | Réalisé alors qu'il n'était pas programmé.                                                                                                     |
| **Abandonné**   | Non                | Annulé alors qu'il n'était pas encore programmé.                                                                                               |
| **Déprogrammé** | Non                | Annulé alors qu'il était programmé.                                                                                                            |
| **Sous-traité** | Non                | Confié à un sous-traitant.                                                                                                                     |

{% hint style="info" %}
L'action **Accepter** fige l'affectation d'un rendez-vous planifié : la date et l'heure peuvent encore changer, mais plus l'intervenant.
{% endhint %}

## Comment un rendez-vous change d'état

Un rendez-vous change d'état lors d'une optimisation, d'une planification manuelle, d'une action sur une sélection de rendez-vous, d'un compte rendu ou d'un import de données. Les règles suivantes s'appliquent :

* un rendez-vous **candidat** devient **programmé** lorsqu'il est placé dans un planning ;
* un rendez-vous **programmé** peut redevenir **candidat** : il est alors déplanifié (état **Demandé**) ou suspendu (état **Suspendu**) ;
* un rendez-vous **programmé** devient **effectué** lorsque sa réalisation est déclarée : il passe à l'état **Réalisé** si la réalisation a lieu le jour prévu, par l'intervenant affecté, et à l'état **Déplacé** sinon ;
* un rendez-vous **candidat** dont la réalisation est déclarée passe à l'état **Imprévu** ;
* un rendez-vous peut être **annulé** à tout moment : il passe à l'état **Abandonné** s'il était candidat, **Déprogrammé** s'il était programmé ;
* un rendez-vous **annulé** peut être réactivé : il redevient candidat.

{% hint style="warning" %}
Lorsqu'un rendez-vous programmé est retiré du planning pour faire place à un autre rendez-vous ou à cause d'une indisponibilité, il redevient candidat. Selon le paramétrage de votre environnement, il passe à l'état **Demandé** ou **Suspendu**.
{% endhint %}

## Actions qui modifient l'état

Les actions suivantes sont proposées dans la fiche d'un rendez-vous. Leur description reprend les info-bulles de l'application.

| Action           | Effet                                                                                                                                                                          |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Planifier**    | Planifier le rendez-vous comme prévu                                                                                                                                           |
| **Réserver**     | Réserver le rendez-vous : l'heure du rendez-vous est définie                                                                                                                   |
| **Accepter**     | Accepter le rendez-vous : le rendez-vous ne doit plus changer d'affectation                                                                                                    |
| **Confirmer**    | Confirmer le rendez-vous                                                                                                                                                       |
| **Suspendre**    | Le client doit être rappelé et le rendez-vous doit être replanifié en temps réel. Aucune replanification par le moteur d'optimisation batch n'est effectuée sur ce rendez-vous |
| **Réactiver**    | Passer le rendez-vous en état demandé, pour qu'il puisse être planifié par l'optimisation batch                                                                                |
| **Déplanifier**  | Repasser le rendez-vous à son état avant planification : demandé ou suspendu                                                                                                   |
| **Replanifier**  | Replanifier le rendez-vous en lançant une optimisation temps réel ou en fixant une date et un intervenant                                                                      |
| **Sous-traiter** | Envoyer le rendez-vous au sous-traitant                                                                                                                                        |

Les actions disponibles dépendent de l'état actuel du rendez-vous. Pour en savoir plus, consultez [Consulter la fiche d'un rendez-vous](../rendez-vous/fiche-rendez-vous.md).

## Suivre l'avancement d'un rendez-vous

En complément de l'état, la section **État de réalisation** de la fiche d'un rendez-vous affiche le champ **Avancement**. Il indique si le rendez-vous a été effectué : **État indéterminé**, **Non Effectué**, **Effectué** ou **Infructueux**.

Pour en savoir plus, consultez [Consulter la fiche d'un rendez-vous](../rendez-vous/fiche-rendez-vous.md).

## Couleurs dans le planning

Dans le planning, la couleur d'un rendez-vous change avec son état. Par exemple, un rendez-vous confirmé s'affiche en vert foncé.

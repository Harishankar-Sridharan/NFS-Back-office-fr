---
description: >-
  Modifier le planning de présence des intervenants par glisser-déposer, gérer
  une sélection et produire des rapports dans le module Disponibilités.
---

# Modifier le planning de présence

Le module **Disponibilités** permet de modifier directement le planning de présence des intervenants : poser une indisponibilité, appliquer un modèle de semaine ou de journée, poser un jalon, puis répéter ou supprimer ces éléments.

## Avant de commencer

* Les éléments proposés dans le panneau gauche dépendent des modèles et des types créés dans l'**Administration** : types d'indisponibilité, modèles de journée et de semaine, natures de jalon… Pour en savoir plus, consultez [Gérer les calendriers](../administration/calendriers.md).
* Chaque action nécessite le droit correspondant. Si vous n'avez pas le droit nécessaire, le message « Vous n'êtes pas autorisé à effectuer cette action. » s'affiche.

## Accéder à la fonctionnalité

**Navigation :** `Lanceur d'applications > Disponibilités`

## Ajouter un élément par glisser-déposer

1. Dans le panneau gauche, sélectionnez l'élément à poser, par exemple un type d'indisponibilité ou un modèle de semaine.
2. Faites-le glisser dans l'agenda :
   * sur le nom d'un intervenant : l'élément s'applique à toute la période affichée pour cet intervenant ;
   * sur l'en-tête d'une colonne : l'élément s'applique à tous les intervenants affichés pour cette période ;
   * sur une cellule : l'élément s'applique à l'intervenant et à la période de la cellule.
3. Relâchez. Si une fenêtre de création s'ouvre, par exemple pour une indisponibilité, vérifiez ses paramètres, puis validez.

> **\[CAPTURE À PRENDRE]**
>
> * **Écran / Menu :** `Disponibilités`, vue hebdomadaire
> * **Contexte / Données à afficher :** glisser-déposer d'un type d'indisponibilité du panneau gauche vers la cellule d'un intervenant de test, avec la fenêtre de création ouverte.
> * **Rappel :** anonymiser les noms des clients et des ressources, ainsi que le nom de l'organisation de l'environnement de test.

## Répéter ou supprimer des éléments

1. Sélectionnez le nom d'un intervenant, l'en-tête d'une colonne ou une cellule pour sélectionner les éléments qu'elle contient. Maintenez la touche **Ctrl** pour une sélection multiple.
2. Utilisez les commandes proposées :
   * **Répéter la sélection** : définissez la récurrence des éléments sélectionnés ;
   * **Annuler la sélection** : désélectionnez les éléments ;
   * **Supprimer la sélection (cliquer, ou déposer des éléments)** : sélectionnez le bouton ou déposez la sélection dessus, puis confirmez.

## Produire un rapport

1. Ouvrez l'icône **Naviguer entre les services**, puis **Rapports**.
2. Choisissez le rapport parmi les modèles paramétrés. Il porte sur le périmètre affiché.
3. Exportez le rapport si votre profil le permet.

Les icônes **Exporter l'agenda** et **Imprimer l'agenda** exportent ou impriment l'agenda affiché.

## Afficher les plannings des clients

Avec le droit correspondant, la vue **Client** affiche les plannings des clients au lieu de ceux des intervenants. Vous pouvez alors y poser des périodes de fermeture. Revenez ensuite à la vue des intervenants.

## Points d'attention

{% hint style="warning" %}
Les modifications faites dans le module **Disponibilités** s'appliquent directement aux plannings utilisés par la planification et l'optimisation.
{% endhint %}

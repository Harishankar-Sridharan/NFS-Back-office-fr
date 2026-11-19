---
description: >-
  Gérer les postes temporaires, attributions de secteurs, jalons, emplacements
  d'hôtels, journées verrouillées, affectations de matériel et ouverture des
  secteurs.
---

# Gérer les autres éléments du planning

En plus des rendez-vous et des indisponibilités, le planning d'un intervenant peut contenir d'autres éléments qui modifient ce qu'il peut faire, où et quand. Ils se gèrent depuis la rubrique **Planification** du menu du module.

## Accéder à la fonctionnalité

**Navigation :** `Planification > Planification`, puis l'entrée voulue.

Chaque page présente des filtres (en général **Intervenant** et période **Du** / **Au**), un bouton **Rechercher** et un bouton de création. Les entrées affichées dépendent de vos droits.

| Entrée                               | Usage                                                        |
| ------------------------------------ | ------------------------------------------------------------ |
| **Postes temporaires**               | Remplacer provisoirement le poste principal d'un intervenant |
| **Visualiser les clients**           | Lister les clients affectés à un intervenant                 |
| **Attribution des sites de travail** | Attribuer temporairement un secteur à un intervenant         |
| **Gérer les jalons**                 | Poser des repères horodatés dans le planning                 |
| **Localisations exceptionnelles**    | Définir un lieu provisoire de départ ou d'arrivée de tournée |
| **Emplacements d'hôtels**            | Enregistrer les hôtels utilisables pour les nuitées          |
| **Journée verrouillée**              | Protéger une journée contre l'optimisation                   |
| **Affectations de matériel**         | Affecter du matériel à une ressource                         |
| **Gestion des secteurs**             | Ouvrir ou fermer un secteur, jour par jour                   |

## Affecter un poste temporaire

Le poste principal d'un intervenant définit les types d'intervention qu'il peut réaliser. Un poste temporaire le remplace pour une période, par exemple pour autoriser un technicien de maintenance à faire des dépannages pendant une semaine chargée.

1. Ouvrez **Postes temporaires**.
2. Sélectionnez **Ajouter un poste** (info-bulle **Ajouter un poste pour l'intervenant**).
3. Choisissez le **Poste**, la durée et la période, puis enregistrez.

Pour retrouver les postes existants, filtrez par **Intervenant**, **Poste** et période, puis sélectionnez **Chercher**.

## Attribuer un secteur à un intervenant

La page **Attribution de secteurs à des intervenants** affecte temporairement à un intervenant un secteur supplémentaire, ou un autre secteur en remplacement du sien.

1. Ouvrez **Attribution des sites de travail**.
2. Sélectionnez **Attribuer un secteur**.
3. Choisissez le secteur et la période, puis enregistrez.

## Poser un jalon

Un jalon est un repère horodaté du planning, par exemple un appel téléphonique ou une promesse de rendez-vous. Il n'a pas besoin d'adresse et peut chevaucher d'autres éléments.

1. Ouvrez **Gérer les jalons**, ou sélectionnez **Poser un jalon** dans la fiche d'un rendez-vous.
2. Choisissez l'intervenant, le **Type** (par exemple **Appel téléphonique**, **Début de journée**, **Fin de journée**, **Promesse de rendez-vous**), la date et l'heure.
3. Enregistrez.

## Enregistrer un emplacement d'hôtel

Les emplacements d'hôtels permettent de positionner rapidement une nuitée lors de la saisie d'une localisation exceptionnelle.

1. Ouvrez **Emplacements d'hôtels**.
2. Sélectionnez **Nouveau**.
3. Renseignez le nom, l'adresse et la période de disponibilité, puis enregistrez.

Pour les localisations exceptionnelles, consultez [Gérer les localisations exceptionnelles](../indisponibilites/localisations-exceptionnelles.md).

## Verrouiller une journée

Une journée verrouillée protège la journée d'un intervenant contre l'optimisation.

1. Ouvrez **Journée verrouillée**.
2. Sélectionnez **Verrouiller une journée dans l'agenda**.
3. Choisissez l'intervenant, la date et l'**État**, puis enregistrez.

| État       | Effet                                                                 |
| ---------- | --------------------------------------------------------------------- |
| **Fermé**  | Aucun rendez-vous ne peut être ajouté à la journée.                   |
| **Scellé** | Aucun rendez-vous ne peut être ajouté à la journée ni en être retiré. |
| **Forcé**  | La journée est verrouillée.                                           |

Pour déverrouiller des journées, cochez-les dans la liste puis utilisez **Déverrouiller les journées sélectionnés**.

Dans le planning, le menu **⋮** d'un intervenant propose **Afficher les journées verrouillées**.

## Affecter du matériel

1. Ouvrez **Affectations de matériel**.
2. Sélectionnez **Ajouter une affectation**.
3. Choisissez le matériel, la ressource et la période, puis enregistrez.

## Ouvrir ou fermer un secteur

La page **Gestion des secteurs** affiche, pour chaque secteur et chaque jour de la période, l'état du secteur et le nombre de rendez-vous.

1. Filtrez la période (**Du**, **Au**) et, si besoin, le **Secteur**, puis sélectionnez **Chercher**.
2. Sélectionnez la case d'un jour pour changer l'état du secteur (info-bulles **Secteur ouvert** / **Cliquez pour fermer ce secteur**).

> **\[CAPTURE À PRENDRE]**
>
> * **Écran / Menu :** `Planification > Planification > Gestion des secteurs`
> * **Contexte / Données à afficher :** grille des secteurs sur une période d'une semaine, avec au moins un secteur ouvert et un secteur fermé.
> * **Rappel :** anonymiser les noms des clients et des ressources, ainsi que le nom de l'organisation de l'environnement de test.

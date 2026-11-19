---
description: Découvrir le module Administration et la gestion commune des données.
---

# Administration

Le module Administration permet de gérer les données de l'entreprise : ressources humaines, équipes, sites de travail, types d'intervention, compétences, calendriers, etc. Il donne aussi accès à l'optimisation, à la mobilité, aux utilisateurs et aux droits, à la personnalisation, aux fichiers d'échange et aux outils.

## Accéder au module

**Navigation :** `Lanceur d'applications > Administration`

La page **À propos de Nomadia Field Service** s'affiche à l'ouverture. Elle indique le nom, la version et l'édition de l'application, ainsi que les informations de licence.

## Menu du module

Le menu de gauche est organisé en groupes.

| Groupe                        | Entrées                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Pages du guide                                                                                  |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------- |
| **Données entreprise**        | Ressource humaine, Type d'intervenant, Type de poste, Sous-traitant, Matériel, Famille de produits (Famille de produits, Produit), Équipe, Domaine, Région, Site de travail, Secteur, Secteur d'astreinte, Type d'indisponibilité, Type de localisation exceptionnelle, Astreintes (Modèle de jour, Modèle de semaine), Compétence, Autorisation, Intervention (Groupe d'interventions, Type d'intervention), Objectifs, Suivi de l'activité (État de réalisation, Suite à donner), Typologie, Calendriers (Jours fériés, Modèle de jour, Modèle de semaine, Période de vente) | Voir la liste ci-dessous                                                                        |
| **Optimisation**              | Paramètres d'optimisation, Planification d'optimisation, Activer/Désactiver une région, Importer/exporter une optim                                                                                                                                                                                                                                                                                                                                                                                                                                                            | [Paramétrer l'optimisation](optimisation.md)                                                    |
| **Mobilité**                  | Véhicules, Équipement de suivi, Affectations, Utilitaires de suivi, Paramètres                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | [Gérer la mobilité](mobilite.md)                                                                |
| **Utilisateurs**              | Profil, Collection de droits, Droits d'accès, Abonnement aux alertes                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | [Gérer les profils et les droits](utilisateurs-droits.md)                                       |
| **Personnalisation**          | Configuration de l'application, Labels, Thèmes, Couleurs (Couleurs du référentiel, Couleurs de l'application)                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | [Personnaliser l'application](personnalisation.md)                                              |
| **Fichiers CSV**              | Importer un fichier CSV, Exporter un fichier CSV, Importation semi-automatique, Import/export CSV global, Modèle d'import/export CSV, Listeners de la circulation, Liens d'exportation prédéfinis                                                                                                                                                                                                                                                                                                                                                                              | [Imports et exports](../imports-exports/), [Gérer les fichiers d'échange](fichiers-echanges.md) |
| **Fichiers spécifiques**      | Exporter des POI TomTom, Exporter des POI Masternaut, Exporter des POI Garmin, Exporter des POI en KML, Importer une simulation GTM                                                                                                                                                                                                                                                                                                                                                                                                                                            | [Gérer les fichiers d'échange](fichiers-echanges.md)                                            |
| **Fichiers XML**              | Fichier d'optimisation, Fichier de circulation, Exemples de circulation, Journaux                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | [Gérer les fichiers d'échange](fichiers-echanges.md)                                            |
| **Outils**                    | Outils avancés, Recalculer la distance, Vérifier l'état des serveurs, Journaux, Dump de la thread JVM, Services cartographiques                                                                                                                                                                                                                                                                                                                                                                                                                                                | [Utiliser les outils d'administration](outils.md)                                               |
| **API Nomadia Field Service** | Documentation, Modèle d'import/export CSV                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | [Utiliser les outils d'administration](outils.md)                                               |

{% hint style="info" %}
Les actions autorisées dans ce module dépendent des droits d'accès de l'utilisateur, par exemple `ADMIN_CREATE_AREA` pour créer une région. Consultez [Gérer les profils et les droits](utilisateurs-droits.md).
{% endhint %}

## Gérer une donnée : principes communs

La plupart des entrées de **Données entreprise** fonctionnent de la même façon.

### Rechercher et lister

1. Sélectionnez l'entrée dans le menu de gauche.
2. Renseignez si besoin les filtres proposés, par exemple **Région**.
3. Selon l'entrée, la liste s'affiche directement ou après avoir sélectionné **Rechercher**.

La liste affiche les éléments existants, ou le message **Aucun résultat trouvé.** Le nombre de lignes par page se règle au-dessus de la liste lorsqu'elle comporte plusieurs pages.

### Créer un élément

1. Sélectionnez le bouton **Créer…** en haut à droite, par exemple **Créer une équipe**.
2. Renseignez les champs. Les champs obligatoires sont signalés par un astérisque.
3. Sélectionnez **Enregistrer**. Pour certaines entrées, la création se fait en plusieurs pages : utilisez **Page suivante** et **Page précédente**, puis **Enregistrer**.

Après l'enregistrement, la notification **Enregistrement effectué** s'affiche et des onglets supplémentaires peuvent apparaître.

### Ouvrir et modifier un élément

1. Dans la liste, sélectionnez la ligne de l'élément.
2. La fiche de l'élément s'ouvre avec ses onglets et le bouton **Enregistrer**.

Le bouton **Retourner à la liste** ramène à la liste des éléments. Les boutons **Désactiver** et **Dupliquer** sont proposés sur la fiche d'un élément enregistré.

### Dupliquer un élément

1. Ouvrez la fiche à copier.
2. Sélectionnez **Dupliquer**. Une nouvelle fiche préremplie s'ouvre.
3. Modifiez au minimum le nom et la **Référence externe**.
4. Sélectionnez **Enregistrer**.

{% hint style="warning" %}
Donnez toujours une référence externe différente à la copie. Lors des échanges de données, deux éléments qui ont la même référence externe peuvent s'écraser.
{% endhint %}

### Désactiver un élément

La plupart des données ne sont pas supprimées mais désactivées : elles n'apparaissent plus dans les listes de choix, mais restent liées à l'historique. Pour désactiver un élément, ouvrez sa fiche et sélectionnez **Désactiver**.

Une ressource humaine ne se désactive pas : renseignez plutôt une date de fin de période d'activité dans sa fiche.

Pour un exemple complet, consultez [Gérer les équipes](equipes.md).

## Dans cette section

### Données entreprise

* [Gérer les ressources humaines](ressources-humaines.md)
* [Gérer les types d'intervenant et les types de poste](types-intervenant-poste.md)
* [Gérer les sous-traitants, le matériel et les produits](sous-traitants-materiel-produits.md)
* [Gérer les équipes](equipes.md)
* [Gérer l'organisation géographique](organisation-geographique.md)
* [Paramétrer les types d'indisponibilité et de localisation exceptionnelle](indisponibilites-localisations.md)
* [Paramétrer les astreintes](astreintes.md)
* [Gérer les compétences et les autorisations](competences-autorisations.md)
* [Paramétrer les interventions](interventions.md)
* [Gérer les objectifs, le suivi de l'activité et les typologies](objectifs-suivi-activite.md)
* [Gérer les calendriers](calendriers.md)

### Paramétrage de l'application

* [Paramétrer l'optimisation](optimisation.md)
* [Gérer la mobilité](mobilite.md)
* [Gérer les profils et les droits](utilisateurs-droits.md)
* [Personnaliser l'application](personnalisation.md)
* [Gérer les fichiers d'échange](fichiers-echanges.md)
* [Utiliser les outils d'administration](outils.md)

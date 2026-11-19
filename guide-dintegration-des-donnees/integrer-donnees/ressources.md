---
description: >-
  Ressources humaines, actions spécifiques, types d'intervenant et types de
  poste.
---

# Intégrer les ressources

La ressource humaine (HumanResource) représente à la fois les intervenants planifiés et les utilisateurs de l'application. Le champ OPTIMIZABLE indique si la ressource va sur le terrain et doit être prise en compte par la planification.

| Champ             | Type          | Oblig. | Référence       | Description                                                                                                                                                                                                                  | Exemple / défaut                         |
| ----------------- | ------------- | ------ | --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| RESOURCEID        | Identifiant   | Oui    |                 | Identifiant de la ressource                                                                                                                                                                                                  | ex. TECH\_001                            |
| RESOURCELASTNAME  | Chaîne        | Oui    |                 | Nom de la ressource                                                                                                                                                                                                          | ex. MARTIN                               |
| RESOURCEFIRSTNAME | Chaîne        | Non    |                 | Prénom de la ressource                                                                                                                                                                                                       | ex. Pierre                               |
| AREAID            | Réf.          | Non    | Région          | Région d'appartenance de cette ressource                                                                                                                                                                                     | ex. REG\_001                             |
| WORKSITEID        | Réf.          | Non    | Site de travail | Identifiant de l'agence principale de rattachement de cette ressource                                                                                                                                                        | ex. WKS\_001                             |
| TEAMID            | Réf.          | Non    | Équipe          | Identifiant de l'équipe de rattachement de cette ressource                                                                                                                                                                   |                                          |
| OPTIMIZABLE       | Booléen       | Non    |                 | Definit si la ressource est optimisable / va sur le terrain                                                                                                                                                                  | ex. 1 (optimisable), 0 (non optimisable) |
| MANPOWER          | Entier        | Non    |                 | Indique si cette ressource est considérée comme une personne unitaire ou bien comme un groupe de plusieurs ressources (sous-traitants dont on ne gère pas les plannings individuels) (min 1, max 10)                         | ex. 1                                    |
| QUALIFICATIONS    | Liste de réf. | Non    | Compétence      | Liste des compétences détenues en permanence par cette ressource                                                                                                                                                             | ex. QUA\_001;QUA\_002                    |
| ADDRESS           | Adresse       | Non    |                 | Adresse postale de départ de la ressource (rue + numéro de rue)                                                                                                                                                              | ex. 66 avenue du Maine                   |
| CODEZONE          | Adresse       | Non    |                 | Code postal de l'adresse de départ de la ressource                                                                                                                                                                           | ex. 75014                                |
| CITY              | Adresse       | Non    |                 | Ville de l'adresse de départ de la ressource                                                                                                                                                                                 | ex. PARIS                                |
| WORKEMAIL         | Chaîne        | Non    |                 | Email de la ressource (professionnel)                                                                                                                                                                                        |                                          |
| ACTION            | Chaîne        | Non    |                 | Verbe d'action commandant un comportement d'importation spécifique (RETRIEVE\_JOB\_PRIORITIES\_LIMITS: récupérer toutes les priorités et limites définies sur un type de ressource et les appliquer à la ressource courante) |                                          |

L'entité comporte plus de 300 champs : horaires par jour de la semaine (DAY1… à DAY7…, 1 = lundi), limites de temps de travail et de trajet, localisations de départ et de retour, champs personnalisés. La liste complète figure dans la [référence du modèle d'échange](../reference-modele/).

## Actions spécifiques

La colonne ACTION de la ressource accepte des valeurs qui recopient sur la ressource le paramétrage de son type de poste : RETRIEVE\_JOB\_WORKWEEK, RETRIEVE\_JOB\_LIMITS, RETRIEVE\_JOB\_PRIORITIES, RETRIEVE\_JOB\_PRIORITIES\_LIMITS.

## Types d'intervenant et types de poste

Selon l'option de modélisation de l'instance (showFunctionsInJobtypes ou showJobtypesInFunctions de la configuration COMPANY\_MODELING\_OPTION), le modèle propose soit les entités ResourceType, ResourcetypePriority et ResourcetypeGroupPriority, soit les entités ResourceJobType, JobTypePriority, JobTypeGroupPriority, ResourceFunction, FunctionPriority et FunctionGroupPriority. Vérifiez la liste des entités de l'instance dans `Administration > Fichiers CSV > Modèle d'import/export CSV` ou avec l'opération ListEntities.

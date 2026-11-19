---
description: Régions, sites de travail, équipes, groupes et types d'intervention.
---

# Intégrer l'organisation et l'activité

## Organisation

La région (Area) regroupe un ensemble de données à planifier ensemble ; elle correspond à un territoire ou à une activité. Le site de travail (Worksite), aussi appelé agence, rattache ressources, clients et interventions. Le secteur (Sector) découpe un site en zones géographiques. L'équipe (Team) regroupe hiérarchiquement des ressources.

| Champ       | Type        | Oblig. | Référence | Description                                                          | Exemple / défaut                             |
| ----------- | ----------- | ------ | --------- | -------------------------------------------------------------------- | -------------------------------------------- |
| AREAID      | Identifiant | Oui    |           | Identifiant de la région (entité géographique ou activité/métier)    | ex. REG\_001 ou ACTIV\_AUTO ou ZONE\_SO ou 1 |
| AREANAME    | Chaîne      | Oui    |           | Nom de la région telle qu'elle apparaîtra à l'utilisateur            | ex. SUD-OUEST ou AUTOMOBILE                  |
| DESCRIPTION | Chaîne      | Non    |           | Commentaire pour décrire cette région                                | ex. Zone Sud-Ouest ou Activité automobile    |
| ACTIVE      | Booléen     | Non    |           | Activation (1,"O",true) / Désactivation du site/client (0,"N",false) | ex. 1 · défaut 1                             |

| Champ            | Type        | Oblig. | Référence       | Description                                                          | Exemple / défaut                                                                             |
| ---------------- | ----------- | ------ | --------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| WORKSITEID       | Identifiant | Oui    |                 | Identifiant de l'agence                                              | ex. WKS\_001                                                                                 |
| WORKSITENAME     | Chaîne      | Oui    |                 | Nom de l'agence tel qu'il apparaîtra à l'utilisateur                 | ex. Agence de PARIS                                                                          |
| AREAID           | Réf.        | Non    | Région          | Région d'appartenance de l'agence                                    | ex. REG\_001 · défaut c'est la région par défaut (id=1) qui est prise si aucune n'est donnée |
| PARENTWORKSITEID | Réf.        | Non    | Site de travail | Agence parente                                                       | ex. PWS\_001                                                                                 |
| ADDRESS          | Adresse     | Non    |                 | Adresse postale de l'agence (rue + numéro de rue)                    | ex. 66 avenue du Maine                                                                       |
| CODEZONE         | Adresse     | Non    |                 | Code postal de l'adresse de l'agence                                 | ex. 75014                                                                                    |
| CITY             | Adresse     | Non    |                 | Ville de l'adresse de l'agence                                       | ex. PARIS                                                                                    |
| ACTIVE           | Booléen     | Non    |                 | Activation (1,"O",true) / Désactivation du site/client (0,"N",false) | ex. 1 · défaut 1                                                                             |

| Champ    | Type        | Oblig. | Référence         | Description                                                          | Exemple / défaut |
| -------- | ----------- | ------ | ----------------- | -------------------------------------------------------------------- | ---------------- |
| TEAMID   | Identifiant | Oui    |                   | Identifiant de l'équipe                                              | ex. EQU\_002     |
| TEAMNAME | Chaîne      | Oui    |                   | Nom de l'équipe tel qu'il apparaîtra à l'utilisateur                 |                  |
| AREAID   | Réf.        | Non    | Région            | Région d'appartenance de l'équipe                                    | ex. REG\_001     |
| LEADERID | Réf.        | Non    | Ressource humaine | Identifiant du chef d'équipe                                         | ex. TECH\_001    |
| PARENTID | Réf.        | Non    | Équipe            | Identifiant de l'équipe mère                                         | ex. EQU\_001     |
| ACTIVE   | Booléen     | Non    |                   | Activation (1,"O",true) / Désactivation du site/client (0,"N",false) | ex. 1 · défaut 1 |

{% hint style="info" %}
Créez au moins une équipe, même si les ressources ne sont pas organisées en équipes : plusieurs vues de planification filtrent par équipe.
{% endhint %}

## Activité : groupes et types d'intervention

Nomadia Field Service gère deux niveaux : le groupe d'intervention (TaskTypeGroup) et le type d'intervention (TaskType). Si le référentiel du client comporte plus de niveaux, concaténez les niveaux inférieurs dans le type d'intervention (par exemple « Entretien – Chaudière gaz »).

| Champ             | Type        | Oblig. | Référence | Description                                                                                                                 | Exemple / défaut |
| ----------------- | ----------- | ------ | --------- | --------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| TASKTYPEGROUPID   | Identifiant | Oui    |           | Identifiant du groupe de type d'intervention                                                                                | ex. TTG\_001     |
| TASKTYPEGROUPNAME | Chaîne      | Oui    |           | Nom du groupe de type d'intervention tel qu'il apparaitra à l'utilisateur                                                   | ex. Maintenance  |
| AREAID            | Réf.        | Non    | Région    | Région d'appartenance du groupe de type d'intervention. Ce groupe est visible dans toutes les régions si ce champ est vide. | ex. REG\_001     |
| ACTIVE            | Booléen     | Non    |           | Activation (1,"O",true) / Désactivation du site/client (0,"N",false)                                                        | ex. 1 · défaut 1 |

| Champ             | Type          | Oblig. | Référence             | Description                                                                           | Exemple / défaut      |
| ----------------- | ------------- | ------ | --------------------- | ------------------------------------------------------------------------------------- | --------------------- |
| TASKTYPEID        | Identifiant   | Oui    |                       | Identifiant du type d'intervention                                                    | ex. TT\_001           |
| TASKTYPENAME      | Chaîne        | Oui    |                       | Nom du type d'intervention tel qu'il apparaîtra à l'utilisateur                       |                       |
| TASKTYPEGROUPID   | Réf.          | Oui    | Groupe d'intervention | Groupe d'appartenance du type d'intervention                                          | ex. TTG\_001          |
| DURATION          | Durée         | Oui    |                       | Durée par défaut pour une intervention de ce type d'intervention (en minutes)         | ex. 90                |
| QUALIFICATIONS    | Liste de réf. | Non    |                       | Liste des compétences nécessaires à la réalisation de ce type d'intervention          | ex. QUA\_001;QUA\_002 |
| DEFAULT\_MANPOWER | Entier        | Non    |                       | Nombre de ressource nécessaire par défaut pour réaliser ce type d'intervention        | ex. 1 · défaut 1      |
| MIN\_MANPOWER     | Entier        | Non    |                       | Nombre minimal de ressources nécessaires pour réaliser ce type d'intervention (min 1) | ex. 1 · défaut 1      |
| MAX\_MANPOWER     | Entier        | Non    |                       | Nombre de ressources maximum nécessaire pour réaliser ce type d'intervention (max 10) | ex. 1 · défaut 1      |
| ACTIVE            | Booléen       | Non    |                       | Activation (1,"O",true) / Désactivation du site/client (0,"N",false)                  | ex. 1 · défaut 1      |

{% hint style="warning" %}
La durée (DURATION) est obligatoire pour un type d'intervention. Elle est exprimée en minutes.
{% endhint %}

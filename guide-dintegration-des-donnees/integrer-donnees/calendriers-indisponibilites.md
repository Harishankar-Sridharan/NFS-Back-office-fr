---
description: >-
  Modèles de journée et de semaine, jours fériés, indisponibilités et autres
  calendriers.
---

# Intégrer les calendriers, horaires et indisponibilités

## Modèles de journée et de semaine

Les horaires standard sont décrits par des types de journée de travail (WorkdayType : heures de début et de fin, pause déjeuner) assemblés en types de semaine de travail (WorkWeekType). Une ressource suit une semaine type ; des exceptions datées s'importent avec ResourceWorkWeek (semaine type sur une période) et ResourceWorkday (journée particulière).

| Champ               | Type        | Oblig. | Référence | Description                                                               | Exemple / défaut           |
| ------------------- | ----------- | ------ | --------- | ------------------------------------------------------------------------- | -------------------------- |
| WORKDAYTYPEID       | Identifiant | Oui    |           | Identifiant du modèle de journée dans le SI de l'entreprise               | ex. MON\_MODELE\_DE\_LUNDI |
| WORKDAYTYPENAME     | Chaîne      | Oui    |           | Identifiant du modèle de journée dans le SI de l'entreprise               |                            |
| DAYBEGINTIME        | Heure       | Non    |           | Horaire de début de journée (HH:MM)                                       | ex. 08:00                  |
| DAYENDTIME          | Heure       | Non    |           | Horaire de fin de journée (HH:MM)                                         | ex. 18:00                  |
| DAYBEGINLUNCHPERIOD | Heure       | Non    |           | Horaire de début de la pause déjeuner glissante (HH:MM)                   | ex. 12:00                  |
| DAYENDLUNCHPERIOD   | Heure       | Non    |           | Horaire de fin de la pause déjeuner glissante (HH:MM)                     | ex. 14:00                  |
| DAYLUNCHDURATION    | Heure       | Non    |           | Durée de la pause déjeuner (en minutes)                                   | ex. 60                     |
| DAYISWORKED         | Booléen     | Non    |           | Définit si cette journée est considérée comme travaillée (1: oui, 0: non) | ex. 1                      |

| Champ            | Type          | Oblig. | Référence                  | Description                               | Exemple / défaut                                                                                       |
| ---------------- | ------------- | ------ | -------------------------- | ----------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| WORKWEEKTYPEID   | Identifiant   | Oui    |                            | Identifiant du type de semaine de travail | ex. SPECIAL\_WEEK01                                                                                    |
| WORKWEEKTYPENAME | Chaîne        | Oui    |                            | Nom du type de semaine de travail         |                                                                                                        |
| WORKDAYTYPES     | Liste de réf. | Oui    | Type de journée de travail | Idenfiant externe des types de jours      | ex. MY\_MONDAY\_TEMPLATE,MY\_TUESDAY\_TEMPLATE,etc.                                                    |
| STARTDAY         | Entier        | Non    |                            | Jour de début de la semaine               | ex. 0=N'IMPORTE QUEL JOUR,1=LUNDI,2=MARDI,3=MERCREDI,4=JEUDI,5=VENDREDI,6=SAMEDI,7=DIMANCHE · défaut 0 |

{% hint style="warning" %}
Le modèle de journée STDWORKDAY est le modèle par défaut de l'instance (d'après la description du modèle d'échange). Modifiez-le avec précaution.
{% endhint %}

## Jours fériés

| Champ       | Type        | Oblig. | Référence       | Description                                             | Exemple / défaut      |
| ----------- | ----------- | ------ | --------------- | ------------------------------------------------------- | --------------------- |
| HOLIDAYID   | Identifiant | Non    |                 | Identifiant du jour férié dans le SI de l'entreprise    | ex. FERIE\_01012012   |
| HOLIDAYDATE | Date        | Oui    |                 | Date du jour férié                                      | ex. 01/01/2012        |
| HOLIDAYNAME | Chaîne      | Oui    |                 | Nom du jour férié tel qu'il apparaitra à l'utilisateur  | ex. Jour de l'an 2012 |
| AREAID      | Réf.        | Non    | Région          | Région à laquelle ce jour férié appartient              | ex. REG\_001          |
| WORKSITEID  | Réf.        | Non    | Site de travail | Site de travail auquel appartient cette journée         | ex. WS001             |
| ACTION      | Chaîne      | Non    |                 | Verbe d'action pour supprimer l'enregistrement (DELETE) |                       |

## Indisponibilités

Une indisponibilité (Unavailability) bloque une ressource sur une période (formation, congé, réunion). Son type (UnavailabilityType) indique notamment si le temps est considéré comme travaillé (ISWORKTIME). Les indisponibilités peuvent être périodiques (PERIODICITY\_\*) et localisées (adresse ou coordonnées).

| Champ                  | Type        | Oblig. | Référence | Description                                                                   | Exemple / défaut |
| ---------------------- | ----------- | ------ | --------- | ----------------------------------------------------------------------------- | ---------------- |
| UNAVAILABILITYTYPEID   | Identifiant | Oui    |           | Identifiant du type d'indisponibilité                                         |                  |
| UNAVAILABILITYTYPENAME | Chaîne      | Oui    |           | Nom de ce type d'indisponibilité tel qu'il apparaîtra à l'utilisateur         |                  |
| ISWORKTIME             | Booléen     | Non    |           | Ce type d'indisponibilité est-elle considérée comme travaillée ? (ex réunion) | ex. 0            |
| DEFAULT\_DURATION      | Durée       | Non    |           | Durée par défaut de l'indisponibilité (en minutes)                            |                  |
| ISREQUIREDVALIDATION   | Booléen     | Non    |           | Cette indisponibilité nécessite-t-elle une validation ?                       | ex. 0 · défaut 0 |

| Champ                  | Type         | Oblig. | Référence              | Description                                                    | Exemple / défaut                                           |
| ---------------------- | ------------ | ------ | ---------------------- | -------------------------------------------------------------- | ---------------------------------------------------------- |
| UNAVAILABILITYID       | Identifiant  | Oui    |                        | Identifiant de l'indisponibilité                               |                                                            |
| RESOURCEID             | Réf.         | Oui    | Ressource humaine      | Nom de l'intervenant qui n'est pas disponible                  | ex. TECH\_001                                              |
| UNAVAILABILITY\_TYPEID | Réf.         | Oui    | Type d'indisponibilité | Type de l'indisponibilité                                      |                                                            |
| DATEBEGIN              | Date (début) | Non    |                        | Date de début de l'indisponibilité (JJ/MM/AAAA)                | ex. 25/12/2012                                             |
| TIMEBEGIN              | Heure        | Non    |                        | Heure de début de l'indisponibilité (HH:MM)                    | ex. 00:00                                                  |
| DATEEND                | Date (fin)   | Non    |                        | Date de fin de l'indisponibilité (JJ/MM/AAAA)                  | ex. 25/12/2012                                             |
| TIMEEND                | Heure        | Non    |                        | Heure de fin de l'indisponibilité (HH:MM)                      | ex. 23:59                                                  |
| DATETIMEBEGIN          | Date-heure   | Non    |                        | Date et heure de début de l'indisponibilité (JJ/MM/AAAA HH:MM) | ex. 25/12/2012 08:00                                       |
| DATETIMEEND            | Date-heure   | Non    |                        | Date et heure de fin de l'indisponibilité (JJ/MM/AAAA HH:MM)   | ex. 25/12/2012 20:00                                       |
| STATUS                 | Entier       | Non    |                        | État                                                           | ex. { 0=INCONNUE ,10 = ANNULÉE,21 = DEMANDÉE, 29=ACCEPTÉE; |
| ACTION                 | Chaîne       | Non    |                        | Verbe d'action pour supprimer l'enregistrement (DELETE)        |                                                            |

## Autres calendriers

* Localisations exceptionnelles (ExceptLocation) : période pendant laquelle une ressource part d'un autre lieu ou à une autre heure.
* Journées verrouillées (AgendaControlledDate) : journées d'agenda d'une ressource protégées des modifications.
* Astreintes (DutyType, DutyWeekType, Duty, DutyWeek, DutyReplacement) et secteurs d'astreinte (DutySectorType, DutySector).
* Établissements (BusinessLocation, hôtels) et dépôts (DepotBusinessLocation) avec leurs périodes de fermeture.

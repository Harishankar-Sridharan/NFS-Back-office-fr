---
description: >-
  Jeu de données fictif complet : fichiers CSV, mises à jour, suppression et
  appels de services web.
---

# Exemples d'intégration

Les exemples suivants forment un jeu de données fictif unique : l'entreprise de maintenance « Démo Services » intègre une région, une agence, une équipe, un type d'intervention, deux techniciens, un client et une intervention. Les fichiers utilisent les paramètres par défaut de l'import par l'interface : séparateur ;, séparateur de liste ,, dates dd/MM/yyyy.

## 1. Organisation

{% code title="01_Area.csv" %}
```csv
AREAID;AREANAME;DESCRIPTION
REG_IDF;Île-de-France;Région de démonstration
```
{% endcode %}

{% code title="02_Worksite.csv" %}
```csv
WORKSITEID;WORKSITENAME;AREAID;ADDRESS;CODEZONE;CITY;COUNTRY;XGEO;YGEO
AG_PARIS_N;Agence Paris Nord;REG_IDF;10 rue de l'Exemple;75018;Paris;France;2.3522;48.8925
```
{% endcode %}

{% code title="03_Team.csv" %}
```csv
TEAMID;TEAMNAME;AREAID;ACTIVE
EQ_NORD;Équipe Nord;REG_IDF;1
```
{% endcode %}

## 2. Référentiels d'activité

{% code title="04_Qualification.csv" %}
```csv
QUALIFICATIONID;QUALIFICATIONNAME;AREAID
QUAL_GAZ;Habilitation gaz;REG_IDF
```
{% endcode %}

{% code title="05_TaskTypeGroup.csv" %}
```csv
TASKTYPEGROUPID;TASKTYPEGROUPNAME;AREAID
TTG_MAINT;Maintenance;REG_IDF
```
{% endcode %}

{% code title="06_TaskType.csv" %}
```csv
TASKTYPEID;TASKTYPENAME;TASKTYPEGROUPID;DURATION;QUALIFICATIONS
TT_ENTRETIEN;Entretien annuel chaudière;TTG_MAINT;60;QUAL_GAZ
TT_DEPANNAGE;Dépannage;TTG_MAINT;90;
```
{% endcode %}

{% code title="07_UnavailabilityType.csv" %}
```csv
UNAVAILABILITYTYPEID;UNAVAILABILITYTYPENAME;ISWORKTIME
IND_FORM;Formation;1
```
{% endcode %}

## 3. Ressources

{% code title="08_HumanResource.csv" %}
```csv
RESOURCEID;RESOURCELASTNAME;RESOURCEFIRSTNAME;AREAID;WORKSITEID;TEAMID;OPTIMIZABLE;QUALIFICATIONS;ADDRESS;CODEZONE;CITY;XGEO;YGEO
TECH_001;MARTIN;Julie;REG_IDF;AG_PARIS_N;EQ_NORD;1;QUAL_GAZ;1 place de l'Exemple;93200;Saint-Denis;2.3580;48.9362
TECH_002;DURAND;Karim;REG_IDF;AG_PARIS_N;EQ_NORD;1;;5 avenue de la Démo;92110;Clichy;2.3060;48.9042
```
{% endcode %}

{% code title="09_TaskPriorities.csv" %}
```csv
PRIORITY_RESOURCEID;PRIORITY_TASK_TYPEID;PRIORITYMANUALOPTIM;PRIORITYREALTIMEOPTIM;PRIORITYBATCHOPTIM
TECH_001;TT_ENTRETIEN;1;100;100
TECH_002;TT_DEPANNAGE;1;100;100
```
{% endcode %}

{% code title="10_Unavailability.csv" %}
```csv
UNAVAILABILITYID;RESOURCEID;UNAVAILABILITY_TYPEID;DATEBEGIN;TIMEBEGIN;DATEEND;TIMEEND
IND_0001;TECH_001;IND_FORM;16/11/2026;08:00;16/11/2026;12:00
```
{% endcode %}

## 4. Clients

{% code title="11_Customer.csv" %}
```csv
CUSTOMERID;CUSTOMERNAME;AREAID;WORKSITEID;ADDRESS;CODEZONE;CITY;XGEO;YGEO
CLI_1001;Boulangerie des Lilas;REG_IDF;AG_PARIS_N;12 rue des Lilas;75019;Paris;2.3912;48.8786
```
{% endcode %}

{% code title="12_Contact.csv" %}
```csv
CONTACTID;CUSTOMERID;CONTACTLASTNAME;CONTACTFIRSTNAME;ISMAIN;CONTACTCELLULARPHONE;CONTACTWORKEMAIL
CT_1001;CLI_1001;BERNARD;Claire;1;0600000000;contact@exemple.invalid
```
{% endcode %}

## 5. Interventions

{% code title="13_Appointment.csv – création d'une intervention à planifier, avec recherche de créneau" %}
```csv
APPOINTMENTID;CUSTOMERID;TASKTYPES;DURATION;DATEMINBEGIN;DATEMAXEND;STATUS;ACTION
ITV_5001;CLI_1001;TT_ENTRETIEN;60;16/11/2026;27/11/2026;21;SCHEDULE
```
{% endcode %}

L'intervention est créée au statut Demandé (21) puis Nomadia Field Service cherche un créneau (SCHEDULE). Seule Julie MARTIN détient la compétence QUAL\_GAZ exigée par le type TT\_ENTRETIEN ; elle est indisponible le 16/11/2026 au matin.

## 6. Mises à jour

{% code title="Prolongation de la période de réalisation (mode mise à jour seule)" %}
```csv
APPOINTMENT$ID;DATEMAXEND
ITV_5001;04/12/2026
```
{% endcode %}

{% code title="Déclaration de réalisation" %}
```csv
APPOINTMENTID;CUSTOMERID;STATUS;ACHIEVEMENT_STARTDATETIME;ACHIEVEMENT_ENDDATETIME;ACHIEVEMENT_RESOURCES
ITV_5001;CLI_1001;3;18/11/2026 09:00;18/11/2026 10:05;TECH_001
```
{% endcode %}

{% hint style="info" %}
Une déclaration « Réalisé » (3) sur une intervention qui n'a jamais été planifiée est convertie en Imprévu (35) ; elle est refusée si aucune date de réalisation n'est fournie.
{% endhint %}

## 7. Suppression et désactivation

{% code title="Suppression d'une intervention" %}
```csv
APPOINTMENTID;CUSTOMERID;ACTION
ITV_5001;CLI_1001;DELETE
```
{% endcode %}

{% code title="Désactivation d'un client" %}
```csv
CUSTOMER$ID;ACTIVE
CLI_1001;0
```
{% endcode %}

## 8. Appel du service web setEntities (REST, JSON)

{% code title="Requête" %}
```http
POST /rest/entities/json/setEntities
Content-Type: application/json

{
  "commonInfo": { "version": "1", "key": "<clé API>", "language": "fr",
    "userLogin": "integration.demo", "userPassword": "<mot de passe>" },
  "dateFormat": "dd/MM/yyyy",
  "separatorInListOfValues": ",",
  "geocodingOptions": { "geocodingType": "AT_STREET_NUMBER", "minScore": 0.8, "defaultWorkSiteId": "" },
  "useSingleTransaction": false,
  "entities": [
    { "APPOINTMENTID": "ITV_5002", "CUSTOMERID": "CLI_1001", "TASKTYPES": "TT_DEPANNAGE",
      "DATEMINBEGIN": "19/11/2026", "DATEMAXEND": "20/11/2026", "STATUS": "21", "ACTION": "SCHEDULE" }
  ]
}
```
{% endcode %}

{% code title="Réponse (structure issue des exemples de l'aide en ligne)" %}
```json
{
  "sessionId": "<identifiant de session>",
  "result": { "success": true, "detail": "One or more entities successfully imported" },
  "nbSuccess": "1",
  "nbFailure": "0",
  "errors": []
}
```
{% endcode %}

## 9. Export par service web (GetEntitiesProperties)

{% code title="Export des interventions modifiées depuis hier (requête)" %}
```http
POST /rest/exportEntities/json/getEntitiesProperties
Content-Type: application/json

{
  "sessionId": "<identifiant de session>",
  "entityName": "Appointment",
  "fieldNames": "APPOINTMENTID,CUSTOMERID,STATUS,DATEAPPOINTMENT,ASSIGNEDRESOURCES",
  "dateFormat": "dd/MM/yyyy",
  "extractionKind": "LASTUPDATED",
  "extractionParam": "1"
}
```
{% endcode %}

## 10. Exemple d'erreur

{% code title="Authentification refusée (WRONG_LOGIN_PASSWORD)" %}
```json
{
  "sessionId": "",
  "result": { "success": false, "errorCode": 20, "detail": "<message>" }
}
```
{% endcode %}

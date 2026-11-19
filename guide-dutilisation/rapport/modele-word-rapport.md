---
description: Préparer le modèle Word d'un rapport d'intervention avec des champs de fusion.
---

# Préparer le modèle Word d'un rapport

Le modèle de rapport est un document Word. Vous y placez des champs de fusion qui sont remplacés par les données de l'intervention lors de la génération du PDF. Les champs utilisent la syntaxe des modèles Freemarker.

## Avant de commencer

Les noms des données disponibles suivent le modèle de données de Nomadia Field Service. Vous pouvez les consulter dans `Administration > Fichiers CSV > Modèle d'import/export CSV`.

## Ajouter un champ de fusion dans Word

1. Placez le curseur à l'endroit souhaité dans le document Word.
2. Appuyez sur **Ctrl + F9** pour insérer un champ.
3. Faites un clic droit sur le nouveau champ et sélectionnez **Modifier le champ…**.
4. Dans **Noms de champs**, sélectionnez **ChampFusion**.
5. Dans **Nom du champ**, saisissez la variable, par exemple `${APPOINTMENT.APPOINTMENTID}`.
6. Validez.

Exemples de variables :

| Variable                       | Donnée                        | Exemple de résultat                 |
| ------------------------------ | ----------------------------- | ----------------------------------- |
| `${APPOINTMENT.CUSTOMERID}`    | Identifiant du client         | CLI-0001                            |
| `${APPOINTMENT.APPOINTMENTID}` | Identifiant de l'intervention | Appointment\_0000001\_20260101-1000 |

## Parcourir les interventions du rapport

Un rapport peut contenir plusieurs interventions. Parcourez-les avec une liste :

```
[#list appointments as appt][#assign apptId=appt.APPOINTMENTID]
  ...
[/#list]
```

### Afficher le nom du client

```
${appt["CUSTOMERID.CUSTOMERNAME"]}
```

### Afficher l'intervenant qui a réalisé l'intervention

Les intervenants qui ont réalisé l'intervention sont dans la collection `ACHIEVEMENT_RESOURCES`. Les éléments sont séparés par un point-virgule :

```
[#list appt["ACHIEVEMENT_RESOURCES()"]?split(";") as achievResources]
${appt["ACHIEVEMENT_RESOURCES(${achievResources?index}).RESOURCEFIRSTNAME"]} ${appt["ACHIEVEMENT_RESOURCES(${achievResources?index}).RESOURCELASTNAME"]}
[/#list]
```

## Afficher une liste dans un tableau

Pour répéter une ligne de tableau Word, placez dans la première cellule de la ligne les balises `@before-row` et `@after-row`. Elles ouvrent et ferment la liste sur la ligne, ce qui évite les balises non fermées.

Exemple : liste des produits de l'intervention (détails de type `productOrder`) :

```
@before-row[#list appt["APPOINTMENTDETAILS()"]?split(";") as apptDetails]
[#if appt["APPOINTMENTDETAILS(${apptDetails?index}).KIND"] == "productOrder"]
${appt["APPOINTMENTDETAILS(${apptDetails?index}).PRODUCTID"]}
@after-row[/#if][/#list]
```

Les autres colonnes de la ligne contiennent les champs à afficher, par exemple la description et la quantité du produit.

## Reprendre les réponses d'un formulaire

Les réponses aux formulaires du module **Rapport** sont enregistrées au format JSON. Vous les récupérez par l'identifiant de l'intervention, puis par le titre du formulaire :

```
[#if jsonSurveyResults[apptId]??]
  [#assign json=jsonSurveyResults[apptId]]
  [#if json["Titre du formulaire"]??]
    ${json["Titre du formulaire"].question1!}
  [/#if]
[/#if]
```

* Remplacez `Titre du formulaire` par le titre du formulaire dans Nomadia Field Service.
* Remplacez `question1` par le nom de la question dans le formulaire.

### Question à choix multiples

Pour une question à cases à cocher, la réponse est une liste de valeurs. Parcourez-la et affichez le libellé de chaque valeur :

```
[#assign reponses = json["Titre du formulaire"].question3]
[#list reponses as reponse]
[#if reponse=='Item 1']Libellé 1[#elseif reponse=='Item 2']Libellé 2[/#if]
[/#list]
```

### Question Oui / Non

```
[#if json["Titre du formulaire"].question2]Oui[#else]Non[/#if]
```

## Insérer des photos et des signatures

Deux ensembles d'images sont disponibles pour une intervention :

| Ensemble       | Contenu                                                                               |
| -------------- | ------------------------------------------------------------------------------------- |
| `mmPhotos`     | Photos du dossier **Images** de l'intervention                                        |
| `mmRootPhotos` | Images à la racine du dossier de l'intervention, par exemple les signatures manuelles |

Exemple de condition pour afficher les photos uniquement si l'intervention en contient :

```
[#if mmPhotos[apptId]?size gt 0]
  [@printAppointmentPhotos appt 90 /]
[/#if]
```

La macro `printAppointmentPhotos` doit être déclarée dans le modèle. Dans le document Word, l'image qui sert d'emplacement aux photos doit porter le signet `photo`.

Pour les signatures manuelles, le modèle déclare une macro pour la signature du technicien et une macro pour la signature du client. Les images d'emplacement portent respectivement les signets `workerSignature` et `clientSignature`.

### Afficher le nom du signataire

```
[#macro printClientSignataire signRows][@initSize id="signRows" bookmark="clientSignature"/]
[#list signRows as row][#if row.isClientSignature]
${row.clientSignatory}
[/#if][/#list]
[/#macro]

[@printClientSignataire mmRootPhotos[apptId]/]
```

{% hint style="info" %}
La récupération des signatures manuelles nécessite une version de l'application postérieure à 2025.2.14. L'affichage du nom du signataire nécessite la version 1.8.0 de l'application mobile.
{% endhint %}

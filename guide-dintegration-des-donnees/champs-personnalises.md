---
description: Champs libres des entités, typologies et libellés affichés.
---

# Champs personnalisés

La plupart des entités disposent de champs libres pour porter des données propres au client. Leur nombre dépend de l'entité ; pour le client, l'intervention et la ressource, on trouve notamment :

| Champs                           | Type           | Nombre (client) |
| -------------------------------- | -------------- | --------------- |
| FILLER1 … FILLER5                | Texte          | 5               |
| QUANTITY1 … QUANTITY5            | Nombre décimal | 5               |
| EXTRAFILLER1 … EXTRAFILLERn      | Texte          | 50              |
| EXTRAQUANTITY1 … EXTRAQUANTITY15 | Nombre décimal | 15              |
| EXTRALOGICAL1 … EXTRALOGICAL15   | Booléen        | 15              |
| EXTRADATE1 … EXTRADATE15         | Date           | 15              |
| EXTRADATETIME1 … EXTRADATETIME15 | Date-heure     | 15              |

Le nombre exact de champs de chaque entité figure dans la [référence du modèle d'échange](reference-modele/).

## Listes de valeurs codifiées (typologies)

Un champ texte peut être associé à une typologie (entité Typology) : liste de codes et de libellés. À l'import, une colonne FILLERn.CODE ou EXTRAFILLERn.CODE reçoit un code, converti en libellé ; à l'export, la conversion inverse est appliquée. Un code inconnu donne une valeur vide.

## Libellés affichés

Les libellés des champs personnalisés dans l'interface et dans les en-têtes d'export en libellés proviennent des fichiers de ressources de l'application, surchargeables par instance. Le nom technique du champ (FILLER1, EXTRAFILLER3…) reste celui à utiliser dans les échanges.

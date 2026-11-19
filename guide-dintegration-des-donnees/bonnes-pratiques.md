---
description: Bonnes pratiques de préparation, de chargement et de performances.
---

# Bonnes pratiques

## Préparation

* Définissez une convention d'identifiants externes stable (préfixe par entité : CLI\_, TECH\_, ITV\_…).
* Fournissez des coordonnées XGEO/YGEO quand elles sont connues : l'import est plus rapide et plus fiable.
* Utilisez UTF-8 pour l'import global ; pour l'import unitaire, choisissez explicitement l'encodage dans le formulaire.
* Gardez la même configuration de format (séparateurs, dates) dans tous vos flux et documentez-la.

## Chargement

* Respectez l'ordre d'intégration (voir [Ordre d'intégration détaillé](annexes/ordre-integration-detaille.md)) ; contrôlez le compte rendu de chaque fichier.
* Testez chaque fichier sur un échantillon de quelques lignes avant le chargement complet.
* Pour les mises à jour, n'envoyez que les colonnes à modifier et utilisez le mode UPDATEONLY (…$ID) pour éviter les créations accidentelles.
* Désactivez (ACTIVE = 0) plutôt que de supprimer les référentiels utilisés par l'historique.

## Performances

* L'import par l'interface est synchrone et valide une transaction par ligne : découpez les très gros volumes en plusieurs fichiers et préférez la circulation pour les flux récurrents.
* Évitez le géocodage de masse à l'import : fournissez les coordonnées ou géocodez en amont.
* Pour les services web, réutilisez la session et regroupez les enregistrements (setEntities, SetEntitiesFromCsv) plutôt que d'appeler le service pour chaque objet.
* Limitez les exports aux champs et aux enregistrements utiles (FieldNames, LASTUPDATED).

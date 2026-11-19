---
description: Erreurs courantes, causes probables, résolutions et démarche de diagnostic.
---

# Diagnostic et résolution des problèmes

| Symptôme                                           | Cause probable                                                             | Résolution                                                                                          |
| -------------------------------------------------- | -------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| Le fichier n'est pas importé, aucune ligne traitée | En-tête non reconnu : un champ obligatoire manque ou est mal orthographié. | Comparer l'en-tête au modèle d'échange ; ajouter les champs obligatoires.                           |
| Une autre entité que prévu est importée            | Les colonnes correspondent aux champs obligatoires de plusieurs entités.   | Vérifier l'entité indiquée sur la ligne « Header » du compte rendu ; compléter l'en-tête.           |
| Une donnée n'est pas prise en compte, sans erreur  | Nom de colonne inconnu (colonne ignorée) ou champ réservé à l'export.      | Corriger le nom ; vérifier la colonne I/E de la [référence du modèle d'échange](reference-modele/). |
| Des valeurs ont été effacées                       | Colonnes présentes avec des cellules vides.                                | Retirer les colonnes à ne pas modifier.                                                             |
| « Object not found for field X with value Y »      | Référence vers un objet absent ou pas encore importé.                      | Importer l'entité référencée d'abord ; vérifier l'identifiant.                                      |
| « Invalid Location, cannot geocode »               | Adresse non géocodable avec la tolérance choisie.                          | Corriger l'adresse, fournir XGEO/YGEO, baisser la tolérance ou définir un site de repli.            |
| « can't convert provided date »                    | Format de date différent de celui de l'import.                             | Aligner le format (dd/MM/yyyy dans l'interface, yyyy/MM/dd côté serveur par défaut).                |
| Caractères accentués altérés                       | Encodage du fichier différent de celui choisi.                             | Choisir le bon encodage, ou convertir le fichier.                                                   |
| Statut d'intervention non modifié                  | Changement interdit ou converti par les règles de cycle de vie.            | Voir [Intégrer les interventions](integrer-donnees/interventions.md).                               |
| Ligne rejetée : trop de champs                     | Séparateur présent dans une valeur non délimitée.                          | Délimiter les valeurs (") ou changer de séparateur.                                                 |
| Service web : code 10                              | Session expirée ou inconnue.                                               | Se réauthentifier avec CommonInfo.                                                                  |
| Service web : code 20                              | Clé, identifiant ou mot de passe incorrect.                                | Vérifier la clé de l'instance et le compte d'intégration.                                           |
| Service web : code 11                              | Appel concurrent sur la même session.                                      | Séquencer les appels ou utiliser une session par fil d'exécution.                                   |

## Démarche de diagnostic

1. Consulter le compte rendu de l'import (fichier ErrResult\_…) ou la réponse du service web.
2. Consulter le journal d'application, filtré sur les types import\_error, service\_fail ou communication\_error.
3. Reproduire avec un fichier d'une seule ligne en recette.
4. Transmettre au support le fichier, le compte rendu, l'horodatage et l'utilisateur.

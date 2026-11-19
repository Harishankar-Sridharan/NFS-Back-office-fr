---
description: Droits nécessaires et écrans d'administration de la circulation.
---

# Prérequis et accès aux écrans

## Prérequis et droits utilisateur

| Élément                                                                                                           | Utilité                                                                                                      |
| ----------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| Licence Nomadia Field Service valide                                                                              | La circulation ne démarre pas sans licence valide.                                                           |
| Droit « Autorise la gestion des informations système »                                                            | Affiche le dossier **Fichiers XML** de l'administration.                                                     |
| Droit « Autorise l'accès à l'importation des fichiers XML de création, modification, suppression de rendez-vous » | Donne accès à **Fichier de circulation** et **Exemples de circulation**.                                     |
| Droit « Autorise la gestion du coffre-fort (identifiants et points d'accès référencés par la configuration) »     | Donne accès à **Coffre-fort**.                                                                               |
| Droit « Accès à l'import CSV » ou « Accès à l'exportation au format CSV »                                         | Donne accès, dans **Fichiers CSV**, à **Listeners de la circulation** et **Liens d'exportation prédéfinis**. |

## Écrans d'administration de la circulation

| Écran                              | Navigation                                                       | Usage                                                                |
| ---------------------------------- | ---------------------------------------------------------------- | -------------------------------------------------------------------- |
| **Fichier de circulation**         | `Administration > Fichiers XML > Fichier de circulation`         | Importer un nouveau fichier, consulter le rapport de chargement.     |
| **Exemples de circulation**        | `Administration > Fichiers XML > Exemples de circulation`        | Consulter les exemples de configuration fournis avec l'application.  |
| **Coffre-fort**                    | `Administration > Fichiers XML > Coffre-fort`                    | Gérer les identifiants et migrer la circulation vers le coffre-fort. |
| **Listeners de la circulation**    | `Administration > Fichiers CSV > Listeners de la circulation`    | Lister les URL HTTP écoutées par la circulation et les tester.       |
| **Liens d'exportation prédéfinis** | `Administration > Fichiers CSV > Liens d'exportation prédéfinis` | Lancer des exports prédéfinis par lien.                              |

Pour en savoir plus sur la gestion des droits, consultez [Gérer les profils et les droits](../guide-dutilisation/administration/utilisateurs-droits.md).

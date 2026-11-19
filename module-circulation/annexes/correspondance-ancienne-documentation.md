---
description: >-
  Correspondance entre les termes et objets de l'ancienne documentation de la
  circulation et la version actuelle.
---

# Correspondance avec l'ancienne documentation

Ce tableau facilite la transition depuis l'ancienne documentation de la circulation.

| Ancienne documentation                                    | Version actuelle                                                                                                                          |
| --------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Rendez-vous                                               | Intervention                                                                                                                              |
| Statut 6 « Déplanifié »                                   | Suspendu                                                                                                                                  |
| Statut 10 « Annulé »                                      | Abandonné                                                                                                                                 |
| Statut 40 « Historisé »                                   | Journalisé                                                                                                                                |
| `appointment-request-receiver`, `reference-data-receiver` | Supprimés. Imports : `exchange-records-csv-processor`, `exchange-records-xml-processor`, `csv-record-processor`, `sql-importer-processor` |
| Ancien processeur de services                             | `gss-services-processor`                                                                                                                  |
| `bulk-outside-listener`                                   | Déprécié : `outside-listener` + `exchange-records-csv-processor`                                                                          |
| Copie manuelle de `circulation_config.xml` après import   | Plus nécessaire : l'import remplace le fichier du serveur                                                                                 |
| Mots de passe en clair dans le fichier                    | Références `${vault:…}` vers le coffre-fort                                                                                               |

---
description: Ordre des entités importables, trié par niveau de dépendance.
---

# Ordre d'intégration détaillé

Ordre des entités importables trié par niveau de dépendance, tel que l'applique l'export global. À niveau égal, l'ordre est alphabétique. Les entités de types d'intervenant ou de types de poste n'apparaissent que selon l'option de modélisation de l'instance.

| #  | Entité                                           | Nom technique              | Niveau |
| -- | ------------------------------------------------ | -------------------------- | ------ |
| 1  | Ressource humaine (RESOURCEID, RESOURCELASTNAME) | HumanResource              | —      |
| 2  | Région                                           | Area                       | 000    |
| 3  | Configuration personnalisée                      | CustomConfiguration        | 000    |
| 4  | Zone restreinte                                  | RestrictedArea             | 000    |
| 5  | Abonnement au journal d'application              | ApplicationLogSubscription | 010    |
| 6  | Autorisation                                     | Authorization              | 010    |
| 7  | Localisation de l'établissement                  | BusinessLocation           | 010    |
| 8  | État de réalisation                              | CompletionType             | 010    |
| 9  | Nature de client                                 | CustomerKind               | 010    |
| 10 | Type de client                                   | CustomerType               | 010    |
| 11 | Dépôt                                            | DepotBusinessLocation      | 010    |
| 12 | Type de secteur d'astreinte                      | DutySectorType             | 010    |
| 13 | Type de périodicité                              | PeriodicityType            | 010    |
| 14 | Famille de produits                              | ProductFamily              | 010    |
| 15 | Jour férié                                       | PublicHoliday              | 010    |
| 16 | Compétence                                       | Qualification              | 010    |
| 17 | Collection de droits                             | RightCollection            | 010    |
| 18 | Contenu de la collection de droits               | RightCollectioncontent     | 010    |
| 19 | Type de secteur                                  | SectorType                 | 010    |
| 20 | Période de vente                                 | SellingPeriod              | 010    |
| 21 | Groupe d'intervention                            | TaskTypeGroup              | 010    |
| 22 | Suivi                                            | ToDoNextType               | 010    |
| 23 | Typologie                                        | Typology                   | 010    |
| 24 | Type du site de travail                          | WorkSiteType               | 010    |
| 25 | Type de journée de travail                       | WorkdayType                | 010    |
| 26 | Site de travail                                  | Worksite                   | 019    |
| 27 | Équipement de suivi                              | Equipment                  | 020    |
| 28 | Type de localisation exceptionnelle              | ExceptLocationType         | 020    |
| 29 | Groupe                                           | Group                      | 020    |
| 30 | Secteur                                          | Sector                     | 020    |
| 31 | Fournisseur                                      | Supplier                   | 020    |
| 32 | Ville                                            | City                       | 030    |
| 33 | Type d'astreinte                                 | DutyType                   | 030    |
| 34 | Type de semaine d'astreinte                      | DutyWeekType               | 030    |
| 35 | Produit                                          | Product                    | 030    |
| 36 | Fermeture de site de travail de secteur          | SectorWorkSiteClosing      | 030    |
| 37 | Matériel                                         | Supply                     | 030    |
| 38 | Équipe                                           | Team                       | 030    |
| 39 | Type d'indisponibilité                           | UnavailabilityType         | 030    |
| 40 | Véhicule                                         | Vehicle                    | 030    |
| 41 | Fermeture du site de travail                     | WorkSiteClosing            | 030    |
| 42 | Type de jour d'astreinte du site de travail      | WorksiteDutyDayType        | 030    |
| 43 | Type de semaine d'astreinte du site de travail   | WorksiteDutyWeekType       | 030    |
| 44 | Type de semaine de travail                       | WorkWeekType               | 040    |
| 45 | Type d'intervention                              | TaskType                   | 050    |
| 46 | Type d'intervenant (fonction)                    | ResourceFunction           | 060    |
| 47 | Type de poste                                    | ResourceJobType            | 060    |
| 48 | Type d'intervenant                               | ResourceType               | 060    |
| 49 | Priorité du type d'intervenant                   | ResourcetypePriority       | 060    |
| 50 | Détail de type d'intervention                    | TaskTypeDetail             | 060    |
| 51 | Secteur d'astreinte                              | DutySector                 | 062    |
| 52 | Priorité du type de l'intervenant                | FunctionPriority           | 062    |
| 53 | Priorité du type de poste                        | JobTypePriority            | 062    |
| 54 | Sous-traitant                                    | SubContractor              | 062    |
| 55 | Ressource humaine                                | HumanResource              | 065    |
| 56 | Journée verrouillée                              | AgendaControlledDate       | 070    |
| 57 | Équipage                                         | Crew                       | 070    |
| 58 | Astreinte                                        | Duty                       | 070    |
| 59 | Localisation exceptionnelle                      | ExceptLocation             | 070    |
| 60 | Hr-Vehicle-Equipment                             | HrVehicleEquipment         | 070    |
| 61 | Objectif                                         | Objective                  | 070    |
| 62 | Commanditaire                                    | Orderer                    | 070    |
| 63 | Secteur d'astreinte d'intervenant                | ResourceDutySector         | 070    |
| 64 | Profil de poste de l'intervenant                 | ResourceJobProfile         | 070    |
| 65 | Priorité de l'intervenant                        | ResourcePriority           | 070    |
| 66 | Compétences de l'intervenant                     | ResourceQualification      | 070    |
| 67 | Jour de travail de l'intervenant                 | ResourceWorkday            | 070    |
| 68 | Site de travail de l'intervenant                 | ResourceWorksite           | 070    |
| 69 | Affectation de matériel                          | SupplyResource             | 070    |
| 70 | Priorité de l'intervention                       | TaskPriorities             | 070    |
| 71 | Ensemble de modèles de tournées                  | ToursPlan                  | 070    |
| 72 | Indisponibilité                                  | Unavailability             | 070    |
| 73 | Périmètre utilisateur                            | UserPerimeter              | 070    |
| 74 | Préférence utilisateur                           | UserPreference             | 070    |
| 75 | Client                                           | Customer                   | 080    |
| 76 | Contact                                          | Contact                    | 090    |
| 77 | Projet                                           | Project                    | 090    |
| 78 | Client de modèle de tournées                     | TourPlanCustomer           | 090    |
| 79 | Rendez-vous                                      | Appointment                | 100    |
| 80 | Période de fermeture                             | ClosingPeriod              | 100    |
| 81 | Détails du projet                                | ProjectDetail              | 100    |
| 82 | Créneau de réalisation                           | AchievementSlot            | 110    |
| 83 | Jalon                                            | AgendaMarker               | 110    |
| 84 | Détail du rendez-vous                            | AppointmentDetail          | 110    |
| 85 | Colis                                            | Parcel                     | 115    |
| 86 | Période de fermeture d'activité                  | BusinessClosingPeriod      | 120    |
| 87 | Période de fermeture de dépôt                    | DepotClosingPeriod         | 125    |
| 88 | Remplacement d'astreinte                         | DutyReplacement            | 130    |
| 89 | Fermeture de secteur d'astreinte                 | DutySectorClosing          | 130    |
| 90 | Stock                                            | Stock                      | 140    |
| 91 | Mouvement de stock                               | StockMovement              | 140    |
| 92 | Apparence                                        | Appearance                 | 990    |
| 93 | Position de l'équipement de suivi                | EquipmentPosition          | 990    |

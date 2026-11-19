---
description: >-
  Référence complète des entités et champs du modèle d'échange de Nomadia Field
  Service.
---

# Référence du modèle d'échange

Cette annexe reprend le modèle d'échange complet et les descriptions de champs de l'application. Les séries de champs numérotés (par exemple FILLER1 … FILLER5) sont regroupées sur une ligne.

| Colonne          | Signification                                                                                          |
| ---------------- | ------------------------------------------------------------------------------------------------------ |
| Champ            | Nom technique à utiliser dans les fichiers et les services web ; synonymes acceptés entre parenthèses. |
| Type             | Type de donnée (voir le dictionnaire des types) ; « Réf. » : identifiant d'une autre entité.           |
| Obl.             | « Oui » si le champ est obligatoire.                                                                   |
| I/E              | I : import seulement ; E : export seulement ; I/E : les deux.                                          |
| Réf.             | Entité référencée.                                                                                     |
| Exemple / défaut | Exemple et valeur par défaut issus du modèle (quand ils existent).                                     |

{% hint style="info" %}
Les descriptions sont reprises du modèle d'échange de l'application. Certaines formulations historiques ont été conservées telles quelles ; seule la terminologie produit a été actualisée.
{% endhint %}

## Domaines

| Domaine                                                                                      | Entités                                                                                                                                                                                                                                                                                                                                                                |
| -------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Organisation](organisation.md)                                                              | Area, WorkSiteType, Worksite, SectorType, Sector, City, Team, DutySectorType, DutySector, WorksiteDutyDayType, WorksiteDutyWeekType, WorkSiteClosing, SectorWorkSiteClosing, DutySectorClosing, RestrictedArea                                                                                                                                                         |
| [Activité et compétences](activite-et-competences.md)                                        | TaskTypeGroup, TaskType, TaskTypeDetail, Qualification, Authorization, CompletionType, ToDoNextType, Objective, SellingPeriod, PeriodicityType                                                                                                                                                                                                                         |
| [Ressources](ressources.md)                                                                  | HumanResource, SubContractor, ResourceType, ResourceFunction, ResourcetypePriority, ResourcetypeGroupPriority, ResourceJobType, JobTypePriority, JobTypeGroupPriority, FunctionPriority, FunctionGroupPriority, ResourceQualification, TaskPriorities, ResourcePriority, ResourceWorksite, ResourceDutySector, ResourceJobProfile, Crew, UserPerimeter, UserPreference |
| [Calendriers, indisponibilités et astreintes](calendriers-indisponibilites-et-astreintes.md) | WorkdayType, WorkWeekType, ResourceWorkday, ResourceWorkWeek, PublicHoliday, UnavailabilityType, Unavailability, ExpressUnavailability, ExceptLocationType, ExceptLocation, AgendaControlledDate, DutyType, DutyWeekType, Duty, DutyWeek, DutyReplacement, BusinessLocation, DepotBusinessLocation, BusinessClosingPeriod, DepotClosingPeriod                          |
| [Clients](clients.md)                                                                        | Orderer, CustomerType, CustomerKind, Customer, Contact, CustomerWorkday, ClosingPeriod, Project, ProjectDetail, ToursPlan, TourPlanCustomer, VisitCustomer                                                                                                                                                                                                             |
| [Interventions](interventions.md)                                                            | Appointment, AppointmentCustomer, AppointmentDetail, AchievementSlot, Parcel, GroupedPickupDelivery, AgendaMarker                                                                                                                                                                                                                                                      |
| [Véhicules, équipements, matériel et stock](vehicules-equipements-materiel-et-stock.md)      | Vehicle, Equipment, EquipmentPosition, HrVehicleEquipment, Supply, SupplyResource, Product, ProductFamily, Stock, StockMovement, Supplier                                                                                                                                                                                                                              |
| [Sécurité et paramétrage](securite-et-parametrage.md)                                        | RightCollection, RightCollectioncontent, Group, ApplicationLogSubscription, CustomConfiguration, Appearance, Typology, Common                                                                                                                                                                                                                                          |
| [Exports uniquement](exports-uniquement.md)                                                  | AgendaEvent, ApplicationEvent, AgendaDaySummary, AgendaWeekSummary, Journal, ReportResult                                                                                                                                                                                                                                                                              |

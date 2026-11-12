# Smart Waste & Recycling

## Description détaillée du projet (version 6 microservices)

**Type de projet :** application de gestion intelligente des déchets, de collecte et de recyclage fondée sur une architecture microservices\
**Contexte :** projet académique -- module Architecture Web Distribuée (AWD)\
**Équipe :** 5 membres\
**Durée indicative :** 5 semaines\
**Organisation :** 6 microservices = 5 microservices individuels (un par membre) + 1 microservice avancé commun aux cinq membres\
**Contraintes :** outils gratuits et open source ; prototype démontrable sans capteurs physiques ni partenariat réel avec une municipalité ou un centre de recyclage.

------------------------------------------------------------------------

## 1. Présentation générale

Smart Waste & Recycling est une plateforme numérique qui facilite la gestion des déchets à l'échelle d'un quartier ou d'une ville. Elle permet au citoyen d'agir de trois façons :

1.  **Signaler** un problème : dépôt sauvage, poubelle débordante, déchets encombrants.
2.  **Participer** à la propreté de son quartier par une **collecte volontaire** de déchets (ramassage organisé par le citoyen, seul ou en groupe).
3.  **Faire collecter ou déposer des produits recyclables** : plastique, papier et carton, verre, métal, textiles, petits appareils électroniques.

La plateforme met en relation quatre catégories d'acteurs :

-   **Les citoyens**, qui signalent, déclarent des collectes volontaires ou demandent la collecte de produits recyclables.
-   **Les agents et administrateurs**, qui vérifient les demandes, gèrent les catégories et les règles de tri et suivent les opérations.
-   **Les collecteurs et équipes**, qui organisent les interventions et confirment les collectes.
-   **Les centres de collecte et de recyclage**, qui indiquent les types de déchets acceptés et les quantités réceptionnées.

Un service d'intelligence artificielle (vision par ordinateur) analyse les photos envoyées pour suggérer une catégorie de déchet ou une situation (dépôt sauvage, poubelle débordante). Cette classification aide à orienter la demande mais ne remplace pas la validation humaine.

L'objectif est de transformer un simple signalement ou une initiative citoyenne en action concrète : collecte, dépôt dans un point adapté ou orientation vers une filière de valorisation.

## 2. Problématique

Dans de nombreuses zones urbaines, les déchets sont déposés dans des endroits inappropriés, les poubelles débordent et les déchets recyclables sont mélangés aux déchets ordinaires. Le citoyen ne sait pas toujours à qui s'adresser, comment trier ni où déposer. Les citoyens motivés qui nettoient spontanément un espace n'ont aucun cadre pour déclarer leur action ni pour faire évacuer les déchets ramassés. Les équipes de collecte manquent d'informations structurées sur la nature, la localisation et la quantité des déchets.

Une application limitée au signalement transmet une information sans garantir qu'une action suivra. Smart Waste & Recycling couvre une partie plus large du processus :

1.  Identifier et catégoriser les déchets ou le problème.
2.  Informer le citoyen sur le tri et les consignes de séparation.
3.  Déterminer le mode de prise en charge adapté.
4.  Organiser une collecte, accueillir une collecte volontaire ou proposer un point de dépôt.
5.  Suivre l'opération jusqu'à sa confirmation.
6.  Enregistrer les quantités collectées et leur destination déclarée.

## 3. Objectifs du projet

### Objectif général

Développer une plateforme centralisée qui facilite le signalement des problèmes liés aux déchets, la participation citoyenne (collectes volontaires), la collecte de produits recyclables et l'orientation des déchets vers des points de collecte ou des centres adaptés.

### Objectifs spécifiques

-   Permettre aux citoyens de signaler un dépôt sauvage, une **poubelle débordante** ou des déchets encombrants.
-   Permettre aux citoyens de déclarer une **collecte volontaire** de déchets (lieu, date, photos avant et après, quantité estimée) et d'organiser l'évacuation des déchets ramassés.
-   Permettre aux citoyens de demander la **collecte de produits recyclables** ou de trouver un point de dépôt.
-   Collecter des informations utiles : photo, localisation, catégorie, quantité approximative, description.
-   Utiliser un modèle d'IA pré-entraîné pour analyser les images et suggérer une catégorie ou une situation.
-   Fournir au citoyen des consignes de tri et de séparation selon la catégorie.
-   Distinguer les demandes de nettoyage, de collecte volontaire et de collecte de produits recyclables.
-   Permettre aux collecteurs d'accepter, planifier et clôturer une opération.
-   Référencer des points de dépôt et des centres de recyclage selon les catégories acceptées.
-   Suivre les statuts des demandes, informer les citoyens et conserver l'historique de leurs activités.
-   Produire des statistiques simples sur les déchets déclarés et les quantités collectées.

## 4. Périmètre fonctionnel

La plateforme comporte trois parcours qui partagent les mêmes mécanismes de déclaration, de classification et de suivi.

### 4.1. Parcours A -- Signalement d'un problème (dont la poubelle débordante)

Exemples :

-   Poubelle publique débordante.
-   Dépôt sauvage de déchets dans la rue.
-   Accumulation de déchets sur un terrain ou un espace public.
-   Déchets encombrants abandonnés.

**Déroulement :**

1.  Le citoyen crée un signalement en choisissant le type : poubelle débordante, dépôt sauvage, accumulation, encombrants.
2.  Il ajoute une photo, une description et une localisation.
3.  Le service IA propose une catégorie ou une situation avec un niveau de confiance.
4.  Le signalement apparaît dans le tableau de bord de l'agent.
5.  L'agent vérifie, corrige si besoin, puis valide ou rejette.
6.  Une intervention est créée et affectée à un collecteur ou une équipe avec une date et un créneau.
7.  Le collecteur met à jour le statut de l'intervention.
8.  Le citoyen reçoit une notification à chaque étape jusqu'à la clôture.

### 4.2. Parcours B -- Collecte de produits recyclables

Catégories pouvant être prises en charge selon les capacités des centres référencés : plastique, papier et carton, verre, métal, vêtements et textiles, petits appareils électroniques (uniquement si un point de collecte approprié est référencé).

**Déroulement :**

1.  Le citoyen choisit « Demander une collecte de produits recyclables ».
2.  Il ajoute une photo, confirme le type de déchet, indique une quantité approximative et sa localisation.
3.  L'IA suggère une catégorie ; le citoyen peut la corriger. La plateforme affiche les consignes de tri de la catégorie.
4.  La plateforme consulte les centres enregistrés et leurs catégories acceptées.
5.  Le citoyen choisit une collecte à domicile ou à un point de rendez-vous, ou un point de dépôt.
6.  Pour une collecte, un collecteur accepte la demande et confirme un créneau.
7.  Après la collecte ou le dépôt, l'opération est marquée réalisée et la quantité réceptionnée est enregistrée.
8.  Le citoyen reçoit une confirmation ; la quantité alimente les statistiques.

### 4.3. Parcours C -- Collecte volontaire de déchets

Ce parcours permet à un citoyen de nettoyer lui-même un espace (rue, plage, parc, terrain) et de faire reconnaître et évacuer son action.

**Déroulement :**

1.  Le citoyen déclare une collecte volontaire : lieu, date prévue, description, nombre approximatif de participants.
2.  Il ajoute une photo **avant** l'action.
3.  Après l'action, il ajoute une photo **après** et indique la quantité ramassée par catégorie.
4.  Le service IA analyse les photos (catégories visibles et comparaison avant/après, à titre indicatif).
5.  Un agent vérifie les informations et valide ou rejette la déclaration.
6.  Le citoyen choisit comment évacuer les déchets ramassés : **ramassage des sacs** par un collecteur à un point convenu, ou **dépôt dans un centre** adapté pour les déchets recyclables triés.
7.  L'évacuation est confirmée (collecte réalisée ou réception par le centre).
8.  L'action apparaît dans l'historique des activités du citoyen et dans les statistiques.

**Important :** la plateforme ne vérifie pas par elle-même qu'une collecte volontaire a eu lieu : la validation repose sur les photos et sur l'agent. La plateforme n'attribue ni récompense ni point dans ce prototype.

**Important :** la plateforme organise la mise en relation et le suivi. Elle ne réalise pas elle-même le recyclage et ne garantit pas la transformation des déchets. Le devenir des déchets est renseigné par le collecteur ou le centre de réception.

## 5. Acteurs et rôles

| Acteur | Responsabilités |
|---|---|
| Citoyen | Créer un signalement (dont poubelle débordante), déclarer une collecte volontaire, demander une collecte de produits recyclables, consulter les consignes de tri et les centres, suivre ses demandes, consulter ses notifications et son historique d'activités. |
| Agent / administrateur | Vérifier et valider les demandes, gérer les catégories et les règles de tri, gérer les collecteurs et équipes, affecter les opérations, consulter le tableau de bord. |
| Collecteur | Consulter les opérations qui lui sont affectées, accepter ou refuser, confirmer un créneau, mettre à jour le statut, saisir la quantité collectée. |
| Responsable d'un centre | Gérer les informations du centre et les catégories acceptées, confirmer les quantités réceptionnées. |

Pour le prototype, un même compte de démonstration peut cumuler les rôles d'agent et de responsable de centre. Les rôles restent distincts dans la conception.

## 6. Fonctionnalités détaillées

### 6.1. Comptes et accès

-   Inscription et authentification, gestion des rôles (citoyen, agent, collecteur, responsable de centre).
-   Protection des fonctionnalités selon le rôle ; gestion du profil.
-   Authentification déléguée à Keycloak.

### 6.2. Signalements, collectes volontaires et demandes de collecte

-   Création d'un signalement, d'une déclaration de collecte volontaire ou d'une demande de collecte de produits recyclables.
-   Ajout de photos, description, localisation, quantité estimée.
-   Consultation de l'historique des demandes du citoyen.
-   Modification ou annulation tant que la demande n'est pas prise en charge.

### 6.3. Catégories, règles de tri et consignes

-   Référentiel de catégories (plastique, verre, papier et carton, métal, textile, électronique, encombrants, déchets ordinaires...).
-   Règles de tri par catégorie et consignes de séparation (par exemple vider, aplatir, séparer).
-   Informations de valorisation par catégorie, rédigées par l'équipe à partir de sources publiques citées.

### 6.4. Analyse intelligente des images

-   Classification d'une photo par un modèle pré-entraîné exécuté localement.
-   Retour d'une catégorie, d'une situation (dépôt sauvage, poubelle débordante, aucune) et d'un score de confiance.
-   Indication des déchets potentiellement recyclables.
-   Comparaison de photos avant et après pour une collecte volontaire, à titre indicatif.
-   Marquage « revue humaine recommandée » sous un seuil de confiance.
-   Conservation des résultats et mise à disposition des autres services.

Le résultat de l'IA est une **suggestion**. Une photo peut être ambiguë, mal éclairée ou contenir plusieurs types de déchets. La validation humaine reste nécessaire dans les cas incertains. Le score n'est pas une probabilité calibrée.

### 6.5. Gestion des collectes et interventions

-   Gestion des collecteurs et des équipes.
-   Affectation d'une opération, date et créneau, acceptation ou refus.
-   Mise à jour des statuts, date réelle, quantité collectée, clôture.

Cycle de statuts d'une opération : `UNASSIGNED → ASSIGNED → ACCEPTED → SCHEDULED → IN_PROGRESS → COMPLETED` ; autres : `REFUSED` (retour à `UNASSIGNED`), `CANCELLED`.

Types d'opération : `CLEANUP` (nettoyage), `RECYCLABLE_COLLECTION` (produits recyclables), `VOLUNTEER_PICKUP` (ramassage des déchets d'une collecte volontaire).

Cycle d'une demande côté citoyen : `SUBMITTED → UNDER_REVIEW → ACCEPTED → SCHEDULED → IN_PROGRESS → COMPLETED` ; autres : `REJECTED`, `CANCELLED`. Dépôt dans un centre : `SUBMITTED → ORIENTED_TO_CENTER → DROPPED_OFF → RECEIVED`.

### 6.6. Centres de recyclage et points de dépôt

Chaque centre possède : nom, adresse, localisation, catégories acceptées, contact, horaires, statut actif ou inactif. Le prototype contient quelques centres fictifs, clairement identifiés comme données de démonstration.

### 6.7. Notifications et historique d'activités

-   Notifications de changement de statut, d'affectation, de créneau, de clôture, de réception.
-   Historique des notifications.
-   Historique des activités : signalements, collectes volontaires, demandes de collecte, dépôts effectués.

L'envoi de SMS ou d'e-mails réels n'est pas obligatoire : les notifications peuvent être affichées dans l'application.

### 6.8. Tableau de bord et statistiques

Nombre de signalements (dont poubelles débordantes) ouverts et clôturés, de collectes volontaires déclarées et validées, de collectes de produits recyclables réalisées, répartition par catégorie, quantités estimées et réellement collectées ou réceptionnées. Les quantités collectées ne sont pas des quantités recyclées : ce sont des quantités déclarées ou réceptionnées.

## 7. Architecture microservices

L'application suit une architecture de **six microservices** : cinq microservices individuels, un par membre, et un microservice avancé réalisé collectivement. Le frontend et les composants d'infrastructure ne comptent pas parmi les six.

| N° | Microservice | Type | Responsable |
|---|---|---|---|
| 1 | Waste Reporting Service | Individuel | Membre 1 |
| 2 | Collection Management Service | Individuel | Membre 2 |
| 3 | Recycling Center Service | Individuel | Membre 3 |
| 4 | Waste Management Service | Individuel | Membre 4 |
| 5 | Notification & User Activity Service | Individuel | Membre 5 |
| 6 | AI Waste Intelligence Service | Collectif, technologie avancée | Les cinq membres |

### 7.1. Les microservices individuels

#### Microservice 1 -- Waste Reporting Service (Membre 1)

**Responsabilité :** gérer les déclarations des citoyens : signalements, collectes volontaires, demandes de collecte de produits recyclables.

Fonctionnalités principales :

-   Déclarer une poubelle débordante, un dépôt sauvage, une accumulation ou des encombrants.
-   Déclarer une collecte volontaire : lieu, date, photos avant et après, quantités ramassées par catégorie, mode d'évacuation.
-   Demander la collecte de produits recyclables ou orienter vers un centre.
-   Ajouter photo, description, localisation ; consulter l'état des demandes.
-   Conserver la catégorie suggérée et la catégorie confirmée ; gérer le cycle de vie jusqu'à la validation.

Données principales :

-   `Report` : id, citizenId, reportType (OVERFLOWING_BIN, ILLEGAL_DUMP, WASTE_ACCUMULATION, BULKY_WASTE), description, location, imageReference, category, status, createdAt.
-   `CollectionRequest` : id, citizenId, wasteCategory, estimatedQuantity, unit, mode (HOME_COLLECTION, DROP_OFF), targetCenterId, location, imageReference, status, createdAt.
-   `VolunteerCollection` : id, citizenId, location, plannedDate, participantsCount, beforeImageReference, afterImageReference, quantities (catégorie, quantité, unité), evacuationMode (PICKUP, DROP_OFF), targetCenterId, status, createdAt.

Base de données : base dédiée (PostgreSQL).

#### Microservice 2 -- Collection Management Service (Membre 2)

**Responsabilité :** organiser les opérations de collecte et d'intervention.

Fonctionnalités principales :

-   Gérer les collecteurs et les équipes.
-   Affecter les demandes validées aux collecteurs ou équipes.
-   Planifier dates et créneaux (un collecteur ne peut avoir deux opérations sur le même créneau).
-   Suivre les interventions, saisir la quantité collectée et confirmer la collecte.
-   Traiter les trois types d'opération : nettoyage, collecte de produits recyclables, ramassage après collecte volontaire.

Données principales :

-   `CollectionOperation` : id, requestId, requestType, operationType, citizenId, wasteCategory, estimatedQuantity, location, collectorId, teamId, plannedDate, plannedTimeSlot, actualDate, collectedQuantity, unit, status.
-   `Collector` : id, keycloakUserId, name, contact, availability, status.
-   `Team` : id, name, members, status.

Base de données : base dédiée (PostgreSQL).

#### Microservice 3 -- Recycling Center Service (Membre 3)

**Responsabilité :** référencer les centres et points de collecte, leurs catégories acceptées et les quantités réceptionnées.

Fonctionnalités principales :

-   Ajouter, modifier, désactiver un centre.
-   Définir les déchets acceptés par centre.
-   Rechercher un centre selon le type de déchet (et la proximité).
-   Enregistrer les livraisons attendues et les quantités réceptionnées ; conserver l'historique.

Données principales :

-   `RecyclingCenter` : id, name, address, latitude, longitude, contact, openingHours, active, managerId.
-   `AcceptedWasteCategory` : id, centerId, categoryCode.
-   `ExpectedDelivery` : id, centerId, requestId, citizenId, categoryCode, estimatedQuantity, unit, status.
-   `ReceivedWaste` : id, centerId, expectedDeliveryId, requestId, quantity, unit, receivedAt, validatedBy.

Base de données : base dédiée (PostgreSQL).

#### Microservice 4 -- Waste Management Service (Membre 4)

**Responsabilité :** gérer le référentiel des catégories de déchets, les règles de tri, les consignes de séparation et les informations de valorisation. Il décrit **comment trier** ; il n'analyse pas d'image (rôle du microservice 6).

Fonctionnalités principales :

-   Gérer les catégories : plastique, verre, papier et carton, métal, textile, électronique, encombrants, etc.
-   Gérer les règles de tri par catégorie.
-   Définir les consignes de séparation (préparation avant dépôt, ce qui est accepté ou refusé).
-   Gérer les informations de valorisation par catégorie.
-   Exposer le catalogue aux autres services et au frontend.

Données principales :

-   `WasteCategory` : id, code, name, recyclable, active.
-   `SortingRule` : id, categoryCode, ruleText, priority.
-   `SeparationGuideline` : id, categoryCode, title, instructions.
-   `ValorisationInfo` : id, categoryCode, valorisationType, description, sourceReference.

Les autres services ne conservent que le **code de catégorie** et ne copient pas ce référentiel.

Base de données : base dédiée (PostgreSQL).

#### Microservice 5 -- Notification & User Activity Service (Membre 5)

**Responsabilité :** informer les utilisateurs des événements importants et conserver l'historique de leurs activités.

Fonctionnalités principales :

-   Informer le citoyen des changements de statut.
-   Informer le collecteur des nouvelles affectations et le responsable de centre des livraisons attendues.
-   Gérer l'historique des notifications (lues, non lues).
-   Consulter l'historique des activités : signalements, collectes volontaires, demandes, dépôts.

Données principales :

-   `Notification` : id, eventId, recipientId, title, message, type, relatedRequestId, read, createdAt.
-   `UserActivity` : id, eventId, userId, activityType, relatedId, relatedType, summary, occurredAt.

Base de données : base dédiée (MongoDB : documents autonomes, écritures fréquentes, lecture par utilisateur).

### 7.2. Microservice 6 -- AI Waste Intelligence Service (collectif, technologie avancée)

**Responsabilité :** analyser les photos de déchets par vision par ordinateur et mettre les résultats à disposition des cinq autres microservices. Ce service doit avoir une vraie fonctionnalité avancée, et pas seulement relayer un appel vers un modèle externe.

Fonctionnalités :

-   Reconnaissance du type de déchet à partir de l'image.
-   Identification des déchets potentiellement recyclables.
-   Détection de situations : dépôt sauvage, poubelle débordante, aucune situation.
-   Retour d'une catégorie (code), d'une situation, d'un score de confiance et d'un indicateur « revue humaine recommandée » sous un seuil configurable.
-   Comparaison avant/après pour une collecte volontaire (indicatif, jamais décisif).
-   Conservation des analyses et mise à disposition par identifiant.
-   Script d'évaluation sur un petit jeu d'images de test préparé par l'équipe.

**Frontière avec le microservice 4 :** le microservice 6 répond « de quelle catégorie s'agit-il ? » en retournant un code de catégorie. Le microservice 4 répond « comment la trier ? » à partir de ce code. Aucune règle de tri n'est stockée dans le microservice 6.

Technologie : Python et FastAPI ; OpenCLIP ou un modèle de Hugging Face Transformers ; modèle pré-entraîné exécuté localement.

Données principales :

-   `ImageAnalysis` : id, requestId, requestType, imageReference, suggestedCategoryCode, situation, recyclable, confidenceScore, topK, needsHumanReview, modelName, analyzedAt.
-   `BeforeAfterComparison` : id, volunteerCollectionId, beforeAnalysisId, afterAnalysisId, indicator, analyzedAt.

Base de données : base dédiée (PostgreSQL).

**Limites :** le modèle doit être testé sur un petit ensemble d'images représentatives ; le score de similarité n'est pas une probabilité calibrée ; la comparaison avant/après est un indice qui aide l'agent, pas une preuve. Si le résultat est incertain, l'application demande une confirmation humaine.

**Organisation du travail collectif (indicative) :** préparation des images et tests ; intégration du modèle ; API et persistance ; module de comparaison avant/après ; intégration et tests avec les cinq autres services. Chaque membre garde la responsabilité de son microservice individuel ; la part de chacun dans le service collectif doit être consignée dans le dépôt (issues et commits) pour que les contributions restent vérifiables.

### 7.3. Composants d'infrastructure

-   **Frontend :** angular.
-   **API Gateway :** point d'entrée unique.
-   **Eureka Discovery Server :** découverte des services.
-   **Config Server :** configuration centralisée.
-   **Keycloak :** authentification et rôles.
-   **Docker :** conteneurisation ; **RabbitMQ** pour les échanges asynchrones.
-   **Bases de données :** une base indépendante par microservice.

Ces composants ne sont pas des microservices métier supplémentaires.

### 7.4. Communication entre les services

| De → vers | Mode | Échange | Si l'appelé est indisponible |
|---|---|---|---|
| MS1 → MS6 | Synchrone, OpenFeign | Analyse d'une photo : catégorie, situation, score | La demande est créée sans suggestion ; le citoyen choisit la catégorie |
| MS1 → MS4 | Synchrone, OpenFeign | Vérification du code de catégorie, consignes de tri | Liste de catégories mise en cache ; consignes non affichées |
| MS1 → MS2 | Synchrone, OpenFeign | Création d'une opération à la validation (nettoyage, collecte, ramassage volontaire) | Validation annulée, erreur 503, nouvel essai |
| MS1 → MS3 | Synchrone, OpenFeign | Livraison attendue pour un dépôt dans un centre | Orientation refusée ; la collecte reste possible |
| MS1, MS2, MS3, MS6 → MS5 | Asynchrone, RabbitMQ | Événements : demande créée, validée, opération planifiée, collecte réalisée, réception, analyse terminée | Messages conservés dans une file durable, traités au redémarrage |
| MS2, MS3 → MS1 | Asynchrone, RabbitMQ | Mise à jour du statut affiché au citoyen | File durable, rattrapage au redémarrage |
| Frontend → Gateway → MS3, MS4 | Synchrone, REST | Recherche de centres par catégorie ; catalogue et consignes | Message d'erreur sur la page concernée |

Les résultats d'analyse du microservice 6 sont consultables par identifiant par les autres services qui en ont besoin ; MS1 est le principal consommateur.

**Règle d'architecture :** chaque microservice possède sa propre base de données. Aucun service n'accède directement aux tables d'un autre service. Les échanges se font par API ou par messages, avec des références par identifiant. L'asynchrone avec RabbitMQ peut être remplacé par des appels OpenFeign si l'équipe manque de temps.

## 8. Scénarios de démonstration

### Scénario 1 -- Collecte de produits recyclables (plastique)

1.  Un citoyen se connecte, crée une demande de collecte et ajoute une photo de bouteilles en plastique.
2.  Le microservice 6 suggère « Plastique » ; le citoyen confirme et indique 3 kg. Les consignes de tri du microservice 4 s'affichent.
3.  Le citoyen choisit la collecte ; un agent valide ; un collecteur est affecté et un créneau est fixé.
4.  Le collecteur confirme la récupération de 2,8 kg ; le citoyen est notifié ; le tableau de bord est mis à jour.

### Scénario 2 -- Signalement d'une poubelle débordante

1.  Un citoyen photographie une poubelle débordante et envoie le signalement avec sa localisation.
2.  L'IA suggère la situation « Poubelle débordante » ; un agent vérifie et valide.
3.  Une intervention de nettoyage est affectée à une équipe, réalisée et clôturée.
4.  Le citoyen reçoit les notifications et retrouve l'action dans son historique.

### Scénario 3 -- Signalement d'un dépôt sauvage

Même déroulement que le scénario 2, avec la catégorie « Dépôt sauvage ».

### Scénario 4 -- Collecte volontaire

1.  Un citoyen déclare une collecte volontaire dans un parc, avec une photo avant.
2.  Après l'action, il ajoute une photo après et indique les quantités ramassées par catégorie.
3.  Le microservice 6 analyse les photos et fournit un indicateur avant/après ; un agent valide la déclaration.
4.  Le citoyen demande le ramassage des sacs ; un collecteur effectue un ramassage (`VOLUNTEER_PICKUP`) et confirme la quantité.
5.  L'action apparaît dans l'historique des activités du citoyen.

### Scénario 5 -- Orientation vers un point de dépôt

1.  Un citoyen souhaite déposer du carton et choisit la catégorie « Papier et carton ».
2.  La plateforme affiche les centres qui acceptent cette catégorie ; le citoyen en choisit un.
3.  Après le dépôt, le responsable du centre confirme la quantité reçue.
4.  L'opération apparaît dans l'historique du citoyen et dans les statistiques.

## 9. Technologies proposées

| Composant | Technologie  |
|---|---|
| Frontend | Angular |
| Microservices 1 à 5 | Java, Spring Boot |
| Microservice 6 | Python, FastAPI |
| Modèle de vision | OpenCLIP ou Hugging Face Transformers |
| Bases de données | PostgreSQL (une base par service) ; MongoDB pour le microservice 5 |
| API Gateway | Spring Cloud Gateway |
| Découverte | Netflix Eureka |
| Configuration | Spring Cloud Config |
| Authentification | Keycloak |
| Conteneurisation | Docker et Docker Compose |
| Communication synchrone | REST / OpenFeign |
| Communication asynchrone | RabbitMQ |
| Gestion du code | Git et GitHub |

Le choix définitif des versions et bibliothèques est fait au démarrage du développement, en privilégiant des versions compatibles et maintenues.

## 10. Périmètre du prototype et limites

### Inclus dans le prototype

-   Comptes et rôles.
-   Signalements (dont poubelle débordante), collectes volontaires et demandes de collecte de produits recyclables.
-   Photos et localisations.
-   Catalogue de catégories, règles et consignes de tri.
-   Classification assistée par IA avec validation humaine.
-   Affectation, planification, confirmation d'une collecte ou d'une réception.
-   Référencement de centres et points de dépôt.
-   Notifications et historique d'activités.
-   Tableau de bord avec quelques indicateurs.

### Hors périmètre

-   Capteurs IoT ou poubelles intelligentes.
-   Intégration avec les systèmes d'une municipalité ou d'organismes publics.
-   Paiement en ligne, récompenses ou points pour les collectes volontaires.
-   Optimisation avancée des tournées.
-   Application mobile native.
-   Vérification automatique de la qualité réelle du recyclage ou de la réalité d'une collecte volontaire.
-   Reconnaissance parfaite de tous les déchets.
-   Géolocalisation en temps réel des collecteurs.

### Hypothèses de démonstration

-   Collecteurs, équipes et centres fictifs ; catégories acceptées configurées à la main.
-   Images de test issues d'un petit jeu public ou préparées par l'équipe.
-   Quantités saisies par le citoyen puis corrigées ou confirmées par le collecteur ou le centre.
-   Opérations simulées dans l'environnement de démonstration.

Il faut éviter de présenter des données fictives comme des données réelles.

## 11. Répartition du travail entre cinq membres

| Membre | Microservice individuel | Part dans le microservice 6 (indicative) |
|---|---|---|
| Membre 1 | Waste Reporting Service | Intégration avec les services consommateurs |
| Membre 2 | Collection Management Service | Module de comparaison avant/après |
| Membre 3 | Recycling Center Service | API et persistance |
| Membre 4 | Waste Management Service | Intégration du modèle et des prompts de classification |
| Membre 5 | Notification & User Activity Service | Préparation des images, jeu de test et script d'évaluation |

Travail commun : contrats API et modèles d'échange, dépôt Git et conventions, infrastructure, frontend et tableau de bord, tests d'intégration, documentation, démonstration et présentation.

## 12. Résumé du projet

**Smart Waste & Recycling** est une plateforme web intelligente qui permet aux citoyens de signaler les poubelles débordantes et les dépôts sauvages, de déclarer des collectes volontaires de déchets et de demander la collecte de produits recyclables ou de les déposer dans un centre adapté. Un service d'analyse d'images par IA suggère une catégorie ou une situation ; un service dédié fournit les règles et consignes de tri. Les agents valident, les collecteurs réalisent les opérations, les centres confirment les quantités reçues. Le système assure le suivi, les notifications, l'historique d'activités et des statistiques, au sein d'une architecture de six microservices indépendants : cinq individuels et un microservice d'intelligence artificielle réalisé collectivement.

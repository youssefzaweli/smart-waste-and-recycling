# smart-waste-and-recycling
# ♻️ Smart Waste & Recycling

Intelligent waste management, collection and recycling platform built on a **microservices architecture**.

> Academic project: Distributed Web Architecture (AWD) module, team of 5, about 5 weeks.

---

## 📖 About the project

Smart Waste & Recycling is a web platform that helps manage waste at the scale of a neighborhood or a city. It lets citizens:

1. **Report** a problem: overflowing bin, illegal dump, waste accumulation, bulky waste.
2. **Take part** in keeping their area clean through a **volunteer collection** (alone or in a group).
3. **Request the collection or drop-off of recyclables**: plastic, paper and cardboard, glass, metal, textiles, small electronics.

An **AI service** (computer vision) analyzes uploaded photos and suggests a waste category or a situation. The suggestion only guides the request and **never replaces human validation**.

### Actors

| Actor | Responsibilities |
|---|---|
| **Citizen** | Create reports, declare volunteer collections, request recyclable collection, follow requests, view notifications and activity history |
| **Agent / Administrator** | Validate requests, manage categories and sorting rules, manage collectors and teams, assign operations, view the dashboard |
| **Collector** | View assigned operations, accept or refuse, confirm time slots, update status, enter collected quantity |
| **Recycling center manager** | Manage center info and accepted categories, confirm received quantities |

---

## 🧩 Architecture

The application is made of **6 microservices** (5 individual + 1 collective), plus a frontend and infrastructure components that are **not** counted among the six.

| # | Microservice | Type | Owner | Stack | Database |
|---|---|---|---|---|---|
| 1 | **Waste Reporting Service** | Individual | Member 1 | Java, Spring Boot | PostgreSQL |
| 2 | **Collection Management Service** | Individual | Member 2 | Java, Spring Boot | PostgreSQL |
| 3 | **Recycling Center Service** | Individual | Member 3 | Java, Spring Boot | PostgreSQL |
| 4 | **Waste Management Service** | Individual | Member 4 | Java, Spring Boot | PostgreSQL |
| 5 | **Notification & User Activity Service** | Individual | Member 5 | Java, Spring Boot | MongoDB |
| 6 | **AI Waste Intelligence Service** | Collective | All 5 members | Python, FastAPI, OpenCLIP / Hugging Face | PostgreSQL |

### Responsibilities

- **MS1 Waste Reporting**: reports, volunteer collections and recyclable collection requests; keeps suggested and confirmed categories.
- **MS2 Collection Management**: collectors, teams, assignment, planning (no double-booking on the same slot), operation tracking. Operation types: `CLEANUP`, `RECYCLABLE_COLLECTION`, `VOLUNTEER_PICKUP`.
- **MS3 Recycling Center**: centers, accepted categories, search by waste type, expected and received deliveries.
- **MS4 Waste Management**: waste categories, sorting rules, separation guidelines, valorisation info. It describes *how to sort*; it does **not** analyze images.
- **MS5 Notification & User Activity**: status-change notifications and citizen activity history.
- **MS6 AI Waste Intelligence**: waste type recognition, recyclable detection, situation detection (illegal dump, overflowing bin, none), confidence score with a "human review recommended" flag, and before/after comparison for volunteer collections.

### Infrastructure components (not business microservices)

| Component | Technology |
|---|---|
| Frontend | React |
| API Gateway | Spring Cloud Gateway |
| Service discovery | Netflix Eureka |
| Centralized configuration | Spring Cloud Config |
| Authentication and roles | Keycloak |
| Containerization | Docker, Docker Compose |
| Asynchronous messaging | RabbitMQ |

### Service communication

| From → To | Mode | Purpose |
|---|---|---|
| MS1 → MS6 | Sync (OpenFeign) | Photo analysis: category, situation, score |
| MS1 → MS4 | Sync (OpenFeign) | Category code check, sorting guidelines |
| MS1 → MS2 | Sync (OpenFeign) | Create an operation on validation |
| MS1 → MS3 | Sync (OpenFeign) | Expected delivery for a center drop-off |
| MS1, MS2, MS3, MS6 → MS5 | Async (RabbitMQ) | Events for notifications and activity history |
| MS2, MS3 → MS1 | Async (RabbitMQ) | Status updates shown to the citizen |
| Frontend → Gateway → MS3, MS4 | Sync (REST) | Center search, catalog and guidelines |

> **Architecture rule:** each microservice owns its own database. No service accesses another service's tables directly. Exchanges go through APIs or messages, using identifiers as references.

---

## 🛠️ Tech stack

| Component | Technology |
|---|---|
| Frontend | React |
| Microservices 1 to 5 | Java, Spring Boot |
| Microservice 6 | Python, FastAPI |
| Vision model | OpenCLIP or Hugging Face Transformers (pre-trained, run locally) |
| Databases | PostgreSQL (one per service), MongoDB (MS5) |
| API Gateway | Spring Cloud Gateway |
| Discovery | Netflix Eureka |
| Configuration | Spring Cloud Config |
| Authentication | Keycloak |
| Containers | Docker, Docker Compose |
| Sync communication | REST / OpenFeign |
| Async communication | RabbitMQ |
| Version control | Git, GitHub |

---

## 📁 Repository structure

```
smart-waste-and-recycling/
├── Backend/
│   ├── waste-reporting-service/          # MS1 (Spring Boot)
│   ├── collection-management-service/    # MS2 (Spring Boot)
│   ├── recycling-center-service/         # MS3 (Spring Boot)
│   ├── waste-management-service/          # MS4 (Spring Boot)
│   ├── notification-activity-service/    # MS5 (Spring Boot + MongoDB)
│   └── ai-waste-intelligence-service/    # MS6 (Python / FastAPI)
├── Frontend/                             # React web app
├── Documentation/
│   ├── Presentation/                     # Slides / report
│   └── Diagrams/                         # Architecture, use case, sequence, class diagrams
└── README.md
```

---

## 🚀 Getting started

### Prerequisites

- Git
- Docker and Docker Compose
- Java 17+ and Maven (for MS1 to MS5)
- Python 3.10+ (for MS6)
- Node.js 18+ and npm (for the frontend)

### 1. Clone the repository

```bash
git clone https://github.com/youssefzaweli/smart-waste-and-recycling.git
cd smart-waste-and-recycling
```

### 2. Start the infrastructure

```bash
docker compose up -d
```

This starts the databases, RabbitMQ and Keycloak.

### 3. Start the services (recommended order)

1. Config Server
2. Eureka Discovery Server
3. API Gateway
4. Microservices MS1 to MS6

```bash
# Spring Boot services (example for MS1)
cd Backend/waste-reporting-service
./mvnw spring-boot:run

# AI service (MS6)
cd Backend/ai-waste-intelligence-service
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
uvicorn app.main:app --reload
```

### 4. Start the frontend

```bash
cd Frontend
npm install
npm start
```

> Ports, environment variables and credentials are documented in each service's own README. **Never commit secrets** (passwords, API keys); use `.env` files, which are git-ignored.

---

## 🎬 Demo scenarios

1. **Recyclable collection (plastic):** the citizen creates a request with a photo, MS6 suggests "Plastic", the citizen confirms and enters 3 kg, sorting guidelines from MS4 are shown, an agent validates, a collector is assigned and confirms 2.8 kg, the citizen is notified and the dashboard is updated.
2. **Overflowing bin report:** photo and location are sent, the AI suggests the situation, an agent validates, a cleanup operation is assigned, completed and closed, and the citizen receives notifications.
3. **Illegal dump report:** same flow as scenario 2 with the "Illegal dump" category.
4. **Volunteer collection:** the citizen declares a cleanup with a "before" photo, then adds an "after" photo and quantities. MS6 provides a before/after indicator, an agent validates, a collector performs a `VOLUNTEER_PICKUP`, and the action appears in the citizen's history.
5. **Drop-off at a center:** the citizen picks "Paper and cardboard", chooses a center that accepts it, and the center manager confirms the received quantity.

---

## 🎯 Prototype scope and limits

**Included:** accounts and roles, reports, volunteer collections, recyclable collection requests, photos and locations, category catalog and sorting rules, AI-assisted classification with human validation, assignment/planning/confirmation, recycling center directory, notifications and activity history, dashboard with a few indicators.

**Out of scope:** IoT sensors / smart bins, integration with municipal systems, online payment, rewards or points, advanced route optimization, native mobile app, automatic verification of recycling quality or of a volunteer collection's reality, perfect waste recognition, real-time collector geolocation.

**Demo assumptions:** collectors, teams and centers are fictional demo data; test images come from a small public dataset or are prepared by the team; quantities are entered by the citizen and then corrected or confirmed by the collector or center; operations are simulated.

> Collected quantities are **declared or received quantities**, not verified recycled quantities. The AI score is a similarity score, **not a calibrated probability**.

---

## 👥 Team

| Member | GitHub | Individual microservice | Share in MS6 (indicative) |
|---|---|---|---|
| Member 1: *Full name* | [@username](https://github.com/username) | Waste Reporting Service | Integration with consumer services |
| Member 2: *Full name* | [@username](https://github.com/username) | Collection Management Service | Before/after comparison module |
| Member 3: *Full name* | [@username](https://github.com/username) | Recycling Center Service | API and persistence |
| Member 4: *Full name* | [@username](https://github.com/username) | Waste Management Service | Model integration and classification prompts |
| Member 5: *Full name* | [@username](https://github.com/username) | Notification & User Activity Service | Image preparation, test set, evaluation script |

**Shared work:** API contracts and data models, Git repository and conventions, infrastructure, frontend and dashboard, integration tests, documentation, demo and presentation.

---

## 🔀 Git conventions

- **Branches:** one per feature, never push directly to `main`.
  - `feature/ms1-report-api`, `feature/ms6-before-after`, `fix/ms3-center-search`
- **Commits:** `type(scope): message`
  - `feat(ms1): add report creation endpoint`
  - `fix(ms2): prevent double booking on same time slot`
  - `docs: update architecture diagram`
  - Types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`
- **Issues:** every task gets a GitHub Issue assigned to a member. This is especially important for MS6, so each contribution to the collective service stays verifiable.
- **Pull requests:** merge into `main` through a PR with at least one reviewer.

---

## 🗓️ Roadmap (5 weeks)

| Week | Work |
|---|---|
| 1 | Validate subject, actors, user journeys, services, data and interactions; diagrams; Git repository |
| 2 | Create the six projects, their databases, main APIs and priority infrastructure |
| 3 | Report, collection request, volunteer collection and assignment flows; category catalog; AI API |
| 4 | Model integration, notifications and history, frontend interfaces |
| 5 | End-to-end tests, fixes, documentation, demo |

> Priority: deliver one complete working journey (reporting / recyclable collection) end to end before the others.

---

## ✅ Success criteria

- Report an overflowing bin and track it
- Declare a volunteer collection with before/after photos and its evacuation
- Request a recyclable collection
- AI photo analysis by MS6 and correction of its result
- Display sorting guidelines for a category
- Assign an operation with a time slot
- Find a center that accepts a category
- Confirm a collection or a reception
- Notifications and activity history
- Consistent statistics
- Independent startup of the six microservices and their communication
- Database autonomy respected

---

## 📄 License

Academic project, no license defined.

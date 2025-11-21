# AIDAP – Architectural Design Iteration (Iteration 1)

## Step 1 — Design Purpose & Drivers

### **Design Purpose**

This is a **greenfield system** built within a mature university domain.  
Its purpose is to allow users to **easily access campus information** through an **AI-powered chat interface** that integrates with existing university systems.

### **Primary Functional Requirements**

The core use cases supported in this iteration are:

- **UC-1:** Supports the main business goal
- **UC-5:** Supports business goal with a central authentication service
- **UC-6:** Supports external integrations

### **Quality Attribute Scenarios**

Chosen QAs for this iteration: **QA-1, QA-2, QA-4**

| Scenario | Importance to Customer | Difficulty |
| -------- | ---------------------- | ---------- |
| QA-1     | High                   | Medium     |
| QA-2     | Low                    | High       |
| QA-3     | High                   | Medium     |
| QA-4     | Medium                 | High       |
| QA-5     | High                   | Low        |

### **Constraints**

- All Phase 1 constraints included except **CON-2**

### **Concerns**

- All Phase 1 concerns included as drivers

---

## Step 2 — Architectural Drivers for This Iteration

This being the **first iteration** of a greenfield system, the goal is to establish a **cohesive system structure**, addressing architectural concern **CRN-4**.

### **Key Drivers**

- **QA-1:** Performance
- **QA-2:** Modifiability
- **QA-3:** Availability
- **CON-1:** All entry points must go through university SSO
- **CON-3:** Integration layer/API gateway required for external systems
- **CRN-1:** Multi-channel interface layer needed for voice + text interactions

---

## Step 3 — Refinement Scope

Since this is a **greenfield architecture**, the entire AIDAP system must be refined and structured from the ground up.

---

## Step 4 — Design Decisions (Iteration 1)

### **Decision 1: Use RIA (Rich Internet Application) for Client Layer**

**Rationale:**

- Supports browser-based access on any internet-connected device
- Allows rich UI, real-time interactions, dashboard rendering (UC-1)
- Enables client-side business logic for voice/text inputs
- Aligns with performance needs and dynamic conversational UX

---

### **Decision 2: Use Service Application Reference Architecture for Server Layer**

**Rationale:**

- No UI required on the backend side
- Backend exposes services to external systems and front-end
- Supports loose coupling and integration-heavy requirements (CRN-4)

---

### **Decision 3: Use a 3-Tier Distributed Deployment Pattern**

**Rationale:**

- Fits existing institutional infrastructure
- Clean separation of database, application logic, and presentation
- Supports communication with multiple external services (CON-3)
- Database tier isolates institutional data (RD-1, UC-6)

---

### **Decision 4: Use Spring Framework for Component Connections**

**Rationale:**

- Provides dependency injection, modular design, easy wiring
- Supports extensibility for integration modules, NLP, security handlers
- Aligns with CRN-4 and modular architecture goals

---

## Discarded Alternatives

| Alternative                          | Reason for Discarding                                                                                          |
| ------------------------------------ | -------------------------------------------------------------------------------------------------------------- |
| **RCA (Rich Client Application)**    | Requires installation, difficult to deploy/update across thousands of users; not lightweight or browser-based. |
| **Web Application for Server Layer** | Designed for frontend/UI rendering rather than backend logic and integration APIs.                             |
| **4-Tier Deployment Pattern**        | Adds complexity without meaningful benefits for Iteration 1.                                                   |
| **Java Server Faces (JSF)**          | UI-focused framework, unnecessary since UI is handled by RIA; adds unnecessary overhead.                       |

---

## Step 5 — Additional Design Decisions

### **Integration Services Module (Service Layer)**

Handles:

- External API calls
- Data transformation
- Error handling

**Rationale:**  
Supports integration concerns (CRN-4), ensures data consistency (R3, RD1–RD4).

---

### **Conversation/Query Module (Business Layer)**

Handles:

- Routing queries
- Optimizing responses
- Executing dashboard read/search operations

**Rationale:**  
Directly supports conversational data access (R1, R5, R6).

---

## Step 6 — Logical View: Responsibilities of Each Element

| Element                    | Responsibility                                                    |
| -------------------------- | ----------------------------------------------------------------- |
| **Rich Web UI**            | Renders dashboards, chatbox, notifications. Handles user actions. |
| **Dashboard Processing**   | Client-side analytics using cached data.                          |
| **Client Session**         | Stores temporary user data (roles, preferences).                  |
| **Security**               | Protects session/auth tokens on client side.                      |
| **Isolated Storage**       | Holds cached non-sensitive data (offline UI states).              |
| **Client Communication**   | Handles HTTPS communication with server.                          |
| **Operational Management** | Logging, maintenance, performance tracking.                       |
| **Server Security**        | Authorization, encryption, threat protection.                     |
| **API Integration**        | Handles incoming requests and maps them internally.               |
| **Query Module**           | Optimizes/routs queries; performs reads/searches.                 |
| **Application Logic**      | Core workflows (sync, SSO, pushes, state handling).               |
| **Auth Manager**           | SSO authentication and identity flows.                            |
| **Data Access**            | CRUD operations on internal database.                             |
| **Service Agents**         | Connections to external university systems.                       |

---

## Deployment View

### **Components & Responsibilities**

| Element                | Responsibility                                               |
| ---------------------- | ------------------------------------------------------------ |
| **User/Client Server** | Browser-side execution, UI rendering, local caching.         |
| **Application Server** | Business logic, authentication, external system integration. |
| **Database**           | Stores all institutional and local system data.              |
| **External Systems**   | University systems accessed via REST APIs.                   |

### **Relationships**

- **Client ↔ Application Server:** Encrypted HTTPS
- **Application Server ↔ Database:** SQL queries + updates
- **Application Server ↔ External Systems:** REST APIs

---

## Step 7 — Coverage of Architectural Drivers

| Driver | Status               | Notes                                                     |
| ------ | -------------------- | --------------------------------------------------------- |
| UC-1   | Completely Addressed | Dashboard processing + Rich Web UI defined.               |
| UC-5   | Partially Addressed  | SSO supported via Auth Manager; details pending.          |
| UC-6   | Completely Addressed | External sync defined in Service Agents.                  |
| QA-1   | Partially Addressed  | Query/data flow not fully designed.                       |
| QA-2   | Partially Addressed  | Integration gateway defined; design incomplete.           |
| QA-4   | Partially Addressed  | Security defined; encryption config pending.              |
| CON-1  | Partially Addressed  | SSO integrated; endpoints unfinished.                     |
| CON-3  | Completely Addressed | REST API access via Service Agents.                       |
| CON-4  | Partially Addressed  | RBAC supported; data partitioning incomplete.             |
| CON-5  | Partially Addressed  | Availability via isolated storage; no load balancing yet. |
| CRN-1  | Partially Addressed  | Text supported; voice pipeline missing.                   |
| CRN-2  | Not Addressed        | No backup/failover strategy yet.                          |
| CRN-3  | Partially Addressed  | Monitoring exists; alerts not designed.                   |
| CRN-4  | Completely Addressed | Integration through Service Agents + App Logic.           |
| CRN-5  | Partially Addressed  | Personalization supported; model tuning pending.          |

---

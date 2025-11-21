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

Since this is the first iteration in the design of the greenfield system the goal of the iteration is to establish the structure of the overall system which aligns with the architectural concern CRN-4. 
	The drivers that have the most importance for the current iteration are as follows: 

### **Key Drivers**

- **QA-1:** Performance
- **QA-2:** Modifiability
- **QA-3:** Availability
- **CON-1:** Every entry point to AIDAP has to go through the university SSO.
- **CON-3:** An integration layer/API gateway needs to be used to connect external systems.
- **CRN-1:** A multi-channel interface layer must be used for voice and text/voice interactions.

  <img width="612" height="507" alt="image" src="https://github.com/user-attachments/assets/c0c139fd-ac36-4689-a645-4e5793f681f2" />
  <img width="208" height="117" alt="image" src="https://github.com/user-attachments/assets/681f21a9-6e54-4b5d-a3de-4d7795fc32e0" />

---

## Step 3 — Refinement Scope

Since this is a **greenfield architecture**, the entire AIDAP system must be refined and structured from the ground up.

---

## Step 4 — Design Decisions (Iteration 1)

| **Design Decisions and Location (layer/comp)**                                                                          | **Rationale (connect to drivers)**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ----------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Logically structure the client part of the system using the RIA (Rich Internet Application) reference architecture.** | The Rich Internet Application (RIA) reference architecture supports applications that run on a web browser and can be accessed from any internet-connected device (**RS-9**). RIAs also provide a rich and dynamic UI capable of delivering interactive conversational experiences and real-time updates, aligning with requirements for natural-language interaction and contextual responses (**R1, R6**). In addition, RIAs allow certain business logic to run on the client, including dashboard rendering (**UC-1**) and handling voice/text inputs (**R-4**). |
| **Logically structure the server part of the system using the Service Applications reference architecture.**            | The Service Application reference architecture best supports the backend because it has **no user interface** and is **not human-controlled**. Since the system is loosely coupled, the Service Application architecture fits best as it exposes services to external systems and front-ends (**CRN-4**).                                                                                                                                                                                                                                                            |
| **Physically structure the application using the three-tier deployment pattern.**                                       | The 3-Tier distributed deployment pattern supports an existing database server and web-browser access, fitting the system needs (**RS-9**). The business/application tier supports communication and integration between multiple external services (**CON-3**). The database tier allows shared institutional data to be stored separately from the application tier (**RD-1**, **UC-6**).                                                                                                                                                                          |
| **Use the Spring framework for component connection in the application layer.**                                         | Spring provides dependency injection and modular wiring, which simplifies the connection of backend services such as integration modules, NLP handlers, and security components. This supports a loosely coupled and easily extensible application layer aligned with integration and modularity goals (**CRN-4, RM-5**).                                                                                                                                                                                                                                            |

## Discarded Alternatives

| Alternative                          | Reason for Discarding                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **RCA (Rich Client Application)**    | The reference architecture Rich Client Application (RCA) is oriented on running on the clients machine internally and would require some sort of installation for every device the user wants to connect. Although RCA also adds deployment and update complexity for thousands of students and faculty, this option was discarded because AIDAP must remain lightweight, easily accessible, and universally available through a browser.                                                                                        |
| **Web Application for Server Layer** | The Web Application reference architecture was discarded because it’s designed for applications that interact directly with end-users through a graphical user interface. On the other hand, client apps use APIs and service calls to reach AIDAP's server rather than people. A Web Application architecture, which is centered on UI rendering and page delivery, does not satisfy the system's objectives since the backend must function as a service layer that exposes business logic and connectors to external systems. |
| **4-Tier Deployment Pattern**        | The 4-tier deployment model was discarded because it introduces additional layers that add unnecessary complexity for the initial iteration of AIDAP. AIDAP's functional needs can be fully met with a more straightforward 3-tier structure. At this point, adding a fourth tier does not yield significant architectural benefits                                                                                                                                                                                              |
| **Java Server Faces (JSF)**          | JSF is focused on building server-rendered user interfaces, but AIDAP’s client is implemented as a browser-based Rich Internet Application (RIA), not a server-rendered web UI. A UI framework like JSF is unnecessary and would add complexity without supporting any architectural driver (CRN-4, RS9).                                                                                                                                                                                                                        |

---

## Step 5 — Additional Design Decisions

| **Design Decisions and Location (layer/comp)**                                                                            | **Rationale (connect to drivers)**                                                                                                                                                                                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Create a dedicated module for Integration Services in the service layer for the Service Application.**                  | Each external system is accessed through its own integration module, which manages API calls, data transformation, and error handling. This ensures consistent data flow and supports the integration concern (**CRN-4**) as well as interoperability and data consistency (**R3, RD1–RD4**). |
| **Create a dedicated Conversation/Query module in the Business layer of the Service Application reference architecture.** | This module routes queries to the correct integration or data services to assemble and return the optimal answer. It directly supports conversational access to institutional data (**R1, R5, R6**).                                                                                          |

## Step 6 — Logical View: Responsibilities of Each Element

<img width="545" height="901" alt="image" src="https://github.com/user-attachments/assets/c815359d-308b-4f44-8996-53bc666d4f6c" />


| Element                    | Responsibility                                                    |
| -------------------------- | ----------------------------------------------------------------- |
| **Rich Web UI**            | Renders dashboards, chatbox and notifications screens. Handles user actions.  |
| **Dashboard Processing**   | Generates front-end analytics using cached data.                         |
| **Client Session**         | Stores temporary user session data like roles and preferences.                |
| **Security**               | Protects session tokens/data and client-side authentication.                      |
| **Isolated Storage**       | Holds cached and non sensitive client side data like offline dashboards and UI states.             |
| **Client Communication**   | Sends/receives HTTP requests from the server.                         |
| **Operational Management** | Handles maintenance,logging and tracks performance for Application Logic and API Integration (UC-4).                      |
| **Server Security**        | Provides authorization, encryption, input validation and threat protection.                     |
| **API Integration**        | Receives clients requests and maps them to appropriate internal operation.            |
| **Query Module**           | Routes and optimizes query for optimal responses. Also executes read/search operations for dashboards.                  |
| **Application Logic**      | Manages core business rules for AIDAP (sync workflows, SSO flows, push notifications). Ensures consistency between external systems and the database.              |
| **Auth Manager**           | Processes authentication and the Single Sign On (SSO).                            |
| **Data Access**            | Provides CRUD operations on the internal AIDAP database.                          |
| **Service Agents**         | Manages connections and data formatting to the external institutions systems.                    |

---

## Deployment View
<img width="776" height="354" alt="image" src="https://github.com/user-attachments/assets/a399ed31-b5e5-4db2-9fbe-ca463cd2e5e6" />

### **Components & Responsibilities**

| Element                | Responsibility                                                                                                                                                                      |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **User/Client Server** | Handles all user interaction through the browser. Performs lightweight client-side processing (dashboard rendering, UI updates) and stores temporary session/cache data locally.    |
| **Application Server** | Executes the core business logic of AIDAP. Manages authentication, processes client requests, queries the database, and communicates with external university systems through APIs. |
| **Database**           | Stores all internal institutional data including user profiles, system configuration, analytics data, and synchronized academic information.                                        |
| **External Systems**   | Connected university systems accessed via REST API to provide/synchronize academic data (courses, schedules, registration info).                                                    |

### **Relationships**

| Relationship Between                       | Description                                                                   |
| ------------------------------------------ | ----------------------------------------------------------------------------- |
| **Client ↔ Application Server:**           | All communication is done through HTTPS.                                      |
| **Application Server ↔ Database:**         | Application server performs SQL queries and updates on the Database.          |
| **Application Server ↔ External Systems:** | Application server communicates with the external systems through REST API’s. |

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

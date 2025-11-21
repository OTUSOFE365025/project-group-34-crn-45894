
AIDAP – Architectural Design Iteration (Iteration 2)

# Iteration 2 — Focus on Primary Functionalities

---

## Step 2: Selecting Architectural Drivers

In this iteration, the focus is on identifying architectural elements that support primary system functionality.  
We specifically address **CRN-2**, which states:

> **The system must have high availability and scalability, including failover strategies and backup/recovery mechanisms for worst-case scenarios.**

The following use cases apply:

- **UC-1**
- **UC-5**
- **UC-6**

---

## Step 3: Architectural Focus (Client-side vs Server-side)

Since this is the second iteration, the architecture zooms in on modules supporting selected use cases and the availability/scalability driver.

Focus: **Server-side**, with attention to:
- Responsibilities tied to **availability**
- Responsibilities tied to **modifiability**
- Service decomposition and refinement

---

# Step 4: Architectural Decisions

## A. Design Decisions and Rationale

| Design Decision / Location                         | Rationale (Connection to Drivers) |
|----------------------------------------------------|----------------------------------|
| **Service-Oriented Architecture (Server-side)**    | Supports modularity, failover, horizontal scaling → satisfies CRN-2. |
| **Single Sign-On (SSO) with Role-Based Access**    | Provides secure login for UC-5 and scales to multiple roles. |
| **Three-Tier Deployment Pattern**                  | Separation of concerns; application tier can be replicated for high availability; data tier supports backup/recovery. |
| **Stateless Business Logic Services**              | Essential for horizontal scaling, load balancing, and UC-1 performance. |
| **API Gateway with Retry/Recovery Mechanisms**     | Ensures synchronization with external systems (UC-6) and supports graceful degradation under partial failures. |

---

## B. Alternatives Considered

| Alternative                | Reason for Discarding |
|---------------------------|------------------------|
| **Monolithic Architecture** | Poor scalability; difficult to implement failover/backups required for CRN-2. |
| **Stateful Service Design** | State replication complicates failover; reduces scalability. |
| **Custom Authentication Mechanism** | SSO is more secure, interoperable, and scalable; custom auth increases maintenance cost. |

---

# Step 5: Extracted Components (Model Decomposition)

| Component / Layer                                | Responsibility / Rationale |
|--------------------------------------------------|----------------------------|
| **Dashboard Service (Business Layer)**           | Generates personalized dashboards for students, lecturers, and maintainers. |
| **Notification Service (Business Layer)**        | Handles creation, editing, and delivery of notifications; must be reliable under high load. |
| **Data Synchronization Service (Service Layer)** | Syncs AIDAP with external systems; incorporates retry/recovery logic for failover. |
| **System Maintenance Modules (Cross-Cutting)**   | Supports zero-downtime updates; manages secure backup and restoration. |
| **Authentication & Access Control (Cross-Cutting)** | Provides secure login and role-based authorizations. |

**Driver Alignment:**  
These components directly support **CRN-2** (availability + scalability) and the needs of **UC-1, UC-5, and UC-6**.

---

# Step 6: Sketch & Documentation (Diagram Placeholder)

Element
Responsibility
Dashboard Service 
Shows personalized dashboards to users and retrieves analytics data from persistence and integration services.
Notification service
Creation, editing and delivery of notifications reliably even under high loads
System Maintenance Model
Deploys updates with zero downtime. Performs secure backup and restoration of system state.
Data Synchronization Service
Synchronizes data between AIDAP and external systems and preforms backups and recovery
Availability Module
Replication, load balancing, monitoring, and stateless design applied across services to meet CRN‑2
Authentication and Access control 
Provides secure login and role‑based access. Integrates with SSO (Keycloak/OAuth2). Replicated for high availability.
<img width="1250" height="579" alt="image" src="https://github.com/user-attachments/assets/8db98ba1-8c80-4e07-9641-dc738fb4122a" />
<img width="902" height="639" alt="image" src="https://github.com/user-attachments/assets/51457488-831b-4d69-986a-cd41bb4f4245" />
<img width="665" height="700" alt="image" src="https://github.com/user-attachments/assets/4b00f333-c7eb-4a86-b41e-b2225144164b" />
<img width="1250" height="697" alt="image" src="https://github.com/user-attachments/assets/2884141d-cd91-45f7-88e6-d32a92be2de9" />



# Domain Objects Associated With the Use Case → Reference Architecture

---

## Sequence Diagram (Placeholder)
*Sequence diagram will be added here (e.g., via draw.io).*

---

## Component Responsibilities

| Element                        | Responsibility |
|-------------------------------|----------------|
| **Dashboard Service**         | Shows personalized dashboards to users and retrieves analytics data from persistence and integration services. |
| **Notification Service**      | Supports creation, editing, and reliable delivery of notifications even under high load. |
| **System Maintenance Module** | Deploys updates with zero downtime; performs secure backup and restoration of system state. |
| **Data Synchronization Service** | Synchronizes data between AIDAP and external systems; performs backups and recovery operations. |
| **Availability Module**       | Provides replication, load balancing, monitoring, and stateless patterns across services to meet CRN-2. |
| **Authentication & Access Control** | Secure login and role-based access; integrates with SSO (Keycloak/OAuth2); replicated for high availability. |

---

## Methods (To Be Refined)

| Method Name | Description |
|-------------|-------------|
| *TBD* | Methods will be refined in future iterations, tied to UC-1, UC-5, and UC-6. |

---

# Step 7: Kanban (Evaluation Table)

### **Iteration Status Overview**

| Item | Not Addressed | Partially Addressed | Completely Addressed | Notes |
|------|---------------|---------------------|-----------------------|-------|
| **UC-3** | ✅ | | | Not refined in Iteration 2. Course Material Service was identified earlier but deferred. Will be addressed in a later iteration. |
| **UC-2** | | ✅ | | Notifications instantiated but require further refinement for availability & scalability. |
| **UC-5** | | | ✅ | Authentication & Access Control defined with Keycloak/OAuth2; supports all user roles. |
| **UC-1** | | | ✅ | Dashboard Service instantiated with clear responsibilities; interfaces defined to client UI. |
| **UC-4** | | | | No progress in this iteration. |
| **UC-6** | | | ✅ | Data Synchronization Service instantiated. |
| **CRN-2** | | | ✅ | Availability tactics applied system-wide (replication, statelessness, failover, backup recovery). |


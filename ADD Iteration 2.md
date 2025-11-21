
AIDAP – Architectural Design Iteration (Iteration 1)

Iteration 2 - Focuses on Primary Functionalities 
Step 2: Selecting Architectural drivers
In this iteration we will be focusing on identifying elements to support primary functionality. In particular we will be addressing CRN-2 which states the system should have high availability and scalability including failover strategies and backup recovery for worst case outcomes  

We will be considering the following use case to address as well as our CRN-2.
UC-1
UC-5
UC-6

Step 3: Elements to Refine
Given this is the second iteration we will be zooming in on specific modules that support the chosen use cases and our concern. The focus in this section will be on the server-side as we go over responsibilities tied to availability and modifiability which will be refined through decomposition.

Step 4: Design Concept that Satify Drivers
Design Decisions and Location (layer/comp)
Rationale (connect to drivers)
Service-Oriented Architecture(Server-side)
Supports refinement of services and facilitates scalability and failover by isolating services, directly addressing CRN‑2
Use Single Sign‑On (SSO) for authentication and role‑based access
Provides secure login for UC‑5 system access. Must be highly available and scalable to handle multiple roles concurrently
Structuring the application using a three-tier deployment pattern
Separates concerns, the application layer can be replicated for availability while the data layer supports backup and recovery
Stateless service design for business logic modules
Provides horizontal scaling and load balancing which is essential for UC-1 
Introduce an API Gateway with Retry/Recovery Mechanisms
Ensures synchronization with external systems which correlates to UC‑6. Supports graceful degradation under partial failures

Alternative
Reason for discarding
Monolithic Architecture
Discarded due to poor scalability and difficulty in implementing failover/backup strategies required by CRN‑2
Stateful Service Design
Discarded since maintaining state across servers complicates failover and scalability; stateless design better supports CRN‑2.
Custom Authentication Mechanism
Discarded in favor of standardized SSO, which is secure, interoperable, and scalable across multiple roles

Step 5: Create model, extract objects
Design Decisions and Location (layer/comp)
Rationale (connect to drivers)
Dashboard service(Business Layer)
Generates and serves personalized dashboards for students, lecturers, and maintainers.
Notification service(Business Layer)
Manages creation, editing, and delivery of notifications. Ensures reliable delivery under high load.
Data synchronization(service layer)
Synchronizes data between AIDAP and external systems. Includes retry/recovery mechanisms.
System maintenance modules(cross-cutting)
Deploys updates with zero downtime. Performs secure backup and restoration of system state
Authentication and Access Control(Cross-cutting)
Provides secure login and role based authorizations for users

Focused on availability and scalability(CRN-2). Introduced system maintenance and data synchronization service for failover and backup. 

Step 6: Sketch (Diagram) & Record (Table)



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



step 7: Kanban in sheets

Not Addressed
Partially Addressed
Completely Addressed
Design Decisions Made During the Iteration
UC-3




Not refined in Iteration 2. The Course Material Service was identified earlier but deferred. Will be addressed in a later iteration.


UC-2


Notifications have been instantiated, but further refinement needed to determine availability tactics and scalability




UC-5
Authentication & Access Control Interfaces defined with Keycloak/OAuth2 and fully supports user-based acces




UC-1
Dashboard Service instantiated with clear responsibilities. Interfaces defined to client UI




UC-4






UC-6
Data synchronization service has been instantiated 




CRN-2
Cross-cutting availability tactics are applied across modules  ensures availability, scalability, failover and backup recovery  



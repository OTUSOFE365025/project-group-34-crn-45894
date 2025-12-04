# **Quality Attribute Selection**

| Quality Attribute  | Rationale  |
|---|---|
| QA - 1 Performance  | Critical to the AIDAP system because it must handle thousands of concurrent users inputting real-time queries and loading dashboards without delays.  |
| QA - 3 Availability |  AIDAP depends on external university systems and must remain continuously accessible for students, lecturers, and administrators throughout the day. |
| QA - 4 Security  |  The AIDAP system must protect sensitive academic data and ensure safe authentication through the university’s SSO while interacting with multiple external services. |

# **Elements Selected for Refinement**

In this iteration, the focus is on the three critical quality attributes: **Performance, Availability, and Security**.  
The following architectural elements were selected for refinement:

## Elements to Refine

- **Integration Connectors**  
  - Handle communication with external university systems (LMS, Registration, Calendar, Mail).  
  - Refined to improve **availability** through retry/fail‑over mechanisms and monitoring of connector health.  
  - Directly addresses sensitivity to external dependencies and network reliability.

- **Security Layer**  
  - Enforces authentication via institutional SSO and role‑based access control.  
  - Refined to strengthen **security** with encryption at rest/in transit and audit logging.  
  - Directly addresses risks of weak SSO integration and ensures compliance with institutional privacy policies.

- **Data Storage Layer**  
  - Stores historical interactions, personalization data, and cached responses.  
  - Refined to improve **performance** with caching strategies and indexing, while ensuring **security** through encryption.  
  - Supports availability by maintaining local dashboards even if external systems are temporarily unavailable.

# **Design Decisions and Rationale**

In this iteration, design concepts were selected to directly address the three critical quality attributes: **Performance, Availability, and Security**.

## Design Decisions and Rationale

### Performance
- **Decision**: Introduce caching, load balancing, and monitoring agents for latency.  
- **Rationale**: Ensures query response times remain within SLA (<2 seconds) under thousands of concurrent users.

### Availability
- **Decision**: Add redundant connectors, retry and recovery mechanisms, and fail‑over strategies.  
- **Rationale**: Keeps the system continuously accessible even when external university systems fail.

### Security
- **Decision**: Enforce role‑based access, encryption at rest and in transit, and immutable audit logs.  
- **Rationale**: Protects sensitive academic data, ensures compliance with institutional privacy policies, and strengthens authentication.


# **ATAM Risks, Non-Risks, Sensitivities and Trade-offs** 

## Sensitivities
- **S1**: Number of concurrent users may directly affect the query response time  
- **S2**: Dependency of external systems impacts uptime  
- **S3**: Network latency and reliability between the AIDAP and other university systems  

## Tradeoffs
- **T1**: Optimization for peak loads may increase infrastructure costs  
- **T2**: Scheduled maintenance will ensure stability but will affect availability during certain times  
- **T3**: Access control through authentication improves security but makes usability more complicated  

## Risks
- **R1**: Query latency under peak loads could degrade responsiveness of dashboard  
- **R2**: Single point of failure in integration connectors will reduce availability  
- **R3**: Weak integration with SSO could expose authentication vulnerabilities  

## Non-Risks
- **N1**: Horizontal scaling with load balancers is already supported  
- **N2**: Local dashboards remain accessible if external systems become unavailable  
- **N3**: Role-based access control ensures only authorized users can access sensitive data  






# ATAM Risk Assessment Table


| Quality Attribute (QA) | Sensitivity Points (S) | Tradeoff Points (T) | Risks (R) | Non-Risks (N) |
|------------------------|------------------------|----------------------|-----------|----------------|
| **QA 1**               | S1, S3                 | T1                   | R1        | N1, N2         |
| **QA 3**               | S2                     | T2                   | R2        | N2             |
| **QA 4**               | S2, S3                 | T3                   | R3        | N3             |





# ATAM Utility Tree 
<img width="745" height="645" alt="image" src="https://github.com/user-attachments/assets/7b03114c-5a02-46d0-8a42-65ea87f5c80d" />

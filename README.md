<div align="center">

# NSU IT Support Center

### Enterprise IT Service Management, Ticket Orchestration & Resolution Platform

![React](https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=black)
![Vite](https://img.shields.io/badge/Vite-6-646CFF?logo=vite&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-Runtime-339933?logo=node.js&logoColor=white)
![Express.js](https://img.shields.io/badge/Express.js-API%20Layer-000000?logo=express&logoColor=white)
![Supabase PostgreSQL](https://img.shields.io/badge/Supabase-PostgreSQL-3ECF8E?logo=supabase&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind%20CSS-UI%20Engineering-06B6D4?logo=tailwindcss&logoColor=white)
![JWT](https://img.shields.io/badge/Auth-JWT-000000?logo=jsonwebtokens&logoColor=white)
![Deployment](https://img.shields.io/badge/Status-Production%20Deployed-informational)

</div>

> A production-deployed, full-stack IT service management platform engineered for North South University to centralize student support, operational triage, administrative approvals, real-time ticket processing, and automated communication.

---

<details>
<summary><strong>Table of Contents</strong></summary>

- [Executive Overview](#executive-overview)
- [Problem](#problem)
- [Solution](#solution)
- [System Architecture](#system-architecture)
- [Role-Based Operational Model](#role-based-operational-model)
- [Core Capabilities](#core-capabilities)
- [Authentication & Authorization](#authentication--authorization)
- [Real-Time Event Architecture](#real-time-event-architecture)
- [Ticket Lifecycle](#ticket-lifecycle)
- [Helpdesk Agent Portal](#helpdesk-agent-portal)
- [Super Admin Command Center](#super-admin-command-center)
- [Canvas Provisioning Workflow](#canvas-provisioning-workflow)
- [Payment Operations](#payment-operations)
- [Auditability & Governance](#auditability--governance)
- [Automated Communication Pipeline](#automated-communication-pipeline)
- [Operational UX](#operational-ux)
- [Technology Stack](#technology-stack)
- [Engineering Architecture](#engineering-architecture)
- [Engineering Decisions](#engineering-decisions)
- [Engineering Challenges](#engineering-challenges)
- [Product Walkthrough](#product-walkthrough)
- [Email Communication Showcase](#email-communication-showcase)
- [Deployment](#deployment)
- [Engineering Ownership](#engineering-ownership)
- [Capabilities Demonstrated](#capabilities-demonstrated)
- [Project Impact](#project-impact)
- [Future Improvements](#future-improvements)
- [Repository Notice](#repository-notice)
- [Project Classification](#project-classification)
- [Technology Summary](#technology-summary)
- [Final Perspective](#final-perspective)

</details>

---

## Executive Overview

The **NSU IT Support Center** is a full-stack operational platform designed to transform fragmented student IT-support workflows into a centralized, role-aware, auditable service management environment.

The platform supports the complete lifecycle of a support request — from initial submission and diagnostic triage through administrative processing, approval, resolution, and automated student communication.

Rather than functioning as a conventional CRUD-based ticketing application, the system was engineered around **role separation, workflow orchestration, real-time event processing, operational telemetry, auditability, specialized service workflows, and production deployment requirements**.

The platform provides dedicated operational environments for:

- Students
- Helpdesk Agents
- Super Administrators

Supported service domains include:

- Canvas Access
- Email Services
- 2FA & Security
- Payment Issues
- Academic & Special Requests

The system was developed end-to-end, covering requirements analysis, system design, interface engineering, backend services, database integration, authentication, authorization, workflow implementation, real-time event handling, automated communication, validation, and deployment.

---

## Problem

Student IT support often involves significantly more than recording a request and changing its status.

Different categories of requests may require:

- Different information during submission
- Different diagnostic procedures
- Different administrative responsibilities
- Supporting-document verification
- Multi-stage approval
- Priority escalation
- Financial or academic processing
- Batch operations
- Formal resolution notes
- Student-facing communication
- Historical accountability

Without a structured operational platform, these processes can become fragmented across manual communication channels, spreadsheets, disconnected workflows, and repetitive administrative operations.

The core engineering challenge was therefore to create a system capable of representing the **complete operational lifecycle of a support request**, while maintaining role boundaries and providing administrators with the tools required to process specialized cases efficiently.

---

## Solution

The NSU IT Support Center was engineered as a centralized service-management platform with a layered operational model, separating submission, operational processing, and controller authorization while maintaining a unified ticket lifecycle.

```mermaid
flowchart TD
    A[Students] --> B[Student Support Desk<br/>Submission Gateway]
    B --> C[Helpdesk Agent<br/>Level 1 Operations]
    C -->|Approval / Escalation| D[Super Admin<br/>Command Center]
    D --> E[Resolution / Export<br/>Communication / Audit]
```

---

## System Architecture

At a high level, the platform follows a multi-tier architecture.

```mermaid
flowchart TD
    subgraph Users
        U1[Students]
        U2[Helpdesk Agents]
        U3[Super Admins]
    end

    subgraph Presentation["Presentation Layer — React 19 + React Router + Tailwind CSS (Vite)"]
        P1[Student Desk]
        P2[Agent Portal]
        P3[Admin Portal]
    end

    subgraph Application["Application Layer — Node.js + Express.js"]
        A1[Authentication]
        A2[Authorization]
        A3[Workflows]
        A4[Business Logic]
        A5[Validation]
        A6[Events]
        A7[Processing]
    end

    subgraph Data["Data Layer — Supabase PostgreSQL / Realtime"]
        D1[(Supabase PostgreSQL)]
        D2[Supabase Realtime]
    end

    subgraph Communication["Event & Communication Layer"]
        C1[Realtime Events]
        C2[Nodemailer]
        C3[Submission / Resolution / Decline Notifications]
    end

    Users --> Presentation
    Presentation --> Application
    Application --> Data
    Data --> Communication
```

> The architecture shown above intentionally remains at the system level. Private implementation details, credentials, internal endpoints, and proprietary infrastructure are not exposed.

---

## Role-Based Operational Model

The platform is structured around three distinct operational environments.

| Role | Primary Responsibility |
|------|------------------------|
| **Student** | Submit and receive updates for support requests |
| **Helpdesk Agent** | Diagnose, process, correct, and escalate requests |
| **Super Admin** | Authorize, resolve, decline, export, and oversee operations |

This separation establishes clear operational boundaries between request creation, first-level processing, and controller authorization.

---

## Core Capabilities

### Service Request Management

The Student Support Desk provides structured submission workflows for:

- Canvas Access
- Email Services
- 2FA Security
- Payment Issues
- Academic & Special Requests

Each service category can collect the information necessary for its corresponding operational workflow.

### Real-Time KPI Telemetry

Administrative environments expose operational indicators including:

- Daily ticket volume
- Monthly ticket trends
- Pending request volume
- Urgent SLA vectors
- Resolution rates

The objective is to provide staff with immediate operational awareness rather than requiring manual aggregation.

### Master-Detail Ticket Inspection

Administrative users can inspect complete ticket records through a responsive master-detail workspace, providing visibility into:

| Inspection Field | Description |
|---|---|
| Student context | Requesting student information |
| Ticket metadata | Identifiers and classification data |
| Issue category | Service domain of the request |
| Description | Submitted request details |
| Status | Current lifecycle state |
| Priority | Urgency classification |
| Processing history | Record of administrative actions |
| Audit information | Accountability trail |
| Resolution information | Final outcome data |

### Intelligent Ticket Search

Administrative tables support real-time search across operational identifiers including `Ticket ID`, `Student Name`, `NSU ID`, and `Email`.

Pagination is available across **15**, **30**, and **50** records.

### Priority & SLA Visibility

Urgent tickets are visually distinguished from standard requests through dedicated priority indicators and animated urgent-state presentation, allowing staff to identify high-priority operational cases without opening every ticket.

---

## Authentication & Authorization

Security-sensitive administrative operations are protected through dedicated authentication pipelines.

| Security Component | Implementation |
|---|---|
| Authentication Mechanism | `JWT`-based authentication |
| Authentication Flows | Independent Agent and Super Admin flows |
| Credential Protection | `bcrypt` password hashing |
| Session Termination | Token blacklisting on logout |
| Session Management | Inactivity timeouts |
| Authorization Model | Role-aware authorization |
| Network Policy | Controlled CORS policies |
| Response Handling | Sensitive-response cache restrictions |

The authentication model is designed to maintain separation between standard Helpdesk operations and controller-level functionality.

```mermaid
flowchart TD
    Auth[Authentication] --> HA[Helpdesk Agent]
    Auth --> SA[Super Admin]
    HA --> AP[Agent Permissions]
    SA --> CP[Controller Permissions]
```

---

## Real-Time Event Architecture

A central architectural capability of the platform is its use of **Supabase Realtime** for database event propagation. The backend maintains a persistent WebSocket connection to the relevant Supabase Realtime channel.

```mermaid
sequenceDiagram
    participant Student
    participant DB as Supabase PostgreSQL
    participant RT as Supabase Realtime
    participant Node as Node.js Event Listener
    participant Mail as Nodemailer

    Student->>DB: Ticket Submission
    DB->>RT: INSERT Event
    RT->>Node: Event Propagation
    Node->>Node: Asynchronous Processing
    Node->>Mail: Dispatch Notification
    Mail-->>Student: Notification Email
```

This event-driven approach avoids making the client responsible for directly coordinating every downstream communication action.

---

## Ticket Lifecycle

The platform models the ticket lifecycle as an operational workflow rather than a simple status field.

```mermaid
flowchart TD
    A[Student Submission] --> B[Ticket Created — PENDING]
    B --> C[Helpdesk Diagnostics & Processing]
    C --> D{Decision}
    D -->|Approved| E[Controller Processing]
    D -->|Declined| F[Mandatory Explanation]
    E --> G[Resolved]
    F --> H[Student Notification]
    G --> I[Student Notification]
```

---

## Helpdesk Agent Portal

The Helpdesk Agent Portal functions as the **Level 1 operational workspace**.

Agents can:

- Monitor the active ticket queue
- Inspect ticket details
- Search and filter requests
- Identify urgent cases
- Correct student-submitted information
- Create tickets for walk-in students
- Process academic requests
- Manage affected payment semesters
- Verify supporting documentation
- Escalate cases for approval
- Generate printable inspection reports

### Action Engine

Academic requests require specialized processing. The platform provides an **Action Engine** for constructing operational directives:

| Directive | Purpose |
|---|---|
| `ADD COURSE` | Course addition action |
| `DROP COURSE` | Course removal action |
| `SEC CHANGE` | Section change action |
| `WAIVER / OVERRIDE` | Waiver or override action |
| `CUSTOM` | Custom-defined action |

The resulting directive can be processed through the appropriate administrative workflow.

### Payment Semester Management

Financial support cases can span multiple academic semesters. The dedicated workflow allows authorized agents to:

- Add affected semesters
- Remove affected semesters
- Modify affected semesters
- Prepare financial cases
- Escalate cases for controller review

### Document Verification

Certain academic and support cases require physical supporting documents. The platform includes explicit verification controls allowing agents to confirm that required documentation has been reviewed before escalation.

### Ticket Correction

Authorized agents can correct submitted information when a student provides inaccurate information. Supported corrections include: `Name`, `NSU ID`, `Department`, `Email`, `Issue Type`, `Description`.

These modifications are represented within the ticket's audit history.

---

## Super Admin Command Center

The Super Admin environment provides **controller-level oversight and authorization**.

Super Administrators can:

- Review processed requests
- Approve requests
- Decline requests
- Provide mandatory decline explanations
- Finalize resolutions
- Add resolution notes
- Monitor telemetry
- Export financial investigations
- Process Canvas provisioning requests
- Execute batch-oriented operational workflows

This environment represents the highest operational authorization tier within the platform.

---

## Canvas Provisioning Workflow

The platform includes a specialized **Canvas Extraction SPA** designed for LMS provisioning workflows.

### Smart Filtering

Canvas requests can be isolated according to operational vectors such as:

- No Account
- Access & Sync Errors
- Manual Batch Override
- Batch Selection

Administrators can select relevant records for batch processing rather than manually processing every request individually.

### Structured CSV Generation

Selected Canvas records are transformed into a structured CSV representation containing the required provisioning fields:

| Field |
|---|
| `user_id` |
| `integration_id` |
| `login_id` |
| `password` |
| `authentication_provider_id` |
| `first_name` |
| `last_name` |
| `full_name` |
| `email` |
| `department` |
| `status` |

> The internal implementation and provisioning infrastructure remain intentionally private.

### Batch State Transition

Tickets included in the extraction workflow are transitioned into an appropriate processing state to reduce repeated processing of the same records.

---

## Payment Operations

The Super Admin environment includes a dedicated **export capability** for pending payment investigations. Relevant records can be transformed into a structured CSV representation for accounting-oriented review.

---

## Auditability & Governance

Operational accountability is incorporated into the ticket workflow. The platform tracks significant administrative actions including:

- Ticket modifications
- Approval decisions
- Decline decisions
- Decline explanations
- Resolution actions
- Processing history

A decline action requires an explicit written justification.

```mermaid
flowchart TD
    A[Decline Request] --> B[Mandatory Explanation]
    B --> C[Audit History]
    B --> D[Student Email]
```

This ensures that an administrative decision is accompanied by both an internal record and an appropriate student-facing explanation.

---

## Automated Communication Pipeline

The platform incorporates an **event-driven email communication layer** using Nodemailer and Supabase Realtime, supporting three major ticket lifecycle events.

```mermaid
flowchart TD
    L[Ticket Lifecycle] --> S[Submission]
    L --> R[Resolution]
    L --> D[Decline]
    S --> SE[Receipt Email]
    R --> RE[Success Email]
    D --> DE[Warning Email]
```

### Submission Receipt

A branded HTML email is automatically generated after ticket submission. It communicates the Ticket ID, requested category, current status, and submission confirmation.

### Resolution Confirmation

When a request is resolved, the system generates a dedicated resolution email. Resolution notes supplied during processing can be dynamically incorporated into the notification.

### Decline Notification

Declined requests require a mandatory explanation, which is incorporated into the student-facing decline notification.

### Asynchronous Communication Architecture

The communication pipeline is designed so email delivery does not unnecessarily block primary administrative workflows.

```mermaid
flowchart TD
    A[Ticket Event] --> B[Event Detection]
    B --> C[Email Construction]
    C --> D[Asynchronous Dispatch]
    D --> E[Student Mailbox]
```

The outbound messages use responsive HTML templates and incorporate status-specific visual treatment.

---

## Operational UX

The administrative interfaces were designed for high-frequency operational use.

### Responsive Data Grids

The system uses dense operational tables with sticky headers, responsive layouts, pagination, search, status indicators, and priority indicators.

### Command Palette

Administrative navigation supports a command palette interaction model.

| Platform | Shortcut |
|---|---|
| Windows / Linux | `Ctrl + K` |
| macOS | `Cmd + K` |

The palette allows users to rapidly access operational destinations and supported actions without navigating through multiple interface layers.

### Contextual Productivity Tools

The platform includes several small interaction optimizations:

- One-click NSU ID copying
- One-click email copying
- Direct phone call action
- Dynamic category-specific forms
- Rapid navigation
- Toast-based asynchronous feedback

These capabilities are intentionally designed around the daily workflow of support personnel.

### Notification Engine

The administrative portals include a unified toast notification layer.

| Type | Purpose |
|------|---------|
| **Info** | General operational feedback |
| **Success** | Completed actions |
| **Warning** | Important operational conditions |
| **Error** | Failed or invalid operations |

Notifications provide immediate feedback for operations such as synchronization, ticket resolution, draft saving, clipboard actions, and administrative processing.

### Printable Inspection Reports

The ticket inspection workspace includes dedicated print styling. The digital ticket inspection view can be transformed into a structured printable document containing designated signature areas for `Student`, `Helpdesk Agent`, and `Controller`.

This provides continuity between digital ticket processing and operational situations requiring physical documentation.

---

## Technology Stack

| Layer | Technology | Engineering Role |
|-------|------------|-----------------|
| **UI Library** | `React 19` | Component-based interface engineering |
| **Rendering** | `React DOM 19` | DOM reconciliation and rendering |
| **Client-Side Routing** | `React Router DOM 7` | Application navigation and route management |
| **Build Tooling** | `Vite 6` (`@vitejs/plugin-react`) | Development server and production bundling |
| **UI Engineering** | `Tailwind CSS` | Responsive design system and utility-based styling |
| **Backend Runtime** | `Node.js` | Server-side application execution |
| **API Layer** | `Express.js` | HTTP API and application routing |
| **Data Platform** | `Supabase PostgreSQL` | Persistent relational data storage |
| **Event Layer** | `Supabase Realtime` | Database event propagation through WebSockets |
| **Authentication** | `JWT` | Stateless authentication mechanism |
| **Credential Security** | `bcryptjs` | Password hashing |
| **Communication** | `Nodemailer` | Transactional email delivery |

---

## Engineering Architecture

The platform can be conceptually represented through five cooperating layers.

```mermaid
flowchart TD
    P["Presentation Layer<br/>React 19 · React Router DOM 7 · Tailwind CSS · Vite 6"] --> A["Application Layer<br/>Node.js · Express.js · Business Workflows · Validation"]
    A --> D["Data Layer<br/>Supabase PostgreSQL"]
    D --> R["Real-Time Event Layer<br/>Supabase Realtime / WebSockets"]
    R --> C["Communication Layer<br/>Nodemailer"]
```

---

## Engineering Decisions

### Why a Role-Separated Architecture?

The platform operates across fundamentally different responsibility levels — Students submit requests, Agents diagnose and process them, and Super Administrators authorize and finalize operational decisions. Separating these responsibilities reduces unnecessary privilege exposure and provides a clearer operational model.

### Why Event-Driven Notifications?

Student communication is a downstream consequence of ticket lifecycle events. Connecting notifications to database events allows the communication layer to respond to state changes without coupling every frontend interaction directly to email delivery.

### Why Supabase Realtime?

Support operations benefit from immediate awareness of database changes. Realtime event propagation allows the backend to react to ticket insertion events without relying exclusively on repeated client-side polling.

### Why JWT Authentication?

JWT provides a structured mechanism for maintaining authenticated administrative sessions across the application's API layer while allowing distinct authentication flows for different operational roles.

### Why bcrypt?

Administrative credentials require one-way password protection rather than storing plaintext passwords. bcrypt-based hashing provides the credential protection layer used by the administrative authentication system.

### Why Express.js?

Express provides the API and routing layer connecting the presentation layer with backend business workflows, authentication, database operations, and event-driven processing.

### Why Migrate to React 19 + Vite?

The frontend was initially implemented in HTML5 and JavaScript ES6+ before being migrated to a component-based architecture using React 19, with React Router DOM 7 introduced to support client-side routing across the Student, Agent, and Admin portals. Vite 6 was adopted as the build tool for development and production bundling. Tailwind CSS was retained across the migration as the styling layer.

---

## Engineering Challenges

<details>
<summary><strong>01 — Modeling Multiple Operational Roles</strong></summary>

**Challenge:** Different users require fundamentally different capabilities and levels of authorization.

**Engineering Response:** The platform was structured into dedicated environments with separate authentication and authorization workflows.

**Engineering Outcome:** The resulting architecture establishes a clear separation between submission, operational processing, and controller authorization.

</details>

<details>
<summary><strong>02 — Supporting Heterogeneous Workflows</strong></summary>

**Challenge:** Canvas, payment, academic, email, and 2FA requests require different processing procedures.

**Engineering Response:** Service-specific workflows were introduced instead of forcing every ticket through a single generic processing path, including the Academic Action Engine, Payment Semester Management, Canvas Provisioning SPA, Document Verification, and specialized ticket forms.

</details>

<details>
<summary><strong>03 — Real-Time Event Processing</strong></summary>

**Challenge:** The system needs to react to new tickets without requiring constant client-side polling.

**Engineering Response:** Supabase Realtime was integrated with the backend through persistent WebSocket event handling.

**Engineering Outcome:** Database events can initiate downstream processing such as automated student communication.

</details>

<details>
<summary><strong>04 — Administrative Accountability</strong></summary>

**Challenge:** Administrative decisions such as declining requests require contextual justification.

**Engineering Response:** The system requires written decline explanations and associates them with the ticket's audit history and student communication.

</details>

<details>
<summary><strong>05 — Operational Efficiency</strong></summary>

**Challenge:** Support staff frequently perform repetitive actions across large operational queues.

**Engineering Response:** The platform incorporates command palette navigation, search, pagination, batch selection, CSV export, clipboard shortcuts, direct calling, printable reports, and automated notifications.

**Engineering Outcome:** The result is an interface optimized around operational throughput rather than purely visual presentation.

</details>

---

## Product Walkthrough

The following screenshots provide a visual representation of the deployed product, organized by product experience rather than presented as an unstructured image collection.

### Student Support Experience

<div align="center">
<table>
<tr>
<td width="33%" align="center"><img src="assets/1.png" width="100%"/><br/><sub><strong>01 — Support Interface</strong></sub></td>
<td width="33%" align="center"><img src="assets/2.png" width="100%"/><br/><sub><strong>02 — Student Workflow</strong></sub></td>
<td width="33%" align="center"><img src="assets/3.png" width="100%"/><br/><sub><strong>03 — Service Request Experience</strong></sub></td>
</tr>
<tr>
<td width="33%" align="center"><img src="assets/token.png" width="100%"/><br/><sub><strong>04 — Request Processing Interface</strong></sub></td>
<td width="33%" align="center"><img src="assets/5.png" width="100%"/><br/><sub><strong>05 — Warning on Special Cases</strong></sub></td>
<td width="33%" align="center"><img src="assets/8.png" width="100%"/><br/><sub><strong>06 — Warning on Academic Special Cases</strong></sub></td>
</tr>
</table>
</div>

### Administrative Operations

<div align="center">
<table>
<tr>
<td width="33%" align="center"><img src="assets/10.png" width="100%"/><br/><sub><strong>05</strong></sub></td>
<td width="33%" align="center"><img src="assets/11.png" width="100%"/><br/><sub><strong>06</strong></sub></td>
<td width="33%" align="center"><img src="assets/12.png" width="100%"/><br/><sub><strong>07</strong></sub></td>
</tr>
<tr>
<td width="33%" align="center"><img src="assets/13.png" width="100%"/><br/><sub><strong>08</strong></sub></td>
<td width="33%" align="center"><img src="assets/14.png" width="100%"/><br/><sub><strong>09</strong></sub></td>
<td width="33%" align="center"><img src="assets/15.png" width="100%"/><br/><sub><strong>10</strong></sub></td>
</tr>
<tr>
<td width="33%" align="center"><img src="assets/16.png" width="100%"/><br/><sub><strong>11</strong></sub></td>
<td width="33%" align="center"><img src="assets/17.png" width="100%"/><br/><sub><strong>12</strong></sub></td>
<td width="33%" align="center"><img src="assets/18.png" width="100%"/><br/><sub><strong>13</strong></sub></td>
</tr>
<tr>
<td width="33%" align="center"><img src="assets/19.png" width="100%"/><br/><sub><strong>14</strong></sub></td>
<td width="33%" align="center"><img src="assets/20.png" width="100%"/><br/><sub><strong>15</strong></sub></td>
<td width="33%"></td>
</tr>
</table>
</div>

### Ticket Processing & Workflow

<div align="center">
<table>
<tr>
<td width="33%" align="center"><img src="assets/16.png" width="100%"/><br/><sub><strong>16</strong></sub></td>
<td width="33%" align="center"><img src="assets/17.png" width="100%"/><br/><sub><strong>17</strong></sub></td>
<td width="33%" align="center"><img src="assets/18.png" width="100%"/><br/><sub><strong>18</strong></sub></td>
</tr>
<tr>
<td width="33%" align="center"><img src="assets/19.png" width="100%"/><br/><sub><strong>19</strong></sub></td>
<td width="33%" align="center"><img src="assets/20.png" width="100%"/><br/><sub><strong>20</strong></sub></td>
<td width="33%" align="center"><img src="assets/21.png" width="100%"/><br/><sub><strong>21</strong></sub></td>
</tr>
</table>
</div>

### Administration & Specialized Operations

<div align="center">
<table>
<tr>
<td width="33%" align="center"><img src="assets/18.png" width="100%"/><br/><sub><strong>22</strong></sub></td>
<td width="33%" align="center"><img src="assets/19.png" width="100%"/><br/><sub><strong>23</strong></sub></td>
<td width="33%" align="center"><img src="assets/20.png" width="100%"/><br/><sub><strong>24</strong></sub></td>
</tr>
<tr>
<td width="33%" align="center"><img src="assets/25.png" width="100%"/><br/><sub><strong>25</strong></sub></td>
<td width="33%" align="center"><img src="assets/26.png" width="100%"/><br/><sub><strong>26</strong></sub></td>
<td width="33%" align="center"><img src="assets/27.png" width="100%"/><br/><sub><strong>27</strong></sub></td>
</tr>
<tr>
<td width="33%" align="center"><img src="assets/28.png" width="100%"/><br/><sub><strong>28</strong></sub></td>
<td width="33%" align="center"><img src="assets/29.png" width="100%"/><br/><sub><strong>29</strong></sub></td>
<td width="33%"></td>
</tr>
</table>
</div>

---

## Email Communication Showcase

The platform's automated communication layer generates branded HTML emails throughout the ticket lifecycle.

<div align="center">
<table>
<tr>
<td width="33%" align="center"><img src="assets/recieve.png" width="100%"/><br/><sub><strong>Submission Receipt</strong></sub></td>
<td width="33%" align="center"><img src="assets/resolve.png" width="100%"/><br/><sub><strong>Resolution Notification</strong></sub></td>
<td width="33%" align="center"><img src="assets/decline.png" width="100%"/><br/><sub><strong>Decline Notification</strong></sub></td>
</tr>
</table>
</div>

---

## Deployment

The application was taken through the complete development lifecycle:

```mermaid
flowchart TD
    A[Requirements] --> B[System Design]
    B --> C[UI/UX Engineering]
    C --> D[Frontend Development]
    D --> E[Backend Development]
    E --> F[Database Integration]
    F --> G[Authentication & Authorization]
    G --> H[Realtime Event Integration]
    H --> I[Automated Communication]
    I --> J[Validation & Refinement]
    J --> K[Production Deployment]
    K --> L[Operational Software Product]
```

The deployed application is intentionally documented at the architectural and product level rather than exposing private deployment configuration or internal infrastructure.

---

## Engineering Ownership

This project represents **end-to-end software engineering ownership**, spanning multiple layers of the product lifecycle, including:

- Requirement interpretation
- Workflow modeling
- System architecture
- UI/UX engineering
- Frontend development
- Backend API development
- Database integration
- Authentication
- Authorization
- Business workflow implementation
- Real-time event processing
- Automated communication
- Administrative tooling
- Data export workflows
- Validation
- Deployment

The project demonstrates the ability to move beyond isolated feature implementation and engineer a complete operational software system around real-world requirements.

---

## Capabilities Demonstrated

### Software Engineering
- Full-Stack Application Development
- System Architecture
- API Design
- Business Logic Engineering
- Workflow Modeling
- Integration Engineering

### Backend Engineering
- Node.js
- Express.js
- REST-oriented application workflows
- Authentication & Authorization
- Event-driven processing
- Automated communication

### Data Engineering
- PostgreSQL
- Supabase
- Real-time database events
- Structured data export
- Operational data management

### Security Engineering
- JWT authentication
- Role-based authorization
- bcrypt password hashing
- Token invalidation
- Session timeout
- CORS controls
- Cache-control considerations

### Frontend Engineering
- React 19
- React Router DOM 7
- Vite 6
- Tailwind CSS
- Component-based architecture
- Responsive interfaces
- Data-intensive UI
- Command palette interaction
- Dynamic forms
- Administrative dashboards

### Product Engineering
- Requirement analysis
- Workflow design
- Operational UX
- Role-aware interfaces
- Auditability
- Notification systems
- Production deployment

---

## Project Impact

The platform brings multiple IT support workflows into a unified operational system, establishing a structured lifecycle rather than treating support requests as isolated records.

```mermaid
flowchart TD
    A[Submit] --> B[Identify]
    B --> C[Triage]
    C --> D[Process]
    D --> E[Approve / Decline]
    E --> F[Resolve]
    F --> G[Notify]
    G --> H[Audit]
```

This architecture creates a consistent operational path from the student's initial request through administrative resolution.

---

## Future Improvements

The following represent potential future directions and are not currently presented as implemented features:

- Expanded SLA analytics
- More granular permission policies
- Advanced operational reporting
- Additional institutional integrations
- Expanded notification channels
- More automated workflow orchestration
- Enhanced compliance reporting
- Advanced operational analytics
- Extended audit visualization

---

## Repository Notice

This repository is maintained as a **professional technical showcase and engineering case study**.

The NSU IT Support Center is a deployed/proprietary software system. Its source code, internal implementation, credentials, private configuration, infrastructure details, and sensitive organizational information are intentionally not publicly exposed.

Instead, this repository documents the engineering work through:

- System architecture
- Product capabilities
- Workflow design
- Technology choices
- Security considerations
- Engineering challenges
- Deployment lifecycle
- Product screenshots
- Automated communication examples

> The absence of source code is intentional and reflects the proprietary nature of the deployed system.

---

## Project Classification

| Attribute | Description |
|-----------|-------------|
| **Project Type** | Enterprise IT Service Management Platform |
| **Architecture** | Multi-tier, role-based operational system |
| **Primary Users** | Students, Helpdesk Agents, Super Administrators |
| **Core Domain** | IT Support & Ticket Resolution |
| **Development Scope** | End-to-End Software Engineering |
| **Deployment** | Production Environment |
| **Repository Purpose** | Technical Showcase / Engineering Case Study |
| **Source Code** | Proprietary / Not Publicly Exposed |

---

## Technology Summary

| Category | Technologies |
|---|---|
| **Frontend** | `React 19`, `React DOM 19`, `React Router DOM 7`, `Vite 6`, `Tailwind CSS` |
| **Backend** | `Node.js`, `Express.js` |
| **Data** | `Supabase PostgreSQL`, `Supabase Realtime` |
| **Security** | `JWT`, `bcryptjs` |
| **Communication** | `Nodemailer` |

---

## Final Perspective

The NSU IT Support Center is an example of engineering a software product around real operational requirements rather than simply implementing a collection of CRUD screens.

The system combines:

- Role-based access control
- Multi-stage workflows
- Real-time database events
- Event-driven communication
- Administrative authorization
- Auditability
- Specialized academic workflows
- Financial processing
- LMS provisioning workflows
- Operational telemetry
- Responsive administrative interfaces
- Automated student communication
- Production deployment

```mermaid
flowchart TD
    A[Real-World Requirement] --> B[System Architecture]
    B --> C[Product Design]
    C --> D[Software Engineering]
    D --> E[Integration]
    E --> F[Validation & Refinement]
    F --> G[Deployment]
    G --> H[Operational System]
```

> Designed from requirements. Engineered end-to-end. Integrated across multiple operational workflows. Deployed as a real software product.

---

<div align="center">

*NSU IT Support Center — Enterprise IT Service Management Platform*

</div>

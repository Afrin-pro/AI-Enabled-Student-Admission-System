# High-Level Architecture

```mermaid
flowchart TB

    A["Student Admissions & Support Portal"]

    A --> B["Student Management"]
    A --> C["Course Management"]
    A --> D["Enrollment Management"]
    A --> E["Security & User Management"]

    D --> F["Salesforce Flows"]
    D --> G["Approval Process"]

    F --> H["Reports & Dashboards"]
    G --> H

    E --> F

    H --> I["Agentforce AI"]

    subgraph Salesforce Platform
        B
        C
        D
        E
        F
        G
        H
        I
    end
```

## Components

### Student Management

- Student Records
- Student Details
- Admission Status

### Course Management

- Courses
- Capacity
- Course Information

### Enrollment Management

- Student Enrollment
- Approval Workflow
- Enrollment Status

### Automation

- Salesforce Flow
- Approval Process
- Email Notifications

### Security

- Profiles
- Roles
- Permission Sets
- Sharing Rules

### Analytics

- Reports
- Dashboards

### Artificial Intelligence

- Agentforce
- Counselor Assistance
- AI Recommendations
- Record Summaries

## Technology Stack

| Layer | Technology |
|---|---|
| CRM Platform | Salesforce |
| Automation | Flow Builder |
| Security | Profiles, Roles, Permission Sets |
| Analytics | Reports & Dashboards |
| AI | Agentforce |
| Development | Salesforce DX |
| Version Control | Git & GitHub |

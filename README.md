# AI-Enabled Student Admission System

> A Salesforce-native admissions platform combining declarative automation with a Generative AI agent — built as part of the SmartBridge VIP Program (AICTE-affiliated).

## Overview

This project reimagines the student admissions workflow on Salesforce. It pairs traditional declarative automation (Screen Flows, Duplicate & Matching Rules) with **Admissions Assistant Agent**, a Generative AI agent built on Salesforce Agentforce that helps counselors and admissions managers summarize applications, assess enrollment risk, and evaluate discount requests — grounded in live, real-time Salesforce data rather than static or hallucinated responses.

Developed milestone-by-milestone in a Salesforce Developer Edition org (`studentAdmissionOrg`).

## Program Context

- **Program:** SmartBridge Virtual Internship Program (VIP)
- **Affiliation:** AICTE
- **Delivery model:** Milestone-based, with metadata version-controlled in Git and documented per milestone for evaluator review

## Core Data Model

| Object | Purpose | Relationship |
|---|---|---|
| `Student__c` | Student master record | Master in Master-Detail to `Student_Enrollment__c` |
| `Course__c` | Course catalog record | Master in Master-Detail to `Student_Enrollment__c` |
| `Student_Enrollment__c` | Application/enrollment record — links a student to a course, tracks course fee, discount, final payable amount, enrollment status, and AI priority score | Detail object |

## Key Features

### 1. Student Enrollment Screen Flow
Counselor-facing Screen Flow for enrolling students into courses, with automatic discount calculation, formula-field resolution, and post-create record retrieval to surface computed values.

### 2. Duplicate & Matching Rules
Prevents duplicate enrollments using a custom text-based match key (`Enrollment_Match_Key__c`), populated by a Before-Save Record-Triggered Flow that concatenates Student and Course Ids — a workaround for Salesforce's native one-lookup-field-per-Matching-Rule limitation and the fact that formula fields aren't available in Matching Rule criteria.

### 3. Admissions Assistant Agent (Agentforce)
An AI agent built in Salesforce's Agentforce Builder, made up of three purpose-built subagents, each grounded in live Salesforce data via the standard **Query Records** action and backed by an activated Prompt Builder template:

| Subagent | Function |
|---|---|
| **Student Application Summary** | Plain-language summary of an enrollment — student, course, fees, discount, status, AI priority score, and flagged risks |
| **Enrollment Risk Analysis** | Assesses admission probability and financial risk from the discount applied; classifies overall enrollment health as Low, Medium, or High Risk |
| **Student Enrollment Discount Evaluation** | Evaluates whether a specific discount amount should be approved, escalated, or rejected |

A general-purpose **General FAQ** subagent handles anything outside these three, with classification descriptions tuned to avoid overlap between subagents.

### 4. AI Trust & Governance
Data Masking, Zero Data Retention, and Audit Logging enabled via Salesforce's AI Trust & Permissions layer before any Agentforce feature was activated. Agent access is scoped through dedicated permission sets (Admissions Counselors, Admissions Managers) with Enabled Agent Access explicitly granted.

## Tech Stack

- Salesforce Developer Edition (Lightning Experience)
- Agentforce Builder — Subagents, Prompt Builder, Query Records grounding
- Flow Builder — Screen Flows, Record-Triggered Flows
- Salesforce CLI (`sf`) + Salesforce Extensions for VS Code
- Git / GitHub

## Project Structure

```
├── .husky/                    # Git hooks (pre-commit formatting/linting)
├── .vscode/                   # VS Code workspace settings
├── Demo-Video/                # Project demo video (recording or link to hosted walkthrough)
├── Docs/                      # Per-milestone screenshots for evaluators
│   └── screenshots/
│       └── phase<N>/
├── Documentation/             # Full consolidated project documentation — all phases & milestones
├── config/                    # Scratch org definition files
├── force-app/main/default/    # Salesforce metadata — objects, flows, Agentforce components, etc.
├── scripts/                   # Utility scripts (Apex/SOQL helpers)
├── .forceignore
├── .gitignore
├── .prettierignore
├── .prettierrc
└── sfdx-project.json
```

## Getting Started

```bash
# Clone the repo
git clone https://github.com/Afrin-pro/AI-Enabled-Student-Admission-System.git
cd AI-Enabled-Student-Admission-System

# Authorize your Salesforce org
sf org login web --alias studentAdmissionOrg --set-default

# Deploy metadata to your org
sf project deploy start --target-org studentAdmissionOrg
```

## Project Roadmap

### Phase 2: Salesforce Development — Backend & Configuration
- [x] M1: Salesforce Account
- [x] M2: Objects Creation
- [x] M3: Tabs
- [x] M4: Fields & Relationships
- [x] M5: Validation Rules
- [x] M6: Approval Process
- [x] M7: Email Templates
- [x] M8: Email Alerts
- [x] M9: Declarative Automation (Flows) — Student Enrollment Screen Flow, Duplicate/Matching Rule automation via Before-Save Record-Triggered Flow
- [x] M10: Agentforce AI — Admissions Assistant Agent, 3 subagents, Prompt Builder templates, Query Records grounding, deployed to Lightning Experience

### Phase 3: UI/UX Development & Customization
- [x] M11: The Lightning Page
- [x] M12: Editing of Page Layouts
- [x] M13: Dynamic Forms
- [x] M14: Users

### Phase 4: Data Migration, Testing & Security
- [x] M15: Duplicate and Matching Rules
- [x] M16: Profiles
- [x] M17: Roles and Role Hierarchy

### Phase 5: Deployment, Documentation & Maintenance
- [x] Deployment
- [x] Monitoring & post Deployment Support



## Documentation & Demo

- 📄 **Full project documentation:** [`Documentation/`](./Documentation) — consolidated writeup covering all phases and milestones, intended as the single reference document for evaluators.
- 🖼️ **Per-milestone screenshots:** [`Docs/screenshots/phase<N>/`](./Docs) — visual, milestone-by-milestone walkthrough.
- 🎥 **Demo video:** [`Demo-Video/`](./Demo-Video) — _[https://youtu.be/J4AXr-zjHpI]_. 




## Author

**Afrin** — B.Tech Computer Science (2027), SmartBridge VIP Program participant
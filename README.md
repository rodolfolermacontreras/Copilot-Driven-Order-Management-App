# Copilot-Driven Order Management App

A Power Platform solution that replaces manual Excel-based order tracking with a
centralized, AI-assisted order management system built on Dataverse, Power Apps,
Power Automate, and Copilot Studio.

---

## Project Overview

The purchasing team previously managed orders through Excel spreadsheets. Data was
frequently lost, difficult to track, and did not scale as the organization grew.

This project replaces that process with:

- A **Canvas App** connected to Dataverse for browsing, creating, and updating orders
- A **Copilot Agent** (Order Record Assistant) that allows users to create orders
  through natural language conversation in Microsoft Teams and Copilot Chat
- A **Power Automate Agent Flow** that receives Copilot input and writes records
  to Dataverse automatically

---

## Architecture

```
User (Teams / Copilot Chat)
  --> Copilot Agent: Order Record Assistant
    --> Topic: Create New Order
      --> Agent Flow: Create Order Flow
        --> Dataverse: Orders table
      --> Response sent back to user

User (Browser)
  --> Canvas App
    --> WelcomeScreen --> BrowseScreen
      --> Search / View / Create / Edit orders in Dataverse
```

Full architecture details: [docs/SYSTEM_ARCHITECTURE_GUIDE.md](docs/SYSTEM_ARCHITECTURE_GUIDE.md)

---

## Components

| Component | Platform | Description |
|---|---|---|
| Orders table | Dataverse | Central data store for all order records |
| Order Management App | Power Apps (Canvas) | UI for browsing, searching, and managing orders |
| Create Order Flow | Power Automate | Agent Flow that inserts new records into Dataverse |
| Order Record Assistant | Copilot Studio | AI agent for natural language order creation |

---

## Dataverse Table Schema

Source: `data/orders.xlsx`

| Column | Type | Example |
|---|---|---|
| Order Number | Text | ORD-1001 |
| Product Name | Text | Wireless Keyboard |
| Quantity | Whole Number | 25 |
| Order Date | Date Only | 2024-01-05 |
| Expected Delivery Date | Date Only | 2024-05-05 |
| Delivery Status | Text | Pending |

Full schema and mapping: [docs/data_schema.md](docs/data_schema.md)

---

## Repository Structure

```
Copilot-Driven-Order-Management-App/
|-- data/
|   `-- orders.xlsx              # Source data, 10 seed records
|-- docs/
|   |-- PROJECT_STATUS_REVIEW.md # Master change log and status tracker
|   |-- SYSTEM_ARCHITECTURE_GUIDE.md # Architecture, flows, Power FX reference
|   |-- data_schema.md           # Column definitions and Dataverse mapping
|   `-- VERSIONS.md              # Branch tracking, active and archived
|-- Big_Picture.md               # Lean priority checklist, step tracker, rubric
|-- README.md                    # This file
|-- requirements.txt             # Python dependencies (openpyxl)
`-- .gitignore
```

---

## Environment Requirements

- Power Platform environment: **United States region** (required)
- Licenses required: Power Apps, Power Automate, Copilot Studio
- Dataverse must be enabled in the environment

---

## Project Steps

| Step | Description | Status |
|---|---|---|
| 0 | Verify US-based Power Platform environment | Not started |
| 1 | Create Dataverse table from Orders.xlsx | Not started |
| 2 | Build Canvas App (WelcomeScreen, BrowseScreen, navigation) | Not started |
| 3 | Create Power Automate Agent Flow | Not started |
| 4 | Configure Copilot Agent topics and trigger phrases | Not started |
| 5 | Publish and share Copilot Agent | Not started |
| 6 | End-to-end integration test | Not started |
| 7 | Create and export unmanaged solution | Not started |

Current progress: [Big_Picture.md](Big_Picture.md)

---

## Power Automate Agent Flow

The flow accepts four input parameters from the Copilot Agent:

| Parameter | Type |
|---|---|
| Product Name | Text |
| Order Number | Text |
| Quantity | Number |
| Delivery Status | Text |

The flow inserts a new row into the Dataverse Orders table and returns a
confirmation message that includes the product name.

---

## Copilot Agent

- **Name**: Order Record Assistant
- **Topic**: Create New Order
- **Trigger phrases**: Natural language phrases that start an order creation conversation
- **Action**: Calls the Create Order Flow
- **Response**: Sends the flow confirmation message back to the user
- **Channels**: Microsoft Teams, Microsoft 365 Copilot Chat

---

## Solution Export

The final deliverable is an **unmanaged Power Platform solution** containing:

1. Canvas App - Order Management App
2. Copilot Agent - Order Record Assistant
3. Cloud Flow - Create Order Flow
4. Dataverse Table - Orders

---

## Required Submission Screenshots

### Power App Interface
- WelcomeScreen (image, personalized greeting, button)
- BrowseScreen (back icon)
- Create new record form
- Edit existing record form
- Search functionality
- Copilot component in app
- Copilot Agent conversation
- New record created via Copilot

### Configuration and Logic
- Solution components in Power Platform
- Power FX Navigate function
- Power Automate Flow trigger with parameters
- Dataverse action adding new row
- Response action with returned parameter
- Topic trigger and trigger phrases
- Message node sending response to user
- Dataverse table view

---

## Development Workflow

This project follows a branch-based workflow. No direct commits to `main`.

```
git pull origin main
git checkout -b feat/<description>
# make changes, commit incrementally
git push origin feat/<description>
# create pull request, merge after review, delete branch
```

Branch naming: `feat/`, `fix/`, `docs/`, `refactor/`, `test/`, `chore/`

Commit style: `feat: add welcome screen greeting`, `fix: resolve navigation error`

Branch history: [docs/VERSIONS.md](docs/VERSIONS.md)

---

## Required Environment Variables

No secrets or credentials are committed to this repository.
All sensitive values must be stored as environment variables or in a `.env` file
(excluded from version control via `.gitignore`).

---

## Local Setup

```bash
# Clone the repository
git clone https://github.com/rodolfolermacontreras/Copilot-Driven-Order-Management-App.git
cd Copilot-Driven-Order-Management-App

# Create and activate virtual environment
python -m venv .venv
.\.venv\Scripts\Activate.ps1   # Windows PowerShell

# Install dependencies
pip install -r requirements.txt
```

---

## Documentation

| File | Purpose |
|---|---|
| [Big_Picture.md](Big_Picture.md) | Current priorities, step tracker, rubric checklist |
| [docs/PROJECT_STATUS_REVIEW.md](docs/PROJECT_STATUS_REVIEW.md) | Chronological change log with results and analysis |
| [docs/SYSTEM_ARCHITECTURE_GUIDE.md](docs/SYSTEM_ARCHITECTURE_GUIDE.md) | Technical design, data flows, component overview |
| [docs/data_schema.md](docs/data_schema.md) | Column definitions, Dataverse mapping, Agent Flow parameters |
| [docs/VERSIONS.md](docs/VERSIONS.md) | Branch tracking, active and archived branches |

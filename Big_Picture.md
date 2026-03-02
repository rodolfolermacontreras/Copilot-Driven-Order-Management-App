# Big Picture - Order Fulfillment Tracking System

## What to Work on Right Now

See docs/PROJECT_STATUS_REVIEW.md for full detail, history, and analysis.

---

## Steps Completion Tracker

| Step | Description | Status |
|---|---|---|
| Step 0 | Verify US-based Power Platform environment | [ ] Not started |
| Step 1 | Create Dataverse table from Orders.xlsx | [ ] Not started |
| Step 2 | Create Canvas App (WelcomeScreen, BrowseScreen, navigation) | [ ] Not started |
| Step 3 | Create Power Automate Agent Flow | [ ] Not started |
| Step 4 | Configure Copilot Agent (topics, trigger phrases, action, message) | [ ] Not started |
| Step 5 | Publish and share Copilot Agent | [ ] Not started |
| Step 6 | End-to-end integration test | [ ] Not started |
| Step 7 | Create and export unmanaged solution | [ ] Not started |

---

## Current Phase

**Phase 1: Project Setup and Dataverse Configuration**

---

## Immediate Priorities (This Week)

1. Step 0: Confirm US-based environment in Power Platform Admin Center
2. Step 1: Import Orders.xlsx into Dataverse - create table with external data
3. Step 2: Build Canvas App from Dataverse table, add WelcomeScreen with image + greeting + button
4. Step 3: Create Agent Flow with 4 parameters, Dataverse insert action, product name response

---

## Next Phase (Next 2 Weeks)

- Step 4: Configure Copilot Agent "Order Record Assistant" with topic, trigger phrases, action node, message node
- Step 5: Publish agent, share with at least one user, test in Teams and Copilot Chat
- Step 6: Play the Canvas App, create a record via Copilot, refresh app to verify

---

## Long-term Goals (Next Month+)

- Step 7: Bundle into Power Platform solution, export as unmanaged .zip
- Prepare submission: PDF with all required screenshots + solution .zip
- Stretch: Second Copilot topic to update order status via conversation

---

## Rubric Checklist (Screenshots Required)

### Power App Interface
- [ ] WelcomeScreen with image, personalized greeting, button
- [ ] BrowseScreen with back icon
- [ ] Create new record form
- [ ] Edit existing record form
- [ ] Search functionality
- [ ] Copilot component in app
- [ ] Copilot Agent conversation
- [ ] New record created via Copilot

### Solution and Backend
- [ ] Solution components (app + agent + flow + table)
- [ ] Power FX Navigate function
- [ ] Power Automate Flow trigger with parameters
- [ ] Dataverse action to add new row
- [ ] Response action showing returned parameter
- [ ] Topic trigger and trigger phrases
- [ ] Message node sending response to user
- [ ] Dataverse table view

---

## Key Reference

- Data schema: docs/data_schema.md
- Architecture: docs/SYSTEM_ARCHITECTURE_GUIDE.md
- Full status log: docs/PROJECT_STATUS_REVIEW.md
- Branch tracking: docs/VERSIONS.md

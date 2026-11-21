---
name: ui-visual-regression
description: Run Playwright visual regression and JS tests selectively when frontend, CSS, templates, or UI logic change.
---

# UI & Visual Regression Skill

Use this skill for frontend `Implementer` and `Verifier` roles.

## Rules
1. **Scope Gate**:
   - Run visual UI tests **only** when modifying UI, CSS, templates, or frontend JS logic.
   - **Never** run visual regression suites for purely backend, PHP, API, or database changes.
2. **Commands**:
   - Unit/JS logic tests:
     ```bash
     npm run test:js
     ```
   - Fast UI & visual regression check:
     ```bash
     npm run test:ui:fast
     ```
   - Update golden baselines **only** when visual changes are intentional:
     ```bash
     npm run test:ui:update
     ```
3. **Verification**:
   - Report exact pass/fail results and whether golden snapshots were updated.

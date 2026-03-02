# GitHub Projects v2 — Setup Guide

**Campus Gate Access System** | Team GLITCH | CS360 Software Engineering

This document describes how to set up the GitHub Projects v2 board, create the required labels,
populate it with the 18 backlog issues, and configure the Status workflow.

---

## Table of Contents

1. [One-Step Automated Setup](#1-one-step-automated-setup)
2. [Labels Reference](#2-labels-reference)
3. [Manual Label Creation](#3-manual-label-creation)
4. [Manual Issue Creation Notes](#4-manual-issue-creation-notes)
5. [Create the Projects v2 Board](#5-create-the-projects-v2-board)
6. [Status Workflow Columns](#6-status-workflow-columns)
7. [Adding Issues to the Project](#7-adding-issues-to-the-project)
8. [Setting Project Fields](#8-setting-project-fields)
9. [Optional: Auto-Add Issues by Label](#9-optional-auto-add-issues-by-label)

---

## 1. One-Step Automated Setup

A GitHub Actions workflow is provided that creates all required labels and all 18 backlog issues
in one click.

### Steps

1. Navigate to **Actions → Create Backlog Issues & Labels** in this repository.
2. Click **Run workflow**.
3. (Optional) Enable **Dry run** to preview what will be created without making changes.
4. Click **Run workflow** to confirm.

The workflow is idempotent — re-running it will skip any issue whose title already exists and will
update existing labels with `--force`.

> **Permissions required:** The default `GITHUB_TOKEN` provided by GitHub Actions is sufficient.
> The workflow requests `issues: write` and `contents: read` permissions.

---

## 2. Labels Reference

All labels follow a `namespace:value` naming convention.

### Type

| Label | Color | Description |
|-------|-------|-------------|
| `type:user-story` | `#0075ca` | User story issue |

### Release

| Label | Color | Description |
|-------|-------|-------------|
| `release:checkpoint` | `#e4e669` | Deliverable at the mid-project checkpoint |
| `release:final` | `#f9a825` | Deliverable at the end-of-semester final release |

### Risk

| Label | Color | Description |
|-------|-------|-------------|
| `risk:low` | `#0e8a16` | Low implementation risk |
| `risk:medium` | `#fbca04` | Medium implementation risk |
| `risk:high` | `#d93f0b` | High implementation risk |

### Role (Persona)

| Label | Color | Description |
|-------|-------|-------------|
| `role:security-guard` | `#bfd4f2` | Persona: Security Guard |
| `role:faculty` | `#c2e0c6` | Persona: Faculty member |
| `role:staff` | `#fef2c0` | Persona: Staff member |
| `role:student` | `#d4c5f9` | Persona: Student |
| `role:security-admin` | `#f9d0c4` | Persona: Security Admin |

---

## 3. Manual Label Creation

If you prefer to create labels manually (or via the `gh` CLI):

```bash
# Prerequisites: gh CLI authenticated, REPO set
REPO="CS360S26-glitch/glitch-project"

gh label create "type:user-story"       --color "0075ca" --description "User story issue"                                   --repo $REPO
gh label create "release:checkpoint"    --color "e4e669" --description "Deliverable at the mid-project checkpoint"           --repo $REPO
gh label create "release:final"         --color "f9a825" --description "Deliverable at the end-of-semester final release"    --repo $REPO
gh label create "risk:low"              --color "0e8a16" --description "Low implementation risk"                             --repo $REPO
gh label create "risk:medium"           --color "fbca04" --description "Medium implementation risk"                          --repo $REPO
gh label create "risk:high"             --color "d93f0b" --description "High implementation risk"                            --repo $REPO
gh label create "role:security-guard"   --color "bfd4f2" --description "Persona: Security Guard"                            --repo $REPO
gh label create "role:faculty"          --color "c2e0c6" --description "Persona: Faculty member"                            --repo $REPO
gh label create "role:staff"            --color "fef2c0" --description "Persona: Staff member"                              --repo $REPO
gh label create "role:student"          --color "d4c5f9" --description "Persona: Student"                                   --repo $REPO
gh label create "role:security-admin"   --color "f9d0c4" --description "Persona: Security Admin"                            --repo $REPO
```

---

## 4. Manual Issue Creation Notes

Each issue follows this format:

**Title:** `US-XX: <concise feature name> (<role>)`

**Body sections:**
- `Story Points: N` — near the top so it can be transferred to a Projects v2 number field
- `## User Story` — verbatim from [`wiki/backlog.md`](backlog.md)
- `## Acceptance Criteria` — task-style checklist (`- [ ] ...`)
- `## Notes` — source reference, release, and risk

**Labels applied per issue:**

| Issue | Story Points | Release | Risk | Role Label |
|-------|:---:|---------|------|------------|
| US-01 | 5 | `release:checkpoint` | `risk:medium` | `role:security-guard` |
| US-02 | 3 | `release:checkpoint` | `risk:low` | `role:security-guard` |
| US-03 | 8 | `release:checkpoint` | `risk:high` | `role:security-guard` |
| US-04 | 5 | `release:checkpoint` | `risk:medium` | `role:security-guard` |
| US-05 | 3 | `release:final` | `risk:low` | `role:security-guard` |
| US-06 | 5 | `release:checkpoint` | `risk:low` | `role:faculty` |
| US-07 | 2 | `release:final` | `risk:low` | `role:faculty` |
| US-08 | 3 | `release:final` | `risk:low` | `role:staff` |
| US-09 | 2 | `release:final` | `risk:low` | `role:staff` |
| US-10 | 5 | `release:final` | `risk:medium` | `role:student` |
| US-11 | 3 | `release:final` | `risk:medium` | `role:student` |
| US-12 | 2 | `release:final` | `risk:low` | `role:student` |
| US-13 | 8 | `release:checkpoint` | `risk:high` | `role:security-admin` |
| US-14 | 5 | `release:final` | `risk:medium` | `role:security-admin` |
| US-15 | 3 | `release:final` | `risk:low` | `role:security-admin` |
| US-16 | 8 | `release:final` | `risk:high` | `role:security-admin` |
| US-17 | 5 | `release:final` | `risk:medium` | `role:security-guard` |
| US-18 | 8 | `release:final` | `risk:high` | `role:security-admin` |

All issues also receive the `type:user-story` label.

---

## 5. Create the Projects v2 Board

1. Go to the **CS360S26-glitch** organisation (or the repository) on GitHub.
2. Click the **Projects** tab → **New project**.
3. Select the **Board** layout template.
4. Name the project (e.g., `Campus Gate Access System — Sprint Board`).
5. Click **Create project**.

---

## 6. Status Workflow Columns

GitHub Projects v2 uses a built-in **Status** single-select field. Configure the following options:

| Column | Meaning |
|--------|---------|
| **Backlog** | Story identified but not yet scheduled for a sprint |
| **To do** | Scheduled for the current sprint, not yet started |
| **In progress** | Actively being implemented |
| **Done** | Implemented, reviewed, and merged |

### How to configure Status options

1. Open the project board.
2. Click **⚙ Settings** (top-right of the board view).
3. Under **Fields**, click **Status**.
4. Edit or add options: `Backlog`, `To do`, `In progress`, `Done`.
5. Assign colours as desired (e.g., grey, blue, yellow, green).
6. Save changes.

---

## 7. Adding Issues to the Project

### Via the project board (manual)

1. Open the project board.
2. Click **+ Add item** at the bottom of any column.
3. Type `#` followed by the issue number or title to search, then press **Enter**.

### Via the issue page

1. Open any backlog issue.
2. In the right sidebar under **Projects**, click the gear icon.
3. Select the project name and set the **Status** field to `Backlog`.

### Bulk import

1. Open the project board.
2. Click **+ Add item** → **Add from repository**.
3. Filter by the `type:user-story` label and add all matching issues at once.

---

## 8. Setting Project Fields

After adding issues to the board, set the following custom fields for each item:

| Field | Type | Values |
|-------|------|--------|
| **Status** | Single select | Backlog / To do / In progress / Done |
| **Story Points** | Number | Copy the value from `Story Points: N` in the issue body |
| **Risk** | Single select | Low / Medium / High (matches `risk:*` label) |
| **Release** | Single select | Checkpoint / Final (matches `release:*` label) |

### Creating custom fields

1. In the project board, click **+** (the rightmost column header or the field editor icon).
2. For **Story Points**: choose **Number** field type.
3. For **Risk** and **Release**: choose **Single select** and add the options listed above.
4. Click **Save**.

---

## 9. Optional: Auto-Add Issues by Label

You can configure the project to automatically add new issues when they have specific labels:

1. Open the project board → **⚙ Settings** → **Workflows**.
2. Enable the **"Auto-add to project"** workflow.
3. Set the filter to `label:type:user-story` (and optionally `repo:CS360S26-glitch/glitch-project`).
4. Save. Any future issue tagged with `type:user-story` will be automatically added to the board
   with **Status = Backlog**.

---

*Last updated by the automated backlog-population workflow. Source of truth: [`wiki/backlog.md`](backlog.md).*

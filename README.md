# Issue Ops Automation Workflows

This repository contains a suite of GitHub Actions workflows designed to automate common issue management tasks in an "issue-ops" style. Below you'll find detailed instructions for configuring and utilizing each workflow.

---

## Table of Contents
- [Auto Response to New Issues](#auto-response-to-new-issues)
- [Auto Assign Issues](#auto-assign-issues)
- [Auto Label Stale Issues](#auto-label-stale-issues)
- [Auto Close Stale Issues](#auto-close-stale-issues)
- [Auto Comment Assignee Reminder](#auto-comment-assignee-reminder)
- [Issue Metrics Report](#issue-metrics-report)

---

## Auto Response to New Issues
**Workflow:** `.github/workflows/issue-ops.yml`

- **Purpose:** Automatically responds to issues labeled `new_issue`, removes the label, and adds `assign`.
- **Configuration:**
  - Edit `.github/workflows/configurations/autoresponse_template.md` to customize the auto-response message.
- **How it works:**
  1. Listens for the `new_issue` label on issues.
  2. Posts a comment using the template.
  3. Removes `new_issue` label and adds `assign` label.

---

## Auto Assign Issues
**Workflow:** `.github/workflows/auto-assign.yml`

- **Purpose:** Assigns issues labeled `assign` to a user from a predefined list, avoiding recent assignees.
- **Configuration:**
  - Edit `.github/workflows/configurations/assignees.yml` to specify the list of GitHub usernames.
- **How it works:**
  1. Listens for the `assign` label on issues.
  2. Selects the next user in a round-robin fashion, skipping recent assignees.
  3. Assigns the issue and removes the `assign` label.

---

## Auto Label Stale Issues
**Workflow:** `.github/workflows/auto-assign.yml` (name may differ in workflow file)

- **Purpose:** (If enabled) Automatically labels issues as stale based on custom logic.
- **Configuration:**
  - Edit the workflow file to adjust criteria as needed.

---

## Auto Close Stale Issues
**Workflow:** `.github/workflows/auto-close-stale.yml`

- **Purpose:** Closes issues where the last response was from the assignee and there have been no updates for 7+ days.
- **Schedule:** Runs daily at 5pm EST (22:00 UTC).
- **How it works:**
  1. Finds open issues with no updates for 7+ days after assignee's last response.
  2. Comments to inform the user and closes the issue, adding the `inactive` label.

---

## Auto Comment Assignee Reminder
**Workflow:** `.github/workflows/auto-comment-assignee-reminder.yml`

- **Purpose:** Reminds assignees when a user has responded and the assignee hasn't replied in over 2 business days.
- **Schedule:** Runs daily at 9am EST (14:00 UTC).
- **How it works:**
  1. Finds open issues where the last comment was not from the assignee and it's been more than 2 business days.
  2. Comments on the issue, @mentioning the assignee as a reminder.

---

## Issue Metrics Report
**Workflow:** `.github/workflows/issue-metrics-report.yml`

- **Purpose:** Generates a weekly report of issue metrics, including per-assignee stats.
- **Schedule:** Runs every Monday at 8am EST (13:00 UTC) and can be triggered manually.
- **How it works:**
  1. Calculates open/closed issues, closure percentage, average closure time, and per-assignee metrics.
  2. Posts the report as a comment in a dedicated issue (`📊 Weekly Issue Metrics Report`).

---

## Customization & Maintenance
- Adjust schedules, labels, and user lists as needed in the workflow YAML files.
- Update templates and user lists in `.github/workflows/configurations/`.
- For advanced logic, edit the JavaScript in the `github-script` steps.

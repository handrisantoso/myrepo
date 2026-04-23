---
description: |
  Triages new issues by labeling them by type and priority, identifying duplicates,
  asking clarifying questions when the issue description is unclear, and assigning
  them to the right team members.

on:
  issues:
    types: [opened]
  roles: all

permissions:
  contents: read
  issues: read
  pull-requests: read

tools:
  github:
    lockdown: false
    min-integrity: none
    toolsets: [default]

safe-outputs:
  mentions: false
  add-labels:
    allowed:
      - bug
      - feature
      - enhancement
      - question
      - documentation
      - security
      - duplicate
      - needs-more-info
      - priority:critical
      - priority:high
      - priority:medium
      - priority:low
    max: 5
  add-comment:
    max: 2
    hide-older-comments: true
  update-issue:
    max: 1
---

# Issue Triage

Triage the newly opened issue #${{ github.event.issue.number }}: "${{ github.event.issue.title }}"

## Your Tasks

Perform ALL of the following steps in order:

### 1. Label by Type

Read the issue title and body carefully, then add one or more appropriate type labels:

- `bug` — Something isn't working as expected; unexpected behavior or error
- `feature` — Request for new functionality that does not currently exist
- `enhancement` — Improvement or extension of existing functionality
- `question` — A question, request for help, or clarification
- `documentation` — Relates to docs, README, guides, or in-code comments
- `security` — Security vulnerability, exposure, or hardening request

### 2. Label by Priority

Add exactly one priority label based on impact and urgency:

- `priority:critical` — Blocking functionality, data loss, or security vulnerability; needs immediate attention
- `priority:high` — Significantly impacts users or core functionality; should be addressed soon
- `priority:medium` — Moderate impact; normal priority for the backlog
- `priority:low` — Minor issue, cosmetic, or nice-to-have improvement

### 3. Detect Duplicates

Search existing open issues for similar topics or the same root cause. Use the GitHub search tools to find issues with similar keywords, titles, or symptoms.

- If you find a likely duplicate: add the `duplicate` label and post a comment mentioning the duplicate issue(s) with a brief explanation of why they appear to be the same.
- If no duplicate is found: continue to step 4.

### 4. Ask Clarifying Questions (if needed)

Evaluate whether the issue has sufficient detail to be actionable. Post a comment asking for missing information ONLY when genuinely needed:

- **For bugs**: Are steps to reproduce present? Expected vs. actual behavior? Version/environment info?
- **For features/enhancements**: Is the use case and desired outcome clearly described?
- **For questions**: Is the question clear enough to answer without guessing?

If the description is unclear or incomplete, add the `needs-more-info` label and post a single, concise comment listing the specific information needed. Be friendly and constructive.

If the description is already clear and complete, skip this step entirely.

### 5. Assign to Team

Based on the issue type, content, and any area-specific keywords (e.g., component names, file paths, subsystems), assign the issue to the most appropriate team member(s) using the `update-issue` safe output.

- Look at recent contributors to related areas using your knowledge of the repository
- Assign up to 2 people if the issue spans multiple areas
- If you cannot determine the right assignee from the available context, skip this step

## Guidelines

- Be concise, professional, and friendly in all comments
- Always apply at least one type label and one priority label
- Only comment if you have something meaningful to say (duplicate found, or clarification genuinely needed)
- Do not add labels not in the allowed list above

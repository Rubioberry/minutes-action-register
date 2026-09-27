---
name: minutes-action-register
description: "Extracts an action register from draft or approved minutes: motions, vote results if stated, owners, due dates, and open follow-ups. Use after a council, board, or committee meeting when staff must track what was actually decided. Does not amend the official minutes or notify owners."
license: MIT
compatibility: Claude, Codex, Cursor, OpenCode, Lovable
allowed-tools: Read
inputs:
  - name: source
    type: text
    required: true
    description: Draft or approved minutes, or a clerk’s running notes from the session
outputs:
  - name: artifact_markdown
    type: markdown
    description: Action register
  - name: artifact_json
    type: json
    description: motions, followups, unresolved
side_effects: none
touches:
  - user_input
permissions:
  network: deny
  files: deny
  workspace: read
  secrets: deny
---

# Minutes Action Register

## When to use
Use after a meeting, when minutes or running notes must become a list of decisions and follow-ups.

## Workflow
1. Read only the provided source.
2. Record body, date, and whether the source says draft or approved.
3. For each motion: text, mover/seconder if named, result if named, owner of next staff work.
4. List follow-ups that were assigned but not voted.
5. List items discussed with no motion.
6. Copy due dates only when they appear. Do not invent vote counts.

## Input
Minutes or clerk notes. Include the body name if known.

## Output
Register: Session, Motions, Follow-ups, Discussed-no-action.
JSON: session, status, motions[], followups[], unresolved[].

## Guidelines
- If a vote is not in the source, result is "not recorded."
- Do not tidy motion language so much that the meaning changes.
- This skill does not publish minutes or email assignees.

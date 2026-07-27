# Issues

This file tracks lightweight project issues. Implemented items stay here until the user explicitly asks to clean them up or approves a cleanup suggestion.

## Active Issues

## I-001 Preserve verified export results

Status: implemented
Area: Export / history
Source: 2026-07-20 review
Updated: 2026-07-21

Problem:
Failed reruns used to overwrite the last verified export result.

Decision:
Keep the previous verified result visible and show the new failure separately.

Acceptance:
- A failed rerun does not replace the last verified result.

Verification:
- Verified with focused export history tests.

## I-002 Clarify settings labels

Status: open
Area: UI / settings
Source: 2026-07-22 discussion
Updated: 2026-07-22

Problem:
Two settings actions use labels that are difficult to distinguish.

Decision:
TBD

Acceptance:
- Each action has distinct wording that explains its outcome.

Verification:
- pending

## I-003 Show all import conflicts

Status: implemented
Area: Import / preview
Source: 2026-07-23 review
Updated: 2026-07-24

Problem:
The preview stopped after the first blocking conflict.

Decision:
Show every blocking conflict found in one scan.

Acceptance:
- All blocking conflicts appear in the preview.

Verification:
- Verified with import preview integration tests.

## I-004 Add metadata validation

Status: ready
Area: Import / metadata
Source: 2026-07-25 discussion
Updated: 2026-07-25

Problem:
Imported originals do not yet have a verified content hash.

Decision:
Validate and persist the original file hash during import.

Acceptance:
- Import tests verify the stored hash against the original file.

Verification:
- pending

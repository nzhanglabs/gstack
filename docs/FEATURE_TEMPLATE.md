# Mobile Feature Template

Use this template before building a meaningful mobile feature.

## Feature Name

Short feature name:

## One-Sentence Goal

Describe the feature in one sentence.

Example:

`Users can create a reminder that fires at a chosen time and opens the app to the relevant item.`

## User Problem

- Who is this for?
- What problem are they feeling right now?
- Why does this matter now?

## Success Criteria

Keep this short and testable.

- user can
- user can
- user sees
- state survives
- failure path is understandable
- analytics event fires

## Scope

### In Scope

- 
- 
- 

### Out Of Scope

- 
- 
- 

## Primary User Flow

Describe the happy path step by step.

1. 
2. 
3. 
4. 

## Edge Cases

List the likely failure or edge cases.

- no network
- empty state
- permission denied
- stale session
- background/resume interruption
- duplicate submit

## Screens And Navigation

- entry point:
- screens involved:
- exit point:
- tab or stack impact:

## Data And State

- data source:
- local state:
- persisted state:
- sync or offline concerns:

## Permissions Or Device Capabilities

If applicable:

- notifications
- camera
- photo library
- location
- contacts
- microphone

## Analytics

List the events worth capturing.

- 
- 
- 

## QA Checklist

- happy path works
- loading state works
- empty state works
- error state works
- iOS tested
- Android tested
- background/resume tested
- one edge case tested

## Review Plan

- Run `gstack-plan-ceo-review` if scope is fuzzy or expanding.
- Run `gstack-plan-eng-review` if implementation has technical risk.
- Run `gstack-plan-design-review` if the UX is central to success.
- Run `gstack-review` before merge.

## Definition Of Done

- core user outcome works
- states are complete
- iOS tested
- Android tested
- review completed
- docs updated if behavior changed

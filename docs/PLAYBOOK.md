# Mobile App Playbook

This playbook is a concrete operating guide for building and shipping an iPhone/Android app with `gstack` and Codex.

Assumptions:
- React Native + Expo
- Solo founder or very small team
- Shipping to both iOS and Android
- Using `gstack` as the planning, review, QA, and release layer

## Core Rules

- Build in vertical slices, not layers.
- Every feature must have one primary user outcome.
- No feature is done until it has loading, empty, and error states.
- Test every meaningful feature on iOS and Android.
- Run `gstack-review` before every meaningful merge.
- Ship betas early and tighten with real usage.

## Weekly Cadence

### Monday

- Pick the next feature slice.
- Run `gstack-office-hours` or `gstack-autoplan` if scope is still fuzzy.
- Write short success criteria before coding starts.

### Tuesday to Thursday

- Implement one vertical slice at a time.
- Test continuously on iPhone simulator and Android emulator.
- Use a physical device when the feature touches permissions, notifications, camera, auth, or gestures.
- Run `gstack-review` before the slice is considered complete.

### Friday

- Run a release-candidate QA pass.
- Run `gstack-ship` for anything ready to land.
- Update docs with `gstack-document-release`.
- Run `gstack-retro` after meaningful shipping weeks.

## Planning Workflow

Use the planning skills before writing code for anything substantial.

### `gstack-office-hours`

Use when the feature or product idea is still fuzzy.

Goal:
- define the user
- define the pain
- define the narrowest useful version of the feature

### `gstack-plan-ceo-review`

Use when scope is drifting or the app idea is too broad.

Goal:
- challenge scope
- find the sharpest version of the feature
- decide what belongs in v1 vs later

### `gstack-plan-eng-review`

Use before features with meaningful technical complexity.

Examples:
- auth
- notifications
- offline state
- persistence
- payments
- background sync
- navigation changes

Goal:
- lock architecture and edge cases before implementation

### `gstack-plan-design-review`

Use before important user-facing flows.

Examples:
- onboarding
- home screen
- create/edit flow
- subscription or paywall
- settings

Goal:
- strengthen UX before code hardens

### `gstack-autoplan`

Use when you want the planning pipeline combined in one pass.

## Feature Playbook

Use this for every real feature.

### 1. Define the feature in one sentence

Example:

`Users can create a reminder that fires at a chosen time and opens the app to the relevant item.`

### 2. Write success criteria before coding

Keep the list short and testable.

Example:
- user can create it
- user can edit it
- confirmation is shown
- state survives app restart
- error paths are understandable
- analytics event fires

### 3. Run the right planning skill

Pick the lightest skill that clarifies the work:
- `gstack-office-hours` for fuzzy scope
- `gstack-plan-ceo-review` for scope control
- `gstack-plan-eng-review` for technical risk
- `gstack-plan-design-review` for UX-heavy work

### 4. Create a feature branch

Examples:
- `feature/reminders-v1`
- `feature/onboarding-pass-2`
- `fix/android-notification-permissions`

### 5. Build in this order

For most mobile features:
- route or screen shell
- state and data model
- happy-path UI
- loading state
- empty state
- error state
- analytics
- permission handling if needed
- tests for tricky logic

### 6. Test during development

Do not wait until the end.

Minimum:
- iPhone simulator
- Android emulator

Also test on a physical device when needed.

### 7. Run `gstack-review`

Run it before opening or merging the PR.

Severity guide:
- P1/P2: fix before merge
- P3: fix now or explicitly defer

### 8. Run manual feature QA

Minimum checklist:
- fresh app launch
- navigate to feature from normal entry point
- complete the happy path
- trigger at least one failure path
- background and resume the app
- verify both platforms

### 9. Merge only when the feature is usable

Usable means:
- primary flow works
- states are complete
- feature is reviewed
- feature is tested
- docs are updated if behavior changed

## Definition Of Done

A feature is done only if all of these are true:

- primary user flow works
- loading, empty, and error states exist
- iOS tested
- Android tested
- `gstack-review` run
- analytics or crash implications considered
- docs updated if behavior or setup changed
- no core-flow TODOs are being hidden for later

## Bugfix Playbook

Use this when something is broken.

### 1. Reproduce the bug clearly

Write:
- what the user did
- what happened
- what should have happened
- platform and OS if relevant
- whether it reproduces consistently

### 2. Run `gstack-investigate`

Use it before patching if the bug is non-trivial.

Especially for:
- startup issues
- auth/session problems
- stale state
- race conditions
- notifications
- background or foreground bugs
- platform-specific failures

### 3. Narrow the fix

Avoid broad refactors unless the investigation proves they are necessary.

### 4. Re-test the exact repro path

Then test one nearby edge case before merging.

### 5. Run `gstack-review` if the fix touches important code

Especially:
- auth
- persistence
- navigation
- notifications
- subscriptions
- API contracts

### 6. Add regression protection where practical

That might be:
- a unit test
- a small integration test
- a written QA regression item if automation is not realistic yet

## Release Playbook

Use this when preparing a beta or production release.

### 1. Freeze feature scope

Only bugfixes and release polish after this point.

### 2. Run a release review pass

Run `gstack-review` on the release branch or final diff.

### 3. Run the release QA checklist

Always test:
- fresh install
- signup/login
- returning user session restore
- main app loop
- logout
- app background/resume
- flaky network
- denied permissions
- deep links if used
- push-notification entry path if used
- small and large screen layouts
- iOS and Android both

### 4. Use `gstack-browse` for web-adjacent surfaces

Use it for:
- auth callback pages
- admin tools
- dashboards
- marketing site
- support tools

### 5. Build and distribute

Typical flow:
- Expo EAS build
- TestFlight upload
- Play internal testing upload

### 6. Verify release health

Check:
- crash reporting is live
- analytics events are arriving
- auth hits the correct environment
- notifications behave correctly
- startup is healthy

### 7. Run `gstack-document-release`

Update:
- release notes
- setup docs
- behavior docs
- known issues if needed

### 8. Run `gstack-retro`

Capture:
- what slowed shipping down
- what bugs escaped
- what should become part of the standing checklist

## Skill Map

Use this quick mapping during day-to-day work:

- `gstack-office-hours`: sharpen the product idea
- `gstack-plan-ceo-review`: tighten scope
- `gstack-plan-eng-review`: lock implementation decisions
- `gstack-plan-design-review`: improve UX before building
- `gstack-autoplan`: combine planning into one pass
- `gstack-investigate`: debug before patching
- `gstack-review`: pre-merge risk review
- `gstack-qa`: structured release-candidate bug hunt
- `gstack-browse`: test web/admin/auth surfaces around the app
- `gstack-ship`: make the branch landable
- `gstack-document-release`: keep docs aligned with reality
- `gstack-retro`: improve the process after shipping

## Suggested Repo Structure

```text
app/
components/
features/
services/
hooks/
lib/
docs/
  architecture/
  product/
  releases/
```

Prefer feature-oriented modules that keep screens, logic, and tests close together.

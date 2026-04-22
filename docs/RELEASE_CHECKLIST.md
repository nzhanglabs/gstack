# Mobile Release Checklist

Use this checklist for beta and production releases of a React Native + Expo mobile app.

## Scope Freeze

- Confirm the release scope is frozen.
- Move any non-critical feature work out of the release.
- Document known risks and intentional deferrals.

## Review

- Run `gstack-review` on the release branch or final diff.
- Fix all P1 and P2 issues before release.
- Resolve or explicitly defer lower-priority findings.

## Core App QA

- Fresh install works.
- App launches cleanly.
- Signup works.
- Login works.
- Returning session restores correctly.
- Logout works.
- Main user loop works end to end.
- Loading, empty, and error states appear correctly.

## Mobile Platform QA

- iOS simulator tested.
- Android emulator tested.
- At least one physical device tested for risky features.
- Small-screen layout verified.
- Large-screen layout verified.
- Background and resume flow verified.
- App handles slow or flaky network reasonably.

## Permissions And Device Features

If the release touches any device feature, verify each relevant path.

- First-time permission prompt works.
- Denied permission path is understandable.
- Returning from system settings works.
- Camera or photo flow works if applicable.
- Notification permission flow works if applicable.
- Location flow works if applicable.

## Notifications And Deep Links

If the release uses notifications or deep links:

- Notification scheduling works.
- Notification open path lands on the correct screen.
- Duplicate notifications are not created unexpectedly.
- Deep link opens the correct destination.
- Deep link failure path is safe.

## Web-Adjacent Surfaces

Use `gstack-browse` when these exist:

- auth callback pages
- admin or dashboard flows
- marketing site
- support tools
- billing portal

Verify:
- routing works
- copy matches the shipped behavior
- no obvious browser-side breakage

## Observability

- Crash reporting is live.
- Analytics events are arriving.
- Environment is correct for the release target.
- Logging or monitoring is sufficient to detect release regressions.

## Build And Distribution

- Expo EAS build completed successfully.
- iOS build uploaded to TestFlight.
- Android build uploaded to the correct Play testing track.
- Release notes are attached where needed.

## Docs

- Run `gstack-document-release`.
- Update release notes.
- Update setup or behavior docs if the app changed.
- Record any known issues.

## Final Go/No-Go

- Critical flows verified.
- Critical findings resolved.
- Release artifacts built and distributed.
- Docs updated.
- Rollback or mitigation plan is understood if something breaks.

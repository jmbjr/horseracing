# Horse Racing Iteration Workflow

This project uses small, testable iterations. Each iteration implements one GitHub issue, publishes it to the existing game, and pauses for hands-on player review before the next issue begins.

## Principles

1. **One issue at a time.** Do not bundle unrelated behavior changes.
2. **Easy changes first.** Rank work by implementation complexity, risk, and dependencies.
3. **Pass-the-phone first.** Use local play as the fastest primary test loop whenever the feature applies there.
4. **Test the affected mode.** Online-specific behavior also receives a short separate-phone smoke test.
5. **The player approves the result.** Deployment is not acceptance.
6. **Fix before advancing.** Feedback stays within the active issue until it is approved.
7. **Close only after approval.** Then begin the next ranked issue.

## Iteration Lifecycle

### 1. Select

- Choose the easiest unblocked issue.
- Identify dependencies and affected modes.
- Restate the intended behavior and acceptance criteria.

### 2. Implement

- Change only what the active issue requires.
- Preserve pass-the-phone and online behavior unless the issue intentionally changes them.
- Keep saved-game and room-state compatibility in mind.
- Update the offline cache version when production assets change.

### 3. Verify

- Check JavaScript syntax and configuration files.
- Exercise the changed rule or UI state.
- Check narrow Android layout and touch targets.
- Verify that unrelated game rules still behave normally.

### 4. Publish

- Commit the focused change to `main`.
- Allow GitHub Pages to deploy it.
- Verify that the live page contains the new version.
- Tell the tester if the installed PWA must be refreshed or reopened.

### 5. Player Test

Use this order when applicable:

1. Pass-the-phone test.
2. Installed Android/PWA test.
3. Separate-phone multiplayer smoke test.
4. Refresh or reconnect test when shared state changed.

Record what was tested, what happened, and any adjustment requested.

### 6. Review Gate

The tester chooses one outcome:

- **Approved:** close the issue and select the next ranked issue.
- **Adjust:** keep the issue open, implement the requested correction, and repeat the test.
- **Reconsider:** pause implementation and revise the issue or its acceptance criteria.

## Per-Issue Checklist

Copy this checklist into an issue comment when implementation begins:

```markdown
## Iteration checklist

- [ ] Scope and acceptance criteria confirmed
- [ ] Dependencies resolved
- [ ] Focused implementation complete
- [ ] Syntax/configuration checks pass
- [ ] Pass-the-phone behavior tested
- [ ] Android/PWA layout tested
- [ ] Online multiplayer smoke-tested, if applicable
- [ ] Published to GitHub Pages
- [ ] Live version verified
- [ ] Player review received
- [ ] Requested adjustments completed
- [ ] Player approved
- [ ] Issue closed
```

## Current Ranked Queue

| Order | Issue | Estimated complexity | Dependency note |
|---:|---|---|---|
| 1 | #2 Highlight ticket-matching horses | Easy | None |
| 2 | #1 Always display compact tickets | Easy | Complements #2 |
| 3 | #3 Show actual spaces per horse | Easy–medium | None |
| 4 | #6 Duplicate-scratch behavior toggle | Medium | None |
| 5 | #5 Configurable scratch multipliers | Medium | Shared setup/state work |
| 6 | #7 Dynamic deck scaling | Medium–high | Defines scalable dealing and payout |
| 7 | #4 Configurable chips, bet, and cards | High | Cards-per-player depends on #7 |

Re-rank this table whenever a new issue introduces a dependency or materially changes complexity.

## Definition of Done

An issue is done only when:

- its acceptance criteria are satisfied;
- the live GitHub Pages version is verified;
- the relevant play mode has been tested;
- the player explicitly approves the result; and
- the GitHub issue is closed.

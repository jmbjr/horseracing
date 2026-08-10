# Game Project Blueprint Template

Use this document to start a mobile-first tabletop-style web game with a documentation-first, issue-driven development process. Replace every `<placeholder>` and delete sections that genuinely do not apply.

This template defines the project method. It does not define a particular game's rules.

## 1. Project identity

| Field | Value |
|---|---|
| Working title | `<game title>` |
| Repository | `<owner/repository>` |
| Public URL | `<deployment URL>` |
| Product owner | `<name>` |
| Primary device | `<for example: Android phone>` |
| Reference projects | `<repositories or products to inspect>` |
| Current phase | `<discovery / alpha / beta / released>` |

### Originality and intellectual-property boundary

- Describe the genre and mechanical inspirations: `<inspirations>`.
- Create original branding, terminology, artwork, writing, and visual presentation.
- Do not copy another product's rulebook text, assets, logo, or distinctive trade dress.
- Record which ideas are generic mechanics and which elements must be redesigned.
- Document licenses and attribution for every third-party asset or library.

## 2. Product vision

### One-sentence pitch

`<Who plays, what they do, and why it is enjoyable.>`

### Audience

- Primary players: `<audience>`
- Typical group size: `<minimum–maximum>`
- Typical session length: `<duration>`
- Expected rules familiarity: `<none / casual / expert>`
- Accessibility considerations: `<needs>`

### Design principles

Rank a small set of principles, such as:

1. Phone-readable at a glance.
2. A playable local mode exists before network complexity.
3. Advanced configuration stays out of the normal path.
4. Game state survives refreshes and reconnections.
5. Rules are deterministic, testable, and separate from presentation.
6. Shared identity uses permanent IDs rather than display names.
7. Experimental data cannot silently contaminate ordinary statistics.

### Success criteria

- `<measurable product criterion>`
- `<measurable usability criterion>`
- `<measurable reliability criterion>`
- `<measurable performance criterion>`

## 3. Documentation package

Create these documents before or alongside the first implementation. Existing products should reverse-engineer current behavior and explicitly list contradictions.

### `PRODUCT_REQUIREMENTS.md`

Include:

- Vision, audience, and principles
- Supported devices and browsers
- Functional requirements
- Nonfunctional requirements
- Accessibility
- Performance targets
- Alpha scope
- Deferred scope
- Acceptance criteria

### `GAME_RULES.md`

Include:

- Objective
- Components
- Setup
- Turn or round sequence
- Legal and illegal actions
- Costs, rewards, penalties, and scoring
- End conditions
- Tie handling
- Randomness
- Edge cases
- Worked examples
- Precise rule-engine definitions

Never leave a UI developer to infer rules from screen mockups.

### `USER_GUIDE.md`

Include:

- Starting every game mode
- Creating/selecting players
- Joining and rejoining
- Taking a turn
- Ending, pausing, resuming, or abandoning a game
- Every game option in plain language
- History and statistics
- Troubleshooting
- Hosting/backend setup where relevant

### `GAME_MODES_AND_OPTIONS.md`

For every mode and option record:

| Attribute | Description |
|---|---|
| Name | User-facing name |
| Purpose | Why it exists |
| Default | New-game value |
| Valid range | Accepted values |
| Storage field | Schema location |
| Editable phase | When it may change |
| Lock behavior | What happens after starting |
| Rule effect | How gameplay changes |
| Statistics effect | How records are classified |
| Compatibility | Behavior when older data lacks it |

### `UX_DESIGN.md`

Include:

- Screen inventory
- Navigation and back behavior
- Phone-width layout
- Touch-target requirements
- Visual tokens
- Information hierarchy
- At-a-glance state
- Loading and empty states
- Errors and recovery
- Paused/disconnected/expired/completed states
- Accessibility labels
- Color-independent cues
- Charts, tables, and overflow behavior

### `ARCHITECTURE.md`

Include:

- Deployment topology
- Application modules
- Pure rule engine
- UI/rendering boundary
- Local persistence
- Online synchronization
- Identity/session ownership
- CPU/automation scheduling
- Statistics pipeline
- Idempotent writes
- Offline retry
- Service-worker/cache policy
- Schema migration strategy
- Known technical debt

### `DATA_MODEL.md`

For every entity or collection document:

- Stable identifier
- Schema version
- Required and optional fields
- State transitions
- Timestamps
- Ownership and permissions
- References to other entities
- Idempotency key
- Historical fallback behavior
- Retention/deletion behavior

### `BACKEND_SETUP.md`

Include:

- Account/project creation
- Authentication mode
- Database collections
- Complete development rules
- Production security considerations
- Authorized domains
- Deployment setup
- How to append rules safely
- Common permission/connectivity errors
- Clear separation between public configuration and secrets

Rename this document for the selected backend, such as `FIREBASE_SETUP.md`.

### `TEST_PLAN.md`

Include:

- Pure rule tests
- Scoring/economy tests
- State-transition tests
- Local multiplayer
- Multi-device synchronization
- Rejoin/session displacement
- CPU behavior
- Pause/expiry
- Idempotency and retry
- Statistics correctness
- Simulations/experiments
- Mobile layout
- Accessibility
- Cache upgrades
- Backward compatibility

### `ROADMAP.md`

Separate:

- Completed capabilities
- Current milestone
- Ready backlog
- Features needing refinement
- Experimental work
- Deferred/post-alpha work

### `DECISIONS.md`

Use a lightweight decision record:

```markdown
## DEC-<number>: <decision>

- Date: <YYYY-MM-DD>
- Status: proposed | accepted | superseded
- Context: <problem and constraints>
- Decision: <chosen direction>
- Alternatives: <options considered>
- Consequences: <benefits, costs, follow-up>
```

## 4. Rules-discovery checklist

Before implementation, answer:

- What exactly constitutes game setup?
- What information is public, private, or hidden?
- Who acts, and in what order?
- Can multiple players react to one event?
- What actions are optional versus mandatory?
- How is legality determined?
- What resources can reach zero or a maximum?
- What happens when a player cannot pay or act?
- What ends a turn, round, match, or campaign?
- How are winners, ties, and no-winner outcomes handled?
- Which choices are strategic versus random?
- Which rules are configurable?
- Which settings must be snapshotted into history?
- Which ambiguities materially change implementation?

Ask the product owner only about material choices. Recommend defaults for minor details and record them.

## 5. Recommended game modes

Use only the modes that fit the game.

### Pass the phone

- First playable and primary test harness
- One device owns all local state
- Clearly handle private information before passing
- Resume safely after refresh

### Separate phones

- Short room code or invitation link
- Shared authoritative state
- Permanent player profiles
- Seat reclaim after refresh/disconnection
- Clear host-only versus any-player actions
- Concurrency-safe turns

### CPU players

- Permanent profiles marked Human or CPU
- Legal, deterministic/testable decision policy
- Configurable action delay
- CPU ownership rules for online rooms
- No CPU action while paused

### Durable simulation

- Uses production rules
- Saves normal history when explicitly intended
- Tags every simulated game/run
- One durable run summary
- Progress, stop, interruption, and retry behavior

### Experimental lab

- High-speed in-memory trials
- Seeded randomness
- No individual production-statistics writes
- Aggregate results and confidence measures
- Optional summary persistence
- Engine/model version recorded

## 6. Mobile UX baseline

- Optimize first for `<target viewport>`.
- Use minimum `<touch target>` controls.
- Keep the primary action reachable without horizontal scrolling.
- Put advanced settings inside a collapsed section.
- Show the current actor, phase, instruction, and important resources together.
- Do not rely on color alone.
- Give every icon and chart value an accessible text equivalent.
- Prefer horizontal bars for long labels.
- Preserve readable labels instead of shrinking an entire interface.
- Show exact values alongside visual charts.
- Define safe-area behavior for installed/mobile display modes.

### Visual-language specification

Record:

| Token | Definition |
|---|---|
| Background | `<color/material>` |
| Primary surface | `<color/material>` |
| Primary action | `<color/style>` |
| Secondary action | `<color/style>` |
| Destructive action | `<color/style>` |
| Display type | `<font/fallback>` |
| Body type | `<font/fallback>` |
| Corner radii | `<values>` |
| Shadows | `<values>` |
| Spacing scale | `<values>` |
| Status patterns | `<patterns/icons/text>` |

## 7. Engineering baseline

### Rule engine

- Prefer pure functions with explicit inputs and outputs.
- Inject randomness or use a seeded generator.
- Keep DOM, network, clock, alerts, and storage out of rule calculations.
- Version material rules/model changes.

### Identity

- Use permanent IDs as identity.
- Treat names as editable display data.
- Never merge statistics solely by name.
- Record historical names only when needed.

### State and persistence

- Separate durable game state from transient UI state.
- Give every game and completed result a unique ID.
- Snapshot effective settings into the game/result.
- Make completion writes idempotent.
- Queue safe retries without double counting.
- Define old-schema defaults explicitly.

### Online synchronization

- Define the authoritative document/state.
- Validate actor, seat, session, phase, and revision transactionally.
- Prevent stale clients from overwriting newer state.
- Define rejoin/session displacement.
- Stop automated actions during pause or ownership loss.

### Static deployment and PWA

- Keep the first version compatible with static hosting where practical.
- Version the service-worker cache on every published application update.
- Remove obsolete caches during activation.
- Document refresh/update behavior.
- Do not let a stale shell silently mix with a newer schema.

## 8. Security and privacy checklist

- What can anonymous users read and write?
- Is the application family/private-by-convention or truly access-controlled?
- Which destructive actions require a password or stronger authentication?
- Is a client-visible family password acceptable for the threat model?
- Are private cards/information exposed in shared documents?
- Are secrets absent from the static repository?
- Are exports explicit user actions?
- Are deletion targets narrow, confirmed, and recoverable where practical?

Document limitations honestly.

## 9. GitHub issue template

```markdown
# <Issue title>

## Goal

<User-visible outcome.>

## Approved behavior

- <Requirement>

## User experience

- <Screens, actions, and feedback>

## Rules and data

- <Rule effects>
- <Schema/state effects>

## Edge cases

- <Failure/concurrency/compatibility cases>

## Acceptance criteria

- [ ] <Observable test>

## Staged phone test

1. <Small verification sequence>

## Dependencies

- <Related issues/documents>
```

## 10. Ranking and iteration method

Rank open work using:

1. Clarity: Is behavior fully defined?
2. Complexity: How many systems change?
3. Risk: Can it corrupt shared state or statistics?
4. Testability: Can it be verified quickly in local/pass-phone mode?
5. Dependency value: Does it unlock later work?

Prefer easy, clear, highly testable issues first.

For each iteration:

1. Print or review the issue.
2. Resolve material ambiguities.
3. Implement the smallest coherent change.
4. Validate syntax and targeted behavior.
5. Increment application/cache version.
6. Publish to the repository/static host.
7. Add implementation notes and a focused phone-test checklist.
8. Leave the issue open.
9. Product owner tests on a phone.
10. Close only after explicit approval.
11. Print/refine the next ranked issue.

Do not combine issues unless the product owner approves it or they are inseparable and the reason is documented.

## 11. Release checklist

- [ ] Requirements/issue approved
- [ ] Existing user changes preserved
- [ ] Rule tests pass
- [ ] Syntax/static checks pass
- [ ] Mobile layout checked
- [ ] Online concurrency considered
- [ ] Historical data compatibility checked
- [ ] Statistics remain idempotent
- [ ] Backend rules documented if changed
- [ ] Service-worker cache version incremented
- [ ] Remote files verified after publish
- [ ] Issue comment includes changes and phone tests
- [ ] Issue remains open pending approval

## 12. Fresh-chat starter prompt

Copy, customize, and give this to a new AI development chat:

```text
I want to build <game title> in <repository URL>.

Use <reference repository URLs> as references for process, architecture, mobile UX, and visual quality. Inspect the repositories and issue history before proposing implementation. Separate reusable platform ideas from game-specific mechanics.

The product must have an original identity. It may be inspired by <genre/mechanics>, but do not copy protected branding, artwork, rulebook language, assets, or distinctive trade dress.

Use a documentation-first process. Before gameplay implementation, draft:

- PRODUCT_REQUIREMENTS.md
- GAME_RULES.md
- USER_GUIDE.md
- GAME_MODES_AND_OPTIONS.md
- UX_DESIGN.md
- ARCHITECTURE.md
- DATA_MODEL.md
- BACKEND_SETUP.md
- TEST_PLAN.md
- ROADMAP.md
- DECISIONS.md
- ITERATION_WORKFLOW.md

The documents must be detailed enough for another developer or AI chat to reproduce the intended product without this conversation.

Architecture and workflow expectations:

- Mobile-first, primarily <target device>
- <static host/PWA expectations>
- Pass-the-phone/local mode first
- Separate-phone multiplayer if applicable
- Permanent player IDs
- Rejoin and persistence behavior
- CPU players if applicable
- Shared statistics/history if applicable
- Pure testable rule functions
- Schema versions and backward-compatible defaults
- Idempotent completed-game/statistics writes
- Seeded, non-persisting experimental simulations where applicable
- Advanced settings hidden from the normal path
- Large touch controls and accessible, color-independent state

After I approve the documents:

1. Commit them to the repository.
2. Create and rank GitHub issues by clarity, simplicity, risk, and testability.
3. Implement one staged issue at a time unless I approve combining them.
4. Validate and publish each build.
5. Increment the service-worker cache version.
6. Leave issues open while I test on my phone.
7. Close issues only after explicit approval.

In your first response:

1. Confirm repository access.
2. Summarize reusable findings from the references.
3. Identify only the material unresolved product/rule decisions.
4. Propose the documentation plan.
5. Do not implement gameplay yet.
6. Ask the minimum questions needed to draft authoritative requirements.
```

## 13. Project-specific additions

Add anything the generic template does not cover:

- `<special hardware or input>`
- `<unusual privacy requirement>`
- `<campaign/progression>`
- `<monetization>`
- `<localization>`
- `<analytics>`
- `<content pipeline>`
- `<custom simulation or balancing needs>`

Keep this section project-specific; improve the generic template separately when a lesson applies broadly.

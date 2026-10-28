# V1 Implementation Plan

Deliver the requirements in [PRD.md](./PRD.md) through six milestones. Complete interface agreements and a working foundation before splitting feature delivery across developers.

## Milestone 1 Define interfaces and ownership

Review the template's example features to identify the coding and testing conventions developers should follow. Keep those examples available until the first polling journey can replace them as the reference.

Agree on the shared contracts that connect organizer, participant, and presentation experiences:

- Poll and question definitions, supported answers, validation, and Draft → Open → Closed transitions.
- Organizer access, browser participation, check-in, unfinished drafts, and accepted answers as distinct concepts.
- Poll management, joining, submission, live controls, and result retrieval: their inputs, outcomes, permissions, and failure states.
- The current live stage, how views learn about changes, and how they recover after reconnecting.
- Information available to each audience, including when results become visible and where check-in data must remain private.

Assign one owner to the shared contracts and core rules, including live state transitions, answer acceptance, and result visibility. Assign a delivery owner to each workstream. These are responsibilities, not required headcount; one developer may fill several roles.

**Success criteria:** Developers share a short interface reference, representative examples, and acceptance scenarios derived from the PRD. Ownership and dependencies are explicit. Decisions needed for the foundation are resolved, including what happens when submission overlaps closure or a retry follows an uncertain result. Architectural decisions are recorded in the existing documentation system.

## Milestone 2 Build and prove the foundation

**Depends on:** Milestone 1.

Adapt the boilerplate into the polling application while retaining useful infrastructure and conventions. Establish the application shell, persistent storage, designated organizer access, browser participation, shared validation and lifecycle rules, and separate access to organizer and participant information. Establish development, testing, and deployed preview environments with isolated test data and working verification gates.

Prove one complete journey: the organizer creates and opens an anonymous asynchronous poll with one multiple-choice question; a participant submits; the organizer sees the saved result and closes the poll.

Once that journey provides working examples of the repository's patterns, remove stale template features, sample data, placeholder assets, and their obsolete tests. Retain and adapt the reusable UI, authentication, database, and testing infrastructure. Update documentation and test references to use the polling application as the new example. Commit this cleanup separately; the original examples remain available in Git history.

**Success criteria:** The journey works in the deployed preview using real persistence. Refresh and restart preserve accepted data; retries do not duplicate it; closure rejects new answers; unauthorized access is rejected. Template examples have been replaced by documented application examples, and verification passes after cleanup. The shared interfaces and representative test data are available to other developers. Complete the cleanup before parallel feature delivery begins.

## Milestone 3 Deliver features in parallel

**Depends on:** Milestone 2. Each workstream uses the shared foundation and contracts.

| Workstream | Responsibility | Success criteria |
| --- | --- | --- |
| Organizer experience | Complete poll authoring for all question types, editing restrictions, opening, confirmed closure/deletion, duplication, link/QR sharing, and organizer account recovery. | The organizer can manage the complete poll lifecycle, reuse a poll without copying participant data, share access, and recover their account through delivered email. |
| Participant experience | Shared question inputs, anonymous/check-in entry, asynchronous completion and draft restoration, submission feedback, and live answering using the live-stage contract. | All answer types and entry modes work. Drafts remain separate from accepted responses. Refresh, retry, validation, and closed-poll states follow the PRD. |
| Live session coordination | Host controls, authoritative question/reveal stages, state updates, late arrivals, and recovery after organizer or participant disconnection. | One consistent live stage governs all views. Host disconnection preserves it; closing a question prevents further answers; reconnection catches up. |
| Results and presentation | Counts, percentages, averages and text results; audience-specific visibility; asynchronous result access; passive presentation view. | Results reflect accepted answers only. Participant and projector views expose only permitted information, and the presentation view creates no participation or response. |

Workstream owners implement against the agreed interfaces. The owner of the shared contracts coordinates changes to common rules, data definitions, and shared components. Agree and update affected consumers before merging an interface change. Temporary fixtures can unblock interface work but do not establish completion of a working journey.

**Success criteria:** Each workstream supplies reviewed, tested increments using the common foundation. It identifies its remaining integration dependencies and provides the evidence needed for Milestone 4.

## Milestone 4 Integrate complete journeys

**Begins during Milestone 3** as compatible increments become ready. Merge small working changes continuously and use two explicit integration checkpoints:

1. **Asynchronous checkpoint:** Combine organizer management, sharing, participation, and results. Run all question types with both entry modes and both result settings. Verify draft restoration, completion, duplication, closure, and deletion together.
2. **Live checkpoint:** Combine live controls, shared question inputs, results, and the presentation view. Run a session from waiting room through question answering, reveal or skip, and confirmed ending. Exercise late joins, refreshes, and host/participant reconnects across separate browsers.

The engineering lead owns integration and resolves changes that cross workstream boundaries. Each checkpoint uses the deployed preview and real shared services.

**Success criteria:** Both checkpoints pass in one integrated application. Every PRD acceptance criterion has an implemented journey and a named verification owner. No journey relies on stand-in data or a temporary interface.

## Milestone 5 Verify release quality

**Depends on:** Both Milestone 4 checkpoints.

Review the integrated application against the full PRD. Extend the checks introduced in earlier milestones to cover simultaneous submissions, repeated retries, submission near closure, hidden-result access, safe display of participant text, deletion, and data continuity after restart. Verify mobile and keyboard use and readable presentation output.

Exercise the supported limit of 10 questions and 100 simultaneous participants, including the two-second live-update target under normal connectivity. Verify that counts and stored answers remain correct under this load.

**Success criteria:** Existing repository verification gates and all PRD acceptance scenarios pass against the release candidate. Evidence is tied to that revision. No unresolved defect violates access boundaries, loses or duplicates accepted data, or prevents a required journey. Remaining minor issues have an owner and an explicit disposition.

## Milestone 6 Release and rehearse operation

**Depends on:** Milestone 5.

Prepare the production environment, organizer account, recovery email, and deployment configuration. Assign an operational owner, enable useful error visibility without exposing participant content, and document deployment, recovery, and support procedures. Rehearse restoring data and recovering from an unsuccessful release before launch.

Run a full rehearsal with a phone, organizer browser, and projected presentation view. Keep rehearsal responses separate from real participation by creating a fresh poll. After deployment, repeat the critical joining, submission, results, and organizer-access checks.

**Success criteria:** The product owner accepts the V1 journeys; recovery has been exercised; the operational owner can diagnose failures and restore service; and production checks pass. The released revision and verification evidence are recorded.

## Delivery discipline

The dependency order is **1 → 2 → parallel workstreams in 3, with rolling integration in 4 → 5 → 6**. Parallelize only work whose inputs and interfaces are ready. If staffing is limited, deliver the same workstreams sequentially without skipping their integration checkpoints.

Commit each coherent change as it is completed and verified. Keep changes to shared interfaces and their affected consumers consistent, update relevant documentation alongside behavior changes, and leave the integration branch usable. Track work against these milestone outcomes and the PRD rather than adding features during implementation.

# Polling App Product Requirements

## Users and access

- **Admin:** One organizer account signs in to create and manage polls, run live sessions, and view all responses and results. Public account registration and team administration are outside scope.
- **Participant:** Anyone with a poll’s link can join without creating an account, subject to its check-in requirement. Participants cannot manage polls, retrieve check-in details, or access results that have not been shared with them.

The organizer account is set up before first use. Only that account can administer polls. The organizer can sign out and recover access through a password-reset link delivered to their registered email address.

## Create and manage polls

The admin can list, view, create, edit, and delete polls. Each poll has a title, ordered questions, a live or asynchronous mode, and an anonymous or check-in participation setting. Asynchronous polls also have a show/hide results setting, defaulting to hidden.

| Question type | Answer |
| --- | --- |
| Text | A free-text answer of 1–2,000 characters, supporting short and longer responses. |
| Number | One finite number, including zero, negatives, or decimals. |
| Multiple choice | Exactly one selection from 2–10 choices supplied by the admin. |

Polls move from **Draft → Open → Closed**. Opening requires a nonblank title, at least one question, nonblank question prompts, and nonblank, distinct multiple-choice options within the stated limits. Questions and settings are editable only in Draft and freeze when opened. Closing requires confirmation that participation will end permanently; running another session requires creating or duplicating a poll. Deleting a poll requires confirmation and removes its responses and check-in data from the product; its link then becomes unavailable.

The admin can duplicate any existing poll. Duplication copies its title, questions, and settings into a new editable Draft with a fresh participant link and no responses or check-in data. The original poll is unchanged.

## Share and present

Each poll has a **Copy participant link** action and a QR code pointing to that same link. The admin can access both before opening the poll and while it is running. Participants using a link before the poll opens see that it has not started.

For live polls, the admin can open a projector-friendly presentation view with large, readable content. It shows joining information, the current question or waiting/ended state, and results only during the admin's reveal step. It updates with the live session and excludes admin controls, check-in details, and unrevealed answers. Opening this view does not create a participant or count as a response.

## Join and answer

- **Anonymous:** No name, email, or other personal details are requested or attached by the app to answers.
- **Check-in:** Name and a validly formatted email are required once per poll. Participants are told that the admin can associate these details with their answers. Check-in does not verify identity or email ownership; there are no custom fields.
- Before answering, participants see whether their answers may be shared. Names and email addresses from check-in never appear in shared results. Text answers may be shared verbatim, so participants should avoid including personal details in them.
- A browser can participate once per poll, with one accepted answer per question. Refreshing, repeated clicks, and retries do not create extra answers. Another browser or cleared browser data can allow another participation; the product does not guarantee one vote per person.
- Accepted answers cannot be edited. Missing or invalid answers receive a clear explanation beside the affected question.

## Live and asynchronous behavior

**Live:** Opening the poll creates a waiting room. The admin opens one question at a time, in order. Participants submit that answer and wait. The admin can see the response count, close the question, and either reveal its results or continue directly to the next question. After the final question, the admin may reveal results before ending or end immediately. Results remain visible only during that reveal step. Closed questions cannot be answered or reopened. Late arrivals join the current stage without answering earlier questions. The admin can end the poll at any time; participants then see that it has ended.

**Asynchronous:** While the poll is open, participants answer all questions at their own pace and submit the complete poll once. All questions are required; partial submissions do not count. With results enabled, successful submission unlocks the current combined results for that poll. Otherwise, participants see only a completion confirmation. Here, “at the end” means after the participant submits, not after the admin closes the poll. Returning in the same browser shows completion and any permitted results, including after closure.

Unsubmitted asynchronous answers survive refreshes and leaving and returning in the same browser while the poll remains open. These drafts never contribute to results and are cleared after successful submission. Once the poll closes, unfinished answers can no longer be submitted.

**Results:** The admin always has access to collected responses, including after closure. Multiple choice shows counts and percentages of answers to that question; numbers show count and average; text shows a list of answers. Empty results say “No responses yet.” Shared results contain no check-in identities. Asynchronous results include only completed submissions; live results include each accepted answer.

## Product quality requirements

- Support up to 10 questions per poll and 100 simultaneous participants. The interface is English only and works on phones and desktop browsers.
- Saved polls, accepted answers, and the current live stage survive refreshes and service restarts. Rejoining restores the current stage and previously accepted submission status in the same browser.
- If the organizer leaves or disconnects, the live poll stays at its current stage; an open question continues accepting answers. The organizer can return and resume control. Permanently ending the poll requires confirmation, including when ending early; individual question transitions do not.
- Submission clearly reports success, failure, or an uncertain connection state. Failed attempts preserve entered answers for retry while answering remains open. Closing a question or poll prevents further acceptance, including from an already-open page; previously accepted answers remain saved.
- Live stage changes and response counts appear without manual refresh, targeting two seconds under normal connectivity at the supported capacity. Disconnections are visible, and reconnecting catches up to the current state.
- The main flows support keyboard use, labeled inputs, readable contrast, and clear errors. Participant text is displayed safely as text. Invalid, draft, closed, and deleted poll links have understandable states.

## Acceptance criteria

Before release, demonstrate that:

1. The admin creates and runs both modes with all question types and both participation settings.
2. Participants can join, submit, and see exactly the results allowed by the selected mode; hidden results and check-in details cannot be retrieved by participants.
3. Repeated submission, refresh, and a lost connection never duplicate an accepted answer; a late submission is rejected clearly.
4. A late arrival sees the current live stage, and closing or deleting a poll stops participation.
5. The main journeys work on a phone and by keyboard, and remain correct at the supported capacity.
6. The organizer can recover account access, and no other account can administer polls.
7. The copied link and QR code lead to the same poll. The presentation view follows the live stage, reveals only permitted content, and adds no participant or response.
8. Duplicating a poll produces an editable Draft with a new link and no prior responses or check-in data, leaving the original intact.
9. Unsubmitted asynchronous answers survive refresh and return visits while the poll is open, without affecting results. Organizer disconnection preserves the live stage, and cancelling the close confirmation leaves participation open.

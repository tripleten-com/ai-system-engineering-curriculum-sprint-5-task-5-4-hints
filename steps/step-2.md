# Step 2: Write the workflow boundary

## The idea

Before the agent gets a tool, you write down what it's allowed to do, in words a dispatcher and a reviewer can check. An authority boundary has three lists:

- **What the agent may do on its own:** read, retrieve, propose, ask, refuse, finish.
- **What it may do only after a person approves:** here, one call that opens a handling review.
- **What it must never do:** decide what happens to the shipment, contact a clinic, and anything else outside its job.

The test of a boundary is whether the system keeps it, not whether the model behaves. "The agent never contacts a clinic" holds because no tool the agent holds can reach a clinic, not because the model is asked nicely. So the boundary also decides what the one tool can reach. It gets the services it needs for its one effect, and every other service and credential stays out of its reach.

The tool doesn't exist yet. Writing its contract first is the point: the code you write next must match the document, not the other way round. The same goes for the edges of the workflow: where the approval point sits, who owns an exception the agent didn't act on, and how a review opened by mistake is undone. Every value you permit comes from a list the platform already knows, and you can name which list.

> Covered in **3.3 Authority Boundaries**.

## What's expected

- `docs/agent/workflow-boundary.md`, or your chosen path, has the lesson's six sections in order.
- Every permitted value comes from one of the four sources, and you can say which: next steps, reason codes, roles and exception states.
- Section 3 uses the tool contract's fixed names exactly, and states your two lists and your limit with a reason.
- Every "never" in section 2 is kept by something in the system, and the document says what.
- Escalation names a role that owns the exception when a run ends without a review.
- Rollback names a dispatcher operation, who may run it, and what it doesn't undo.

## When you're stuck

### You don't know where a permitted value comes from

<details><summary>Move 1</summary>

Which kind of value is it: a next step, a reason code, a role or an exception state?

</details>

<details><summary>Move 2</summary>

Open the source the lesson names for that kind and find the value there.

</details>

<details><summary>Move 3</summary>

If the value isn't in any of the four sources, the platform doesn't know it, and the boundary can't permit it. Choose a value the source lists.

</details>

### A prohibition depends on the model behaving

<details><summary>Move 1</summary>

For each "never", ask: what in the system makes it impossible?

</details>

<details><summary>Move 2</summary>

If the answer is "the model won't ask", what would happen the day it does?

</details>

<details><summary>Move 3</summary>

List the ports and credentials the tool will get. Which ones does it need for its one effect, and which ones would it never use?

</details>

<details><summary>Move 4</summary>

The approach: give the tool only the ports its one effect needs, and write every other service and credential as out of its reach. Each "never" then names what keeps it: a missing tool, a missing credential, or the approval point.

</details>

### You can't decide how to store reason codes

<details><summary>Move 1</summary>

Look at the `rejection_reason` stored for your Step 1 exception. Is it a bare code, or a code with a field name after a colon?

</details>

<details><summary>Move 2</summary>

If your list holds bare codes, what does a check compare against a stored code with a colon? If it holds full codes, how many entries would it need?

</details>

<details><summary>Move 3</summary>

Pick one form, write the comparison rule beside the list, and put the reason in your evidence note.

</details>

### You're not sure what a second review would mean

<details><summary>Move 1</summary>

Where does the tool write the review packet? How many files can that path hold for one exception?

</details>

<details><summary>Move 2</summary>

If one run could open two reviews for the same exception, what would the dispatcher find, and which one would they trust?

</details>

<details><summary>Move 3</summary>

Which calls count toward the limit: every call, or only calls that opened a review? Who sees enough to enforce it: the tool, which sees one call, or the agent, which sees the run?

</details>

<details><summary>Move 4</summary>

Set the limit from those answers, and write the reasoning beside it.

</details>

### The approval wait has no place to live

<details><summary>Move 1</summary>

Which section describes the approval point?

</details>

<details><summary>Move 2</summary>

Does the configuration you write in Step 3 have a field for the wait?

</details>

<details><summary>Move 3</summary>

State the wait and what a late decision means in section 4 only, as the lesson says.

</details>

### Escalation and rollback read like the same thing

<details><summary>Move 1</summary>

One answers "the agent didn't act, who owns this now?". The other answers "the agent acted by mistake, how is it undone?". Which run endings belong to each?

</details>

<details><summary>Move 2</summary>

Who runs the undo operation? If your answer is the agent, read the boundary's lists again.

</details>

<details><summary>Move 3</summary>

For rollback, also write what it doesn't undo. Something already sent can't be unsent by a marker.

</details>

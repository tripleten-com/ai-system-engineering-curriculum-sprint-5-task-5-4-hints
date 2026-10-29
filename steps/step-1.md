# Step 1: Map one run of your graph

## The idea

A graph is a claim about control flow, and a claim you haven't traced is a guess. Mapping a run means putting what happened next to why it happened, line by line. The printout says what happened: which node ran, what the model proposed, how the run ended. The code says why: which handler turned that proposal into that ending, and which condition in your rule sent the run on or stopped it.

Keep three things apart while you map:

- **Nodes:** the pieces of work, `propose` and `act`. A printed step is one node running, not one proposal.
- **Action kinds:** what `propose` returned. A kind is data flowing through the graph, not a place in it.
- **Edge values:** what your rule returned after each `act`, one per `act`.

Two different "states" also need keeping apart. The run's status lives in the run. The exception's state lives in Coldline's record. Your graph doesn't write to the record yet, so after any run the exception still reads `NEEDS_REVIEW`, whatever the run did. In Step 2 you'll describe what every edge value means, including ones this one run doesn't produce, so the map has to come from the code as well as the printout.

> Covered in **3.1 Agents as State Graphs**.

## What's expected

- You have one exception in `NEEDS_REVIEW` and the `reason_code` from its `output_rejected` event.
- You have one run's id, from a script your graph can complete today.
- Your map has three lists: the node of each step in order, one edge value per `act`, and the final status.
- Every line of the map points to a line of code: a handler for each kind, a condition for each edge value.
- Reading the exception afterwards still shows `NEEDS_REVIEW`.

## When you're stuck

### You can't find the reason code

<details><summary>Move 1</summary>

Which record holds the guardrail's verdict: the trace, or the audit trail?

</details>

<details><summary>Move 2</summary>

Run `poe audit-trail` with your exception id and find the event that carries a `reason_code`.

</details>

<details><summary>Move 3</summary>

Note the code exactly as stored, including anything after a colon. Step 2 asks you to decide how your boundary compares codes, and you'll need the stored form for that.

</details>

### Your well-behaved script ends `refused`, not `finished`

<details><summary>Move 1</summary>

Which script did you run? Read its first entry.

</details>

<details><summary>Move 2</summary>

What does your graph do today with that kind of proposal? Find the handler.

</details>

<details><summary>Move 3</summary>

Is that ending wrong, or exactly what the graph should do with a tool call or an approval request in this Task?

</details>

<details><summary>Move 4</summary>

Map a run of a script your graph can complete today, such as a single `finish`. Or keep the refused run, if you prefer. Either way, say in your note which script you mapped and why.

</details>

### The map has more steps than the script has entries

<details><summary>Move 1</summary>

What does one printed step stand for: one proposal, or one node running?

</details>

<details><summary>Move 2</summary>

How many nodes run for each proposal?

</details>

<details><summary>Move 3</summary>

List the node sequence, then write the kind beside each `propose` step only, and an edge value beside each `act` step.

</details>

### Your dev command doesn't print the edge's value

<details><summary>Move 1</summary>

What does your rule return after an `act`? Read its single condition.

</details>

<details><summary>Move 2</summary>

Given the status your run printed after each `act`, which branch of that condition ran?

</details>

<details><summary>Move 3</summary>

Write the value from the condition, or add the value to your dev command's output if you'd rather see it. Either is allowed. Say which you did.

</details>

### A line in your map has no code behind it

<details><summary>Move 1</summary>

Which line is it: a node, a kind, an edge value or the final status?

</details>

<details><summary>Move 2</summary>

For a kind, which handler did `act` look up? For an edge value, which condition produced it? For the final status, which handler set it?

</details>

<details><summary>Move 3</summary>

If you still can't find it, the map may be describing what you expected, not what ran. Run again and read the printout line by line.

</details>

### The exception's state didn't change after the run

<details><summary>Move 1</summary>

Which code in your graph writes to the exception record?

</details>

<details><summary>Move 2</summary>

If none does, what should the record say after any run?

</details>

<details><summary>Move 3</summary>

Keep the two apart in your note: the run's status from your dev command, and the exception's state from the record.

</details>

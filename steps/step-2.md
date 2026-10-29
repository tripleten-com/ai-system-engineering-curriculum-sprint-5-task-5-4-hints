# Step 2: Write the workflow boundary

## A prohibition depends on the model behaving

<details><summary>Hint 1</summary>

For each "never" in your list, ask: what in the system makes it impossible? If the answer is "the model won't ask", it isn't kept yet.

</details>

<details><summary>Hint 2</summary>

What can the tool reach? List the ports and credentials it gets. A service it can't reach is a service it can't misuse.

</details>

## You can't decide how to store reason codes

<details><summary>Hint 1</summary>

Look at a stored `rejection_reason` from your Step 1 exception. Does it hold a bare code, or a code with a field name after a colon?

</details>

<details><summary>Hint 2</summary>

If your list holds bare codes, what does the check compare? If it holds full codes, how many entries do you need? Pick one, and write down why.

</details>

## You're not sure what a second review would mean

<details><summary>Hint 1</summary>

Where does the packet go? How many files can that path hold for one exception?

</details>

<details><summary>Hint 2</summary>

If one run could open two reviews for the same exception, what would the dispatcher find, and which one would they trust?

</details>

## The approval wait has no place to live

<details><summary>Hint 1</summary>

Which section of the document describes the approval point? Does the configuration you write in Step 3 have a field for the wait?

</details>

## Escalation and rollback read like the same thing

<details><summary>Hint 1</summary>

One answers "the agent didn't act, who owns this now?". The other answers "the agent acted by mistake, how is it undone?". Which run endings belong to each?

</details>

<details><summary>Hint 2</summary>

Who runs the undo operation? If the answer is the agent, read the boundary again.

</details>

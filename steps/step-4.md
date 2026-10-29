# Step 4: Prove it with tests and write the evidence note

## The idea

The loader is the boundary's guard, so its tests answer one question: does every rule refuse the file that breaks it, and only that file? Two groups cover it:

- **The committed file:** it loads, with the values your document states.
- **The bad files:** one per rule, each refused with that rule's field named.

The trick is building the bad files. Start from the committed file, change one value, write the copy to a temporary folder, load the copy. With one change per copy, a failing test tells you exactly which rule broke. With the expected values read from the committed file, a test can't drift from the configuration. A refusal test also has to check the field name in the error. A loader that refuses everything, or refuses for the wrong reason, passes a test that only checks for an error.

Your evidence note for this Task holds more design than the earlier ones: the run map, the choices behind your lists and your limit, which services the tool may reach, and what rollback can't undo. Your instructor reads why, so write the reasons, not just the values.

> Covered in **CI Gates and Release Verification**.

## What's expected

- Your test file sits where `poe student-tests` collects it, beside your earlier tests.
- One test loads the committed file and checks its values against the file itself.
- There's one test per loader rule. Each builds a copy with one change in a temporary folder and checks the error names the field.
- You removed a rule once and saw its test fail. Do this at least for the next-step check, the limit and approval.
- `poe demo` still runs the vaccine exception to its summary.
- `poe verify` passes after your last edit.

## When you're stuck

### A refusal test passes for the wrong reason

<details><summary>Hint 1</summary>

What does your test assert: that the loader raised, or that it raised about the field you broke?

</details>

<details><summary>Hint 2</summary>

Change two values in one bad copy. Can your test still tell which rule refused it?

</details>

<details><summary>Hint 3</summary>

Assert that the error names the field, and keep one change per copy.

</details>

### The good-file test breaks whenever you edit the configuration

<details><summary>Hint 1</summary>

Where does the test get its expected values?

</details>

<details><summary>Hint 2</summary>

If they're typed into the test, which copy is right after an edit to the file?

</details>

<details><summary>Hint 3</summary>

Read the committed file in the test and compare the loaded object with what the file holds.

</details>

### Bad files leak into the repository

<details><summary>Hint 1</summary>

Where do your tests write the broken copies?

</details>

<details><summary>Hint 2</summary>

Is there a test fixture that gives each test its own temporary folder, cleaned up afterwards?

</details>

<details><summary>Hint 3</summary>

Write every copy there, and run `git status` after your tests to confirm nothing new appeared.

</details>

### The demo stopped working

<details><summary>Hint 1</summary>

Run `poe demo`. Where does it stop, and what does it print last?

</details>

<details><summary>Hint 2</summary>

Did this Task change a file the demo reads, such as a script or a setting?

</details>

<details><summary>Hint 3</summary>

Compare a demo run before and after your changes. Restore whatever the demo depended on, or update the demo so it still runs the vaccine exception to its summary.

</details>

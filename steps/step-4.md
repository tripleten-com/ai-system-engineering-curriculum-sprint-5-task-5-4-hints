# Step 4: Prove it with tests and write the evidence note

## A refusal test passes for the wrong reason

<details><summary>Hint 1</summary>

What does your test assert: that the loader raised, or that it raised about the field you broke?

</details>

<details><summary>Hint 2</summary>

Change two values in one bad file. Can your test still tell which rule refused it?

</details>

## The good-file test breaks whenever you edit the configuration

<details><summary>Hint 1</summary>

Where does the test get its expected values? If you typed them in, which copy is right after an edit?

</details>

## Bad files leak into the repository

<details><summary>Hint 1</summary>

Where do your tests write the broken copies? Is there a test fixture that gives each test its own temporary folder?

</details>

## The demo stopped working

<details><summary>Hint 1</summary>

Did anything in this Task change a file the demo reads? Run `poe demo` before and after your changes and compare where each run ends.

</details>

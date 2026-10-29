# Step 3: Encode the boundary in configuration and write the loader

## The idea

A boundary in prose can't stop a tool call. A configuration file the code reads can. If the document limits how many reviews a run may open but no file carries that number, the agent has nothing to enforce. So the nine things your document says become nine fields in a file under `config/`, next to the platform's other settings.

A file alone isn't enough either, because files get edited. The loader is the guard: it reads the file once, checks every field, and refuses a bad file with a message that names the field. A broken configuration should fail when the agent starts, never at the moment a dispatcher is waiting.

Three ideas make the loader trustworthy:

- **Read lists from their sources:** next steps from the schema file, states from the domain, reason codes from the guardrail's code. A copy goes stale the day the source changes, and no check notices.
- **Refuse what you don't define:** a misspelled field name would otherwise be ignored silently, and the agent would run with a default nobody chose.
- **Some rules aren't yours to choose:** approval must stay on. That rule comes from the boundary itself, so the loader refuses a file that turns it off.

The platform already reads its token settings this way, so your loader can follow a pattern you can read rather than inventing one.

> Covered in **3.3 Authority Boundaries**.

## What's expected

- One configuration file under `config/` holds the nine fields, with the same names and values as your document.
- In the shell, the loader returns an object holding your values.
- Copies of the file are each refused with the field's name:
  - one with a field missing
  - one with an unknown next step
  - one with an unknown reason code
  - one with a limit of zero
  - one with approval off
  - one with a misspelled field name
- A check command in `pyproject.toml` prints `valid` on the committed file, and prints the error and exits non-zero on a bad one.

## When you're stuck

### A misspelled field loads without an error

<details><summary>Hint 1</summary>

What does your model do with a field it doesn't define? Try a misspelled one in the shell.

</details>

<details><summary>Hint 2</summary>

How did your Task 1 contract handle extra fields? Use the same setting here.

</details>

<details><summary>Hint 3</summary>

Check nested blocks too, such as escalation and rollback. Each nested model needs the same rule.

</details>

### Your reason-code check accepts everything or nothing

<details><summary>Hint 1</summary>

What exactly does the guardrail's code list hold? Print it in the shell.

</details>

<details><summary>Hint 2</summary>

Compare one entry with the stored `rejection_reason` from Step 1. Same form?

</details>

<details><summary>Hint 3</summary>

Is your check doing what you decided in Step 2: comparing whole codes, or the part before the colon?

</details>

<details><summary>Hint 4</summary>

The approach: check each code in your list against the guardrail's own code list, imported from the guardrail module, in the form you chose. Keep the comparison rule for stored codes in one helper, so the tool can reuse it in the next Task.

</details>

### You can't find a code list for the roles

<details><summary>Hint 1</summary>

Search `src/` and `config/` for a role name such as `dispatcher`. Where does the full list of roles actually live?

</details>

<details><summary>Hint 2</summary>

The lesson offers two ways to check an owner role. Which one survives a change to the access policy, and which one is simpler to test?

</details>

<details><summary>Hint 3</summary>

Choose one, say why in your note, and test that an unknown role is refused.

</details>

### The loader looks nothing like the platform's

<details><summary>Hint 1</summary>

Open `src/api/security/tokens.py`. How does it turn `config/auth.yaml` into a checked object?

</details>

<details><summary>Hint 2</summary>

What does it do when the file can't be read, or when a value is wrong?

</details>

<details><summary>Hint 3</summary>

The approach: a typed model for the nine fields, one function that takes a path, reads the file and validates it into that model, and one error type that carries every failing field's name.

</details>

### The file loads, but you're not sure it says what the document says

<details><summary>Hint 1</summary>

Put the file and the document side by side.

</details>

<details><summary>Hint 2</summary>

For each field in the file, which section of the document states it?

</details>

<details><summary>Hint 3</summary>

Change one place and you must change the other. Run the check command after your last edit to the file.

</details>

### You can't add the check command

<details><summary>Hint 1</summary>

Read how an existing small command is declared in `pyproject.toml`, one that runs a Python module.

</details>

<details><summary>Hint 2</summary>

What should it print on success, and what exit code should it return on failure?

</details>

<details><summary>Hint 3</summary>

Give your loader module a small entry point that loads the committed file, prints `valid` or the error, and returns the exit code. Then declare the task the same way the existing ones are declared.

</details>

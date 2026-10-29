# Step 3: Encode the boundary in configuration and write the loader

## You can't find a code list for the roles

<details><summary>Hint 1</summary>

Search `src/` and `config/` for a role name such as `dispatcher`. Where does the full list of roles actually live?

</details>

<details><summary>Hint 2</summary>

The lesson gives you two ways to check an owner role. Which one keeps your loader working if the access policy gains a role, and which one is simpler to test?

</details>

## Your reason-code check accepts everything or nothing

<details><summary>Hint 1</summary>

What exactly does `REASON_CODES` hold? Print it in the shell and compare one value with a stored `rejection_reason`.

</details>

<details><summary>Hint 2</summary>

Does your check compare a whole code, or the part before the colon? Is that the decision you made in Step 2?

</details>

## A misspelled field loads without an error

<details><summary>Hint 1</summary>

What does your model do with a field it doesn't define? Look at how the contract you wrote in Task 1 handles that.

</details>

## The loader looks nothing like the platform's

<details><summary>Hint 1</summary>

Read how `src/api/security/tokens.py` turns `config/auth.yaml` into a checked object. What does it do when the file is wrong?

</details>

<details><summary>Hint 2</summary>

Does your loader raise and name the field, or does it log a warning and carry on with defaults?

</details>

## The file loads, but you're not sure it says what the document says

<details><summary>Hint 1</summary>

Read the two side by side, field by field. For each value in the file, which section of the document says it?

</details>

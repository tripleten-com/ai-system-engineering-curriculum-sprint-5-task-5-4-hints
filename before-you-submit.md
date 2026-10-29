# Before you submit

The basic checks confirm that your work is there. They don't judge whether it's right. Your instructor reads your pull requests and evidence notes with four questions. Ask them of your own work first.

## Did you meet the Task's requirements?

- Does your document have all six sections, with the tool contract's names exactly as the lesson fixes them?
- Does every value in your configuration come from one of the platform's lists, and can you name which one?
- Does the loader refuse a missing field, an unknown field, an unknown value, a limit below one and approval turned off?
- Does `poe authority-check`, or your equivalent, pass on the committed file, and does `poe demo` still pass?

## Did you explain your design choices?

- Does your note say why you chose your limit and your two lists?
- Does it say which services the tool may reach, who owns an escalated exception, and what rollback doesn't undo?
- Does it say how you store reason codes, and why?

## Can your tests fail when the code is wrong?

- Does each refusal test assert the field name in the error?
- Did you remove a rule once and see its test fail?

## Did you state the limits of what your checks show?

- Does your note say what the loader can't tell you: whether the boundary itself is right?
- Is every prohibition kept by the system, and does your note say how?

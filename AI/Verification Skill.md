Think about how you normally check Claude's work. You ask it to refactor something, it finishes, and then you have to remember to double-check it. Maybe you ask it to run the tests. Maybe you read the diff yourself. The problem is that the checking depends on you remembering to ask for it. Skip that step once and bad code slips through.

A verification skill removes that dependency. Here's the shape of it. You ask Claude to refactor something. When it finishes, the change matches the skill's description, so the skill fires on its own. From there it:

- Runs the test suite.
- Reads the diff.
- Checks that no test was weakened just to make things pass.
- Reports pass or fail, with the evidence attached.

The whole flow runs without you asking. The description on the skill is what triggers it, and once triggered it walks the same steps every time. For this skill it might be a good idea to add more context to it and more functionalities for that you can check the [[Skill Specification]] to know all the files a skill could have.
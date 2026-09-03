Temperature is a decimal value between 0 and 1 that allows to control which token Claude decides to take (The probability of selecting a certain word as we now an LLM is an autocomplete bot with steroids') It will influence the exact distribution of probabilities.
![[Pasted image 20260813210421.png]]
At temperature 0, Claude becomes deterministic - it will always pick the most probable token. At temperature 1, lower-probability tokens have a much better chance of being selected, leading to more creative and varied outputs.
### Low Temperature (0.0 - 0.3)

- Factual responses
- Coding assistance
- Data extraction
- Content moderation

### Medium Temperature (0.4 - 0.7)

- Summarization
- Educational content
- Problem-solving
- Creative writing with constraints

### High Temperature (0.8 - 1.0)

- Brainstorming
- Creative writing
- Marketing content
- Joke generation

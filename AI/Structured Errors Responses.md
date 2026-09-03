Imagine you ask an assistant to book a flight and they come back with just: "It didn't work." What now? Should they try again? Try a different airline? Give up and ask you? They — and you — have no idea, because 'it didn't work' contains no information to act on. Now imagine instead: "The airline's site timed out; this usually clears up in a minute — shall I retry?" That tells you exactly what happened and what to do. The difference between those two messages is the difference between an agent that recovers gracefully and one that flails.

Not all failures are the same, and the right response depends on the KIND. There are four categories worth distinguishing, and the key thing each tells you is whether retrying could possibly help.

|Category|Example|Retry?|Right response|
|---|---|---|---|
|Transient|Timeout, rate limit, service briefly down|Yes|Retry with backoff|
|Validation|Malformed or invalid input|Yes*|Fix the input, then retry|
|Business|Policy violation (e.g. refund not allowed)|No|Explain to the user / escalate|
|Permission|Access denied|No|Escalate; retrying won't grant access|

Four failure categories. Transient and validation errors are worth retrying (validation only after correcting the input); business and permission errors are not — retrying just wastes attempts.

Picture a search tool. Case one: the search service was unreachable — an ACCESS FAILURE. The agent genuinely doesn't know the answer; retrying might help. Case two: the search ran perfectly and returned zero matches — a VALID EMPTY RESULT. 'No matches' IS the answer; retrying is pointless and will just return zero again. In MCP terms, the access failure sets isError: true (something went wrong), while the valid empty result sets isError: false with a result count of zero (nothing went wrong — there simply are no matches).
Designing the tool to clearly signal which case it is — failure versus legitimately empty — is what keeps the agent from chasing answers that aren't there.
## The description is the WHOLE Game
How does the model that a tool fits a request? The answer is that the model chooses a tool almost entirely by reading its DESCRIPTION.
NOT the tool name.
NOT some hidden wiring
It is the plain-language description written the primary thing the model uses to pick
The descriptions are the labeled keys that a new employed uses to know which key opens which door.

Most of the time, to design a good tool isn't about the code behind, it is about writing a description clear enough that the model never has to guess

## What Separates a Minimal Description From a Production One
**A Minimal Description**: Retrieves customer information
**A Production-grade**: Retrieves a customer's account details by customer ID or email. Use for profile, contact, and account-status questions. Do NOT use for order-specific queries — use lookup_order instead. Input: a customer_id (format: CUST-12345) or an email address.

A production-grade description carries five things, and you can treat them as a checklist. Miss any of them and you've left the model room to guess.
1) **Primary purpose**: What the tool does, in one clear sentence.
2) **Input expectation**: Types, formats, constraints, and which inputs are required vs optional
3) **Example queries**: The kinds of requests that should route here, in the words a user would actually use.
4) **Edge cases and limitations**: What it can't do, so the model doesn't over-reach.
5) **Explicit boundaries vs similar tools**: 'use this NOT that'

| Category    | Minimal (✗)                      | Production-grade (✓)                                |
|-------------|----------------------------------|-----------------------------------------------------|
| Purpose     | "Retrieves customer information" | "Retrieves account details by customer ID or email" |
| Inputs      | (unspecified)                    | "customer_id (CUST-12345) or email"                 |
| When to use | (left to guess)                  | "profile, contact, account-status questions"        |
| Boundaries  | (none)                           | "Do NOT use for orders — use lookup_order"          |
To route an AI correctly to the expected tool the first approach should be to check the description and adjust it. 
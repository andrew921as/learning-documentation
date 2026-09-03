## Question 1
A legal-review pipeline must guarantee that every submitted contract receives a result within 30 hours of arrival, using the Message Batches API's up-to-24-hour processing window. How often must the pipeline start a new batch submission cycle to guarantee this SLA in the worst case?

Correct answer:

A) At least once every 6 hours, since a contract can wait up to that interval before inclusion and still finish within 24 hours before the 30-hour deadline

My answer:

D) At least once every 24 hours, since that matches the batch processing window and therefore satisfies any SLA built on top of it

## Question 2
A coordinator agent delegates a three-step data migration to a subagent: extract, transform, and load, but the load step fails twice on a database connection reset, a known transient condition, before finally succeeding on the third attempt inside the subagent's own execution. What should the subagent report back to the coordinator?

Correct answer:
A) A success result summarizing the completed migration, since the transient failures were resolved locally and never needed to surface above the subagent

My answer:
B) An `isError: true` result describing both connection resets in detail, so the coordinator can decide independently whether the migration should be retried

## Question 3
A customer onboarding workflow always performs three steps for every new account in the same order: create the account record, provision default permissions, and send a welcome email. None of these steps ever branch based on account data. Separately, a fraud investigation workflow examines a flagged account by pulling transaction history, and the specific records to inspect next depend entirely on what suspicious patterns are found in the transactions already reviewed. Which pairing of decomposition strategies correctly matches each workflow?

Correct answer:
A) Onboarding should use a fixed prompt chain since its steps never branch, while fraud investigation should use adaptive decomposition based on findings

My answer:
C) Onboarding should use adaptive decomposition since account creation always carries some risk of failure, while fraud investigation should use a fixed three-step chain

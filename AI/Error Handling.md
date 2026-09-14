Handling correct errors in AI is crucial to know what happened, also this helps the model to know what to do next depending the error occurred. Also there are Silent Failure, those are errors that are cached as succeed, but actually have the wrong information making the model to continue working with corrupted data
Agentic systems fail in three distinct ways, each requiring a different recovery strategy.

**Tool error**: An external tool, API, or service errors or times out. May be transient or permanent
**Reasoning error**: The model produces a wrong plan or misreads a result. Retrying identical input fails again
**Environment Error**: Infrastructure below the tool fails, like network, database, or file system. Often transient

### Tool error:
This is when an external tool, API, or service errors or times out. May be transient or permanent
It is important to know that the tool manage the error correctly giving a status code of 2 (Error) or 0 (No error) but with empty data (expected result since no records found).

To handle this error we should: Retry with backoff, or switch to a different tool (Fall back chain).

>[!Note]
>A **fall back chain** is the act of have different steps if something goes wrong. Do A, if it fails do B if it also fails, do C.

There are 2 main tool erros:
- **Transient**: Those are caused by Network time outs or rate limit temporary unavailability. Those are usually signal as 5xx, and can be solved by Retrying with backoff 
- **Permanent**: Invalid input, permission denied, resource not found. Those are usually signal as 4xx and should NOT be retried.

To transient errors we could use Exponential Backoff with Jitter, the exponential backoff doubles the time waiting for retrying after each failure: 1s, 2s, 4s, 8s. Jitter add randomness to prevent synchronized retry storms across clients.
### Reasoning error:
This happens when everything runs well, but the model does not produce the expected result.

To handle this we should Modify the prompt or correct the context of the model. DO NOT RETRY with the same data, it will produce the same error.

### Environment errors
Infrastructure below the tool fails, like network, database, or file system. Often transient
If the tool worked fine this just often is resolved by waiting and retrying after a delay

## How to avoid error propagation
The error propagation occurs when there are silent erros, usually one error in an early stage could make the program to fail many steps later wasting time and resources.

To avoid this we could use a **Validation Gate** it is a checkpoint that inspects step output against criteria before letting execution continue.

### How to implement a Validation Gate?
**Output Validation** These strategies validates the output of a task, it could be from a tool or from a model finishing its execution.

- **Schema checks**: Required fields present; correct types, no unexpected nulls
- **Range Checks** Numeric values stay in bounds; string lengths stay capped.
- **Completeness Checks**: All required sections populated; no truncated responses.
All of the methods above are the Schema validation, they validate thins like code would do, but it also exist the **Semantic Validation** Those verify the meaning: is the output plausible given the input? Are values in expected range?



As we want to keep the human in the loop for different reasons, some times for critical multi-step workflows, relying solely on prompts to enforce ordering is insufficient. Programmatic guardrails provide deterministic guarantees.
#### The Problem

Prompt-based instructions ("always verify customer first") can be ignored or inconsistently followed. Production data may show agents skipping critical steps in 10-15% of cases. When deterministic compliance is required (e.g., identity verification before financial operations), prompt instructions alone have a non-zero failure rate.
#### Levels of Enforcement

1. **Prompt only**: Suggest ordering (unreliable)
2. **Prompt + examples**: Demonstrate ordering (better)
3. **Programmatic guards**: Block unauthorized calls (deterministic)
4. **State machine**: Full workflow engine (most robust)
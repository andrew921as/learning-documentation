A workflow is a fixed, developer-authored sequence of steps that executes predictably. The control flow is decided up front at design time, not while the model is running.
Of course we could combine Agents with our workflow pattern but the core **difference** with an Agentic System is that no matter what does the agent result, we continue to the next step and we define the next step NOT the agent.

Workflows are:
- Fixed control flow
- Predictable, auditable output
- Lower latency and token cost
- Each step is individually testable.

### Trade offs
- Workflows trade adaptability for predictability
- Agentic systems trade off 'debugability' for flexibility

> [!important]
> Choosing agents when workflows suffice adds cost and risk without adding value

## Workflow Patterns
Anthropic defines 5 main Workflow Patters:
- **Prompt Chaining**: Sequential LLM calls where each output feeds the next step
- **Routing:** a classifier step directs input to the right specialized prompt or sub-agent.
- **Parallelization**: multiple LLM calls run simultaneously with results collected at a fan-in step.
- **Orchestrator-Subagent**: a controlling component decomposes a goal and delegates to specialized workers.
- **Evaluator-Optimizer** One call generates output, another evaluates it, looping until quality criteria met.
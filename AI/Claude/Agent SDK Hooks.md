Agent SDK hooks provide programmatic interception points in the agentic loop, enabling deterministic enforcement and data transformation without relying on prompt instructions.
#### PostToolUse Hooks (Result Transformation)

Intercept tool results **BEFORE** the model processes them. Use cases:

- **Data normalization**: Convert Unix timestamps, ISO 8601 dates, and numeric status codes from different MCP tools into consistent human-readable formats
- **Result enrichment**: Add computed fields or metadata
- **Filtering**: Remove sensitive data before the model sees it

#### Tool Call Interception Hooks (Outgoing)

Intercept outgoing tool calls **BEFORE** they execute. Use cases:

- **Compliance enforcement**: Block refunds exceeding $500 and redirect to human escalation
- **Policy gates**: Prevent actions that violate business rules
- **Audit logging**: Record all tool calls for compliance
#### Hooks vs Prompt Instructions

|Approach|Guarantee|Use When|
|---|---|---|
|Prompt instructions|Probabilistic (non-zero failure rate)|Soft preferences, style guidance|
|Hooks|Deterministic (100% enforcement)|Business rules, compliance, financial thresholds|

When a business rule MUST be followed every time (e.g., refund limits, identity verification), use hooks. Prompt instructions are appropriate for soft guidance where occasional deviation is acceptable.
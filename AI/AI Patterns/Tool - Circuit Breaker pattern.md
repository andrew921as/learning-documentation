A circuit breaker pattern manages the relationship between your tool and an unreliable downstream service, it has three states:
- **Closed:** Healthy. Calls pass through; failures are counted
- **Open**: Calls blocked at once; a fallback or error returns
- **Half-Open**: A probe call tests recovery

We should add a circuit breaker when a downstream tool has intermittent outages that are predictable
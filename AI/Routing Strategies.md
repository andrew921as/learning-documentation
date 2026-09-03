In the AI context routing means the use of different models depending the task to be completed.
### Routing by Complexity

Route tasks to the cheapest model that meets quality requirements:

- Use Haiku as a classifier to determine routing for more expensive models
- Simple tasks go to faster/cheaper models; complex ones escalate
- Monitor quality metrics per tier to validate routing decisions
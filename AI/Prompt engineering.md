Build a good prompt is crucial when we want to get good results to our tasks working with AI, there are different techniques that can be applied together to get good based prompts.
Also we can refine our prompts in case those are going to be used multiple times, for that we can [[Prompt eval|evaluate our prompts]] and apply these techniques to get a better score.

## Being clear and Direct
### Clear Communication

Being "clear" means:

- Use simple language that anyone can understand
- State exactly what you want without beating around the bush
- Lead with a straightforward statement of Claude's task

Instead of writing something vague like "I need to know about those things people put on their roofs that use sun - those solar panel things, I think they're called," 
be direct and write: "Write three paragraphs about how solar panels work."

### Direct Instructions

Being "direct" focuses on how you structure your request:

- Use instructions, not questions
- Start with direct action verbs like "Write," "Create," or "Generate"

Rather than asking "I was reading about renewable energy and geothermal energy sounds neat. What countries use it?" try: "Identify three countries that use geothermal energy. Include generation stats for each."
## Be specific
When working with Claude, one of the most effective ways to improve your results is to be specific about what you want. Instead of leaving everything up to the model's interpretation, you can provide clear guidelines or steps that direct Claude toward the kind of output you're looking for.
### Quality Guidelines

The first type focuses on listing qualities that your output should have. These guidelines control attributes like:

- Length constraints (keep under 1,000 words)
- Structural requirements (include a clear action that reveals the character's talent)
- Content specifications (include at least one supporting character)

### Process Steps

The second type provides specific steps for the model to follow. This approach makes Claude think through the problem systematically:

1. Brainstorm 3 talents that would create dramatic tension
2. Pick the most interesting talent
3. Outline a pivotal scene that reveals the talent
4. Brainstorm 3 supporting character types that could increase the impact of this discovery

Quality guidelines control what the output looks like, while process steps control how Claude arrives at that output.

![[Pasted image 20260815191253.png]]
## Structure with XML tags
When you're building prompts that include a lot of content, Claude can sometimes struggle to understand which pieces of text belong together or what different sections are supposed to represent. XML tags provide a simple way to add structure and clarity to your prompts, especially when you're interpolating large amounts of data.

![[Pasted image 20260815192121.png]]
we can wrap the information of sales records in some XML custom tags so the model knows that the information inside are the sales records
```code
<sales_records>
{sales_records}
</sales_records>
```

Other example:
![[Pasted image 20260815193823.png]]

## Provide examples
Providing examples in your prompts is one of the most effective prompt engineering techniques you'll use. This approach, known as "one-shot" or "multi-shot" prompting, involves giving Claude sample input/output pairs to guide its responses.
### Handling Corner Cases

For tricky scenarios like sarcasm, you can provide multiple examples (multi-shot prompting). Add context to highlight what Claude should watch for:

```
Be especially careful with tweets that contain sarcasm.
For example:
<sample_input>
Oh yeah, I really needed a flight delay tonight! Excellent!
</sample_input>
<ideal_output>
Negative
</ideal_output>
```
Examples are particularly useful for:

- Capturing corner cases or edge scenarios
- Defining complex output formats (like specific JSON structures)
- Showing Claude exactly what "good" output looks like
### For increasing prompt eval
When running prompt evaluations, look for your highest-scoring outputs in the HTML report. These make excellent examples to include in your prompt.
Find a response that scored well (ideally a 10, or your highest score), then copy both the input and output to use as your example.
Beyond crafting better prompts, there are two powerful techniques for controlling Claude's output: prefilled assistant messages and stop sequences. These methods give you precise control over how Claude responds and when it stops generating text.

## The Prefilled assistant messages
This will provide the start of a message, then Claude will continue from there and ti will steer Claude's response
**IMPORTANT**: Claude will continue the response from the text provided It means that the beginning of the text will not come into the answer.

**Start answer**: Coffe is better because
**Claude's response**: it has more caffeine and energy

To get the full answer you should concatenate bot parts of the text.

```Python
# Think about the messages chain where we have user - assistant messages chain, if the last message of the chain is the assistant message, then Claude will continue from there
messages[user,assistan,user,assistant]
response = client.converse(
	modelId=model_id,
	messages=messages
)
# This will force Claude to continue from the last message from the assistant
```

## Stop sequences
Forces Claude to end the response as soon as it generates a string matching your stop sequence.

These are provided as an additional parameter to the converse function

```Python
response = client.converse(
	modelId=model_id,
	messages=messages,
	inferenceConfig= {
		"temperature": 0.2,
		"stopSequences": ['finisher']
	},
	system=[{"text": system_prompt}]
)

```
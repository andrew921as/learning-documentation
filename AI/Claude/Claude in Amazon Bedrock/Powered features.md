Claude in AWS bedrock can has handle many things including different datatypes and rasoning.

## Images
Images has several limitations but can be sent to claude, and even those limitations exist it doesn't means that it is hard to send images.

![[Pasted image 20260819174815.png]]

## PDF Support
Similar as images, we can send PDF to Claude, to do it so we have to change a little bit the code:
```Python
with open("./earth.pdf", "rb") as f:
	file_bytes = f.read()

add_user_message(
	messages,
	[{"document":{
		"format": "pdf",
		"name": "earth",
		"source": {"bytes": file_bytes}
		}},
	{"text": "Summarize this document in one sentence"},
	],
)
```

### Citations
With the PDF support we can enable citations so we get from were does the AI gets the information.
```Python
with open("./earth.pdf", "rb") as f:
	file_bytes = f.read()

add_user_message(
	messages,
	[{"document":{
		"format": "pdf",
		"name": "earth",
		"source": {"bytes": file_bytes},
		"citations": {"enabled": True} # Notice that we enabled this capability
		}},
	{"text": "Summarize this document in one sentence"},
	],
)
```
This can be seen like this the response:
![[Pasted image 20260819183320.png]]

## Prompt Caching
Prompt caching is a feature that speeds up Claude's responses and reduces the cost of text generation by reusing computational work from previous requests.

When you send a message to Claude, a lot happens behind the scenes before you get a response back. Claude doesn't just immediately start generating text - it first does extensive work on your input message.

Here's what Claude does with your message:

- Tokenize the prompt
- Create embeddings for each token
- Add context based on surrounding text
- Generate output text

This creates an inefficiency when you're having conversations with Claude. Let's say you make a follow-up request that includes the same message from earlier, plus Claude's previous response, plus a new message to continue the conversation.

Prompt caching offers several advantages:

- Requests that use cached content are cheaper and faster to execute
- Initial request will write to the cache
- Follow up requests can read from the cache
- Cache lives for 5 minutes
- Only useful if you're repeatedly sending the same content (but this happens extremely frequently)

The cache has a 5-minute lifespan, so it's most beneficial for conversations or workflows where you're making multiple requests with overlapping content within a short timeframe. This pattern is actually very common in real applications - think about chatbots, document analysis tools, or any system that maintains conversation context.

Prompt caching is particularly valuable because many AI applications do repeatedly send the same content. Whether it's system prompts, conversation history, or large documents being analyzed, the same text often appears across multiple requests in a session.

![[Pasted image 20260819202319.png]]

> [!warning] 
> The content must be **AT LEAST** 1024 tokens long to be cached (sum of all messages / parts to be cached)
 

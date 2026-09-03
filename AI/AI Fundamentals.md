AI is a discipline that has to do with the theory and methods to build machines that think and act like humans

The **Machine Learning** process has 2 main forms of "Learn":

- **Supervised:** Labeled data (Expected outcome)
- **Unsupervised:** Unlabeled data (weights)

The **Deep Learning** is more like a recreation of neural network and there are 2 main models:

- **Discriminative model:** Are used to classify models through datapoins (Predicts if an image is a dog)
- **Generative model:** Generate new data, based on existing data (Generates a new dog based on a original dog)

## Gen AI
It is a type of Artificial Intelligence that creates new content based on what it has learned from existing content

## Large Language Models (LLMs)
These are a subset of Deep Learning and are trained to solve common language problems, like:
Text classification, Question Answering, Document summarization, Text generation.

Now how does these models works, well most of the models works in a similar way, they al have their own functions or strategies, but the bases are pretty similar, we will take as an example [[ClaudeCode]] for this explanation, but in a similar way works with any other model.

### Divide the request in tokens (Tokenization)
First the model divides the question in tokens the tokens are chunks of the original request, a chunk could be a word, a line, white spaces or a word and part of other word, it variates depending the model or the LLM.

### Give to each token a value (Embedding)
Embedding is a long list of numbers of different values, each position of the list represent how much a token fits in to a specific classification, we don't know what represents each position exactly but based on that the LLM is how it understand the question.

This technique is also used into [[RAG Retrieval Augmented Generation#Text Embedding|RAG implementations]]
![[Pasted image 20260822153332.png]]
### Contextualization
After Embedding, we have a problem, and is that a word can have different meanings depending the context, and the context depends of the whole phrase and the context itself. In order to get a better result the LLM adjust the initial values of the lists with the values of the other chunks.
![[Pasted image 20260822154957.png]]

### Generation
The contextualized embeddings pass through an output layer that calculates probabilities for each possible next word. Claude doesn't always pick the highest probability word - it uses a mix of probability and controlled randomness to create natural, varied responses.
![[Pasted image 20260822155059.png]]

After selecting each word, Claude adds it to the sequence and repeats the entire process for the next word.
## The Three Major Generations of LLMs
### 1. Completion Models
The earliest style.

Examples:
- GPT-2
- GPT-3 (original)
- Many open-source base models

They simply continue text.
```
Question:What is 2 + 2?Model:The answer is 4.
```

No special reasoning process. Just next-token prediction.
### 2. Instruction-Tuned Models

Examples:
- GPT-3.5
- GPT-4
- Llama Instruct models
- Mistral Instruct models

These models are trained to follow instructions.

```
User:Summarize this article.

Model:Here is the summary...
```

They still predict tokens sequentially, but they've learned conversational behavior.

### 3. Reasoning Models

Examples:
- OpenAI's reasoning-oriented models
- Some DeepSeek reasoning variants
- Other research reasoning models

These models are optimized to spend more computation before producing the final answer.
Instead of:
```
Question↓Answer
```
They operate more like:
```
Question
↓
Internal reasoning
↓
Verification
↓
Answer
```
Advantages:
- Better math
- Better planning
- Better debugging
- Better multi-step reasoning

Disadvantages:
- Slower
- More expensive
- Sometimes overkill

## How to manage them:

There are different techniques about how to manage an LLM or an agent depending the expected result and the tasks that are performing.
For developers we use [[What is SDD|Spec Driven Development]] in order to make a more accurate response in code.
For Project manager there are Planner-Executor or even for Research there are a Scientific Agent to get the better results in the research.

## State of art in Software Development
In software development there are many standards to use AI agents and tools that helps users works with them, some of them are:
- [[What is SDD|SDD]]
- [[MCP]]
- [[RAG Retrieval Augmented Generation||RAG]]
- Automation(n8n,openCode)

Also there are different tools to use them, as they have their own configuration and main files to use them correctly:
- [[ClaudeCode]] (Anthropic)
- ChatGPT (OpenIA)
- Copito (Microsoft)
- Gemini (Google)



To make requests to the AWS bedrock there is the simplest structure:
```python
import boto3 

client = boto3.client("bedrock-runtime", region_name="us-west-2")# Inizialized the model, notice that it was inicialized in a specific region (us-west-2)
user_message = { 
	"role": "user",
	"content": [
		{"text": "What's 1+1?"}
	] 
}

model_id = "us.anthropic.claude-sonnet-4-20260614-v1:0"# This is the inference profile route for the spected model (Just in case this model isn't in us-west-2).

response = client.converse(
	modelId=model_id,
	messages=[user_message]
)# The converse is a function that allows to send messages to the bedrock model

response["output"]["message"]["content"][0]["text"] # This is just to get througt the json response to the actual response "text"

```

This is ok but this will create that each time a new message is sent, then this will be a brand new question. This solution do not keep track of the context of the chat.
To solve that we should send an array with the questions and responses made before.
```python
import boto3 

client = boto3.client("bedrock-runtime", region_name="us-west-2")# Inizialized the model, notice that it was inicialized in a specific region (us-west-2)
model_id = "us.anthropic.claude-sonnet-4-20260614-v1:0"# This is the inference profile route for the spected model (Just in case this model isn't in us-west-2).
messages=[]

def add_user_message(messages, text):
	user_message = { 
		"role": "user",
		"content": [
			{"text": text}
		] 
	}
	messages.append(user_message)

def add_assistant_message(messages, text):
	assistant_message = { 
		"role": "assistant",  # The assistant is the response of the agent
		"content": [
			{"text": text}
		] 
	}
	messages.append(assistant_message)
while true:
	# suppouse that the user enter a message to keep track of.
	any_user_message = "tell me how to deploy a PostgreSQL database"
	#-----------------------------
	add_user_message(messages, any_user_message)
	#-----------------------------
	# The converse is a function that allows to send messages to the bedrock model
	response = client.converse(
		modelId=model_id,
		messages=messages 
	)
	#Notice that in the last example the messages were the text inside an array. Over here it is the array
	assistant_text_response = response["output"]["message"]["content"][0]["text"] # This is just to get througt the json response to the actual response "text"
	#----------------------------
	add_assistant_message(assistant_text_response)
	#----------------------------
```
Now with this implementation the model will keep track of the historial of the conversation cause now we passes the questions and the answers **Important ALWAYS it should keep the  structure** [user, assistant, user, assistant] It should never be 2 users questions in a row or assistant.

## System Prompt
When building AI chatbots for specific use cases, you need a way to control how the AI responds. System prompts are the key to transforming a general-purpose AI into a specialized assistant that follows specific guidelines and stays on topic.

Let's implement a System prompt to create a AWS specialist:
```Python
system_prompt = """ You are an AWS cloud support specialist. Your job is to answer user queries related to cloud hosting services on AWS. """
```
Now when calling the client we should pass the system_prompt:
```Python
response = client.converse(
	modelId=model_id,
	messages=messages,
	system=[{"text": system_prompt}] ## This will avoid different answers
)
```
## Setting Temperature in Code

By default, Claude's [[Temperature]] is set to 1.0, which means maximum creativity. You can override this by adding temperature to your inference configuration:

```Python
response = client.converse(
	modelId=model_id,
	messages=messages,
	"inferenceConfig": {"temperature": 0.2},
	system=[{"text": system_prompt}]
)
```

## Adding tools:
[[Tool Use|Tools]] are the best way give the models power-ups due it allows it to interact with the 'world', tools are no more than code that can be executed to perform any action we want, with a result.
If we want the model to use a tool we need first pass the [[JSON schema spec]] of the allowed tools:
```Python
response = client.converse(
	modelId=model_id,
	messages=messages,
	"inferenceConfig": {"temperature": 0.2},
	system=[{"text": system_prompt}]
	toolConfig={
		"tools":[...tools ] # List of all the json Schemas of the tools
		"toolChoise":{
			"auto":{} # This is the default value of the toolChoise
		}
	}
)
```
The *tooChoise* param, could have the next attributes:
![[Pasted image 20260818092906.png]]

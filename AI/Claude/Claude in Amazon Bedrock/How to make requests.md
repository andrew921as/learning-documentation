First of all, the models in Amazon Bedrock are independent models from the Anthropic API, those are self hosted in the Amazon servers and has their own documentation, so when building from there, make sure to follow the right documentation.

## Models Id's and region Availability

Not every model is available in every AWS region. If you try to run a model that doesn't exist in your chosen region, you'll get a cryptic error message saying the model doesn't exist.

![[Pasted image 20260812233737.png]]

To solve this we have **Inference Profile**
Inference profiles solve the regional availability problem by automatically routing your requests to a region where your chosen model is actually hosted.
![[Pasted image 20260812233831.png]]

## Now how to make the requests?
With Python this is an example code to make the requests:
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

There are other several parameters to work with see [[Enriching requests]]
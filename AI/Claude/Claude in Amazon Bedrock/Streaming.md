There is a property with the client that is the converse_stream, the converse_stream allows us to get chunks of the response while the LLM generates the whole response. This will give a more chat like view to the app or response.
```Python
response = client.converse_stream(messages, modelId=model_id) # Notice we use converse_stream and no converse
for event in response["stream"]:
	print(event)
```

![[Pasted image 20260814102416.png]]

```Python
text = "" 
for event in response["stream"]:
	if "contentBlockDelta" in event:
		chunk = event["contentBlockDelta"]["delta"]["text"]
		print(chunk, end="")
		text += chunk
		
print("\n\nTotal Message:\n" + text)
```

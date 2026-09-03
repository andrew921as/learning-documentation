 The schema has two main parts: the name and description at the top (which help Claude understand when to use the tool), and the actual schema that describes the function's arguments.
 ![[Pasted image 20260818084530.png]]

There are tons of tools online that helps to build a JSON schema, so we can use it.

We just simply past the JSON of our arguments with examples to one of the converters like *JSON to JSON schema* in internet and it will return an example of the schema for the function, at least of the inputSchems.

![[Pasted image 20260818085732.png]]

Then we just need to add it to the whole schema of the function in the section of 
```json
'toolSpec':{
	'name':"descriptive_function_name"
	'description':"",
	'inputSchems'{
		'json':{
			... //The generated code goes here
		}
	}
}
```

**Best practices:**
- [[Tool Design Interface|Explain what the tool does, when to use it and what it returns]]
- Aim for 3 to 4 sentences
- Provide super detailed descriptions
![[Pasted image 20260818085013.png]]


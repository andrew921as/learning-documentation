A typical prompt evaluation workflow follows a systematic approach to objectively measure and improve your prompts. While there are many different ways to assemble these workflows and various open source and paid tools available, understanding the core process helps you start small and scale up as needed.

![[Pasted image 20260814153838.png]]

As the image described up there are 5 different phases, and those are:

### Draft a Prompt
First we will start with a prompt that we think it could achieve the results we are expecting (Take into account that these promps are designed to enrich the actual user prompt like a [[Enriching requests|System Prompt]])
### Create an Eval Dataset
Then we need to create a dataset of possible questions or 'continuation' for a prompt. It could be tens, hundreds or thousands of questions to feed with.

**Hint:** We wan use the AI to generate the datasets, using the SDK of any IA assistant and similar functionalities like the ones on: [[Enriching requests]], [[Temperature]] or [[Controlling model output]]

### Feed it to a LLM
In the example it says Claude but this iteration can be done with any model. The expectation is to ask the selected LLM all the information of the Eval Dataset

### Feed Through a Grader
Then we need it to be pass all the  answers of the LLM to a grader, the grader will put a score to each one of the answers of the LLM and the we should take the average score.

![[Pasted image 20260814203646.png]]



### Change prompt and repeat
Now it is time to change words, add phrases or think of what should be done so the average score increases. Then repeat each one of the steps until you get a 'good' average score.


![[Pasted image 20260814155325.png]]

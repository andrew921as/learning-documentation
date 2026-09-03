Retrieval Augmented Generation (RAG) is a technique that helps you work with large documents by breaking them into smaller pieces and only feeding the LLM the most relevant chunks for each question. Instead of overwhelming the model with an entire 800-page financial report, RAG lets you extract just the sections that matter for answering specific queries.

When you have a massive document and want to ask LLM specific questions about it, you face a fundamental challenge: how do you get the right information to Claude without hitting limits or degrading performance?

![[Pasted image 20260819085512.png]]

## Chunk source text
To chunk the source text is the most complex step in the RAG process, depending on how do we chunk the text this is how easy will be for the LLM to answer the questions provided, and if it has enough context to answer it.
![[Pasted image 20260819090217.png]]
## How to find the relevant chunk?
Finding the right chunk is more a search problem - you need to look through all the text chucks and identify the ones that relate to what the user is asking about.
The challenge is determining which chunks are "related" to a user's question. This isn't as simple as keyword matching - you need to understand the meaning and context of both the question and the chunks.

The most common solution is **semantic search**, which uses text embeddings to understand what each piece of text is actually about, rather than just looking for exact word matches.

### Text Embedding
A text embedding is a numerical representation of the meaning contained in some text. Think of it as converting words and sentences into a format that computers can work with mathematically.
Here's how it works:

- You feed text into an embedding model
- The model outputs a long list of numbers (typically 1024 numbers)
- Each number represents a "score" for some quality of the input text
- The numbers range from -1 to +1

Each number in an embedding is like a score for some aspect of the text. While we don't know exactly what each position represents, it's helpful to think of them as measuring different qualities.

Example of how we can see each number
![[Pasted image 20260819093325.png]]
For creating these embedding text we can use some AWS services to analyze each chunk.
```Python
def generate_embedding(
    text,
    embedding_model_id="amazon.titan-embed-text-v2:0",
    dimensions=1024,
    normalize=True,
):
    request_body = {
        "inputText": text,
        "dimensions": dimensions,
        "normalize": normalize,
    }
    
    request_json = json.dumps(request_body)
    response = client.invoke_model(
        modelId=embedding_model_id,
        body=request_json,
        accept="application/json",
        contentType="application/json",
    )
    
    response_body = json.loads(response.get("body").read())
    return response_body["embedding"]
```

Then the Array resulted from this embedding will be stored in a vector database ad some calculations should be done in order to find the closest vector value to the user query.
![[Pasted image 20260819105114.png]]

## How to improve the search

We can use a combination of the **semantic search** an a lexical search to find the most relevant chunks. To le lexical search the most common and used is the BM25

BM25 (Best Match 25) is a popular algorithm for lexical search in RAG pipelines. Here's how it processes a search query:

![[Pasted image 20260819113800.png]]
So now we want to combine the results of the semantic search and the lexical search as both has some similar methods as we can see:
![[Pasted image 20260819132845.png]]

So if we can put both values together we should create a Reciprocal Rank Function
![[Pasted image 20260819135103.png]]
And has the formula:
![[Pasted image 20260819135214.png]]

## Reranker?
Yes we need a reranker to increase the accuracy of which chunks we select to pass to the AI
![[Pasted image 20260819140646.png]]
The re-ranking prompt is designed to be clear and specific. You provide Claude with the user's question and all the documents that seem relevant, then ask for a simple task: return the most relevant documents in order of decreasing relevance.

The re-ranker function gets called automatically by your retriever after the initial hybrid search. Here's the basic structure:

```Python
def reranker_fn(docs, query_text, k):
    # Format documents with IDs
    joined_docs = "\n".join([
        f"<document><document_id>{doc['id']}</document_id>"
        f"<document_content>{doc['content']}</document_content></document>"
        for doc in docs
    ])
    
    # Create prompt with user question and documents
    prompt = f"""You are about to be given a set of documents...
    {query_text}
    {joined_docs}
    """
    
    # Get Claude's response and parse the document IDs
    result = chat(messages, stop_sequences=["```"])
    return json.loads(result["text"])["document_ids"]
```

## Contextual retrieval
We will ask the LLM to add more context to the text or chunk so now we have a contextualized chunk
![[Pasted image 20260819142530.png]]

To handle large documents maybe these documents might me too much to the LLM to process, so for that we could feed the context of a chuck with a bunch of other chunks:
![[Pasted image 20260819142746.png]]
The chunking strategies is one of the most important things in our RAG system, all the answers that our agent will provide are going to be based on the chunks that we provide it. If we have bad chunks we will have bad answers. the final answer generation is only as good as our chunks.

### Problems with bad chunking:
1. **Too small:** Lacks context
2. **Too large**: Too much noise, hits embedding model/context window limits.
3. **Poor boundaries:** Splits related information
4. **No structure awareness:** Ignores document format.

## Character Text Splitter
This is the basic chunk strategy where we select a number of characters that will cover a chunk, we give them a margin of more or less characters to overlap and then we just separate the selected number of words.

It is useful for simple, uniform documents or when speed matters most.

The objective of the overlap is that 2 chunks will have text duplicated and at the beginning and at the end so it could keep more context, for example if I want to divide my text every 50 word I could give the chunk 10 words of margin; it would take the last 10 words of the last chunk and the first 10 words of the next chunk.

## Recursive Character Text Splitter
The objective here is to split the chunks at natural language boundaries like paragraphs, sentences or words, the idea is to keep a better context, since it is supose for example that the end of a paragraph is the end of an idea.
- Falls back gracefully if chunks too big
- Preserves more context than basic splitting
## Document-Specific Splitting
The idea here is to split depending the document type, since each document could have valuable information depending the type and each one will gets appropriate treatment , for example:
- **PDF**: Splits by pages, sections, headers
- **Markdown:** Splits by headers, code blocks, lists

## Semantic Splitting (Content-aware boundaries)
This strategy uses embeddings to detect topic shifts, the objective is to keep related concepts together and only splits when the meaning changes, not just by size or arbitrary limits.
This is more intelligent but computationally expensive.

## Agentic Splitting (AI-powered chunking)
The concept is that an LLM analyzes content and decides optimal splits, this allows the chunking to be as rich as possible since this could understand complex relationships between ideas and concepts. Also this brings an adaptability that no other model until now could reach since no matter the content the LLM could understand the topic.

The bad part is that is the most expensive method and the slowest one

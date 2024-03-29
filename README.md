OCHA AI Chat Module
===================

This module provides a "chat" functionality to perform queries against ReliefWeb documents via AI (large language models).

This implements a RAG (retrieval augmented generation) approach:

1. Get ReliefWeb documents so that we have a limited scope for the question.
2. Extract texts from the documents and their attachments
3. Split the texts into passages (smaller texts)
4. Generate embeddings for the passages
5. Store the passages and their embeddings in a vector database
6. Uppon query, generate the embedding for the question
7. Retrieve relevant passages from the vector store using a cosine similarity between the question embedding and the passage embeddings.
8. Generate a prompt with the relevant passages, asking the AI to only answer based on the information in those passages
9. Pass the prompt to a Large Language Model to get an answer to the question

Plugins
-------

The module uses a system of [plugins](src/Annotation) to handle the different components of the
functionality

- Completion plugins: handle the answer generation from inference models
- Embedding plugins: handle the generation of embeddings from embedding models
- Source plugins: handle the source of documents
- TextExtractor plugins: handle text extraction for files
- TextSplitter plugins: handle splitting texts into smaller ones
- VectorStore plugins: handle storage and retrieval of texts and embeddings

Service
-------

The "chat" functionality is provided by the [OchaAiChat](src/Sercices/OchaAiChat.php) service. This service glues the different plugins together.

TODO
----

**Plugins**

- [ ] OpenSearch vector store plugin.
- [ ] Cache RW search conversion separately.

**Improve answer**

- [ ] Filter on the length of the extract (ex: at least 4 words)?
- [ ] Refine prompt, maybe separate each extract with some prefix like "Fact:" so that the AI understands they are separate pieces of information.

**Logging**

- [ ] Log requests (debug mode --> add setting to plugins).
- [ ] Log number of pages, passages and estimated count of tokens.

**Dependencies**

- `apt install mupdf-tools`


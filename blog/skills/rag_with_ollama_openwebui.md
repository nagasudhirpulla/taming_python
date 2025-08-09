# Offline RAG with Ollama and Openwebui

## Overview of the setup

-   The following example setup implements an LLM with RAG capability to serve as an expert system that uses documentation to answer user queries.
-   The required pdf documents are provided as a knowledge base to the system.
-   Since the whole setup is offline, confidential data can be provided to the LLM

### Overview of RAG

-   Expert systems based on a knowledge base of PDF documents can be created using Retrieval Augmented Generation (RAG).
-   This requires an LLM and a searchable knowledge base (content indexed in a vector database for performing similarity searches)
-   The user query will be used to retrieve most relevant content from the knowledge base by performing a semantic search on the knowledge base. The LLM will summarize the content from vector database and provide it as a response.

### Illustration of RAG
![rag architecture](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/RAG%20architecture.png?raw=true)
### Illustration of vector database for documents
![vector database for embeddings architecture](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/Vector%20database%20for%20embeddings%20architecture.png?raw=true)

-   Data is stored as document snippets with embedding attached to it​ 
-   Embedding is a vector that positions a document to similar ones​
![vector database embeddings illustration.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/vector%20database%20embeddings%20illustration.png?raw=true)

## Solution Architecture

-   Ollama is a platform to run various large language models (LLMs) locally on a machine.
-   Openwebui provides a web interface for interacting with large language models. It also provides a UI to add RAG capability to the LLM models. It is a web server that can be run as a docker container

## Installation

-   Ollama is installed
-   A base language model like Llama 3.2 (3 billion parameter model) can be installed with ollama using a command like ollama run llama3.2
-   Docker desktop is installed and openwebui docker container is created in docker using the command

```bash
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main

```

-   The logs of the container can also be viewed in docker desktop interactively.
![openwebui docker logs demo](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/Openwebui%20docker%20logs%20demo.png?raw=true)

## Setup Knowledge base in Openwebui

-   Create a knowledge base with the required pdf documents in the Workspace->Knowledge tab

![openwebui knowledge base demo](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/Openwebui%20knowledge%20base%20demo.png?raw=true)

## Create an expert system in Openwebui

-   Create a model in the workspace->Models section with the following settings. Document from the knowledge tab is also linked to the model

![openwebui expert system config](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/Openwebui%20expert%20system%20config.png?raw=true)

-   Now the model will provide answers by looking up the knowledge base

![openwebui expert system demo](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/Openwebui%20expert%20system%20demo.png?raw=true)

## References

-  Openwebui docs - https://docs.openwebui.com/features/rag
-  Openwebui GitHub - [https://github.com/open-webui/open-webui?tab=readme-ov-file#installation-with-default-configuration](https://github.com/open-webui/open-webui?tab=readme-ov-file#installation-with-default-configuration)
-   Ollama Models - [https://ollama.com/library/llama3.2](https://ollama.com/library/llama3.2)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA2NTMyMDUwMywtMzUwMjIxNjYyLDE2Mj
AwNzg2NTZdfQ==
-->
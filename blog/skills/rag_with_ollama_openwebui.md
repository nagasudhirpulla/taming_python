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

### Illustration of vector database for documents

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

## Setup Knowledge base in Openwebui

-   Create a knowledge base with the required pdf documents in the Workspace->Knowledge tab

## Create an expert system in Openwebui

-   Create a model in the workspace->Models section with the following settings. Document from the knowledge tab is also linked to the model

-   Now the model will provide answers by looking up the knowledge base

## References

-   Openwebui - [https://github.com/open-webui/open-webui?tab=readme-ov-file#installation-with-default-configuration](https://github.com/open-webui/open-webui?tab=readme-ov-file#installation-with-default-configuration)
-   Ollama - [https://ollama.com/library/llama3.2](https://ollama.com/library/llama3.2)

[https://youtu.be/2TJxpyO3ei4?si=A7q-rFwkZ7FcP2RW](https://youtu.be/2TJxpyO3ei4?si=A7q-rFwkZ7FcP2RW)

-   [https://youtu.be/fFgyOucIFuk?si=fFht9KCXmaY-937X](https://youtu.be/fFgyOucIFuk?si=fFht9KCXmaY-937X)
    -   [https://youtu.be/xHxIq5Xvzx4?si=2mT46xnVKfDPqVVH](https://youtu.be/xHxIq5Xvzx4?si=2mT46xnVKfDPqVVH)
    -   [https://youtu.be/DYhC7nFRL5I?si=FskpeOPhbDuHgC8s](https://youtu.be/DYhC7nFRL5I?si=FskpeOPhbDuHgC8s)

[Embeddings and Vector Databases](https://www.notion.so/Embeddings-and-Vector-Databases-16247f92c7558014a77dfabf456bf299?pvs=21)

[https://www.gpu-mart.com/blog/how-to-install-and-use-ollama-webui-on-windows](https://www.gpu-mart.com/blog/how-to-install-and-use-ollama-webui-on-windows)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk1MDEzOTAyNV19
-->
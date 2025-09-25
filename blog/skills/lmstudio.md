## What is LM Studio

-   LM Studio is used to run LLMs locally in servers or laptops running Windows / macOS / Linux
-   LM Studio can also Intel or AMD integrated GPUs in addition to NVDIA GPUs. This is useful to run LLMs faster in laptops that do not have NVDIA GPUs

## Installation

-   Download the software (exe / dmg / AppImage) from [https://lmstudio.ai/download](https://lmstudio.ai/download) and install

## Download Models in LM Studio

-   Models can be downloaded from LM Studio application in the explore tab as shown below

![](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/lmstudio_model_explorer.png?raw=true)

-   Models can be downloaded from commad line interface using the `lms get` command as shown below. The documentation for `lms get` can be found at [https://lmstudio.ai/docs/cli/get](https://lmstudio.ai/docs/cli/get)

```bash
lms get llama-3.1-8b --yes

```

![](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/lmstudio_model_download_from_cli.png?raw=true)

## LM Studio chat interface

-   LM Studio application provides chat interface
-   First load a downloaded model in the top bar and then chat with the loaded model

![](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/lmstudio%20chat%20interface.png?raw=true)

## Chat in command line with LM Studio CLI

-   lms command line tool can be used to chat with models in command line
-   First load a model with `lms load` command
-   Then chat with model using `lms chat`

## LM Studio python SDK

-   Python code can interact with LM Studio models using the python SDK
-   The SDK can be installed in python environment using `pip install lmstudio`
-   The following example demonstrates using lmstudio python SDK

```python
import lmstudio as lms

with lms.Client() as client:
    model = client.llm.model("meta-llama-3.1-8b-instruct")

    # Create a chat with an initial system prompt.
    chat = lms.Chat()
    chat.add_system_prompt("Answer the upcoming questions with in 20 words")

    queries = ["Who is Einstein",
               "What countries did this person live in"]
    
    for q in queries:
        chat.add_user_message(q)
        responseStream = model.respond_stream(chat)
        for fragment in responseStream:
            print(fragment.content, end="", flush=True)
        print("\\n*****************************************************")

```

-   The output would be something like below

```
Theoretical physicist Albert Einstein, famous for relativity and E=mc² theory.
*****************************************************
Albert Einstein was a famous physicist and mathematician.

Countries he lived in:
1. Germany
2. Switzerland (permanent residence)
3. Austria
4. Portugal
5. Belgium
6. Italy
7. United States (on vacation)
*****************************************************

```

-   Documentation on chatting with LLM in python can be found at [https://lmstudio.ai/docs/python/llm-prediction/chat-completion](https://lmstudio.ai/docs/python/llm-prediction/chat-completion)

## RAG in LM Studio (Talk with documents)

-   For answering queries using RAG (Retrieval Augmented Generation), the documents will be converted to a searchable vector database where the model will use relavent citations to produce a response
-   Documents can be attached in a chat to use the RAG feature as shown below

![](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/lmstudio_rag.png?raw=true)

## Delete Models from LM Studio

-   In LM Studio app, goto Models directory menu and delete the models

![](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/lmstudio_models_folder.png?raw=true)

## References

-   LM Studio docs - https://lmstudio.ai/docs/app
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY2OTM4OTMzNiwtMTMzMzM1NDQ3MV19
-->
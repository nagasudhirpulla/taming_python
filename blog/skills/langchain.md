# Chat with OpenAI / Ollama / LM Studio LLMs in python using Langchain
- Langchain is a framework to easily create LLM based apps

## LLM vendor abstraction in Langchain

- Langchain creates a wrapper around multiple LLM types (OpenAI, Anthropic, Ollama) to provide a single python interface
- In the below example, the `model` object can be any of OpenAI or Anthropic or Ollama LLM. But the `invoke` function can be called in all the cases. This results in effortless switching of LLM platforms

```python
# pip install langchain-openai
from langchain_openai import ChatOpenAI
model = ChatOpenAI(
    model="llama-3.2-3b-instruct",
    base_url="http://localhost:1234/v1",
    api_key="not_required",
)

# pip install langchain-anthropic
from langchain_anthropic import ChatAnthropic
model = ChatAnthropic(
    model="claude-3-7-sonnet-20250219",
    temperature=0,
    max_tokens=1024,
    timeout=None,
    max_retries=2,
    # api_key="...",
    # base_url="...",
    # other params...
)

# pip install langchain-ollama
from langchain_ollama import ChatOllama
model = ChatOllama(
    model="llama3.1",
    temperature=0,
    # other params...
)

messages = [
    (
        "system",
        "You are a helpful assistant that translates English to French. Translate the user sentence.",
    ),
    ("human", "I love programming."),
]
aiMsg = model.invoke(messages)
print(aiMsg.content)
```

## Message type

- Each message passed to an LLM can have a `type` as any of `system`, `ai`, `human`, `tool` to make LLM understand the message type
- A message can be a simple tuple like `("human", "Tell me a joke.")` or an object like the following
    
    ```python
    from langchain_core.messages import HumanMessage
    HumanMessage(content="I love programming.")
    ```
    

## Prompt Template

- Prompt template can be used to give multiple messages in a structured way to the model. This increases code readability
- In the below example, a prompt is passed to model using `prompt | model` (chaining)
- Notice that the messages are passed to the prompt template using `MessagesPlaceholder`

```python
from langchain_core.prompts import ChatPromptTemplate, MessagesPlaceholder
from langchain_core.messages import SystemMessage, HumanMessage
from langchain_openai import ChatOpenAI

prompt = ChatPromptTemplate.from_messages(
    [
        SystemMessage(
            content="You are a helpful assistant that translates English to French. Translate the user sentence."
        ),
        MessagesPlaceholder(variable_name="messages")
    ]
)

model = ChatOpenAI(
    model="llama-3.2-3b-instruct",
    base_url="http://localhost:1234/v1",
    api_key="not_required",
)

chain = prompt | model

messages = [
    HumanMessage(content="I love programming."),
]

aiMsg = chain.invoke({"messages": messages})
print(aiMsg.content)

```

## Chat history

- Context of an ongoing conversation can be provided to an LLM by providing the list of messages of the conversation till now
- The below example, simply uses a list of messages to maintain the conversation history

```python
from langchain_core.messages import HumanMessage, SystemMessage, AnyMessage, trim_messages
from langchain_core.prompts import ChatPromptTemplate, MessagesPlaceholder
from langchain_openai import ChatOpenAI

prompt = ChatPromptTemplate.from_messages(
    [
        SystemMessage(
            content="You are a helpful assistant. Answer all questions to the best of your ability within 15 words."
        ),
        MessagesPlaceholder(variable_name="messages")
    ]
)

model = ChatOpenAI(
    model="llama-3.2-3b-instruct",
    base_url="http://localhost:1234/v1",
    api_key="not_required",
)

chain = prompt | model

queries = [
    "Who is Albert Einstein?",
    "When did he die?",
    "What is he known for?",
    "What were his notable awards?",
    "Who am I talking about?"
]

chatHistory = []

def trimMessages(messages: list[AnyMessage], maxMsgsLimit: int = 4) -> list[AnyMessage]:
    # count each message as 1 "token" (token_counter=len) and keep only the last n messages
    trimmer = trim_messages(
        strategy="last", max_tokens=maxMsgsLimit, token_counter=len)
    return trimmer.invoke(messages)

def summarizeMessages(
    messages: list[AnyMessage], minMsgCntForSumm: int = 6
) -> list[AnyMessage]:
    if len(messages) < minMsgCntForSumm:
        return messages
    else:
        # Invoke the model to generate conversation summary
        summaryPrompt = (
            "Distill the above chat messages into a single summary message. "
            "Include as many specific details as you can."
        )
        summaryMessage = model.invoke(
            messages + [HumanMessage(content=summaryPrompt)]
        )
        return [summaryMessage]

for qStr in queries:
    q = HumanMessage(content=qStr)

    # option 1 - trim messages
    # chatHistory = trimMessages(chatHistory)
    
    # option 2 - summarize messages
    # chatHistory = summarizeMessages(chatHistory)
    
    # print(f"Chat length = {len(chatHistory)}")

    chatHistory.append(q)
    print(f"Question:\n{qStr}")
    aiResponse = chain.invoke({
        "messages": chatHistory,
    })
    chatHistory.append(aiResponse)
    print(f"Response:\n{aiResponse.content}\n")

# print(chatHistory)

```

- In scenarios where the conversation history crosses the context token limit of the LLM, chat history can be trimmed or summarized to limit the chat history fed to the LLM
- `trimMessages` function in the above example considers only latest messages and ignores old messages
- `summarizeMessages` function in the above example replaces the chat history with a summarized version to reduce the chat history size

## Multiple chat sessions

- The chat history can be saved by grouping on chat sessions / threads
- Only the chat messages corresponding to the required thread can be passed to LLM
- This way multiple chat threads can be executed with a single LLM

```python
from langchain_core.messages import HumanMessage, SystemMessage
from langchain_core.prompts import ChatPromptTemplate, MessagesPlaceholder
from langchain_openai import ChatOpenAI

prompt = ChatPromptTemplate.from_messages(
    [
        SystemMessage(
            content="You are a helpful assistant. Answer all questions to the best of your ability within 15 words."
        ),
        MessagesPlaceholder(variable_name="messages"),
    ]
)

model = ChatOpenAI(
    model="llama-3.2-3b-instruct",
    base_url="http://localhost:1234/v1",
    api_key="not_required",
)

chain = prompt | model

queryThreads = [
    ("Who is Albert Einstein?", 1),
    ("What are the famous opensource LLM models", 2),
    ("When did he die?", 1),
    ("What companies are behind these models", 2),
    ("What were his notable awards?", 1),
    ("Who am I talking about?", 1),
]

chatHistory = {}
for threadId in set([x[1] for x in queryThreads]):
    chatHistory[threadId] = []

for qStr, threadId in queryThreads:
    q = HumanMessage(content=qStr)
    threadChats = chatHistory[threadId]
    threadChats.append(q)
    print(f"Thread {threadId}, Question:\n{qStr}")
    aiResponse = chain.invoke(
        {
            "messages": threadChats,
        }
    )
    threadChats.append(aiResponse)
    print(f"Response:\n{aiResponse.content}\n")

print(chatHistory)

```

## In-built chat threads persistence with Langgraph

- Langgraph provides in-built chat threads persistence support
- Various storage options like in-memory, sqlite, postgres are also present out of the box
- A simple one node Langgraph workflow can be used to create an llm with chat history as shown below
- Langgraph nodes store chat history in the state (a serializable python object). The state can be restored and saved easily using a checkpointer

```python
from typing import Annotated

from langchain_core.messages import HumanMessage, SystemMessage
from langchain_core.prompts import ChatPromptTemplate, MessagesPlaceholder
from langchain_openai import ChatOpenAI
from langgraph.checkpoint.memory import InMemorySaver
from langgraph.graph import StateGraph
from langgraph.graph.message import add_messages
from typing_extensions import TypedDict

prompt = ChatPromptTemplate.from_messages(
    [
        SystemMessage(
            content="You are a helpful assistant. Answer all questions to the best of your ability within 15 words."
        ),
        MessagesPlaceholder(variable_name="messages"),
    ]
)

model = ChatOpenAI(
    model="llama-3.2-3b-instruct",
    base_url="http://localhost:1234/v1",
    api_key="not_required",
)

chain = prompt | model

class State(TypedDict):
    messages: Annotated[list, add_messages]

graph_builder = StateGraph(State)

def callModel(state: State):
    return {"messages": [chain.invoke({"messages": state["messages"]})]}

graph_builder.add_node("chatbot", callModel)
graph_builder.set_entry_point("chatbot")

memory = InMemorySaver()

app = graph_builder.compile(checkpointer=memory)

queryThreads = [
    ("Who is Albert Einstein?", 1),
    ("What are the famous opensource LLM models", 2),
    ("When did he die?", 1),
    ("What companies are behind these models", 2),
    ("What were his notable awards?", 1),
    ("Who am I talking about?", 1),
]

for qStr, threadId in queryThreads:
    state = app.invoke(
        {"messages": HumanMessage(content=qStr)},
        config={"configurable": {"thread_id": threadId}},
    )
    print(f"Thread {threadId}, Question:\n{qStr}")
    print(f"Response:\n{state['messages'][-1].content}\n")

```



## References

- Checkpointer to persist langgraph app state - https://langchain-ai.github.io/langgraph/tutorials/get-started/3-add-memory/#1-create-a-memorysaver-checkpointer
- trimming and summarizing chat history - https://python.langchain.com/docs/how_to/chatbots_memory/#modifying-chat-history
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgxNjUyMjc1NCwtMTU5OTU0MzIwMl19
-->
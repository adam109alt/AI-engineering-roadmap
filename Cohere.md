# 🧠 The Complete Cohere Guide
### For AI Engineers & Developers — From Zero to Agents

---

## 📌 Table of Contents

1. [What is Cohere?](#what-is-cohere)
2. [Why Cohere? (vs OpenAI, Anthropic, etc.)](#why-cohere)
3. [Cohere Models Explained](#cohere-models)
4. [Free Tier vs Paid Tier](#pricing)
5. [Getting Started — Installation & Setup](#getting-started)
6. [Simple Examples](#simple-examples)
   - Chat / Text Generation
   - Embeddings
   - Reranking
7. [RAG (Retrieval-Augmented Generation)](#rag)
8. [Building Agents with Cohere](#agents)
9. [Critical Thinking — When to Use Cohere?](#critical-thinking)
10. [Full Project: Smart Search + Agent](#full-project)

---

## 1. What is Cohere? <a name="what-is-cohere"></a>

### 📖 Theory

Cohere is an **AI company** that gives developers access to powerful language models through an API.

Think of it like this:
> You don't build your own engine when you buy a car. You use the engine Ford or Toyota built. Cohere is that engine for language AI.

Cohere was founded in **2019** by ex-Google researchers (the people who wrote the famous "Attention is All You Need" paper — the paper that invented Transformers, the technology behind ALL modern AI).

Cohere is **enterprise-focused** — meaning it's designed for businesses who need:
- Privacy (you can deploy it on your own servers)
- Customization (fine-tune on your own data)
- Reliability (not just a chatbot, a production system)

Cohere has **three main tools** it gives you:

| Tool | What it does | Simple analogy |
|---|---|---|
| **Command** | Generates text, answers questions, chats | The brain |
| **Embed** | Turns text into numbers (vectors) | The memory |
| **Rerank** | Re-orders search results by relevance | The filter |

> 💡 **New word — "Vector"**: A vector is just a list of numbers. For example, the word "cat" might become `[0.2, 0.8, -0.1, ...]`. Similar words end up having similar numbers. This is how AI understands *meaning*.

---

## 2. Why Cohere? <a name="why-cohere"></a>

### 📖 Theory

Here is a fair comparison:

| Feature | Cohere | OpenAI | Anthropic (Claude) |
|---|---|---|---|
| **Private Deployment** | ✅ Yes (on your servers) | ❌ No | ❌ No |
| **Enterprise Focus** | ✅ Very strong | ⚠️ Moderate | ⚠️ Moderate |
| **Reranking** | ✅ Built-in | ❌ Need third party | ❌ Need third party |
| **Embed Models** | ✅ World-class | ✅ Good | ❌ None |
| **Price (budget models)** | ✅ Cheapest | ❌ Expensive | ❌ Expensive |
| **RAG Support** | ✅ First-class | ⚠️ Needs work | ⚠️ Needs work |
| **Creative Writing** | ⚠️ Moderate | ✅ Great | ✅ Great |

### When should you pick Cohere?
- You need **search** in your app (semantic search, document search)
- You need **private deployment** (your data never leaves your company)
- You are building **enterprise tools** (summarization, search, agents over documents)
- You want **cheaper costs** for high-volume apps

### When should you pick something else?
- You need very creative writing → Claude or GPT-4 is better
- You are building a general chatbot for consumers → GPT is more known

---

## 3. Cohere Models Explained <a name="cohere-models"></a>

### 📖 Theory

Cohere has a **family** of models. Each one is built for a different job.

### 🔵 Command Family (Text Generation)

| Model | Speed | Power | Best For |
|---|---|---|---|
| **Command A** | ⚡ Fastest | 🧠🧠🧠 | Agents, reasoning, enterprise |
| **Command R+** | Medium | 🧠🧠🧠 | Complex tasks, RAG |
| **Command R** | Fast | 🧠🧠 | Everyday tasks, balance |
| **Command R7B** | Very Fast | 🧠 | High-volume, cheap tasks |

> 💡 **Command A** is their newest and most powerful model. It was built *specifically* for agents (multi-step tasks). This is special — most companies don't have a model built just for agents.

### 🟢 Embed Family (Vectors / Semantic Search)

| Model | What's special |
|---|---|
| **Embed v4** | Multimodal — works with text AND images |
| **Embed v3** | Text only, very good |
| **Embed Light** | Smaller, faster, cheaper |

### 🟡 Rerank Family

| Model | Use |
|---|---|
| **Rerank 3.5** | Re-orders search results by relevance |
| **Rerank 3** | Older version, still good |

> 💡 **New word — "Multimodal"**: Multi = many, Modal = type. So multimodal means the model can understand multiple types of data — like both text AND images at the same time.

---

## 4. Free Tier vs Paid Tier <a name="pricing"></a>

### 📖 Theory

Cohere gives you **two types of API keys**:

### 🆓 Trial Key (Free)
- **1,000 API calls per month** — free
- Access to ALL models including Command R+, Rerank, Embed
- Rate limited: 5 calls/minute for Embed, 20 calls/minute for Chat
- ❌ Cannot be used for real production/business apps
- ✅ Perfect for learning, testing, building projects

### 💳 Production Key (Paid)
- Pay-as-you-go (you pay for what you use)
- Billing at end of each month

**Current Prices (2025/2026):**

| Model | Input (per 1M tokens) | Output (per 1M tokens) |
|---|---|---|
| Command R+ (08-2024) | $2.50 | $10.00 |
| Command R | $0.15 | $0.60 |
| Command R7B | $0.0375 | $0.15 |
| Embed v4 (text) | $0.12 | — |
| Rerank 3.5 | per 1K searches | — |

> 💡 **Command R7B is very cheap** — 27x cheaper than competitors for the same task quality. If you are building something that runs millions of requests, this matters a lot.

> 💡 **1M tokens ≈ ~750,000 words** — that is like 10 full novels.

---

## 5. Getting Started <a name="getting-started"></a>

### Step 1 — Get your API key

1. Go to [cohere.com](https://cohere.com)
2. Sign up (free)
3. Go to **Dashboard → API Keys**
4. Copy your Trial key

### Step 2 — Install the SDK

```bash
pip install cohere
```

### Step 3 — Set up your key safely

Never put your API key directly in your code! Use environment variables:

```bash
# In your terminal (or .env file)
export COHERE_API_KEY="your-key-here"
```

```python
import os
import cohere

# os.environ.get() reads from your system environment
# This is safer than writing the key directly in code
co = cohere.ClientV2(api_key=os.environ.get("COHERE_API_KEY"))
```

> ❓ **What happens if you don't use environment variables?**
> If you put your key directly in code and push it to GitHub, anyone can find it, use your account, and you get billed. Many developers have lost hundreds of dollars this way. Always use environment variables.

---

## 6. Simple Examples <a name="simple-examples"></a>

### Example 1 — Chat / Text Generation

#### 📖 Theory
The `chat` endpoint is how you send a message and get a reply. It works exactly like ChatGPT — you send a message, you get text back.

#### 💻 Code

```python
import cohere
import os

co = cohere.ClientV2(api_key=os.environ.get("COHERE_API_KEY"))

response = co.chat(
    model="command-r-plus",     # Which model to use
    messages=[                  # List of messages (like a conversation)
        {
            "role": "user",     # "user" = the human speaking
            "content": "Explain what a neural network is in simple terms."
        }
    ]
)

# The reply is inside response.message.content[0].text
print(response.message.content[0].text)
```

#### 🔍 Code Explanation (slow and careful)

```python
co = cohere.ClientV2(api_key=...)
```
- `ClientV2` — creates a connection to Cohere's server
- `api_key` — proves to Cohere that you are you (like a password)

```python
messages=[{"role": "user", "content": "..."}]
```
- `messages` is a **list** (you can pass a whole conversation history)
- Each message is a **dictionary** with two keys:
  - `role` — who is speaking: `"user"` (you) or `"assistant"` (AI)
  - `content` — what they said

```python
response.message.content[0].text
```
- `response` — the full response object from Cohere
- `.message` — the reply message
- `.content[0]` — the first content block (there could be multiple)
- `.text` — the actual text string

> ❓ **What if you don't pass `model`?**
> Cohere will use a default model, but it might not be what you expect. Always be explicit — it makes your code predictable.

---

### Example 2 — Multi-turn Conversation (Chat History)

#### 💻 Code

```python
import cohere
import os

co = cohere.ClientV2(api_key=os.environ.get("COHERE_API_KEY"))

# We keep a list of messages to remember the conversation
conversation_history = []

def chat(user_message):
    # Add the user's message to history
    conversation_history.append({
        "role": "user",
        "content": user_message
    })
    
    # Send the FULL history to the model
    response = co.chat(
        model="command-r",
        messages=conversation_history
    )
    
    # Get the reply text
    reply = response.message.content[0].text
    
    # Add the AI's reply to history too
    conversation_history.append({
        "role": "assistant",
        "content": reply
    })
    
    return reply

# Test the conversation
print(chat("My name is Ahmed."))
print(chat("What is my name?"))  # The model will remember!
```

> ❓ **What happens if you don't pass conversation history?**
> The model has no memory. It forgets everything said before. Every message is treated as the first message. This is why you must manually pass history — LLMs have NO built-in memory between API calls.

---

### Example 3 — Embeddings

#### 📖 Theory
Embeddings turn text into a list of numbers (a vector). Words/sentences with **similar meaning** end up with **similar numbers**. This is the foundation of semantic search — searching by *meaning*, not just keywords.

For example:
- "I love cats" and "I adore kittens" → similar vectors (close in space)
- "I love cats" and "The stock market crashed" → very different vectors (far in space)

#### 💻 Code

```python
import cohere
import os

co = cohere.ClientV2(api_key=os.environ.get("COHERE_API_KEY"))

response = co.embed(
    texts=[
        "I love programming in Python",
        "Python is my favorite coding language",
        "I enjoy cooking pasta"
    ],
    model="embed-v4.0",          # Use the latest embed model
    input_type="search_document", # We are embedding documents to search later
    embedding_types=["float"]     # Return numbers as floats (decimals)
)

# Each text gets its own vector (list of numbers)
vectors = response.embeddings.float

print(f"Number of vectors: {len(vectors)}")
print(f"Vector size: {len(vectors[0])}")  # How many numbers per vector
print(f"First few numbers of vector 1: {vectors[0][:5]}")
```

#### 🔍 Code Explanation

```python
input_type="search_document"
```
- This tells Cohere *how* the text will be used
- `"search_document"` = these texts will be stored and searched later
- `"search_query"` = this text is what the user is searching for
- This matters! The same sentence embedded as a query vs document gives slightly different vectors, optimized for matching against each other.

> ❓ **What if you don't use embeddings and just do keyword search?**
> If a user searches "car" and your document says "automobile", keyword search fails. With embeddings, it succeeds because both words have similar vectors.

---

### Example 4 — Reranking

#### 📖 Theory
Reranking takes a list of documents and a query, and **re-orders** them by relevance. Think of it as a second pass: first you get 100 results from a fast (but rough) search, then you rerank to pick the best 5.

This is called a **two-stage retrieval pipeline** — used in almost every serious search system.

#### 💻 Code

```python
import cohere
import os

co = cohere.ClientV2(api_key=os.environ.get("COHERE_API_KEY"))

query = "What is the best programming language for AI?"

documents = [
    "Python is widely used in AI and machine learning",
    "JavaScript is popular for web development",
    "Python has libraries like TensorFlow and PyTorch for AI",
    "Java is used in enterprise applications",
    "R is used in statistics and data analysis"
]

response = co.rerank(
    model="rerank-v3.5",
    query=query,           # What the user is searching for
    documents=documents,   # The list of documents to rerank
    top_n=3               # Return only the top 3 results
)

print("Top results after reranking:")
for result in response.results:
    print(f"Score: {result.relevance_score:.3f} | {documents[result.index]}")
```

#### Expected output:
```
Top results after reranking:
Score: 0.985 | Python is widely used in AI and machine learning
Score: 0.971 | Python has libraries like TensorFlow and PyTorch for AI
Score: 0.432 | R is used in statistics and data analysis
```

> ❓ **What if you skip reranking and just return the first results?**
> Your search quality drops significantly. Without reranking, your top results might be *related* but not the *most relevant*. Reranking is what separates mediocre search from great search.

---

## 7. RAG — Retrieval-Augmented Generation <a name="rag"></a>

### 📖 Theory

RAG is one of the most important patterns in AI engineering today. Here's the problem it solves:

**Problem:** LLMs are trained on old data. They don't know your documents. You can't put 1000 PDFs in a prompt (too expensive, too slow).

**Solution:** RAG
1. **Store** your documents as vectors (embeddings)
2. When user asks a question, **search** for the most relevant documents
3. **Give those documents to the LLM** as context
4. LLM answers **based on your documents**

```
User Question → Embed Question → Search Vector DB → Get Top Docs → LLM answers with docs
```

#### 💻 Simple RAG Example (no database, just in memory)

```python
import cohere
import os
import numpy as np

co = cohere.ClientV2(api_key=os.environ.get("COHERE_API_KEY"))

# ---- STEP 1: Your "knowledge base" ----
documents = [
    "Cohere was founded in 2019 by ex-Google researchers.",
    "The Command R model is optimized for retrieval-augmented generation.",
    "Cohere's Embed model converts text into high-dimensional vectors.",
    "Python was created by Guido van Rossum in 1991.",
    "Cohere offers private deployment for enterprise customers."
]

# ---- STEP 2: Embed all documents ----
doc_response = co.embed(
    texts=documents,
    model="embed-v4.0",
    input_type="search_document",
    embedding_types=["float"]
)
doc_vectors = np.array(doc_response.embeddings.float)  # shape: (5, 1536)

# ---- HELPER: cosine similarity ----
# Cosine similarity measures how "close" two vectors are
# Result is between -1 (opposite) and 1 (identical meaning)
def cosine_similarity(a, b):
    return np.dot(a, b) / (np.linalg.norm(a) * np.linalg.norm(b))

# ---- STEP 3: RAG function ----
def rag_answer(user_question, top_k=2):
    
    # Embed the user's question
    q_response = co.embed(
        texts=[user_question],
        model="embed-v4.0",
        input_type="search_query",  # Different input_type for queries!
        embedding_types=["float"]
    )
    q_vector = np.array(q_response.embeddings.float[0])
    
    # Find the most similar documents
    similarities = [cosine_similarity(q_vector, dv) for dv in doc_vectors]
    top_indices = np.argsort(similarities)[-top_k:][::-1]  # Top-k indices
    
    relevant_docs = [documents[i] for i in top_indices]
    
    # Build context from retrieved documents
    context = "\n".join([f"- {doc}" for doc in relevant_docs])
    
    # Ask the LLM to answer based on the context
    response = co.chat(
        model="command-r",
        messages=[{
            "role": "user",
            "content": f"""Answer this question using ONLY the context below.
            
Context:
{context}

Question: {user_question}"""
        }]
    )
    
    return response.message.content[0].text, relevant_docs

# ---- STEP 4: Test it ----
answer, sources = rag_answer("Who founded Cohere?")
print("Answer:", answer)
print("\nSources used:")
for s in sources:
    print(" -", s)
```

> ❓ **What if you don't use RAG and just ask the LLM directly?**
> The LLM will either:
> - Make up an answer (hallucinate — invent false facts)
> - Say "I don't know"
> - Give you outdated information
> RAG solves all three problems.

---

## 8. Building Agents with Cohere <a name="agents"></a>

### 📖 Theory

An **agent** is an AI that can:
1. Understand a goal
2. Decide what **tools** to use
3. Use those tools (call APIs, search, calculate, etc.)
4. Combine results and take the next step

Think of the difference between:
- **Normal LLM**: You ask → It answers → Done
- **Agent**: You give a goal → It plans → It uses tools → It reasons → It gives final answer

Cohere's **Command A** model was built specifically for agents. It is very good at **tool use** — deciding when and how to call external functions.

> 💡 **New word — "Tool use"**: Giving the AI a list of Python functions it can "call". The AI decides when to use them, what arguments to pass, and how to use the result.

#### 💻 Agent with Tool Use

```python
import cohere
import os
import json

co = cohere.ClientV2(api_key=os.environ.get("COHERE_API_KEY"))

# ---- STEP 1: Define tools ----
# These are descriptions of Python functions that the AI can choose to call
tools = [
    {
        "type": "function",
        "function": {
            "name": "get_weather",
            "description": "Get the current weather for a given city",
            "parameters": {
                "type": "object",
                "properties": {
                    "city": {
                        "type": "string",
                        "description": "The name of the city, e.g. Istanbul"
                    }
                },
                "required": ["city"]
            }
        }
    },
    {
        "type": "function",
        "function": {
            "name": "calculator",
            "description": "Do a math calculation",
            "parameters": {
                "type": "object",
                "properties": {
                    "expression": {
                        "type": "string",
                        "description": "A math expression like '25 * 4 + 10'"
                    }
                },
                "required": ["expression"]
            }
        }
    }
]

# ---- STEP 2: Define the actual Python functions ----
def get_weather(city: str) -> str:
    # In real life, call a weather API like OpenWeatherMap
    # For this example, we fake it
    fake_weather = {
        "istanbul": "20°C, Sunny",
        "london": "12°C, Cloudy",
        "dubai": "38°C, Hot and clear"
    }
    return fake_weather.get(city.lower(), "Weather data not available")

def calculator(expression: str) -> str:
    try:
        result = eval(expression)  # eval() runs math expressions
        return str(result)
    except Exception as e:
        return f"Error: {e}"

# ---- STEP 3: Run the agent loop ----
def run_agent(user_message):
    messages = [{"role": "user", "content": user_message}]
    
    print(f"\n👤 User: {user_message}")
    
    while True:
        # Ask Cohere what to do
        response = co.chat(
            model="command-a-03-2025",  # Command A is best for agents
            messages=messages,
            tools=tools
        )
        
        # Add the assistant's response to history
        messages.append({
            "role": "assistant",
            "content": response.message.content
        })
        
        # Check if the AI wants to use a tool
        if response.stop_reason == "tool_use":
            
            tool_results = []
            
            for content_block in response.message.content:
                if content_block.type == "tool_use":
                    tool_name = content_block.name
                    tool_args = content_block.parameters
                    tool_call_id = content_block.id
                    
                    print(f"\n🔧 Agent calling tool: {tool_name}({tool_args})")
                    
                    # Call the actual Python function
                    if tool_name == "get_weather":
                        result = get_weather(**tool_args)
                    elif tool_name == "calculator":
                        result = calculator(**tool_args)
                    else:
                        result = "Tool not found"
                    
                    print(f"📦 Tool result: {result}")
                    
                    tool_results.append({
                        "type": "tool_result",
                        "tool_use_id": tool_call_id,
                        "content": result
                    })
            
            # Add tool results back to the conversation
            messages.append({
                "role": "tool",
                "content": tool_results
            })
        
        else:
            # The AI has finished — give the final answer
            final_answer = ""
            for block in response.message.content:
                if hasattr(block, "text"):
                    final_answer += block.text
            
            print(f"\n🤖 Agent: {final_answer}")
            return final_answer

# ---- STEP 4: Test it ----
run_agent("What is the weather in Istanbul? Also, if there are 7 days in a week and 52 weeks in a year, how many days is that?")
```

#### 🔍 Code Explanation

```python
tools = [{"type": "function", "function": {...}}]
```
- This is a JSON description of tools the AI can use
- The AI does NOT call the function directly
- It *tells us* which function to call and with what arguments
- We then call the real function and give the result back

```python
if response.stop_reason == "tool_use":
```
- When Cohere decides to use a tool, it stops and says "tool_use"
- This is the signal for us to run the real Python function

```python
messages.append({"role": "tool", "content": tool_results})
```
- After running the function, we add the results back to the conversation
- The AI then continues reasoning with this new information

> ❓ **What happens if you don't give tools to the agent?**
> The AI can only use its training data. It cannot look up real-time data, call APIs, do calculations accurately, search your database, or take any action in the world. It becomes just a chatbot.

---

## 9. Critical Thinking <a name="critical-thinking"></a>

### 🤔 Questions to ask yourself

**1. When should I use Cohere Embed vs OpenAI Embed?**
- Cohere Embed v4 supports both text AND images (multimodal)
- Cohere is generally considered to produce better embeddings for non-English languages
- OpenAI's `text-embedding-3-large` is strong for English
- For most RAG projects, both work — test and measure!

**2. Should I always use the biggest model?**
No. Think about cost vs quality:
- For simple summarization → Command R7B (cheap, fast)
- For complex reasoning → Command R+ or Command A
- For agents that need to make decisions → Command A specifically

**3. What is the real difference between RAG and fine-tuning?**

| | RAG | Fine-tuning |
|---|---|---|
| Your data stays updated? | ✅ Yes | ❌ No (snapshot in time) |
| Cost to update? | Low | High (retrain) |
| Model knows "how" things work? | ❌ No | ✅ Yes |
| Best for | Facts, documents, search | Style, format, behavior |

---

## 10. Full Mini Project: Document Q&A System <a name="full-project"></a>

This project combines everything: embeddings + reranking + chat.

```python
import cohere
import os
import numpy as np

co = cohere.ClientV2(api_key=os.environ.get("COHERE_API_KEY"))

class DocumentQA:
    """A simple document Q&A system using Cohere."""
    
    def __init__(self):
        self.documents = []
        self.vectors = []
    
    def add_document(self, text: str):
        """Add a document to the knowledge base."""
        self.documents.append(text)
        
        # Embed it and store the vector
        response = co.embed(
            texts=[text],
            model="embed-v4.0",
            input_type="search_document",
            embedding_types=["float"]
        )
        self.vectors.append(response.embeddings.float[0])
        print(f"✅ Added document: {text[:50]}...")
    
    def search(self, query: str, top_k: int = 5) -> list:
        """Find the most relevant documents using embeddings."""
        
        # Embed the query
        q_response = co.embed(
            texts=[query],
            model="embed-v4.0",
            input_type="search_query",
            embedding_types=["float"]
        )
        q_vector = np.array(q_response.embeddings.float[0])
        
        # Compute similarity with all docs
        vectors_array = np.array(self.vectors)
        similarities = np.dot(vectors_array, q_vector) / (
            np.linalg.norm(vectors_array, axis=1) * np.linalg.norm(q_vector)
        )
        
        # Get top-k indices
        top_indices = np.argsort(similarities)[-top_k:][::-1]
        return [self.documents[i] for i in top_indices]
    
    def rerank_and_answer(self, query: str) -> str:
        """Search, rerank, then answer the question."""
        
        print(f"\n🔍 Searching for: {query}")
        
        # Step 1: Get candidate documents
        candidates = self.search(query, top_k=5)
        
        # Step 2: Rerank them for better precision
        rerank_response = co.rerank(
            model="rerank-v3.5",
            query=query,
            documents=candidates,
            top_n=3
        )
        
        # Get top 3 most relevant docs
        top_docs = [candidates[r.index] for r in rerank_response.results]
        
        print(f"📄 Top documents found:")
        for doc in top_docs:
            print(f"   - {doc[:80]}...")
        
        # Step 3: Build a prompt with the context
        context = "\n".join([f"{i+1}. {doc}" for i, doc in enumerate(top_docs)])
        
        # Step 4: Generate answer
        response = co.chat(
            model="command-r-plus",
            messages=[{
                "role": "user",
                "content": f"""You are a helpful assistant. Answer the question based ONLY on the context provided.
If the context doesn't have enough information, say so.

Context:
{context}

Question: {query}

Answer:"""
            }]
        )
        
        return response.message.content[0].text


# --- Use it ---
qa = DocumentQA()

# Add documents (could be paragraphs from PDFs, website pages, etc.)
qa.add_document("Cohere was founded in 2019 by Aidan Gomez, Ivan Zhang, and Nick Frosst, who were ex-Google Brain researchers.")
qa.add_document("The Command A model by Cohere is specifically optimized for agentic AI tasks and multi-step reasoning.")
qa.add_document("Cohere's Embed v4 model is multimodal, supporting both text and images with 1536-dimensional vectors.")
qa.add_document("Cohere offers private deployment, meaning companies can run Cohere models on their own servers.")
qa.add_document("Python was created by Guido van Rossum and first released in 1991.")
qa.add_document("Reranking is a technique that takes a list of documents and reorders them by relevance to a query.")

# Ask questions
answer = qa.rerank_and_answer("Who are the founders of Cohere?")
print(f"\n💬 Answer: {answer}")

answer = qa.rerank_and_answer("What makes Command A special?")
print(f"\n💬 Answer: {answer}")
```

---

## 🎯 Summary

| You learned | Why it matters |
|---|---|
| What Cohere is | Foundation |
| Models: Command, Embed, Rerank | Know your tools |
| Free tier: 1000 calls/month | Start building for free |
| Chat API | The basics |
| Embeddings | The key to semantic search |
| Reranking | Better search results |
| RAG | Give AI access to YOUR data |
| Agents with tool use | AI that takes actions |

---

## 🔗 Resources

- **Official Docs**: https://docs.cohere.com
- **Pricing**: https://cohere.com/pricing
- **Cohere Playground**: https://dashboard.cohere.com/playground
- **API Keys**: https://dashboard.cohere.com/api-keys
- **Discord**: https://discord.gg/co-mmunity (community help)

---

*Guide written for AI Engineers learning Cohere from scratch. Built with ❤️*

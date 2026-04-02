# 🤖 AI Engineer Roadmap

> My personal learning journey following the [roadmap.sh/ai-engineer](https://roadmap.sh/ai-engineer) roadmap — every concept explained, tracked, and documented.

---

## 📌 About This Repository

This repository is my **complete AI Engineering roadmap** based on [roadmap.sh/ai-engineer](https://roadmap.sh/ai-engineer).  
Each section covers the key concepts, what they mean, why they matter, and the tools used in the industry.

---

## 🗺️ Table of Contents

1. [Introduction](#1-introduction)
2. [Using Pre-trained Models](#2-using-pre-trained-models)
3. [OpenAI Platform](#3-openai-platform)
4. [Prompt Engineering & AI Safety](#4-prompt-engineering--ai-safety)
5. [Open Source AI](#5-open-source-ai)
6. [Embeddings & Vector Databases](#6-embeddings--vector-databases)
7. [RAG & Implementation](#7-rag--implementation)
8. [AI Agents](#8-ai-agents)
9. [Multimodal AI](#9-multimodal-ai)
10. [Development Tools](#10-development-tools)

---

## 1. Introduction

### 🧠 What is an AI Engineer?
An **AI Engineer** uses pre-trained models and existing AI tools to build intelligent applications and improve user experiences. Unlike ML Engineers or AI Researchers, AI Engineers **don't build models from scratch** — they focus on applying AI practically in real-world products.

### ⚖️ AI Engineer vs ML Engineer

| | AI Engineer | ML Engineer |
|---|---|---|
| **Focus** | Applying existing models | Building & training models |
| **Skills** | APIs, RAG, Agents, Prompting | Math, ML theory, model architecture |
| **Output** | AI-powered products | ML models & pipelines |

### 🔑 Core Concepts to Know

| Concept | What It Means |
|---|---|
| **LLMs** | Large Language Models — AI trained on massive text data to understand and generate language |
| **Inference** | Running a trained model to get predictions/outputs (e.g., sending a prompt and getting a reply) |
| **Training** | The process of teaching a model by exposing it to data and adjusting its parameters |
| **Embeddings** | Numerical vector representations of text/data that capture semantic meaning |
| **Vector Databases** | Databases optimized to store and search embeddings using similarity |
| **RAG** | Retrieval-Augmented Generation — combining search with LLMs for grounded answers |
| **Prompt Engineering** | The art of crafting inputs that guide model behavior and outputs |
| **AI Agents** | Autonomous systems that use LLMs to reason, plan, and take actions |
| **AI vs AGI** | Narrow AI solves specific tasks; AGI (Artificial General Intelligence) would match human-level reasoning across all tasks — not yet achieved |

### 🎯 Impact on Product Development
AI Engineers directly accelerate product development by integrating intelligence into:
- Search and recommendations
- Chatbots and virtual assistants
- Document analysis and summarization
- Code generation and automation

---

## 2. Using Pre-trained Models

### What are Pre-trained Models?
Models trained on massive datasets by large organizations (OpenAI, Google, Anthropic, Meta) and made available via APIs or direct download. Instead of training from scratch, you use these as a powerful starting point.

### ✅ Benefits
- Saves time and resources — no need for expensive training runs
- State-of-the-art performance out of the box
- Ready-to-use APIs with minimal setup

### ⚠️ Limitations & Considerations
- **Knowledge cut-off dates** — models don't know about events after their training data ends
- **Context length limits** — models can only process a fixed amount of text at once
- **Hallucinations** — models can confidently produce incorrect information
- **Cost** — API usage is billed per token
- **Privacy** — sending sensitive data to third-party APIs may raise concerns

### 🌐 Popular AI Models

| Provider | Model(s) | Notes |
|---|---|---|
| **OpenAI** | GPT-4o, o1, o3 | Industry standard, powerful reasoning |
| **Anthropic** | Claude 3.5 / Claude 4 | Strong at long context, safety-focused |
| **Google** | Gemini 1.5 / 2.0 | Multimodal, massive context window |
| **Meta** | LLaMA 3 | Open-source, self-hostable |
| **Mistral AI** | Mistral, Mixtral | Fast, efficient, open-source friendly |
| **Cohere** | Command R+ | RAG-optimized, enterprise-focused |
| **Hugging Face** | Various | Hub for thousands of open-source models |
| **Azure AI** | Azure OpenAI | Enterprise-grade OpenAI on Microsoft cloud |
| **AWS SageMaker** | Various | ML platform for training & deploying models |

---

## 3. OpenAI Platform

The most widely used AI API in the industry — understanding it well is foundational.

### 🔌 OpenAI API

**Chat Completions API** — the core endpoint for interacting with GPT models:
```python
from openai import OpenAI

client = OpenAI()
response = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Explain RAG in simple terms."}
    ]
)
print(response.choices[0].message.content)
```

### 📝 Writing Prompts
Effective prompts follow a structure:
- **System message** — define the AI's role and behavior
- **User message** — the actual input or question
- **Assistant message** — prior model responses (for multi-turn conversations)

### 🛝 OpenAI Playground
A browser-based tool to experiment with models, test prompts, adjust parameters (temperature, max tokens), and prototype without writing code.

### 🎯 Fine-tuning
Fine-tuning adapts a base model to your specific task by training on your own examples.

| When to Fine-tune | When NOT to Fine-tune |
|---|---|
| Consistent format/style needed | Prompt engineering can solve it |
| Domain-specific language | You lack enough quality examples |
| Reducing prompt length at scale | Knowledge injection (use RAG instead) |

### 🪙 Managing Tokens

| Concept | Explanation |
|---|---|
| **Tokens** | The units models process — roughly 1 token ≈ 0.75 words in English |
| **Maximum Tokens** | The context window limit — input + output combined cannot exceed this |
| **Token Counting** | Use `tiktoken` library to count tokens before sending requests |
| **Pricing** | Billed per 1M tokens (input and output priced separately) |

---

## 4. Prompt Engineering & AI Safety

### ✍️ Prompt Engineering

The skill of designing inputs to reliably guide model behavior.

| Technique | What It Does |
|---|---|
| **Zero-shot** | Ask the model directly with no examples |
| **Few-shot** | Provide 2–5 examples in the prompt to guide the output format |
| **Chain-of-Thought** | Ask the model to "think step by step" to improve reasoning |
| **ReAct Prompting** | Reason → Act → Observe loop for agentic tasks |
| **Role prompting** | Give the model a persona ("You are an expert SQL developer...") |
| **Output constraints** | Specify format explicitly ("Respond only in JSON") |

📖 See the full [Prompt Engineering Roadmap](https://roadmap.sh/prompt-engineering)

---

### 🛡️ AI Safety and Ethics

Building AI responsibly is a core part of being an AI Engineer, not an afterthought.

#### Key Issues

| Issue | Explanation |
|---|---|
| **Prompt Injection** | Malicious input that hijacks the model's instructions |
| **Bias and Fairness** | Models trained on biased data can produce discriminatory outputs |
| **Hallucinations** | Confident-sounding but factually incorrect responses |
| **Security & Privacy** | Risk of leaking sensitive data through prompts or model outputs |

#### Safety Best Practices
- **Know your customers and use cases** — tailor safety measures to your specific context
- **Constrain outputs and inputs** — validate and sanitize all model I/O
- **Conduct adversarial testing** — red-team your system before deployment
- **Use OpenAI Moderation API** — classify harmful content automatically
- **Add end-user IDs in prompts** — enables tracking and abuse detection
- **Robust prompt engineering** — use system prompts to restrict behavior

---

## 5. Open Source AI

### Open vs Closed Source Models

| | Open Source | Closed Source |
|---|---|---|
| **Access** | Weights available to download | API only |
| **Cost** | Free to use (compute cost only) | Pay per token |
| **Privacy** | Data stays on your infrastructure | Sent to provider |
| **Customization** | Full fine-tuning control | Limited |
| **Examples** | LLaMA 3, Mistral, Qwen | GPT-4, Claude, Gemini |

### 🤗 Hugging Face
The central hub for open-source AI.

| Feature | Description |
|---|---|
| **Hugging Face Hub** | Repository of 500k+ models, datasets, and demos |
| **Hugging Face Tasks** | Organized by task: text generation, image classification, translation, etc. |
| **Finding Models** | Filter by task, language, license, and size |
| **Using Models** | Load with `transformers` library or via Inference API |

```python
from transformers import pipeline

generator = pipeline("text-generation", model="mistralai/Mistral-7B-Instruct-v0.2")
output = generator("Explain what RAG is in one paragraph:")
print(output[0]["generated_text"])
```

### 🦙 Ollama — Run Models Locally
Ollama lets you run open-source LLMs on your own machine with a simple CLI.

```bash
# Pull and run a model locally
ollama run llama3
ollama run mistral
ollama run phi3
```

**Ollama SDK** — interact with local models programmatically:
```python
import ollama

response = ollama.chat(model='llama3', messages=[
    {"role": "user", "content": "What is a vector database?"}
])
print(response['message']['content'])
```

### ⚡ Inference SDK & Transformers.js
- **Inference SDK** — run Hugging Face models via API without downloading weights
- **Transformers.js** — run transformer models directly in the browser using JavaScript

---

## 6. Embeddings & Vector Databases

### 🔢 What are Embeddings?
Embeddings are **dense numerical vectors** that represent the meaning of text, images, or other data. Items with similar meanings are placed close together in vector space.

```
"cat"  → [0.21, -0.45, 0.78, ...]
"dog"  → [0.19, -0.41, 0.80, ...]   ← similar meaning → close vectors
"car"  → [-0.55, 0.32, -0.12, ...]  ← different meaning → far vectors
```

### 📦 Use Cases for Embeddings

| Use Case | How Embeddings Help |
|---|---|
| **Semantic Search** | Find documents by meaning, not just keyword match |
| **Recommendation Systems** | Suggest similar items based on vector proximity |
| **Anomaly Detection** | Find outliers — points far from all others in vector space |
| **Data Classification** | Group or label data based on vector clustering |

### 🔌 OpenAI Embeddings API

```python
from openai import OpenAI

client = OpenAI()
response = client.embeddings.create(
    model="text-embedding-3-small",
    input="How does RAG work?"
)
vector = response.data[0].embedding  # List of floats
```

**OpenAI Embedding Models:**
- `text-embedding-3-small` — fast and affordable
- `text-embedding-3-large` — higher quality, more dimensions

### 🌐 Open-Source Embeddings
- **Sentence Transformers** — popular Python library for generating embeddings locally
- **BGE, E5, nomic-embed** — high-quality open-source embedding models on Hugging Face

---

### 🗄️ Vector Databases

Specialized databases that store embeddings and enable **fast similarity search**.

| Database | Notes |
|---|---|
| **Chroma** | Lightweight, great for local development |
| **Pinecone** | Fully managed, production-ready |
| **Weaviate** | Open-source, supports hybrid search |
| **FAISS** | Facebook's library, in-memory, very fast |
| **Qdrant** | Open-source, Rust-based, highly performant |
| **LanceDB** | Columnar vector DB, great for local use |
| **Supabase** | PostgreSQL + pgvector, familiar SQL interface |
| **MongoDB Atlas** | Vector search built into MongoDB |

### ⚙️ How Vector Search Works
1. **Indexing** — embed your documents and store vectors in the DB
2. **Query** — embed the user's question into a vector
3. **Similarity Search** — find the top-K vectors closest to the query vector
4. **Return** — retrieve the original documents linked to the closest vectors

---

## 7. RAG & Implementation

### 🔍 What is RAG?
**Retrieval-Augmented Generation (RAG)** combines a vector search system with an LLM to produce answers grounded in your own data — solving the hallucination and stale knowledge problems.

```
User Query
    ↓
Embed Query → Search Vector DB → Retrieve Top-K Chunks
    ↓
Inject Retrieved Chunks into Prompt → Send to LLM
    ↓
Grounded, Accurate Response
```

### 🆚 RAG vs Fine-tuning

| | RAG | Fine-tuning |
|---|---|---|
| **Best for** | Dynamic, up-to-date knowledge | Style, format, tone consistency |
| **Data required** | Documents/chunks | Labeled input-output examples |
| **Updatable?** | Yes, just update the vector DB | Requires retraining |
| **Cost** | Storage + retrieval + LLM call | Expensive training run |

### 🧩 RAG Pipeline Components

| Step | What Happens |
|---|---|
| **Chunking** | Split documents into smaller pieces (fixed-size, semantic, or recursive) |
| **Embedding** | Convert each chunk into a vector |
| **Vector Database** | Store and index all chunk vectors |
| **Retrieval** | At query time, find the most relevant chunks |
| **Generation** | LLM generates a response using the retrieved chunks as context |

### 🛠️ Ways of Implementing RAG

| Method | When to Use |
|---|---|
| **Using SDKs directly** | Full control, custom pipelines |
| **LangChain** | Feature-rich framework with many integrations |
| **LlamaIndex** | Optimized for document indexing and RAG |
| **OpenAI Assistant API** | Managed RAG with file search built-in |
| **Replicate** | Deploying open-source models with APIs |

---

## 8. AI Agents

### 🕵️ What are AI Agents?
AI Agents are systems that use LLMs to **reason, plan, and take actions** autonomously — going beyond a single question-answer interaction to complete multi-step tasks.

```
Goal → Think → Choose Action → Execute Tool → Observe Result → Think Again → ...
```

### 🔄 ReAct Prompting
The foundational pattern for agents:
- **Re**ason — think about what to do next
- **Act** — choose and call a tool/action
- **Observe** — process the result and continue

### 🛠️ Building AI Agents

| Component | Description |
|---|---|
| **Tools / Functions** | External capabilities the agent can call (search, calculator, code runner, APIs) |
| **Memory** | Short-term (conversation history), long-term (vector store) |
| **Planning** | Breaking a goal into executable steps |
| **Orchestration** | Managing the loop of reason → act → observe |

### ⚙️ Implementation Options

| Option | Notes |
|---|---|
| **Manual Implementation** | Full control using raw API calls and custom logic |
| **OpenAI Functions/Tools** | Native function calling in the Chat Completions API |
| **OpenAI Assistant API** | Managed agent with threads, tools, and file search |
| **LangChain Agents** | Pre-built agent types with many tool integrations |

### 🤔 Agents vs RAG
- **RAG** — best when you need to answer questions from a static knowledge base
- **Agents** — best when you need multi-step reasoning, tool use, or autonomous task completion

---

## 9. Multimodal AI

### 🎨 What is Multimodal AI?
Multimodal AI models can process and generate **multiple types of data** — not just text, but also images, audio, and video.

### 🧩 Multimodal Tasks & APIs

| Task | Tool / API |
|---|---|
| **Image Understanding** | OpenAI Vision API, GPT-4o |
| **Image Generation** | DALL-E API |
| **Audio Processing** | OpenAI Whisper API |
| **Speech-to-Text** | Whisper (OpenAI), open-source alternatives |
| **Text-to-Speech** | OpenAI TTS API |
| **Video Understanding** | Gemini 1.5 Pro, emerging tools |

### 🔌 Using Multimodal APIs

**Image Understanding (Vision):**
```python
response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{
        "role": "user",
        "content": [
            {"type": "image_url", "image_url": {"url": "https://example.com/chart.png"}},
            {"type": "text", "text": "What does this chart show?"}
        ]
    }]
)
```

**Speech-to-Text with Whisper:**
```python
with open("audio.mp3", "rb") as audio_file:
    transcript = client.audio.transcriptions.create(
        model="whisper-1",
        file=audio_file
    )
print(transcript.text)
```

### 🧰 Frameworks for Multimodal Apps
- **LangChain** — supports multimodal chains and agents
- **LlamaIndex** — multimodal document parsing and indexing
- **Hugging Face Models** — thousands of vision, audio, and video models

---

## 10. Development Tools

### 🧑‍💻 AI Code Editors

| Tool | Description |
|---|---|
| **Cursor** | AI-powered VS Code fork with chat, autocomplete, and codebase understanding |
| **GitHub Copilot** | Inline code suggestions and chat inside VS Code / JetBrains |
| **Windsurf** | Agentic IDE with multi-file editing and autonomous task execution |

### ⚡ Code Completion Tools
- **Supermaven** — ultra-fast code completion
- **Tabnine** — AI completion with privacy-focused options
- **Codeium** — free AI code assistant

---

## 🛠️ My Tech Stack

```
LLM APIs:         OpenAI · Anthropic · Groq
Open Source:      Ollama · Hugging Face · Mistral
Embeddings:       OpenAI Embeddings · Sentence Transformers
Vector DBs:       Chroma · Qdrant · Pinecone
RAG Frameworks:   LangChain · LlamaIndex
Agent Frameworks: LangGraph · OpenAI Assistants
Languages:        Python · JavaScript
```

---

## 📈 Progress Tracker

| Section | Status |
|---|---|
| Introduction & Core Concepts | ✅ Done |
| Using Pre-trained Models | ✅ Done |
| OpenAI Platform | 🔄 In Progress |
| Prompt Engineering & AI Safety | 🔄 In Progress |
| Open Source AI (Hugging Face, Ollama) | 🔜 Next |
| Embeddings & Vector Databases | 🔜 Next |
| RAG & Implementation | ⏳ Planned |
| AI Agents | ⏳ Planned |
| Multimodal AI | ⏳ Planned |
| Development Tools | ⏳ Planned |

---

## 🔗 Resources

- 🗺️ [roadmap.sh/ai-engineer](https://roadmap.sh/ai-engineer) — The official roadmap this repo follows
- 📖 [OpenAI Docs](https://platform.openai.com/docs)
- 🤗 [Hugging Face Docs](https://huggingface.co/docs)
- 🦜 [LangChain Docs](https://python.langchain.com)
- 🦙 [LlamaIndex Docs](https://docs.llamaindex.ai)
- 🦙 [Ollama](https://ollama.com)

---

## 📜 License

This project is open source and available under the [MIT License](LICENSE).

---

<div align="center">

**Following [roadmap.sh/ai-engineer](https://roadmap.sh/ai-engineer) step by step 🚀**

⭐ Star this repo if it's useful to you!

</div>

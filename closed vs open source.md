================================================================
        FULL GUIDE: OPEN vs CLOSED SOURCE AI MODELS
        For AI Engineering & Agent Development
================================================================

Written for: AI Engineering Learners
Level: Intermediate → Advanced
Topic: Open Source vs Closed Source LLMs


================================================================
PART 1 — THEORY: WHAT ARE THEY?
================================================================

--- CLOSED SOURCE MODELS ---

A closed source model (also called "proprietary") is a model where:
  - The weights are NOT public (you cannot download the brain of the model)
  - The training data is NOT public
  - The architecture might be partially described in papers, but you can't see the full code
  - You access it ONLY through an API (Application Programming Interface)

"Weights" = The numbers inside a neural network that define how it thinks.
Think of it like: you can USE the calculator, but you can't open it and see the circuits.

Examples of Closed Source Models:
  → GPT-4o, GPT-4-turbo (OpenAI)
  → Claude 3.5 Sonnet, Claude 3 Opus (Anthropic)
  → Gemini 1.5 Pro (Google)
  → Command R+ (Cohere)


--- OPEN SOURCE MODELS ---

An open source model is a model where:
  - The weights ARE public (you can download the actual model)
  - Sometimes training code is public too
  - You can run it locally on your machine
  - You can fine-tune it (train it more on your own data)
  - You can modify it, deploy it yourself, even sell it (depending on license)

"Fine-tuning" = Taking an existing model and training it more on YOUR specific data
so it becomes better at YOUR specific task.

Examples of Open Source Models:
  → LLaMA 3.1 (Meta) — 8B, 70B, 405B sizes
  → Mistral 7B / Mixtral 8x7B (Mistral AI)
  → Falcon (TII UAE)
  → Phi-3 / Phi-4 (Microsoft)
  → Gemma 2 (Google)
  → DeepSeek-V3, DeepSeek-R1 (DeepSeek)
  → Qwen2.5 (Alibaba)

IMPORTANT NOTE: "Open Source" has different levels:
  Level 1 → Weights only (most common — Meta LLaMA)
  Level 2 → Weights + Training code
  Level 3 → Weights + Training code + Training data (very rare)
  True open source = Level 3. Most "open source" models are Level 1.


================================================================
PART 2 — KEY DIFFERENCES (COMPARISON TABLE)
================================================================

FEATURE                  | CLOSED SOURCE        | OPEN SOURCE
-------------------------|----------------------|----------------------
Access                   | API only             | Download + run locally
Cost                     | Pay per token        | Free (compute costs only)
Privacy                  | Data goes to company | Data stays with you
Control                  | No control           | Full control
Fine-tuning              | Limited / paid       | Fully possible
Speed (latency)          | Network dependent    | Local = faster
Reliability              | 99.9% uptime (SLA)   | You manage uptime
Quality (generally)      | Higher (frontier)    | Catching up fast
Context window           | Very large           | Varies
Offline usage            | Not possible         | Possible
Customization            | Prompt engineering   | Prompt + fine-tune + merge
Transparency             | Black box            | Inspectable weights


================================================================
PART 3 — WHEN TO USE WHICH (DECISION FRAMEWORK)
================================================================

USE CLOSED SOURCE WHEN:
  ✓ You need the BEST possible quality (medical, legal, complex reasoning)
  ✓ You don't want to manage infrastructure
  ✓ You need the largest context windows (1M+ tokens)
  ✓ You're building an MVP and want to move fast
  ✓ You need reliable uptime guarantees
  ✓ Multimodal tasks (image + text, audio, etc.)

USE OPEN SOURCE WHEN:
  ✓ You have SENSITIVE DATA (healthcare, finance, legal documents)
  ✓ You need to fine-tune on your private dataset
  ✓ You want to reduce costs at scale (high volume = expensive API)
  ✓ You need offline / edge deployment (no internet)
  ✓ You want full control and reproducibility
  ✓ You want to build custom agents with model-level access
  ✓ Compliance requirements (GDPR, HIPAA — data cannot leave your server)


================================================================
PART 4 — COST ANALYSIS (REAL NUMBERS)
================================================================

CLOSED SOURCE — Cost per 1 million tokens (approx. May 2026):
  Claude Sonnet 4     → ~$3 input / $15 output
  GPT-4o              → ~$5 input / $15 output
  Gemini 1.5 Pro      → ~$3.5 input / $10.5 output

OPEN SOURCE — Cost:
  Model download      → Free
  Running cost        → You pay for compute (GPU/CPU)
  
  Example: Running LLaMA 3.1 70B on 1x A100 GPU (cloud):
    ~$2-3/hour for the GPU
    If you process 1M tokens/hour → $2-3 per 1M tokens
    At scale (10M tokens/hour) → same $2-3 per 1M tokens (cost stays flat)
    
  KEY INSIGHT: Closed source cost SCALES with usage.
               Open source cost is FIXED (just the hardware).
               
  Break-even point: Usually around 100M-500M tokens/month
  → Below that: closed source is cheaper (no infra to manage)
  → Above that: open source saves money


================================================================
PART 5 — CODE EXAMPLES
================================================================

--- EXAMPLE 1: Calling a Closed Source Model (Anthropic) ---

import anthropic

client = anthropic.Anthropic(api_key="your-api-key")

message = client.messages.create(
    model="claude-sonnet-4-20250514",
    max_tokens=1024,
    messages=[
        {"role": "user", "content": "Explain quantum entanglement simply."}
    ]
)

print(message.content[0].text)

# What happens here:
# 1. Your text leaves YOUR machine
# 2. Goes to Anthropic's servers
# 3. The model runs on THEIR GPU
# 4. Response comes back to you
# 5. Anthropic may log this (check their privacy policy)


--- EXAMPLE 2: Calling an Open Source Model (locally with Ollama) ---

# First, install Ollama: https://ollama.ai
# Then run: ollama pull llama3.1

import requests
import json

def call_local_llm(prompt: str, model: str = "llama3.1") -> str:
    """
    Call a locally running open source model via Ollama.
    Everything runs on YOUR machine. No data leaves.
    """
    response = requests.post(
        "http://localhost:11434/api/generate",
        json={
            "model": model,
            "prompt": prompt,
            "stream": False
        }
    )
    return response.json()["response"]

result = call_local_llm("Explain quantum entanglement simply.")
print(result)

# What happens here:
# 1. Your text stays on YOUR machine
# 2. Ollama runs the model on YOUR CPU/GPU
# 3. No internet needed after download
# 4. Full privacy. Full control.


--- EXAMPLE 3: Calling Open Source via API (Groq — cloud-hosted open models) ---

# Groq hosts open source models (LLaMA, Mistral) on their fast hardware
# This gives you SPEED of closed source + MODELS of open source
# But data still goes to their servers

from groq import Groq

client = Groq(api_key="your-groq-api-key")

completion = client.chat.completions.create(
    model="llama-3.1-70b-versatile",
    messages=[
        {"role": "user", "content": "Explain quantum entanglement simply."}
    ],
    max_tokens=1024
)

print(completion.choices[0].message.content)

# Important: Groq is NOT fully private (data goes to Groq's servers)
# But the MODEL is open source — you could also run it yourself


--- EXAMPLE 4: Fine-tuning an Open Source Model ---

# This is the HUGE advantage of open source
# You CANNOT fine-tune Claude or GPT-4 on your private data (fully)
# You CAN fine-tune LLaMA 3.1 completely

from transformers import AutoModelForCausalLM, AutoTokenizer, TrainingArguments
from trl import SFTTrainer  # SFT = Supervised Fine-Tuning
import torch

# Load base model
model_name = "meta-llama/Llama-3.1-8B-Instruct"
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForCausalLM.from_pretrained(
    model_name,
    torch_dtype=torch.bfloat16,  # bfloat16 = 16-bit precision (saves memory)
    device_map="auto"            # automatically put model on GPU if available
)

# Your custom training data
training_data = [
    {
        "instruction": "What is our return policy?",
        "response": "Our return policy is 30 days for all items."
    },
    # ... more examples from YOUR company data
]

# Training arguments
training_args = TrainingArguments(
    output_dir="./my-fine-tuned-model",
    num_train_epochs=3,
    per_device_train_batch_size=4,
    learning_rate=2e-4,
    save_steps=100,
)

# Fine-tune
trainer = SFTTrainer(
    model=model,
    args=training_args,
    train_dataset=training_data,
    tokenizer=tokenizer,
)

trainer.train()
# Now you have YOUR OWN model with YOUR OWN data
# Deploy it, keep it private, use it however you want


================================================================
PART 6 — CRITICAL THINKING SECTION
================================================================

QUESTION 1: "If open source models are free, why do companies still pay for GPT-4?"

Think about this:
  - "Free" model ≠ free to run at scale
  - OpenAI has entire teams managing reliability, safety, updates
  - Running 70B parameter model needs serious hardware
  - Many companies don't want to hire ML engineers to manage models
  - The BEST models are still closed source (for now)
  
  The real question is: what is your bottleneck?
  → Speed to market? → Closed source
  → Data privacy + customization? → Open source
  → Cost at scale? → Open source


QUESTION 2: "Can I trust an open source model's weights?"

This is a deep question. When Meta releases LLaMA:
  - You get the weights, but NOT the training data
  - The model could have biases from unknown data
  - You cannot audit what it was trained on
  - "Open weights" ≠ "fully transparent"
  
  True transparency would require: weights + data + training code
  Very few models provide all three.


QUESTION 3: "Does open source mean less safe?"

Counter-intuitive answer: MAYBE safer in some ways.
  - Researchers can audit the weights for backdoors/malware
  - Security through obscurity (closed source) is weak security
  - BUT: open source models are easier to misuse (no API guardrails)
  - Closed source models have safety filters at the API level
  - Open source: you can remove those safety filters (good and bad)


================================================================
PART 7 — FOR AI AGENTS SPECIFICALLY
================================================================

This is CRITICAL for you as an AI engineer building agents.

CLOSED SOURCE AGENTS:
  Pros:
    + Best function calling / tool use (GPT-4, Claude)
    + Best instruction following
    + Handles complex multi-step reasoning
    + Large context = can see entire codebase
  
  Cons:
    - Every agent action sends data to external API
    - API costs multiply fast (agents make MANY calls)
    - Latency on every tool call
    - Rate limits can block your agent


OPEN SOURCE AGENTS:
  Pros:
    + Run locally = fast, private, no rate limits
    + Can fine-tune for specific agent behaviors
    + Use quantized models (4-bit) to fit on consumer GPU
    + Full control over system prompts and safety
  
  Cons:
    - Smaller models struggle with complex tool use
    - Function calling quality is lower (but improving)
    - Need to manage the infrastructure yourself

"Quantization" = Compressing a model to use less memory.
  Example: LLaMA 3.1 70B normally needs ~140GB RAM
           With 4-bit quantization → only ~40GB RAM
           Small quality loss, huge memory savings.


HYBRID APPROACH (MOST COMMON IN PRODUCTION):
  - Use closed source for planning / reasoning (the "brain")
  - Use open source for execution / embedding / classification (the "hands")
  
  Example Architecture:
    Agent Orchestrator → GPT-4o (closed, best reasoning)
    Embedding Model   → nomic-embed-text (open, local, fast)
    Code Execution    → CodeLlama (open, specialized)
    Safety Filter     → Local Llama 3 (open, private)


================================================================
PART 8 — WHAT HAPPENS IF YOU IGNORE THIS TOPIC?
================================================================

If you ONLY use closed source:
  → You will hit situations where you CANNOT give user data to an API
  → You will spend huge money at scale
  → You will be blocked by rate limits in your agents
  → You will be dependent on companies' pricing changes (price increases)
  → You cannot fine-tune = stuck with generic behavior

If you ONLY use open source:
  → Your agent quality will be lower (for now)
  → You will spend more time managing infrastructure
  → You might struggle with complex reasoning tasks
  → Missing the best multimodal capabilities


================================================================
PART 9 — POPULAR TOOLS TO WORK WITH BOTH
================================================================

LOCAL OPEN SOURCE RUNNERS:
  → Ollama          - Easiest way to run models locally (like Docker for LLMs)
  → LM Studio       - GUI for running models on your laptop
  → llama.cpp       - Highly optimized C++ inference engine
  → vLLM            - High-throughput serving for production

UNIFIED APIs (use same code for open and closed):
  → LiteLLM         - One Python interface for 100+ models
  → LangChain       - Agent framework supporting both
  → LlamaIndex      - RAG framework supporting both

CLOUD OPEN SOURCE HOSTING:
  → Groq            - Fastest inference for open models
  → Together.ai     - Wide selection of open models
  → Replicate       - Deploy any model with one click
  → Hugging Face    - Central hub for all open models


--- LiteLLM Example (same code, switch models easily) ---

from litellm import completion

# Closed source
response = completion(
    model="claude-sonnet-4-20250514",
    messages=[{"role": "user", "content": "Hello"}]
)

# Open source via Groq — just change the model string!
response = completion(
    model="groq/llama-3.1-70b-versatile",
    messages=[{"role": "user", "content": "Hello"}]
)

# Local via Ollama — just change the model string!
response = completion(
    model="ollama/llama3.1",
    messages=[{"role": "user", "content": "Hello"}]
)

# The rest of your code stays IDENTICAL
# This is called an "abstraction layer" — it hides the differences
print(response.choices[0].message.content)


================================================================
PART 10 — CHALLENGE FOR YOU (NOT EASY!)
================================================================

BUILD THIS:

Create a Python class called "ModelRouter" that:

1. Takes a task description as input
2. Classifies the task into one of these categories:
     - "sensitive"  (medical/legal/finance data → must use local)
     - "complex"    (multi-step reasoning → use closed source)
     - "simple"     (basic Q&A → use local to save money)
3. Routes to the correct model automatically
4. Falls back to the other model if one fails
5. Logs: which model was used, how many tokens, estimated cost

Example usage:
  router = ModelRouter()
  result = router.route("Analyze this patient's blood test results: ...")
  # Should automatically use local model (sensitive data)
  
  result = router.route("Plan a 10-step strategy to build a startup")
  # Should use Claude/GPT-4 (complex reasoning needed)

Think about:
  - How do you CLASSIFY the task? (Maybe use a small local model for this!)
  - How do you handle the fallback logic?
  - How do you estimate cost before sending?
  - What if the local model is too slow?

This is a real pattern used in production AI systems.
It's called "LLM routing" or "model cascading."


================================================================
SUMMARY: THE GOLDEN RULE
================================================================

There is NO single correct answer.

The best AI engineers know BOTH worlds:
  → Use closed source when quality matters most
  → Use open source when privacy / cost / control matters most
  → Combine them in hybrid architectures for production systems

The trend: open source is catching up to closed source FAST.
  In 2023: GPT-4 was far ahead.
  In 2025: LLaMA 3.1 405B, DeepSeek-V3 are genuinely competitive.
  In 2026+: The gap is closing further.

Learning open source skills NOW = huge advantage.
Most engineers only know how to call an API.
You want to know how to RUN and CONTROL the model.

================================================================
END OF GUIDE
================================================================

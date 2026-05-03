# Open source VS closed source models
## Open source
It's an LLM trained by companies like: Meta AI, Mistral AI, DeepSeek AI
And for every company it's models 
Meta AI = Llama 3.1
Mistral AI = Mistral 7B / Mixtral 8x7B
DeepSeek = DeepSeek-V3 / DeepSeek-R1

### What cases it's good to use *open-source* models
There are **pros** and **cons** for using *open-source* models

**The Pros:**
1. If you want to fine tune the model on your data, **Because you can fine tune data freely on most of the open source models**
2. If you want privacy to your Data, **When using open-source models there is no any data going from your prompts to the API, it's just: your prompt -> the model installed on your environment -> the response**
3. Faster than the API, **"If your GPU/CPU is fast", Because as we said it's from your prompt to the LLM that is on your laptop then the response**
4. Cheaper than the API models, **Because you will just pay for the cloud you are using most likely: $2-3/hour (You can use as many tokens as you want for that flat price)**
5. No vendor lock-in, **You own the weights forever. Nobody can raise the price, shut down the API, or take the model away from you**
6. Offline usage, **The model works with no internet connection at all, useful for edge devices or high-security environments**

**The Cons:**
1. Harder to *setup* than closed-source, **You need to manage the infrastructure yourself (downloading weights, running a server, handling updates)**
2. Lower quality on complex tasks, **Smaller open source models still struggle with deep multi-step reasoning compared to GPT-4o or Claude**
3. You need strong hardware, **Running a 70B model needs ~70GB RAM minimum, which means expensive GPUs or cloud machines**
4. No built-in safety filters, **Closed source APIs have safety layers built in. Open source gives you raw model access — you have to build safety yourself**
5. You manage reliability yourself, **If your server crashes, your app goes down. No uptime guarantee like closed source APIs (99.9% SLA)**

---

## Closed source
It's an LLM trained by companies like: OpenAI, Anthropic, Google
And for every company it's models:
OpenAI = GPT-4o, GPT-4-turbo
Anthropic = Claude 3.5 Sonnet, Claude 3 Opus
Google = Gemini 1.5 Pro, Gemini 2.0 Flash

### What cases it's good to use *closed-source* models
There are **pros** and **cons** for using *closed-source* models

**The Pros:**
1. Best quality on complex tasks, **These are frontier models trained on massive compute that open source hasn't matched yet for hard reasoning**
2. Easiest to setup, **Just get an API key and you are running in 5 minutes, no hardware needed**
3. Largest context windows, **Claude supports up to 200K tokens, Gemini up to 1M tokens — meaning you can feed entire codebases or books**
4. Managed reliability, **The company guarantees 99.9% uptime via SLA (Service Level Agreement — a contract promising availability)**
5. Built-in safety, **The API has guardrails already built in so you don't have to build them yourself**
6. Best multimodal support, **Image + text + audio + video in one model, open source is still catching up here**

**The Cons:**
1. Your data leaves your machine, **Every prompt you send goes to the company's servers — serious problem for medical, legal, or financial data**
2. Cost scales with usage, **You pay per token. At high volume (millions of requests) the bill grows fast**
3. Vendor lock-in, **If the company raises prices, changes the API, or shuts down — your system breaks**
4. No fine-tuning on private data, **You cannot fully train these models on your secret company data**
5. No offline usage, **100% dependent on internet connection and the company's servers being up**

---

## When to use which — Quick Decision Guide

| Situation | Use |
|---|---|
| Sensitive / private data | Open source |
| Need to fine-tune on your data | Open source |
| High volume (millions of tokens/month) | Open source |
| Offline or edge deployment | Open source |
| Best reasoning quality needed | Closed source |
| Fast MVP / prototype | Closed source |
| Multimodal (image + text) | Closed source |
| No ML engineering team | Closed source |

---

## Quantization — Running big models on small hardware

**The problem:** A 70B parameter model needs ~140GB RAM in full precision.
**The solution:** Quantization — compress the model numbers to use less memory.

```python

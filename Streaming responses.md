# Streaming Response

## What is a Streaming Response?
When an AI replies to our message, it looks bad if we wait 10 seconds 
and then all the text appears at once. It's much better if the response 
streams word by word — just like how ChatGPT and Claude type in real time.

Each piece that arrives is called a **chunk** (also called a **token** — 
roughly one word or part of a word).

---

## Code Example with Google Gemini SDK

### Without Streaming
```python
from google import genai
import os
from dotenv import load_dotenv

load_dotenv("api.env")
api_key = os.getenv("GEMINI_API_KEY")

client = genai.Client(api_key=api_key)

response = client.models.generate_content(
    model="gemini-2.0-flash",
    contents="What are the most famous novels of all time?"
)

print(response.text)  # Waits for full response, then prints all at once
```

### With Streaming
```python
from google import genai
import os
from dotenv import load_dotenv

load_dotenv("api.env")
api_key = os.getenv("GEMINI_API_KEY")

client = genai.Client(api_key=api_key)

for chunk in client.models.generate_content_stream(  # loop over each chunk as it arrives
    model="gemini-2.0-flash",                        # the model we will use
    contents="What are the top best countries in history?"  # our question
):
    print(chunk.text, end="", flush=True)
    # end=""   → don't add a new line after each chunk (keeps text flowing)
    # flush=True → show each chunk immediately, don't wait to buffer

print()  # move to a new line after streaming is done
```

---

## Key Differences

| | Without Streaming | With Streaming |
|---|---|---|
| User experience | Waits, then sees everything | Sees output in real time |
| Function used | `generate_content()` | `generate_content_stream()` |
| Feel | Slow and frozen | Fast and natural |

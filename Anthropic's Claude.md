# Claude

## What is claude

Claude is an LLM that have been made by company called **Anthropic**

## What is the things that claude is better than the other LLM's in

Claude beat another LLMs with:

1. Coding

Claude is one if not the best coding AI right now, It have trained very good on nearly all the proggraming languages

2. Long documents

Claude can write and read very long documents, and in the same time it's provide to you an very long explination for this *topic*

3. And an another things like: **Saftey, writing quality, etc**

## Simple code for it

```
import os
from anthropic import Anthropic

# Step 1: Create a client (your connection to Claude)
client = Anthropic()
# It automatically reads ANTHROPIC_API_KEY from your environment

# Step 2: Send a message to Claude
message = client.messages.create(
    model="claude-sonnet-4-6",   # Which Claude model to use
    max_tokens=1024,              # Maximum length of the reply
    messages=[
        {
            "role": "user",        # You are the "user"
            "content": "Hello Claude! What is 2 + 2?"
        }
    ]
)

# Step 3: Print Claude's reply
print(message.content[0].text)
```
